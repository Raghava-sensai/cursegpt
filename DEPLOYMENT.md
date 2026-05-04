# Vercel Deployment Checklist

## Project Settings

- Root Directory: `dashboard`
- Framework Preset: `Vite`
- Install Command: `npm ci`
- Build Command: `npm run build`
- Output Directory: `dist`
- Node.js Version: `20.x`

This dashboard is npm-only. Keep `package-lock.json` and do not add `pnpm-lock.yaml` or `yarn.lock`, otherwise Vercel may select the wrong package manager.

## Environment Variables

Set this in Vercel:

```text
VITE_API_BASE=https://cloudflare-email-automation-worker.veeraraghava698.workers.dev
```

## API Routing

All dashboard API calls are routed through `src/api.ts` and use `VITE_API_BASE`.

Authenticated calls include:

```text
Authorization: Bearer <dashboard_token>
```

## Required Worker State

Deploy the Worker before deploying this dashboard, because the dashboard expects:

- `POST /auth/login`
- `GET /auth/me`
- `GET/POST /users`
- `GET/POST/PATCH/DELETE /triggers`
- `GET/PATCH /templates`
- `GET /logs`
- `POST /preview`
- `POST /events`

## Exit 126 Checklist

If Vercel shows `exit code 126`, check these first:

- The Vercel Root Directory is exactly `dashboard`, or deploy from the repo root with the root `vercel.json`.
- Install Command is `npm ci`.
- Build Command is `npm run build`.
- Output Directory is `dist` when Root Directory is `dashboard`.
- Only `package-lock.json` exists in `dashboard`; no `pnpm-lock.yaml` or `yarn.lock`.
- Node.js version is `20.x`.
