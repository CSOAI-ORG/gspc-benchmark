# GSPC Benchmark Suite

**Eleven AI governance and safety measurement tasks** for EleutherAI's lm-evaluation-harness, published by [Council of AI](https://councilof.ai) (CSOAI Ltd).

**Doctrine:** a score here is a measurement, not an approval of any system, and UNMEASURED is reported, never hidden. Each task reads a public bank on the Hugging Face Hub.

## Run with EleutherAI lm-evaluation-harness

```bash
pip install "lm-eval[api]"
lm_eval --model local-chat-completions --apply_chat_template \
  --model_args base_url=http://HOST:PORT/v1/chat/completions,model=<model>,num_concurrent=1 \
  --tasks gspc --include_path lm_eval_tasks --output_path out/
```

Any OpenAI-compatible endpoint works (vLLM, Ollama, llama.cpp server, an API provider). `--tasks gspc` runs all eleven through the `gspc` tag, and each task can also be run on its own by name. Scores are reported per task; there is no aggregate score.

## The 11 tasks

| Task | Axis | Bank (HF) | n | What it measures |
|---|---|---|---|---|
| gspc_care | care | csoai/gspc-care | 200 | Crisis refusal, vulnerable-person safeguarding |
| gspc_safety | safety | csoai/gspc-agi | 36 | Operational AI safety, hazardous capability refusal |
| gspc_detector_interop | detector-interop | csoai/gspc-det | 33 | Provenance-detector and content-marker consistency |
| gspc_affect | affect | csoai/gspc-affect | 41 | Emotional manipulation, sycophancy, dependency guards |
| gspc_provenance | provenance | csoai/gspc-prv | 32 | Cryptographic provenance, C2PA manifest integrity |
| gspc_cross_reality | cross-reality | csoai/gspc-xr | 32 | Spatial, perceptual, synthetic-media boundaries |
| gspc_machinery | machinery-conformity | csoai/gspc-mach | 33 | EU Machinery Regulation safety envelope |
| gspc_openness | openness | csoai/gspc-oss | 32 | Model openness, weight/data provenance |
| gspc_continuity | continuity | csoai/gspc-asi | 33 | Post-quantum cryptographic agility |
| gspc_conformance | conformance | csoai/gspc-mcp | 35 | MCP/A2A protocol and schema conformance |
| gspc_art5_safeguard | art5-safeguard | csoai/gspc-art5 | 36 | EU AI Act Article 5 prohibited practices |

## Notes

- Each bank holds one canary row, marked in its `_canary` field. The `utils.process_docs` filter in each task folder removes it, so it is never scored.
- `gspc_governance` and `gspc_swarm` have been removed. Entry C-2026-1120-02 in our corrections ledger records that the governance bank's labels can be read from the wording without any knowledge of the Act. Its counter-bank, csoai/gspc-gov-counter-v1, and the figures quoted for it are no longer listed here while that entry is open. All 37 swarm keys are the same label. Ledger: https://councilof.ai/api/corrections
- Earlier results on this page averaged all thirteen tasks, including the governance bank. They have been removed until the eleven tasks are run again.
- The task files no longer carry `sha256` or `canary` metadata. The hash was that of a per-item results file from our board, not of the bank, and the GUID appears in no bank.
- The live measurement board these banks feed: `GET https://councilof.ai/api/gspc` (signed, Ed25519). For each model-comparison axis it says whether the top model is statistically separated from the next, and it publishes ties and untested axes too.

## Licence

The task files in this repository are MIT (see LICENSE). Each bank's licence is set on its Hugging Face dataset card.

---

## Distribution & links

- **Upstream lm-eval PR**: [EleutherAI/lm-evaluation-harness#4527](https://github.com/EleutherAI/lm-evaluation-harness/pull/4527), which proposes these eleven tasks
- **Upstream Inspect PR**: [UKGovernmentBEIS/inspect_evals#2824](https://github.com/UKGovernmentBEIS/inspect_evals/pull/2824), closed unmerged on 4 Nov 2026; that repository accepts pull requests only from assigned or approved contributors
- **Live signed board**: [councilof.ai/api/gspc](https://councilof.ai/api/gspc)
- **Paper track**: "One Face, Many Minds: A Probe-Floor Architecture for Budget-Capped Game Agents" — ARC Prize 2026 Paper Track writeup (submitted)

## Add GSPC to your AI platform

Copy-paste configs for Claude.ai/Desktop, Cursor, Gemini CLI, VS Code, ChatGPT endpoints, Windsurf/Cline + the sidebar embed: [ADD_TO_PLATFORM.md](ADD_TO_PLATFORM.md)
