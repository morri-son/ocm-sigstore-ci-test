# ocm-sigstore-ci-test

End-to-end live test for the **Sigstore (CI)** how-to in
[open-component-model/open-component-model#2591](https://github.com/open-component-model/open-component-model/pull/2591).

## What this exercises

The `.github/workflows/sign.yml` workflow follows the **Sigstore (CI)** tab
of `sign-component-version.md` literally:

1. Workflow declares `permissions: id-token: write`
2. Installs the OCM CLI via the upstream installer
3. Runs `ocm sign cv` against a CTF archive, transferred to `ghcr.io/morri-son/ocm-sigstore-ci-test/...`
4. OCM auto-detects `ACTIONS_ID_TOKEN_REQUEST_TOKEN` and uses GitHub Actions OIDC
5. Public Sigstore (Fulcio + Rekor) issues the cert and logs the entry

If this passes, the docs are accurate. If it fails, the docs need fixing
before #2591 lands.

The component being signed is trivial: a `plainText` resource pointing
at this README. The signature is what's interesting, not the payload.
