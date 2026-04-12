# GoFlight Investor Site

Live at [investors.goflight.ai](https://investors.goflight.ai)

## Files
- `index.html` — Authenticated investor wiki (standalone HTML)
- `GOFLIGHT-BRIEF-2026-04-10.md` — Investor brief document

## Deploy
Push to `main` → GitHub Actions auto-syncs to S3 + invalidates CloudFront cache.

## Manual deploy (emergency only)
```bash
aws s3 sync . s3://investors-goflight.ai/ --delete --exclude ".git/*" --exclude ".github/*" --exclude "README.md"
```
