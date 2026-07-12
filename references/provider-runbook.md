# Provider runbook

## Preflight

Check tools and authenticated identities before mutating external state:

```bash
gh auth status
vercel whoami
```

Restricted environments can make valid sessions appear broken. Retry important auth and network checks with the environment's approved escalation flow.

Never print token values. Listing environment variable names with redacted values is acceptable when diagnosing credential availability.

## GitHub

From the verified project directory:

```bash
git init -b main
git add .
git commit -m "feat: launch <brand> website"
gh repo create <repo-slug> --public --source=. --remote=origin --push
```

Use `--private` if user policy or source sensitivity requires it. Do not publish `.env*`, provider files, credentials, or local deployment metadata.

## Vercel

Deploy from the project root:

```bash
vercel --prod --yes
vercel domains add example.com <project>
vercel domains add www.example.com <project>
vercel domains verify example.com
vercel domains verify www.example.com
```

If the command resolves to an old CLI, locate current installations with `command -v -a vercel` and use the current absolute path. A successful deploy must report `READY` or an equivalent production-ready state.

## External DNS

Use records returned by the current `vercel domains verify` output; do not rely on memorized IPs because Vercel can return project-specific recommendations.

Typical pattern:

- apex: one or more `A` records named `@`;
- `www`: a `CNAME` to a project-specific `vercel-dns` hostname;
- alternative: change nameservers to Vercel only when the user wants Vercel to manage the whole DNS zone.

Prefer record changes over nameserver replacement when the existing zone contains mail, verification, or other service records. Remove only conflicting `A`, `AAAA`, or `CNAME` records for the exact host being attached.

Registrar access can come from an authenticated provider API, CLI, or browser session. Domain ownership alone does not create registrar access. If no authenticated path exists, provide the exact records and wait for the user to apply them.

## Propagation and verification

DNS may update quickly but can remain cached. Re-run Vercel verification, then check HTTPS through the actual hostname. Do not test only the `.vercel.app` alias.

Verify both hosts and record the canonical behavior:

```bash
python3 scripts/check_live.py example.com "Expected Brand"
python3 scripts/check_live.py www.example.com "Expected Brand"
```

Treat TLS errors, registrar parking pages, `404`, and an old deployment as incomplete.
