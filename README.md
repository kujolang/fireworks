# Kujo Fireworks Provider

[![Version](https://img.shields.io/badge/version-0.1.1-black)](https://github.com/kujolang/fireworks/releases/tag/v0.1.1)
[![License](https://img.shields.io/badge/license-MIT-lightgrey)](LICENSE)
[![built with Kujo](https://img.shields.io/badge/built%20with-Kujo-white.svg)](https://github.com/kujolang/kujo)

Fireworks AI inference and hosted-model controls for Kujo.

## Install

```bash
kujo run /path/to/kennel/kennel.kujo --interpreter -- add github:kujolang/fireworks@v0.1.1 --alias fireworks
kujo run /path/to/kennel/kennel.kujo --interpreter -- install
export FIREWORKS_API_KEY=your-key
```

## 30-second quick start

```kujo
from fireworks import create_client, client_chat

client := create_client({})
request := {
    "model": "accounts/fireworks/models/kimi-k2-instruct-0905",
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

The native layer preserves Fireworks response fields, tools, structured output, reasoning, multimodal inputs, model metadata, and usage. Deployments, files, batches, and fine-tuning remain provider-owned.

## AI SDK integration

`fireworks_provider({"model": "accounts/fireworks/models/kimi-k2-instruct-0905"})` supplies normalized chat and streaming semantics through the compatible driver.

## Authentication and security

Set `FIREWORKS_API_KEY`. Remote endpoints require HTTPS; credentials are redacted and protected headers cannot be overridden.

## Testing and documentation

```bash
bash scripts/release_quality_gate.sh
bash scripts/verify_installed_package.sh
```

The default gate is deterministic and offline. See [docs/](docs/) for implementation and Contract v1 evidence.
