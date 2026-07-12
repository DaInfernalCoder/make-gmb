---
name: domain-to-live-site
description: "Turn a domain name into a polished, production-ready brochure or lead-generation website end to end: infer the business and brand, research the market, design and build in a new repository, source licensed imagery, QA desktop/mobile/accessibility, commit and publish to GitHub, deploy to Vercel, attach apex and www domains, configure or precisely hand off registrar DNS, and verify the live site. Use when the user says they bought a domain, asks to make or launch a website from a domain, wants a site built and hosted with minimal input, or provides only a domain and expects the rest handled autonomously."
---

# Domain to Live Site

Launch the strongest credible site the domain supports. Treat the domain as the only required input. Infer ordinary details, disclose important assumptions, and ask only when a missing fact would make the result misleading or unsafe.

## Operating contract

- Own the complete path: research, design, implementation, GitHub, deployment, DNS, and live verification.
- Default to a separate project directory and repository. Never add an unrelated site to the current app repository.
- Continue through reversible, in-scope steps without seeking confirmation.
- Never invent addresses, phone numbers, prices, certifications, reviews, customer counts, guarantees, service areas, or “past work.”
- Use licensed stock photography for launch material and label it honestly in repository documentation. Prefer original assets when they exist.
- Make every contact path truthful. Use a real configured form destination when available; otherwise use an explicitly labeled email-app fallback and flag mailbox setup as an operational requirement.
- Do not expose tokens, passwords, provider keys, or registrar credentials in code, git, client JavaScript, logs, or the final response.
- A Vercel preview URL is not completion when the user supplied a custom domain.

## Workflow

### 1. Resolve the brief from the domain

Parse the domain into likely brand words and category. Browse the domain, DNS, exact brand phrase, and local competitors when web access is available. Check nearby repository or user context for ownership, geography, contact details, templates, and deploy conventions.

Choose and record internally:

- concrete business and audience;
- page's single conversion job;
- credible offer and service structure;
- SEO title/description;
- important unknowns that must remain unstated.

If the domain is ambiguous, choose the most commercially coherent interpretation and proceed with transparent placeholder-free general copy. Ask only if competing interpretations would create materially different or potentially deceptive businesses.

### 2. Set a distinct design direction

Use the frontend-design skill when available. Before coding, define a compact system: 4–6 named colors with hex values, display/body typefaces, layout thesis, and one business-specific signature element. Reject generic SaaS gradients, decorative metrics, fake badges, and recycled section numbering unless the subject truly calls for them.

Use existing local starters only as engineering foundations. Restyle and restructure them enough that the result belongs to this business.

### 3. Select the smallest suitable stack

- Use dependency-free HTML/CSS/JS for a fast brochure site with simple interactions.
- Use Next.js or another existing project stack only when server routes, CMS, authenticated features, or a real integration justify it.
- Keep launch images local to the deployment; do not rely on random-image endpoints or fragile hotlinks.
- Include responsive navigation, accessible focus states, reduced-motion handling, semantic headings, useful alt text, favicon, metadata, and a clear CTA.

Create the project outside the unrelated working repository. If the preferred permanent path is unavailable, build in a writable temporary path, publish it, and report the local path honestly.

### 4. Build for conversion without fabrication

Include only sections supported by the inferred business: hero, offer/services, process, proof through observable workmanship rather than fake social proof, FAQ, and contact/quote flow. Write from the visitor's point of view and make the primary CTA consistent throughout.

When no verified phone, address, service area, rate, or business email exists, omit it. It is better to say “request a quote” than fabricate a starting price.

### 5. Validate locally

Run `scripts/preflight_site.py <project-dir>` for static sites. Then serve locally and use a real browser at desktop and phone widths.

Verify:

- all local images and internal anchors load;
- one H1 and a useful title/description exist;
- no console/page errors or horizontal mobile overflow;
- menu, accordion, and form behavior work;
- images appear during normal scrolling;
- keyboard focus and reduced motion are usable;
- no TODO, lorem ipsum, broken placeholder, unverified claim, or secret is present.

Fix discovered issues and rerun the relevant checks.

### 6. Publish deliberately

Initialize `main`, commit the full verified site with a terse Conventional Commit, and create a repository named from the brand/domain. Default to public for a marketing site unless the user or local policy indicates private. Push immediately.

Prefer authenticated GitHub CLI. If an in-sandbox auth check fails, retry outside restricted networking before concluding credentials are invalid.

### 7. Deploy to Vercel

Read `references/provider-runbook.md` before deployment or DNS work. Deploy production, not only preview. Use the current installed CLI explicitly when multiple versions exist. Attach both the apex domain and `www` unless the user requested otherwise.

Do not claim launch success until the deployment reports `READY`.

### 8. Configure DNS and verify the real domain

Inspect Vercel's domain verification output for exact records. Apply them through an authenticated registrar API or browser session if available and authorized. Preserve unrelated mail and verification records.

If registrar access is unavailable, give the user the exact record operations and the provider screen to use. This is the only acceptable manual handoff; keep the goal active or blocked rather than calling the custom-domain launch complete.

After changes, poll within reasonable DNS propagation time. Use `scripts/check_live.py <domain> [expected-title-text]` plus Vercel verification. Confirm:

- apex and `www` resolve;
- HTTPS is valid;
- the intended production deployment is served;
- the final title/content is present;
- one hostname redirects or canonically resolves as intended.

### 9. Hand off concisely

Lead with live status. Link the custom domain, GitHub repository, and Vercel project/deployment. State QA completed, any honest operational limitation (for example an unprovisioned mailbox), and the exact remaining blocker if DNS could not be changed.

Never say “done” when only the repository or preview deployment exists.
