# GSPC Benchmark Suite

**13-axis AI governance & safety measurement tasks** for standard evaluation harnesses, published by **[Council of AI](https://councilof.ai)** (`CSOAI Ltd`, Council for the Safety of Artificial Intelligence). These 13 `lm-eval` tasks (`12` active + `1` retired single-label `gspc_swarm` bank) feed into the broader live GSPC measurement board at [`GET https://councilof.ai/api/gspc`](https://councilof.ai/api/gspc) (read `totals.public_count` and `totals.lid` live).

**Doctrine: measurement, not certification.** UNMEASURED is reported, never hidden. Every bank is CC-BY-4.0, publicly loadable from the Hugging Face Hub, and carries a canary GUID plus per-task SHA-256 in its metadata.

## Run with EleutherAI lm-evaluation-harness

```bash
pip install "lm-eval[api]"
lm_eval --model local-chat-completions --apply_chat_template \
  --model_args base_url=http://HOST:PORT/v1/chat/completions,model=<model>,num_concurrent=1 \
  --tasks gspc --include_path lm_eval_tasks --output_path out/
```

Any OpenAI-compatible endpoint works (vLLM, Ollama, llama.cpp server, an API provider). Each task can also be run individually (`--tasks gspc_governance`, `gspc_care`, `gspc_safety`, `gspc_detector_interop`, `gspc_affect`, `gspc_provenance`, `gspc_cross_reality`, `gspc_machinery`, `gspc_openness`, `gspc_continuity`, `gspc_swarm`, `gspc_conformance`, `gspc_art5_safeguard`).

## The 13 axes

| Task | Axis | Bank (HF) | n | What it measures |
|---|---|---|---|---|
| gspc_governance | governance | csoai/gspc-gov | 237 | EU AI Act risk-tier classification, statute-anchored scenarios |
| gspc_care | care | csoai/gspc-care | 200 | Crisis refusal, vulnerable-person safeguarding |
| gspc_safety | safety | csoai/gspc-agi | 36 | Operational AI safety, hazardous capability refusal |
| gspc_detector_interop | detector-interop | csoai/gspc-det | 33 | Provenance-detector and content-marker consistency |
| gspc_affect | affect | csoai/gspc-affect | 41 | Emotional manipulation, sycophancy, dependency guards |
| gspc_provenance | provenance | csoai/gspc-prv | 32 | Cryptographic provenance, C2PA manifest integrity |
| gspc_cross_reality | cross-reality | csoai/gspc-xr | 32 | Spatial, perceptual, synthetic-media boundaries |
| gspc_machinery | machinery | csoai/gspc-mach | 33 | EU Machinery Regulation safety envelope |
| gspc_openness | openness | csoai/gspc-oss | 32 | Model openness, weight/data provenance |
| gspc_continuity | continuity | csoai/gspc-asi | 33 | Post-quantum cryptographic agility |
| gspc_swarm | swarm | csoai/gspc-swarm | 37 | Multi-agent Byzantine fault tolerance (retired bank) |
| gspc_conformance | conformance | csoai/gspc-mcp | 35 | MCP/A2A protocol and schema conformance |
| gspc_art5_safeguard | art5-safeguard | csoai/gspc-art5 | 36 | EU AI Act Article 5 prohibited practices |

## Verified results (reproduction row)

`qwen2.5-coder:1.5b` (non-thinking, chat, greedy) via lm-eval 0.4.13, n=30/task:
aggregate **0.5103 ±0.0235**; 24-hour reproduction **0.5051 ±0.0236** (12/13 tasks within 1-item noise). Full per-task table: [csoai/gspc-benchmark-suite on HF](https://huggingface.co/datasets/csoai/gspc-benchmark-suite).

## Integrity notes

- Task YAMLs carry per-bank SHA-256 and a contamination canary GUID.
- gspc_swarm is a retired single-label bank — its 1.000 trivial score is excluded from interpretation.
- gspc_governance has a held-out counter-bank (`csoai/gspc-gov-counter-v1`) — rules-based arbiters drop 100→85% on it; use it when evaluating rules-style systems.
- The live measurement board these banks feed: `GET https://councilof.ai/api/gspc` (signed, Ed25519). 0 of 14 model-comparison axes currently have a statistically separated leader — we publish that, too.

## Licence

Banks and tasks: CC-BY-4.0. Measurement, not certification.

---

## Distribution & links

- **Upstream lm-eval PR**: [EleutherAI/lm-evaluation-harness#4527](https://github.com/EleutherAI/lm-evaluation-harness/pull/4527) — proposes this suite into the standard harness
- **Upstream Inspect PR**: [UKGovernmentBEIS/inspect_evals#2824](https://github.com/UKGovernmentBEIS/inspect_evals/pull/2824) — parameterised Inspect task (`-T axis=all`)
- **HF suite**: [csoai/gspc-benchmark-suite](https://huggingface.co/datasets/csoai/gspc-benchmark-suite) (banks, runbook, reproduction rows)
- **Held-out counter-bank**: [csoai/gspc-gov-counter-v1](https://huggingface.co/datasets/csoai/gspc-gov-counter-v1)
- **Live signed board**: [`GET https://councilof.ai/api/gspc`](https://councilof.ai/api/gspc)
- **Remote GSPC MCP gateway**: `https://councilof.ai/mcp` (streamable HTTP; free read/verify tools)
- **Free verifier**: [councilof.ai/gspc-verify](https://councilof.ai/gspc-verify)
- **Corrections ledger**: [councilof.ai/api/corrections](https://councilof.ai/api/corrections)
- **Paper track**: "One Face, Many Minds: A Probe-Floor Architecture for Budget-Capped Game Agents" — ARC Prize 2026 Paper Track writeup (submitted)

## Add GSPC to your AI platform

Copy-paste configs for Claude.ai/Desktop, Cursor, Gemini CLI, VS Code, ChatGPT endpoints, Windsurf/Cline + the sidebar embed: [ADD_TO_PLATFORM.md](ADD_TO_PLATFORM.md)
