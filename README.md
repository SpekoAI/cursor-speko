# Speko for Cursor

Voice AI inside Cursor. One install gives the agent the Speko platform as MCP tools, plus two
skills and a rule that teach it to use them correctly.

Speko routes every leg of a voice pipeline — speech-to-text, LLM, text-to-speech — from its own
benchmark readings rather than a hardcoded vendor: measured latency, measured quality, published
price, per language, with automatic failover. Model selection can be justified before a request
is spent.

## Install

Add it from the [Cursor Marketplace](https://cursor.com/marketplace), or install this repository
directly. On first use Cursor completes an OAuth sign-in against `mcp.speko.ai` — no key needs to
be pasted for the MCP tools.

## What you get

**MCP — `https://mcp.speko.ai/mcp`** (OAuth, or a platform key as `Authorization: Bearer sk_live_…`)

Agents (`agents.create`, `agents.update`, `agents.deploy`, `agents.rollback`, `agents.test_call`),
sessions and calls (`sessions.create`, `sessions.phone_create`, `sessions.transcript_get`,
`sessions.recording_get`, `calls.get`), phone numbers, knowledge bases, evals and monitors,
credits and usage, `docs.search` for in-band API answers, and migration helpers for importing an
existing config.

**Skills**

| Skill | Use it for | Credential |
| --- | --- | --- |
| `speko` | Transcribe audio, synthesize speech, choose and justify a model, cap voice spend | `SPEKO_API_KEY` (router) |
| `speko-calls` | Place and follow real outbound phone calls | `SPEKO_PLATFORM_API_KEY` (platform) |

Telephony is a separate skill on purpose. Dialing rings a physical device, costs money and cannot
be recalled, so it carries its own higher-impact credential and confirms the number, the purpose
and the local hour before every call. Installing speech support never grants calling ability.

**Rule** — `rules/speko.mdc` keeps the agent on the right host with the right key, since a router
key and a platform key both look like Speko keys and each returns 401 on the other's host.

## Configuration

| Variable | Needed for | Where |
| --- | --- | --- |
| `SPEKO_API_KEY` | The `speko` skill's direct router calls | [platform.speko.dev/api-keys](https://platform.speko.dev/api-keys) |
| `SPEKO_PLATFORM_API_KEY` | The `speko-calls` skill | Same dashboard, platform scope |

Neither is required for the MCP tools, which use OAuth. Only supply the platform key in an
environment where outbound dialing is approved and audited.

## Links

- Docs — <https://docs.speko.ai>
- Benchmarks the routing is built on — <https://benchmarks.speko.ai>
- MCP quickstart — <https://docs.speko.ai/quickstart/mcp>

## License

MIT — see [LICENSE](LICENSE).
