# AI Medical Notes SaaS

AI assistant for doctors that turns consultation notes into structured outputs, streamed in real time:

- Summary of the visit for the doctor's records
- Next steps for the doctor
- Draft email to the patient in patient-friendly language (Farsi)

Access is gated by authentication and a paid subscription plan.

## Stack

- **Frontend:** Next.js (Pages Router), React, TypeScript, Tailwind CSS
- **Backend:** FastAPI serverless function on Vercel (`api/index.py`)
- **LLM:** OpenAI Chat Completions with streaming, delivered to the browser as Server-Sent Events
- **Auth and billing:** Clerk (JWT verification in FastAPI, subscription-protected product page)
- **Deployment:** Vercel

## How it works

1. The doctor signs in and opens the product page (premium plan required).
2. The form sends patient name, visit date and notes to `POST /api` with the Clerk JWT.
3. FastAPI verifies the token, builds the prompt and streams the model output.
4. The frontend renders the streamed Markdown as it arrives.

## Run locally

```bash
npm install
pip install -r requirements.txt
# .env.local: OPENAI_API_KEY, CLERK_JWKS_URL, NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY, CLERK_SECRET_KEY
vercel dev
```
