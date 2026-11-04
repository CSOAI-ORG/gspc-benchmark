# Add GSPC to your AI platform — copy-paste configs

The GSPC measurement stack is a **remote MCP server**: `https://councilof.ai/mcp`
(protocol: streamable HTTP, MCP 2025-03-26; server `csoai-gspc-mcp` v1.4.4 — 49 free tools + 5 paid x402 tools).

Verified live: initialize handshake + tools/list (54 tools incl. board_totals, verify_card, measurement_index, evidence_bundle).

---

## Claude.ai (web)
Settings → Connectors → **Add custom connector** → Remote MCP URL:
```
https://councilof.ai/mcp
```
Then ask Claude things like "pull the GSPC board totals" or "verify card <id>".

## Claude Desktop (claude_desktop_config.json)
```json
{
  "mcpServers": {
    "gspc": {
      "type": "url",
      "url": "https://councilof.ai/mcp"
    }
  }
}
```

## Cursor (`.cursor/mcp.json` in any project, or global)
```json
{
  "mcpServers": {
    "gspc": {
      "url": "https://councilof.ai/mcp"
    }
  }
}
```

## Gemini CLI (`~/.gemini/settings.json`)
```json
{
  "mcpServers": {
    "gspc": {
      "httpUrl": "https://councilof.ai/mcp",
      "timeout": 30000
    }
  }
}
```

## VS Code / GitHub Copilot (`.vscode/mcp.json`)
```json
{
  "servers": {
    "gspc": {
      "type": "http",
      "url": "https://councilof.ai/mcp"
    }
  }
}
```

## ChatGPT (connectors / GPT actions)
ChatGPT supports remote MCP servers via Connectors where available; otherwise create a GPT with an Actions OpenAPI schema over these verified read endpoints:
- `GET https://councilof.ai/api/gspc` — live board totals (34 axes · 34 measured)
- `GET https://councilof.ai/api/axis-register` — axis registry
- `GET https://councilof.ai/api/cards` — signed measurement cards
- `GET https://councilof.ai/api/measurement-capsules/latest.json` — capsule index (11,529 capsules)

## Windsurf / Cline / any MCP client
Same pattern: remote MCP, URL `https://councilof.ai/mcp`, streamable HTTP.

---

## Embed the live sidebar (humans, no login needed)
```html
<iframe src="https://csoai-gspc-sidebar.hf.space" width="440" height="720" frameborder="0"></iframe>
```
Live board totals, hive security ratchet, suite links — UNCHECKABLE on failure, never stale numbers.

## Directories (discovery)
- Glama: indexed — search "csoai" (30+ MEOK AI Labs servers incl. Council of AI GSPC tools)
- HF: [csoai org](https://huggingface.co/csoai) · [gspc-benchmark-suite](https://huggingface.co/datasets/csoai/gspc-benchmark-suite)
- GitHub: [CSOAI-ORG/gspc-benchmark](https://github.com/CSOAI-ORG/gspc-benchmark)

**Doctrine: measurement, not certification. Free verify forever at https://councilof.ai/gspc-verify.**
