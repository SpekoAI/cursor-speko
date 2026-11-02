---
name: speko-receptionist
description: Set up an AI phone receptionist through Speko that answers incoming calls for a small business. It answers on its own number or on the owner's existing business line through call forwarding, takes messages, takes booking requests or escalates emergencies, transfers to the owner, speaks English, Spanish or French, and emails or texts the owner a summary after every call. Use when asked to answer calls, set up a receptionist or answering service, handle missed calls, get a business phone number, or take messages. Buying a number costs money, so it states the price and gets the owner's OK first. For calls the user wants placed, use the speko-calls skill.
---

# Speko receptionist

A receptionist answers calls that come in. It is an agent linked to a phone number, with a
greeting that says it is an AI, a set of facts about the business, and a transfer to the owner.

Everything here runs through the Speko MCP tools that ship with this plugin. No key is needed
beyond the OAuth sign-in.

## Set it up

1. **`receptionist.setup`** with `business_name`, `owner_phone` (E.164), `mode` and `languages`.
   - `mode`: `message_taking` (default), `booking_requests`, or `emergency_escalation`
     (also needs `backup_phone`).
   - `languages`: up to three of `en`, `es`, `fr`.
   - Pass `website_url` when the business has a site; Speko reads it for facts.
   - Nothing is live yet. The result has a preview of what it will say, and `missingFacts`.
2. **Ask the owner the `missingFacts` questions** and send the answers to
   `receptionist.update_facts`.
3. **`agents.test_call`** to hear it. An AI caller talks to the receptionist; no phone rings.
   Show the owner the transcript.
4. **`receptionist.go_live`** to get a number and deploy.
   - `number_source: "new"` buys a US or Canadian number, optionally by `area_code`.
     **It costs $1 setup plus $2 a month from prepaid credits, and calls cost $0.09 per
     connected minute. Say this and get the owner's OK before calling it.**
   - `number_source: "existing"` reuses a number the workspace already owns and buys nothing.
   - To keep the owner's current business line, pass `owner_business_number`,
     `owner_carrier` and `owner_line_type`. The result has the call-forwarding code to dial and
     the code that undoes it. `forwarding_mode: "overflow"` (default) sends only missed or busy
     calls; `"all"` sends every call.
   - `notify_email` and `notify_sms_number` set where call summaries go.
   - `status: "action_required"` means nothing was bought; `requiredAction` says what the
     owner must do (for example business verification, or adding credits).
5. **`receptionist.verify_forwarding`** after the owner dials the forwarding code.

## Change or stop it

- `receptionist.settings_update` changes the greeting, voice, notifications and similar settings.
- `receptionist.pause` stops answering and keeps the number. The number is still billed.
- `receptionist.resume` turns it back on.
- `receptionist.cancel` stops it and releases the number. Confirm with the owner first.

## Rules

- Never buy a number without stating the price and getting an explicit yes.
- Never enable `forwarding_mode: "all"` unless the owner asked for every call to go to the AI.
- The greeting always says the caller is talking to an AI. Do not remove that.
- A number from the owner's own carrier, in any country, can be connected with
  `phone_numbers.sip_connections.create` and `phone_numbers.import` with an `agent_id`.
