# Fireworks repository hardening

Reviewed public main `101c9f2` and the installed `v0.1.1` tag on
2026-11-26. Scope covered all native operations, the pure AI SDK driver,
provider transport and response contracts, package exports, offline gates,
examples, and release metadata.

- Native chat, embeddings, and model listing now use the same HTTPS and
  bearer checks, finite timeout, and redirect policy. Model listing retains
  its public transport Result. Successful inference requires a JSON object
  or a complete event stream. Configured credentials are redacted from
  response data, raw error bodies, and stream fragments.
- Chat streaming parses fragmented SSE with CRLF or LF and verifies the
  documented completion marker. The SDK driver retains prepared reasoning,
  multimodal messages and tool continuations. It normalizes indexed tool
  fragments, terminal usage, finish reason and documented cache/reasoning
  counts. The driver also interprets structured validation errors.
  [Chat completions](https://docs.fireworks.ai/api-reference/post-chatcompletions),
  [tool calling](https://docs.fireworks.ai/guides/function-calling.md),
  [reasoning](https://docs.fireworks.ai/guides/reasoning.md).
- The current example model follows the official serverless quickstart.
  [Fireworks quickstart](https://docs.fireworks.ai/getting-started/quickstart.md).

Four existing cases passed at baseline. Six additional cases failed against
the baseline and passed on released Kujo 1.5.0 and 1.10.0 with pinned AI SDK
1.1.0. All ten also passed on 1.10.0 with the current AI SDK checkout. Kujo
1.4.0 passed the native tests and lost a raw nested stream choice through the
SDK, so the manifest minimum is 1.5.0. A clean candidate archive produced
identical output in both 1.10.0 engines and passed package examples' static
checks. Kennel installed and reinstalled the public `v0.1.1` tag plus the
pinned SDK, validated the manifest, and passed its installed export test.

On Intel macOS, five alternating 5,000-event runs with released Kujo 1.5.0
produced identical event digests and medians of 3,931.408 ms at baseline and
120.740 ms with the new parser. Seven 2,500-event runs with released 1.10.0
matched event digests and measured 49.730 ms at baseline and 54.763 ms with
input and completeness validation.

The tests use injected transport responses. The repository has no hosted
workflow. Provider requests, including paid inference, were outside offline
verification.
