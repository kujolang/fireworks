# Kujo Fireworks Provider

[![Version](https://img.shields.io/badge/version-0.1.1-black)](https://github.com/kujolang/fireworks/tree/v0.1.1)
[![License](https://img.shields.io/badge/license-MIT-lightgrey)](LICENSE)
[![built with Kujo](https://img.shields.io/badge/built%20with-Kujo-white.svg)](https://github.com/kujolang/kujo)

Fireworks AI inference and hosted-model controls for Kujo.

## Install

The current branch requires Kujo 1.6.0 or newer. Kujo 1.10.0 supports the
injected transport examples in both execution engines.

```bash
kujo run /path/to/kennel/kennel.kujo \
  -- add github:kujolang/fireworks@v0.1.1 \
  --alias fireworks
kujo run /path/to/kennel/kennel.kujo -- install
export FIREWORKS_API_KEY=your-key
```

## 30-second quick start

```kujo
from fireworks import create_client, client_chat

client := create_client({})
request := {
    "model": "accounts/fireworks/models/glm-5p3-flash",
    "messages": [
        {
            "role": "user",
            "content": "Hello from Kujo!"
        }
    ]
}

result := client_chat(client, request)

print(result["data"]["choices"][0]["message"]["content"])
```

## Native API

The native layer preserves Fireworks response fields for chat and embeddings.
`client_models` returns the transport Result from the compatible model-list
endpoint. For a chat request with `"stream": true`, read the buffered SSE
events from `result["events"]`. The SDK normalizes chat text, usage,
finish reason, and tool calls and retains reasoning in raw provider data.

## AI SDK integration

`fireworks_provider({"model": "accounts/fireworks/models/glm-5p3-flash"})` supplies normalized chat and streaming semantics through the compatible driver.

## Authentication and security

Set `FIREWORKS_API_KEY`. Native requests validate HTTPS endpoints and
disable redirects. Native responses redact configured credentials. The SDK
driver declares its bearer and content headers as protected.

## Testing and documentation

```bash
bash scripts/release_quality_gate.sh
bash scripts/verify_installed_package.sh
```

The default gate is deterministic and offline. See [docs/](docs/) for implementation and Contract v1 evidence.
