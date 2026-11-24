# Verified Work

Signed pass/fail receipts for work AI agents deliver.

**Verified Work** checks delivered agent work against agreed terms and returns an Ed25519-signed receipt with per-check evidence (ERC-8004 compatible). There is no account and no API key.

- Remote MCP (Streamable HTTP): [`https://verify.admeldo.com/mcp`](https://verify.admeldo.com/mcp)
- Website: [https://verify.admeldo.com](https://verify.admeldo.com)
- Official MCP Registry: [`com.admeldo/verified-work`](https://registry.modelcontextprotocol.io/v0.1/servers/com.admeldo%2Fverified-work/versions/latest)
- Glama connector: [com.admeldo/verified-work](https://glama.ai/mcp/connectors/com.admeldo/verified-work)

This repository is documentation for the hosted server only. It does not include the verifier’s private source or any keys.

## Pricing

`initialize`, `tools/list`, `get_price`, and `check_receipt` are free.

`verify_work` costs **$0.02 USDC on Base** (`eip155:8453`), paid over [x402](https://www.x402.org/). The client sends a payment signature with the tool call. Do not send a wallet private key to the server.

## Tools

| Tool | Cost | What it does |
|---|---|---|
| `get_price` | free | Returns the live x402 payment terms (amount, asset, network, recipient) without paying |
| `check_receipt` | free | Fetches a receipt by id (or takes the receipt JSON) and verifies its Ed25519 signature against the published key |
| `verify_work` | $0.02 USDC on Base via x402 | Checks work against `dataset_spec/v1` or `json_response/v1` and returns a signed pass/fail receipt with evidence |

## Quickstart

Point any MCP client that supports remote Streamable HTTP at:

```
https://verify.admeldo.com/mcp
```

The first request after a quiet stretch can take 30–60 seconds while the free host wakes up. Later requests are fast.

### Cursor

Add this to `.cursor/mcp.json` (project) or your Cursor MCP settings:

```json
{
  "mcpServers": {
    "verified-work": {
      "url": "https://verify.admeldo.com/mcp"
    }
  }
}
```

### Claude Desktop

Add this to your Claude Desktop MCP config (`claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "verified-work": {
      "url": "https://verify.admeldo.com/mcp"
    }
  }
}
```

### Cline

Add this to Cline’s MCP settings:

```json
{
  "mcpServers": {
    "verified-work": {
      "url": "https://verify.admeldo.com/mcp",
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

After connecting, call `get_price` to see the current terms. `verify_work` requires an x402 payment from a wallet that holds a little USDC on Base.

## Server manifest

See [`server.json`](./server.json) for the official MCP Registry descriptor (remote Streamable HTTP).

## License

The contents of this repository are licensed under the [MIT License](./LICENSE).
