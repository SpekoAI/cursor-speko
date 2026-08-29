# Changelog

## 0.2.0

- One Speko key now covers both hosts. Removed the claim that a router key and a platform key
  return 401 on each other's host — that stopped being true and would have sent a reader
  hunting for a second credential that no longer exists.
- `speko-calls` still reads `SPEKO_PLATFORM_API_KEY`, now described honestly: the same key under
  a second name, so the dialing gate stays deliberate.
- Key minting link corrected to `platform.speko.ai/api-keys`.

## 0.1.0

- First release: hosted Speko MCP, the `speko` and `speko-calls` skills, and the host/key rule.
