# Kujo Fireworks Provider

Native Fireworks OpenAI-compatible chat client with Fireworks reasoning, tools, vision, and an AI SDK adapter.

```bash
kujo package-add github:kujolang/fireworks@v0.1.0
export FIREWORKS_API_KEY=your-key
```

```kujo
from fireworks import create_client, client_chat
c := create_client({})
r := client_chat(c, {"model":"accounts/fireworks/models/kimi-k2-instruct-0905","messages":[{"role":"user","content":"Hello"}],"reasoning_effort":"high"})
```

Native use preserves Fireworks response fields, reasoning controls, tools, and usage metadata. `fireworks_provider()` supplies normalized AI SDK chat and streaming semantics. Tests are offline and credential-free.
