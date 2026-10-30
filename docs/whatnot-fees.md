# Whatnot Fee Notes (as of late 2026)

These numbers are approximate and can change. Always verify on Whatnot seller dashboard.

## Commission
- Standard: 8% of item price (not including shipping)
- Sports cards / certain categories: 0% commission on orders over $1,500 in a single order (confirm current threshold)

## Payment Processing
- 2.9% + $0.30 per order
- Charged on the full amount the buyer pays (item + shipping + tax if applicable)

## Effective Rate Example

Item sells for $27 average:
- 8% of $27 = $2.16 commission
- Processing on ~$30 total (item + shipping) ≈ $1.17
- Rough total take: ~$3.33 → ~12.3% effective

On higher average order values the percentage drops because of the fixed $0.30.

## Implications for Sourcing Agent

Fees come off the Whatnot **sell** price, not the price you pay (asking/buy price):

```
whatnot_fees = sell_price × 0.08 + (sell_price + buyer_shipping) × 0.029 + 0.30
net_profit   = sell_price - whatnot_fees - your_shipping_cost - asking_price
margin_pct   = net_profit / asking_price × 100
```

Example: sell $80, buyer shipping $5, your shipping $5, buy $40 → fees $9.17, net profit $25.83, margin 64.6%.
