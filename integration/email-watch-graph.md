# Email Watch - Microsoft Graph

How to set up a PaperTrail **Email Account** to import mail from a Microsoft 365 mailbox over the
Microsoft Graph API (app-only).

---

## PaperTrail Email Account fields

| Field | Value                            | Notes |
|---|----------------------------------|---|
| **URL** | `https://graph.microsoft.com`                | Not used by the Graph store. Set to any placeholder. |
| **Port** | `443`                            | Not used by the Graph store. Set to any placeholder. |
| **Type** | `Graph`                          | Selects the Graph store (`graphstore`) instead of IMAP/POP3. |
| **Username** | The `email address` to read from | e.g. `invoices@contoso.com`. This is the mailbox Graph reads and deletes from (`/users/{username}/…`). |
| **Password** | The `client secret`              | The app registration's client secret value (not the secret id). |
| **Advanced** | `tenantId=xxxx`<br>`clientId=xxxx` | Entra tenant id and app registration (application/client) id, passed through as properties. |

> **URL and Port are ignored.** The Graph store talks to `https://graph.microsoft.com` and
> authenticates against `https://login.microsoftonline.com/`. URL/Port only exist because the
> Email Account Dialog requires them; their values have no effect on the inner workings of the mail import.

### Advanced field

The Advanced field carries the per-account properties. Provide both:

```
tenantId=00000000-0000-0000-0000-000000000000
clientId=11111111-1111-1111-1111-111111111111
```

These map to `ms.graph.tenantId` and `ms.graph.clientId`. Together with the **Password**
(`ms.graph.clientSecret`) and **Username** (target mailbox), they are everything the app-only
client-credentials flow needs.

---

## How the fields map to config

| Account field | Internal property | Purpose |
|---|---|---|
| Username | — (target mailbox) | Mailbox to read and import from |
| Password | `ms.graph.clientSecret` | App registration client secret |
| Advanced → `clientId` | `ms.graph.clientId` | App registration (application) id |
| Advanced → `tenantId` | `ms.graph.tenantId` | Entra tenant id |

---

## Azure / Entra prerequisites

The mailbox import uses the **app-only (client-credentials) flow**, so the app registration — not a
user — is granted access. Delegated permissions are ignored.

1. **Register an app** in Entra ID (Azure AD). Note its **Application (client) id** and
   **Directory (tenant) id** → these go in the Advanced field.
2. **Create a client secret** (Certificates & secrets → New client secret). Copy the secret
   **value** immediately → this is the account **Password**.
3. **API permissions** → Microsoft Graph → **Application** permissions → add **`Mail.ReadWrite`**.
   - `Mail.ReadWrite` is required because consumption is by **deletion** — handled messages are
     deleted (moved to Deleted Items) on the server, not just marked read.
4. **Grant admin consent** for the permission (the token's `roles` claim must appear, or Graph
   calls return 403).
5. The target **mailbox** (Username) must be a **licensed Exchange Online mailbox**.
6. *(Optional, recommended)* If an **Application Access Policy** restricts which mailboxes the app
   can touch, scope it to include this app + this mailbox.

---

## Setup checklist

- [ ] App registered; client id and tenant id recorded.
- [ ] Client secret created; value copied.
- [ ] `Mail.ReadWrite` **Application** permission added **and admin-consented**.
- [ ] Target mailbox is a licensed Exchange Online mailbox.
- [ ] PaperTrail account: Type = `Graph`, URL = `login.microsoft`, Port = `443`.
- [ ] Username = email address.
- [ ] Password = client secret value.
- [ ] Advanced = `tenantId=…` and `clientId=…`.

---

## System-level settings (not per-account)

These are environment-wide system properties, **not** entered on the account. Defaults are usually
fine; set them only if your environment requires it. They can be added to the `papertrail.properties` file.

| Property | Default | Purpose |
|---|---|---|
| `ms.graph.authority` | `https://login.microsoftonline.com/` | MSAL authority host |
| `ms.graph.scope` | `https://graph.microsoft.com/.default` | Token scope (app permissions) |
| `ms.graph.max.messages` | `1000` | Max messages loaded per poll (newest-first) |
| `ms.graph.proxy.host` | — | Outbound proxy host (enables proxy when set) |
| `ms.graph.proxy.port` | — | Proxy port |
| `ms.graph.proxy.user` | — | Proxy username (optional) |
| `ms.graph.proxy.password` | — | Proxy password (optional) |

---

## Troubleshooting

| Symptom | Likely cause |
|---|---|
| 401 / token request fails | Wrong client secret (Password), wrong tenantId, or expired secret. |
| 403 on mailbox calls | Admin consent not granted, or an Application Access Policy excludes the mailbox. |
| 404 / mailbox not found | Username is not the mailbox address, or mailbox is unlicensed. |
| Messages re-imported | Deletion (consumption) failing — confirm `Mail.ReadWrite`, not `Mail.Read`. |
| Connection times out | Proxy required but `ms.graph.proxy.*` not set. |
| Error on Admin Section for Email Account / Import  | Database table email_account still has records where accounttype = 'HTTPS' |
