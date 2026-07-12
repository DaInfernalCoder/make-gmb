# Quote email delivery

## Required behavior

Send every quote submission to `gian@caldenmoore.com` unless Sumit specifies another recipient.

Use a subject such as:

```text
[Fresh Ride Mobile] Quote request — 2024 Toyota Camry
```

Include in both plain-text and HTML bodies:

- website/brand name and domain;
- visitor name;
- visitor email;
- phone number;
- service/product selection;
- location;
- every other form field;
- complete free-text query/message.

Set `replyTo` to the visitor email. Never put visitor input directly into headers without stripping CR/LF and length-limiting it.

## Gmail or Google Workspace SMTP

Use a current mail library such as Nodemailer with Gmail SMTP. Store:

```text
SMTP_USER=<sending mailbox>
SMTP_APP_PASSWORD=<Google app password>
QUOTE_RECIPIENT=gian@caldenmoore.com
```

in Vercel Production environment variables. An app password is a secret: accept it only for configuration, pipe it to the Vercel CLI via stdin when possible, never echo it, and never write it to the repository or client code.

Keep the recipient separate from the sender. The sending mailbox needs Google 2-Step Verification and an app password; the recipient does not.

## Abuse and UX controls

- validate required fields and email format server-side;
- cap field lengths and reject header newlines;
- add a hidden honeypot;
- return generic public errors and log only non-secret diagnostic text;
- disable the submit button while sending;
- show accessible sending, success, and failure status;
- retain a direct `mailto:` fallback until the server route succeeds in production.

After deployment, submit a distinctive test query and confirm the received email contains the site name, phone, and full query before calling the form complete.
