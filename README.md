# GoFlight Investor Site

Live at [investors.goflight.ai](https://investors.goflight.ai)

## Files
- `index.html` — Authenticated investor wiki (standalone HTML, inline CSS)
- `assets/` — Brand logo and Flyn imagery
- `GOFLIGHT-BRIEF-2026-04-10.md` — Investor brief document

## Deploy

**There is no auto-deploy.** Pushing to `main` does not update the live site. The previous GitHub Actions workflow was removed (commit `7787f83`); the only path to production is to run the sync manually.

```bash
cd ~/repos/investors && aws s3 sync . s3://investors-goflight.ai/ \
  --delete --exclude ".git/*" --exclude ".github/*" --exclude "README.md"
```

CloudFront cache invalidation, if needed:

```bash
aws cloudfront create-invalidation --distribution-id <DIST_ID> --paths "/*"
```
