# Whatnot Sourcing Agent — Full Pipeline

## Stage 1: Triggers

- Cron job every 30 minutes during your active sourcing hours (e.g. 8am–9pm local)
- Optional webhooks from eBay saved searches, Facebook Marketplace alerts, OfferUp, and liquidation pallet sites
- Can also be triggered manually from Telegram/Discord with a /scan command

## Stage 2: Scrape & Filter

Sources:
- eBay (official API preferred — free tier is generous)
- Facebook Marketplace (via Apify actor)
- OfferUp (via Apify)
- Liquidation / pallet sites (custom scrapers or Apify)

Filter rules (configurable):
- Categories: sports cards, TCG, graded cards, sealed product
- Max asking price (e.g. $150)
- Minimum seller rating / feedback
- Location radius preference (optional)
- Exclude keywords (lots of commons, damaged, etc.)

Normalize every listing into a standard shape:
- title
- price
- location / distance
- photos (first 1–3)
- seller rating
- listing URL
- source (ebay / fb / offerup / etc.)

## Stage 3: Brain — Margin Evaluation

For each surviving listing:
1. Extract key identifiers (player/set/year/grade if present)
2. Query recent sold comps (eBay sold listings + other sources)
3. Estimate realistic sell-through price on Whatnot
4. Subtract estimated Whatnot fees (~12% effective: 8% commission + ~2.9% + $0.30 processing)
5. Subtract estimated shipping cost and your time
6. Calculate true profit margin

Only pass listings that clear your minimum margin threshold (default 40%).

## Stage 4: Rank & Alert

Rank remaining deals by:
`score = estimated_profit_margin × (1 / (1 + distance_miles))`

Push the top 10 (or top N) to:
- Telegram bot (recommended for speed)
- Discord channel
- Optional email summary once per day

Each alert contains:
- Photo
- Title + asking price
- Estimated Whatnot net after fees
- Estimated profit $
- Distance / location
- Direct link
- One-tap reply buttons: Save / Skip / Bought

## Stage 5: Inventory Tracker

Everything you mark "Save" or "Bought" lands in Airtable (or Notion / Google Sheet):

| Field          | Purpose                          |
|----------------|----------------------------------|
| Title          | Item name                        |
| Source URL     | Original listing                 |
| Asking Price   | What you might pay               |
| Est. Margin    | Calculated                      |
| Status         | watching / bought / listed / sold |
| Date Added     | Timestamp                        |
| Notes          | Free text                        |
| Tracking #     | After purchase                   |

Optional: daily digest of items that are about to expire or have price drops.

## Recommended Stack

- Orchestration: n8n (self-hosted preferred for cost)
- LLM: Claude (via Anthropic API) with MCP connectors if available
- Scraping: eBay official API + Apify for Marketplace/OfferUp
- Alerts: Telegram Bot API
- Database: Airtable (easy UI) or Postgres if you want to self-host everything
- Optional: Discord webhook as secondary alert channel
