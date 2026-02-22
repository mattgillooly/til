# Deploying the TIL site (Fly + S3)

This repo deploys Datasette to Fly.io and uses S3 to store `tils.db` and screenshots.

## Prereqs
- A Fly app named `mattgillooly-tils`
- S3 bucket `til.mattgillooly.com` (public read)
- GitHub repo secrets:
  - `FLY_TOKEN`
  - `AWS_ACCESS_KEY_ID`
  - `AWS_SECRET_ACCESS_KEY`

## One-time setup
1. Create the Fly app:
   - `fly apps create mattgillooly-tils`
2. Add the custom domain in Fly and update DNS for `til.mattgillooly.com`.
3. Create and add the GitHub secrets listed above.

## CI deploy flow
On every push to `main`, `.github/workflows/build.yml` will:
1. Build the database.
2. Generate missing screenshots.
3. Upload `tils.db` to S3.
4. Verify S3 is reachable.
5. Deploy to Fly.

## Local deploy (optional)
If you want to deploy from your machine:
1. Install dependencies:
   - `pip install -r requirements.txt`
2. Build:
   - `script/build`
3. Deploy:
   - `script/deploy`
