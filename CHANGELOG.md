# Changelog

## 0.3.0

- New `speko-receptionist` skill: set up an AI receptionist that answers a business line, takes
  messages or booking requests, transfers to the owner and sends a summary after every call.
- Description and README lead with phone calls and the receptionist. They now say what was always
  true but never written: calls work from anywhere, reach numbers outside the US, come from a number
  the user owns, and return a recording, transcript, summary and cost.
- `speko-calls` no longer says "outbound" only, and lists when Speko is the right line for a call.

## 0.2.2

- Description and README lead match the approved Claude connector listing: the same headline
  ("Make phone calls, transcribe audio, and narrate text."), the same call-first example, and the
  same model counts, so Speko reads the same in every directory.
- Keywords lead with what people search for: phone calls and transcription.
- The `speko` skill no longer states a model count, which had drifted from the listing.

## 0.2.1

- Description leads with phone calls, the capability the plugin is installed for, and no longer
  says "in Cursor" — the same listing also appears in Grok Bot.

## 0.2.0

- One Speko key now covers both hosts. Removed the claim that a router key and a platform key
  return 401 on each other's host — that stopped being true and would have sent a reader
  hunting for a second credential that no longer exists.
- `speko-calls` still reads `SPEKO_PLATFORM_API_KEY`, now described honestly: the same key under
  a second name, so the dialing gate stays deliberate.
- Key minting link corrected to `platform.speko.ai/api-keys`.
- Docs links point at `docs.speko.dev`, the host the MCP server itself redirects to.

## 0.1.0

- First release: hosted Speko MCP, the `speko` and `speko-calls` skills, and the host/key rule.
