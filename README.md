# Algo Trading Platform

A no-code algorithmic trading platform UI ("AlgoSensei") built with Next.js,
React, and Tailwind CSS. It offers a trading dashboard with live market data,
a strategy studio for building trading strategies, backtesting views, a trading
terminal, community pages, and an AI assistant that gives trading-strategy
advice powered by OpenAI.

> Demo/prototype: market data comes from the public Binance API and the AI
> assistant requires an OpenAI key. Order execution against a real exchange is
> not wired up — this is a frontend + server-actions prototype.

## Features

- 📊 **Trading dashboard** — live market data (BTC/ETH/BNB + more) from Binance
- 🧪 **Strategy studio** — no-code strategy builder interface
- 🔁 **Backtesting** — backtest view for evaluating strategies
- 💹 **Trading terminal** — trading page with market data components
- 🤖 **AI assistant** — strategy advice via OpenAI GPT-4o (server action)
- 🔐 Binance API key/secret support for authenticated endpoints
- 👥 Community page + login page scaffolding
- 🌗 Dark-mode ready theming via `next-themes`
- 🧩 shadcn/ui component library (tabs, cards, inputs, avatars, …)

## Tech Stack

- **Framework:** Next.js 15 (App Router, React 19, TypeScript)
- **Styling:** Tailwind CSS + `tailwindcss-animate`, shadcn/ui
- **UI primitives:** Radix UI
- **Icons:** Lucide React
- **AI:** Vercel AI SDK (`ai` + `@ai-sdk/openai`) — GPT-4o strategy advice
- **Data:** Binance public REST API (market data, klines)
- **Server actions:** `"use server"` actions in `lib/binance.ts`, `lib/openai.ts`
- **Analytics:** Vercel Analytics

## Quick Start

```bash
# Install dependencies (pnpm or npm)
pnpm install
# or: npm install

# Run the dev server
pnpm dev
# or: npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### Production build

```bash
pnpm build
pnpm start
```

## Environment Variables

Create a `.env.local` file:

```bash
# Enables the AI strategy assistant (getAiStrategyAdvice in lib/openai.ts)
OPENAI_API_KEY=sk-...

# Optional: enables authenticated Binance endpoints in lib/binance.ts
BINANCE_API_KEY=your-binance-api-key
BINANCE_API_SECRET=your-binance-api-secret
```

The app runs without keys — the AI assistant will show a "not configured"
message and public market data works anonymously.

## Project Structure

```
.
├── app/
│   ├── layout.tsx          # Root layout (theme provider, analytics)
│   ├── page.tsx            # Landing page
│   ├── trading/page.tsx    # Trading terminal
│   ├── studio/page.tsx     # Strategy studio (no-code builder)
│   ├── strategy/page.tsx   # Strategy view
│   ├── backtest/page.tsx   # Backtesting view
│   ├── community/page.tsx  # Community page
│   ├── login/page.tsx      # Login page
│   └── globals.css         # Tailwind + global styles
├── components/
│   ├── trading-dashboard.tsx
│   ├── market-data.tsx
│   ├── ai-assistant.tsx
│   ├── navigation.tsx
│   ├── main-scene.tsx
│   ├── login-background.tsx
│   ├── theme-provider.tsx
│   └── ui/                 # shadcn/ui primitives
├── lib/
│   ├── binance.ts          # Server actions: Binance market/account data
│   ├── openai.ts           # Server action: AI strategy advice (GPT-4o)
│   └── utils.ts            # cn() class-merge helper
├── public/                 # Static assets & placeholder images
├── next.config.mjs         # Next.js config (images unoptimized)
└── components.json         # shadcn/ui config
```

## Deployment Notes

- This app **requires a Node.js server runtime** because it uses Next.js
  server actions (`"use server"`) and secret env vars (Binance/OpenAI keys).
  It cannot be statically exported.
- **Vercel:** push to GitHub and import the repo — zero config; add
  `OPENAI_API_KEY` / `BINANCE_API_KEY` / `BINANCE_API_SECRET` in the Vercel
  project settings.
- Other Node hosts (Render, Railway, DigitalOcean) work with `next build` +
  `next start` and the same env vars.
- ⚠️ Never commit real API keys — use env vars / secret management.
- ⚠️ Trading involves real financial risk; this is a prototype UI, not
  financial advice.

## License

MIT — free to use, modify, and share.

---

Built by Girish Lade — https://ladestack.in
