# 0003: Use Outlook/Hotmail For The First Inbox

## Status

Accepted

## Context

The first release will process one owner-controlled email account. In the generalized pilot persona, school communication is spread across multiple household inboxes. The product owner chose whichever provider offers the easier first integration; exact household account assignments are not part of this public record.

Microsoft Graph delegated `Mail.Read` access is available for personal Microsoft accounts and does not require administrator consent. Google classifies `gmail.readonly` as a restricted scope; server-side storage or transmission can require restricted-scope verification and a security assessment. Google also limits refresh tokens to seven days while an external app requesting more than basic identity scopes remains in testing.

References:

- [Microsoft Graph permissions reference](https://learn.microsoft.com/en-us/graph/permissions-reference#mailread)
- [Microsoft identity account types](https://learn.microsoft.com/en-us/security/zero-trust/develop/identity-supported-account-types)
- [Gmail API scopes](https://developers.google.com/workspace/gmail/api/auth/scopes)
- [Google OAuth 2.0 authorization](https://developers.google.com/identity/protocols/oauth2)

## Decision

Use one owner-controlled personal Outlook/Hotmail inbox and Microsoft Graph as the first inbox integration. Request delegated read access only and keep provider access inside application-controlled services.

## Consequences

- The first pilot covers approved-source school communication in the connected inbox.
- The first pilot cannot claim coverage for messages available only in other household inboxes.
- Gmail remains a later provider integration.
- Provider-neutral interfaces remain required so Gmail can be added without changing digest behavior.
