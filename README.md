# GoFlight Investor Site

Live at [investors.goflight.ai](https://investors.goflight.ai)

## Files
- `index.html` — Authenticated investor wiki (standalone HTML, inline CSS)
- `assets/` — Brand logo and Flyn imagery
- `GOFLIGHT-BRIEF-2026-04-10.md` — Investor brief document

## Deploy

**There is no auto-deploy.** Pushing to `main` does not update the live site. The previous GitHub Actions workflow was removed (commit `7787f83`); the only path to production is to run the sync manually.

Requires the `goflight-production` AWS profile (`aws sso login --profile goflight-production` first).

```bash
cd ~/repos/investors && AWS_PROFILE=goflight-production aws s3 sync . \
  s3://goflight-investors-prod-138893339755/ \
  --delete --exclude ".git/*" --exclude ".github/*" --exclude "README.md"
```

Then invalidate the CloudFront cache so the change is visible immediately:

```bash
AWS_PROFILE=goflight-production aws cloudfront create-invalidation \
  --distribution-id E1CCEIUELJV5XB --paths "/*"
```

## Infrastructure

- **S3 bucket:** `goflight-investors-prod-138893339755` (account `138893339755`, us-east-1)
- **CloudFront distribution:** `E1CCEIUELJV5XB` (alias: `investors.goflight.ai`)
- **Origin:** S3 website endpoint (`*.s3-website-us-east-1.amazonaws.com`)
