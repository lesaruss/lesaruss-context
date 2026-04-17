# LESARUSS Project Cartridge

**For:** lesaruss.ai platform development
**Stack:** Next.js 16, TypeScript, Tailwind CSS v4, React 19, Supabase, Vercel

---

## Repository

- GitHub: lesaruss/lesaruss-project
- Branch: main
- Auto-deploys to Vercel on push to main
- Vercel team slug: contact-2245s-projects

## Environment Variables

| Variable | Purpose |
|----------|---------|
| GHL_WEBHOOK_URL | GoHighLevel inbound webhook |
| NEXT_PUBLIC_CIRCLE_URL | Community URL (default: https://lesaruss.circle.so) |
| NEXT_PUBLIC_PROJECT_URL | Platform base URL |
| NEXT_PUBLIC_SUPABASE_URL | Supabase project URL |
| NEXT_PUBLIC_SUPABASE_ANON_KEY | Supabase anonymous key |

## File Conventions

- New pages: app/[route]/page.tsx
- New API routes: app/api/[route]/route.ts
- Shared components: components/
- Static assets: public/
- No separate CSS files, all Tailwind inline
- Server components by default; "use client" only when needed

## Rules

- App Router only (no pages/ directory)
- No CSS files, Tailwind classes only
- No hardcoded URLs, use environment variables
- No SVG code in chat, save as files in /public/
- No em-dashes anywhere
- layout.tsx MUST import globals.css or all Tailwind breaks
- Keep bundle lean

## Current State

- Login broken (white screen mobile, redirect loop desktop)
- Briefings system live on lesaruss.ai (behind auth)
- Supabase: lesaruss-directory project (ID: fwbhwfxpncrsfhttimna)

## Fieldy Pipeline

- Webhook: https://fwbhwfxpncrsfhttimna.supabase.co/functions/v1/fieldy-webhook
- Table: public.fieldy_transcripts
- Command scanner: every 2 min (trigger phrase + context scan)
- Sean Report: every 2 hours
- Notifications: Google Chat webhook
