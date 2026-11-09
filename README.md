# Frontend

A Vue 3 + Vite frontend with Tailwind and shadcn-vue components.

## Prerequisites

- Node.js 18+
- pnpm
- Backend running locally or on your machine

## Setup

1. Copy the environment example file:

```bash
cp .env.example .env
```

2. Update the API URL in `.env` to match your backend:

```env
VITE_API_URL=http://localhost:8080
```

3. Install dependencies:

```bash
pnpm install
```

4. Run the app locally:

```bash
pnpm dev --host
```

## Environment variables

- `VITE_API_URL` - backend base URL
- `VITE_APP_NAME` - app display name
- `VITE_PORT` - local dev server port

## Production build

```bash
pnpm build
```
