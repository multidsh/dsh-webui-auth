# Changelog

## 0.3.7

Fix the post-login redirect on deployments whose reverse proxy overwrites `Host`.

- `postLoginRedirect()` now prefers the proxy-supplied `X-Forwarded-Host` header when
  choosing the redirect authority, falling back to `Host` only when that header is
  absent or malformed. A proxy that pins `Host: localhost` (a common nginx recipe, and
  required for the core loopback trust fence) previously produced
  `http://localhost/?token=...` instead of the public domain.
- The forwarded value is validated as a bare `host[:port]` authority; values carrying
  credentials, path, query or fragment are discarded, so the change adds no open-redirect
  surface.
- Behavior without the header is byte-for-byte identical to 0.3.6.

## 0.3.6 and earlier

See the git history of the upstream package `dsh-webui-auth` (MIT, © 2026 Yuuz12).
