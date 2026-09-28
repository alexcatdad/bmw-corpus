# Corpus normalization

The workflow caller pins a reviewed full commit of
`alexcatdad/bmw-knowledge`. Review that commit's normalization package, CLI,
reusable workflow, tests, and local fixture smoke before changing the pin.
Application development and acquisition happen in that software project.

This repository has no acquired source files yet. Keep this workflow on its
review branch until a permitted capture and live configuration are ready.
Create a draft PR for the caller; do not merge it as proof of end-to-end collection.

## Enable on the personal development deployment

The software project must be deployed to the identified personal Convex dev
deployment. Set one dedicated base64url random machine secret (32 characters or
longer) on that deployment and in this repository's scoped Actions secrets.
Do not use a GitHub token or staging credential as the callback secret.

From the software checkout, after announcing the exact dev target:

```sh
pnpm exec convex env set PROCESSING_CALLBACK_SECRET \
  --deployment '<personal-dev-name>' --from-file /private/path/to/processing-secret
gh secret set PROCESSING_CALLBACK_SECRET --repo alexcatdad/bmw-corpus \
  < /private/path/to/processing-secret
gh variable set PROCESSING_CALLBACK_URL --repo alexcatdad/bmw-corpus \
  --body 'https://<personal-dev-name>.convex.site/processing/result'
```

The workflow has not been enabled merely by preparing these instructions. Keep
secret values outside Git and logs. The callback is disabled without its secret.
It verifies captured input and normalized result bytes at immutable Git commits
before storing processing success. Live acquisition has its own separate
dedicated MinIO access, corpus-scoped publication token, and source approval.

## Process and inspect

After review and setup, capture/raw pushes to `main` run the pinned CLI. Derived
commits do not retrigger it. The job uses only the corpus-scoped Actions token to
commit `normalized/` and `processing/` outputs. It never fetches new sources or
executes captured HTML. Concurrent branch changes get a bounded non-force
fetch/rebase/push retry; unresolved conflicts stay visible as job failures.

Use the Actions run to inspect errors and manually dispatch the workflow to
retry. Inspect collection and processing separately from the software checkout:

```sh
pnpm collection status --job '<job-id>'
```

For local reproduction, use a clean software checkout at the workflow's pinned
commit and this corpus checkout at the declared input commit:

```sh
pnpm install --frozen-lockfile
pnpm normalize --corpus /absolute/path/to/bmw-corpus --capture '<capture-id>' \
  --processor-revision '<pinned-software-commit>' \
  --input-revision '<corpus-head-commit>' --summary /private/tmp/new-processing-summary.json
```

Identical receipts/output bytes are reusable. Changed files at an existing
capture/processor path are conflicts, not overwrite requests. Existing receipts
retain their original input commit on newer corpus heads. Each result belongs
to a capture's source context; identical raw hashes can have different derived
links. UTF-8 HTML/XHTML produces Markdown; text stays text. Images, layout, and
other losses are declared rather than silently claimed to be preserved.
