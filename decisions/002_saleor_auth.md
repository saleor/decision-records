# Saleor authorization

Status: accepted

Summary: What's our take on Saleor authorization, how much we'd like to invest in it and what does it depend on?


## Current status

Saleor Cloud users can use login & password to sign in to Dashboard. We also have an OIDC plugin. There was also the concept of Auth API or External Auth API mentioned in a few places. This document is going to outline the general direction and approach of what we want to do with authorisation.

## TL;DR
✨ The general recommendation for our community is to use external authorisation services through OpenID Connect (OIDC).

## Saleor’s builtin auth

### Present state

Saleor's login + password is a stopgap solution and is limited to the absolute minimum as we expect community to use external auth. 

**What about MFA, passkeys and all that jazz?**

We don't support MFA and/or passkeys. This is expected and a known limitation.

**What about preventing password reuse?**

Saleor is not tracking previous passwords, as those could leak. Preventing password reuse and forcing password rotation are anti-patterns frowned upon in the security industry. The problem of unauthorized access is best solved by passwordless access (passkeys) or multi-factor authentication.

**Future state of builtin auth**

In the long run we will want to invest in Auth API through WebAuthn. WebAuthn ups the game by moving to public certificate-based security. It natively supports physical tokens, virtual tokens, and—most importantly—passkeys, the current gold standard of protection, locking private keys behind biometric gates.

There is no timeline of introducing this change. It will probably depend on PCI DSS requirements.

### Saleor’s recommendation: external auth

### Present state: OIDC Plugin

We have an OIDC Plugin our clients are using. We recommend to use it whenever possible. It might have limitations so it might not cover complex permission/user group cases. In general we would like to fix bugs and avoid building more features into it.

But if any of our cloud clients is blocked we will probably reconsider depending on the case.

Related docs:

https://docs.saleor.io/developer/app-store/plugins/oidc

### Future state: External Auth API

In the future we would like to move OIDC to be part of Saleor API. This means we will deprecate the plugin and the responsible bits related to external authentication will be moved to live as a first party citizen in the saleor/saleor repo.

Related:

[[RFC] User API for integrators · saleor saleor · Discussion #11800](https://github.com/saleor/saleor/discussions/11800)