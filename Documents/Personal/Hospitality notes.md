```
Profile auto-create on first login: Add Better Auth hook to create guest_profile immediately after first successful auth (today it’s created on
    first update).
  - Admin CRUD UI for profiles: Minimal list/search/edit in the admin area.
  - Email delivery for Magic Link: Wire SMTP/Resend, add rate limiting, SPF/DKIM/DMARC, and templates.
```

Small client utils in apps/web/src/utils/api.ts (thin wrappers around oRPC if desired)