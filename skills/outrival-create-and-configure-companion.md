---
name: Create and configure an OutRival companion
description: Create an AI companion (assistant) and configure its voice, SMS, and chat modalities.
api: openapi/outrival-v1-openapi-original.json
operations: [AssistantsController_create, VoiceController_create, SmsController_create, ChatController_create, ThemeController_create]
---

# Create and configure an OutRival companion

Authenticate every request with the `X-API-Key` header (get a key at
https://builder.outrival.com/api-keys). Base URL: `https://api.outrival.com`.

## Steps

1. **Create the companion** — `POST /rest/v1/assistants` (`AssistantsController_create`)
   with a `CreateAssistantDto` body. Capture the returned assistant `id`.
2. **Configure voice** — `PATCH /rest/v1/assistants/{assistantId}/voice`
   (`VoiceController_create`) to set the voice provider/model and background sound.
3. **Configure SMS** — `PATCH /rest/v1/assistants/{assistantId}/sms`
   (`SmsController_create`).
4. **Configure chat** — `PATCH /rest/v1/assistants/{assistantId}/chat`
   (`ChatController_create`).
5. **Configure appearance** — `PATCH /rest/v1/assistants/{assistantId}/theme`
   (`ThemeController_create`) for the shareable-demo / widget look.

## Notes

- List existing companions with `GET /rest/v1/assistants` (`AssistantsController_findAll`)
  or start from a template via `GET /rest/v1/assistants/templates`.
- Errors return plain JSON with HTTP 400 (validation / not found) or 404. See
  `errors/outrival-problem-types.yml`.
- No idempotency key is supported; do not blind-retry create calls.
