# JoyHoops

A full-stack web app for a youth basketball nonprofit, where parents register and enroll their children in classes and pay online, and admins manage classes and coaches. 

I learned a lot building this before coding agents/vibe-coding really became mainstream. Went through so many dead-ends and stupid mistakes using Supabase. When Claude Code came along it really sped up the process. 

## Stack

- **Frontend:** Next.js 16 (App Router), React 19, TypeScript, Tailwind CSS, shadcn/ui
- **Backend:** Supabase (Postgres, Auth, Row-Level Security, Edge Functions on Deno)
- **Payments:** Stripe Checkout with a webhook handler
- **Forms/validation:** React Hook Form, Zod
- **Deployment:** Vercel

## Features

- Parent accounts with email/password and OAuth sign-in
- Add children, browse classes, enroll, and unenroll
- Stripe-powered checkout for paid classes, plus free enrollment
- Admin dashboard for creating and editing classes, managing coach profiles, and viewing registrant info
- Route protection through middleware (admin-only and authenticated-only areas)

## Design Notes

- **Three Supabase clients:** a cookie-based server client (RLS enforced), a browser client, and a service-role admin client used only where RLS must be bypassed.
- **Server/client split:** Server Component pages fetch data and pass it to client components that handle interactivity.
- **Privileged operations in Edge Functions:** checkout, the Stripe webhook, and class and enrollment mutations run in Supabase Edge Functions. Next.js API routes validate input and forward to them.

## Running Locally

```bash
pnpm install
pnpm dev
```

Create a `.env.local` with:

```
NEXT_PUBLIC_SUPABASE_URL
NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY
NEXT_PUBLIC_OAUTH_SUPABASE_URL
NEXT_PUBLIC_BASE_URL
SUPABASE_SECRET_KEY
ADMIN_EMAIL
```

Edge Functions also need Stripe keys, set as Supabase secrets.

## About

I built JoyHoops as a real tool for a nonprofit that was handling registration manually. It covers the full path from database schema and auth to payments and deployment. 
