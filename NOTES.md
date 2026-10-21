# CI Security Drill — Workshop Checklist

## Run order
1. Open the repo's **Actions** tab and locate the **CI Security Drill** workflow.
2. Confirm it has **no push/pull_request triggers** — it can only be started manually via **Run workflow** (workflow_dispatch). This is deliberate: it demonstrates the principle of least privilege for trigger scope.
3. Trigger the workflow manually from the Actions tab (or via API).
4. Watch the live logs for the job steps: writing `run-report.txt`, then uploading the artifact.
5. When the run finishes, open the run summary and inspect the **run-report** artifact (download it and show the one-line contents).

## What to watch for
- **Trigger hygiene:** manual-only dispatch — no automatic execution on push or PR, so nothing runs without a human decision.
- **Principle of least privilege:** the job has no `permissions:` block beyond defaults; discuss what tokens the job gets by default and why you'd scope them.
- **Secrets:** point out that no secrets are referenced — a good baseline. Never paste tokens into workflow files or logs.
- **Artifact handling:** artifacts inherit repo visibility; don't upload anything sensitive to public repos.
- **Untrusted input:** discuss `pull_request_target` dangers and script injection via untrusted context in `run:` blocks (e.g., `${{ github.event... }}`).

## Cleanup reminder
- Delete this drill repository after the workshop.
- Delete the workshop gist.
- Close out the follow-up issue ("Workshop follow-ups: tear down the drill repo").
- Living notes live in the gist, not in the repo.
