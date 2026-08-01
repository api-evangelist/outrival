---
name: Initiate an outbound phone call
description: Place an outbound phone call with a companion and retrieve the conversation logs.
api: openapi/outrival-v1-openapi-original.json
operations: [VapiController_phoneCallInitiate, AssistantLogsController_logs, AssistantLogsController_log]
---

# Initiate an outbound phone call

Authenticate with the `X-API-Key` header. Base URL: `https://api.outrival.com`.

## Steps

1. **Start the call** — `POST /rest/v1/call/phone` (`VapiController_phoneCallInitiate`)
   with a `CreatePhoneCallConfiguration` body (the target assistant/companion and phone
   number). A 400 is returned when the assistant is not found or the organization id is invalid.
2. **Attach metadata (optional)** — pass a `metadata` object (e.g. an encoded `userId`) so it is
   echoed back on webhooks and function calls without being visible to the LLM. See
   `conventions/outrival-conventions.yml`.
3. **Read the logs** — `GET /rest/v1/assistants/{assistantId}/logs`
   (`AssistantLogsController_logs`) to list conversations, then
   `GET /rest/v1/assistants/{assistantId}/log/{logId}` (`AssistantLogsController_log`) for one.

## Notes

- To receive real-time updates instead of polling, configure a webhook (Webhook URL + Secret)
  and verify the `x-signature` HMAC-SHA256 header on each `status-changed` /
  `conversation-updated` / `function-call` event. See `asyncapi/outrival-webhooks.yml`.
