# Fireworks Implementation Report

## Executive Summary

Initial Kujo Fireworks package for the documented Fireworks REST API, with a provider-qualified native client and pure AI SDK driver.

## Official API Evidence / Evidence Date

Fireworks's official SDK documents `FIREWORKS_API_KEY`, chat completions, embeddings, image generation, files, and fine-tuning. Evidence date: 2026-08-27.

## Protocol Classification

OPENAI-COMPATIBLE WITH PROVIDER EXTENSIONS. Fireworks exposes OpenAI-compatible chat and embeddings plus native image, audio, video, files, and fine-tuning APIs.

## Architecture / Native API Coverage

Native client: `src/fireworks.kujo`; AI SDK adapter: `src/provider.kujo`; root exports: `fireworks.kujo`. Chat, model listing, embeddings, SSE parsing, tools, reasoning options, and usage are covered.

## Public Exports

`create_client`, `chat`, `client_chat`, `client_models`, `client_embeddings`, `embeddings`, `parse_stream`, `fireworks_provider`, `fireworks_driver`.

## Kujo Requirement / AI SDK Dependency

Kujo >= 1.0.2; `github:kujolang/ai-sdk@v1.1.0`.

## Authentication / Native Semantics / Streaming

Bearer `FIREWORKS_API_KEY`, HTTPS enforcement, URL credential rejection, redaction, protected headers, and OpenAI-compatible SSE parsing. Native response fields remain in raw provider data.

## Tools / Structured Output / Reasoning / Multimodal / Embeddings

Tools, response format, reasoning, and multimodal request fields remain provider-owned. Vision is declared where model-supported. Embeddings are not claimed.

## Usage / Finish Reasons / Errors

Prompt/completion/total usage maps where supplied. Native error payloads and provider codes are retained subject to redaction.

## AI SDK Driver / Security / Tests

Pure descriptor/decoder hooks with no network I/O or policy bypass. Two deterministic offline files plus installed consumer smoke are included.

## Clean-Room Install / Installed Consumer Smoke

Passed with Kujo v1.0.2, including immutable Kennel add/install/reinstall/validate and installed consumer smoke with `KUJO_MODULE_PATH` unset.

## Live Validation

SKIPPED — credentials/environment unavailable.

## AI SDK Changes / Kujo Changes / Kennel Changes

None.

## Contract Conformance / Limitations

See `FIREWORKS_PROVIDER_PACKAGE_CONFORMANCE.md`. Native gRPC SDK semantics, image/video generation endpoints, files, batch jobs, and realtime features are outside this initial HTTP package.
