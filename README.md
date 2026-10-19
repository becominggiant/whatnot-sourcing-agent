# Whatnot Sourcing Agent

AI-powered sourcing pipeline for Whatnot sellers. Continuously monitors eBay, Facebook Marketplace, OfferUp, and liquidation sites for underpriced sports cards, TCG, graded, and sealed product. Calculates true margin after Whatnot fees and alerts you only on high-profit opportunities.

## Pipeline Overview

1. **Triggers** — Cron every 30 minutes during store hours + webhooks from saved searches
2. **Scrape & Filter** — Pull listings matching target categories under your price cap
3. **Brain (Claude + MCP)** — Pull recent sold comps, compute margin after ~12% Whatnot cut, only flag deals >40% profit
4. **Rank & Alert** — Rank by margin × distance, push top 10 to Telegram/Discord with photo + link
5. **Inventory Tracker** — Drop saved items into Airtable with status (watching / bought / listed / sold)

## Cost Stack (monthly)

| Service          | Approx Cost     |
|------------------|-----------------|
| eBay API         | Free (5k calls/day) |
| Apify (FB/OfferUp) | $5–20          |
| Claude API       | $10–30          |
| n8n (self-host)  | Free            |
| n8n Cloud        | $24             |
| Telegram         | Free            |
| **Total**        | **$40–75**      |

## What It Does NOT Do

- Physical pickup / buying (you still have to go get the item)
- Live stream hosting (keep that human)

## Quick Start

1. Clone this repo
2. Set up n8n (self-hosted or cloud)
3. Import the workflow JSON from `/n8n`
4. Add your API keys (eBay, Claude, Apify, Telegram bot token)
5. Configure your target categories, max price, and minimum margin %
6. Point Airtable base + table
7. Go live

## Project Structure

```
whatnot-sourcing-agent/
├── README.md
├── docs/
│   ├── pipeline.md          # Full stage-by-stage explanation
│   └── whatnot-fees.md      # Current fee structure notes
├── n8n/
│   └── sourcing-workflow.json  # Importable n8n workflow (skeleton)
├── prompts/
│   └── margin-evaluator.md     # Claude system prompt for comps + margin
└── config/
    └── example.env             # Required environment variables
```

## License

MIT — use it, modify it, sell with it.
