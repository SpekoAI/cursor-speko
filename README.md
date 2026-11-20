# Speko for Cursor and Grok Bot

AI phone calls, an AI receptionist and natural speech synthesis on one account. Say "Call this
restaurant and book a table for two at 7" and your agent places the call, in the US or abroad,
then brings back the transcript, recording and summary. Say "Answer my business line when I
miss a call" and it sets up a receptionist that takes messages or booking requests and sends you a
summary after every call. Say "Read this aloud in a calm voice" and it turns the text into spoken
audio in 100+ voices, so you can hear a voice or a greeting before it goes on a call. It also
transcribes audio. One install gives your agent the Speko platform as MCP tools, plus three
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

**MCP — `https://mcp.speko.ai/mcp`** (OAuth, or your Speko key as `Authorization: Bearer sk_live_…`)

Agents (`agents.create`, `agents.update`, `agents.deploy`, `agents.rollback`, `agents.test_call`),
sessions and calls (`sessions.create`, `sessions.phone.create`, `sessions.transcript.get`,
`sessions.recording.get`, `calls.get`), speech and transcription (`audio.synthesize`,
`voices.list`, `audio.transcribe`), phone numbers, knowledge bases, evals and monitors,
credits and usage, `docs.search` for in-band API answers, and migration helpers for importing an
existing config.

**Skills**

| Skill | Use it for | Credential |
| --- | --- | --- |
| `speko` | Read text aloud, narrate, hear a voice before a call, transcribe audio, choose and justify a model, cap voice spend | None with the plugin's sign-in (MCP tools). `SPEKO_API_KEY` for direct router calls |
| `speko-calls` | Place and follow real phone calls, in the US or abroad, from a shared Speko caller ID or your own number | None with the plugin's sign-in (MCP tools). `SPEKO_PLATFORM_API_KEY`, the same key set deliberately, for direct calls |
| `speko-receptionist` | Answer incoming calls on a business line: messages, booking requests, transfers, call summaries | None — MCP tools with OAuth |

Telephony is a separate skill on purpose. Dialing rings a physical device, costs money and cannot
be recalled, so it reads its own environment variable and confirms the number, the purpose and the
local hour before every call. One Speko key covers both skills, so the second variable is a
deliberate gate rather than a different credential: installing speech support does not by itself
put a calling instruction in play.

**Rule** — `rules/speko.mdc` keeps the agent on the right host for the surface it needs.

## Configuration

| Variable | Needed for | Where |
| --- | --- | --- |
| `SPEKO_API_KEY` | The `speko` skill's direct router calls | [platform.speko.ai/agents/keys](https://platform.speko.ai/agents/keys) |
| `SPEKO_PLATFORM_API_KEY` | The `speko-calls` skill — same key, second name | Same dashboard |

One key covers both hosts. Neither variable is required for the MCP tools, which use OAuth. Only
set the calls variable in an environment where outbound dialing is approved and audited.

## Links

- Docs — <https://docs.speko.ai>
- Benchmarks the routing is built on — <https://speko.com/benchmarks>
- MCP quickstart — <https://docs.speko.ai/quickstart/mcp>

## License

MIT — see [LICENSE](LICENSE).
