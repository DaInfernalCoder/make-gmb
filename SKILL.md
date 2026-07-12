---
name: make-gmb
description: "Build and launch a polished local-business marketing website end to end from only a domain name: infer the brand and offer, create the project in the permanent websites-and-apps folder, design and build the site, source licensed imagery, add a real quote form, publish to GitHub, deploy through Vercel, connect apex and www domains, guide or automate Spaceship DNS, and verify HTTPS. Use when Sumit says he bought a domain, asks to make a website or GMB site, wants a local-service business launched with minimal input, or explicitly invokes make-gmb."
---

# Make GMB

Turn one domain into a credible local-business website and finish the operational launch. Require only the domain. Infer ordinary details, keep unknown facts unstated, and ask only for secrets or decisions that cannot be derived safely.

## Definition of done

Complete all of the following:

- permanent local repository under `/Users/sumit/Documents/websites & apps/<project-slug>`;
- polished responsive site with honest conversion copy and licensed local images;
- working quote form that includes the lead's complete query and phone number;
- clean `main` commit in a dedicated GitHub repository;
- GitHub connected to Vercel for push-to-production deploys;
- production deployment ready;
- apex domain and `www` attached;
- registrar DNS changed and propagated;
- HTTPS and final page content verified through the real custom domain.

A `.vercel.app` URL alone is not completion.

## 1. Resolve the business from the domain

Parse the domain into brand words and likely service category. Browse the domain, exact phrase, competitors, and current DNS when available. Inspect nearby repositories and user context for templates, geography, contact details, provider conventions, and existing credentials.

Choose the audience, primary conversion, credible services, and SEO language. Never fabricate an address, phone number, price, certification, service area, review, guarantee, portfolio claim, or customer count. If the domain has several plausible meanings, choose the strongest commercial interpretation unless that would create a deceptive result.

## 2. Create the project in the right place

Create a sibling repository at:

```text
/Users/sumit/Documents/websites & apps/<project-slug>
```

Do not build an unrelated business inside the active app repository. Do not leave the permanent copy in `/private/tmp`; temporary staging is acceptable only when filesystem permissions require it, followed by a move to the permanent folder before handoff.

## 3. Design before coding

Use the frontend-design skill when available. Define a compact palette, deliberate display/body type pairing, layout thesis, and one subject-specific signature element. Start from existing engineering templates when useful, but reshape them enough that the site belongs to this business.

Use properly licensed stock photos for launch material and record the source in repository documentation. Never present stock photos as the business's past work. Prefer downloaded local assets over fragile hotlinks.

Build a real local-service funnel: hero, services, process, observable-workmanship proof, FAQ, and quote/contact flow. Keep one primary CTA consistent.

## 4. Choose the smallest suitable stack

- Default to dependency-free HTML/CSS/JS for brochure sites.
- Add Vercel functions only for real server behavior such as email delivery.
- Use Next.js only when server rendering, CMS, authentication, or application state justifies it.
- Include semantic headings, metadata, favicon, responsive navigation, keyboard focus, reduced motion, useful alt text, and readable contrast.

Treat the header as part of the hero composition. Verify logo and navigation contrast over the actual hero image at desktop and phone widths; do not combine a light translucent header with white text.

## 5. Wire quote email correctly

Read `references/quote-email.md` before implementing a lead form.

Default notification recipient for Sumit's sites:

```text
gian@caldenmoore.com
```

Include the website/brand name in the subject and body. Include every submitted field, especially phone number, visitor email, vehicle/service selection, location, and the complete free-text query. Set `replyTo` to the lead's email.

Use SMTP credentials only in Vercel environment variables. If the sender uses Gmail or Google Workspace, request the sending mailbox and its app password. Never commit or expose the app password. Keep a transparent direct-email fallback until server delivery is configured and tested.

## 6. Validate locally

For static sites, run:

```bash
python3 scripts/preflight_site.py <project-dir>
```

Serve locally and use a real browser at desktop and phone widths. Verify images and anchors, one H1, title/description, menu and form behavior, no console errors, no mobile overflow, readable header contrast, keyboard focus, and no placeholder/fabricated content.

For forms, test validation and failure states without secrets first. After SMTP env configuration, send one real test and confirm the recipient sees the website name and every query field.

## 7. Publish and deploy

Read `references/provider-runbook.md` before GitHub, Vercel, or DNS work.

Initialize `main`, use a terse Conventional Commit, create a dedicated GitHub repository, and push immediately. Default to public for a marketing site unless source sensitivity requires private. Connect the GitHub repository to Vercel so later pushes deploy automatically.

Deploy production and confirm `READY`. Attach both the apex and `www` hosts.

## 8. Connect Spaceship correctly

For a new Spaceship domain, use the domain's main **Advanced DNS → Nameservers → Change → Custom nameservers** control.

Do not use **Brand nameservers**, **Personal nameservers**, or any screen asking for a host plus IP address; those create glue records and are the wrong place.

Enter the nameservers Vercel currently recommends, normally:

```text
ns1.vercel-dns.com
ns2.vercel-dns.com
```

Save and confirm the custom-DNS warning. If mail or other DNS services already exist, preserve/recreate their records before switching. Use registrar browser automation only when an authenticated session is available; otherwise give the user the exact clicks and resume after they save.

Treat old nameservers immediately after saving as propagation, not a failed change. Poll reasonably; Spaceship documents that propagation can take up to 48 hours. Stop polling when the user asks.

## 9. Verify and hand off

Run Vercel verification for apex and `www`, then:

```bash
python3 scripts/check_live.py example.com "Expected Brand"
python3 scripts/check_live.py www.example.com "Expected Brand"
```

Confirm authoritative nameservers, HTTPS, intended production content, and canonical apex/`www` behavior. Lead the handoff with live status and link the custom domain, GitHub repository, Vercel project, and permanent local folder. State any operational limitation such as an SMTP secret still needed.
