# Zerion API Skill for Claude

A Claude skill that provides structured access to the [Zerion API](https://developers.zerion.io/) via its MCP connector, enabling real-time querying of crypto wallet portfolios, token prices, transaction history, PnL, NFTs, and more across 38+ blockchains.

## What This Skill Does

When installed, this skill teaches Claude how to:

- **Query wallet portfolios**: total value, distribution by chain and position type
- **List token positions**: fungible holdings and DeFi positions
- **Fetch transaction history**: trades, sends, receives, mints, claims, with full filtering
- **Calculate Profit & Loss**: realized/unrealized gains, fees, net invested (FIFO method)
- **Chart wallet balances**: time-series data from 1 hour to max history
- **Search token prices**: look up any fungible by name/symbol, get market data and price charts
- **View NFT holdings**: positions, collections, floor prices, and portfolio value
- **Build live dashboards**: generate React/HTML artifacts that pull Zerion data in real time

## Prerequisites

1. **Zerion API Key**: Get one at [dashboard.zerion.io](https://dashboard.zerion.io/). Dev keys start with `zk_dev_`, production keys with `zk_prod_`.
2. **Zerion MCP Connector**: Add the Zerion MCP integration in your Claude settings. The MCP server URL is `https://developers.zerion.io/mcp`.

## Installation

Upload the `zerion-api.skill` file to Claude as a skill. Once installed, Claude will automatically activate the skill when you ask about wallets, tokens, portfolios, or any crypto/DeFi data.

## Authentication

The Zerion API key is **not** stored in the MCP connector's OAuth settings. Instead, you provide it at the start of each chat session. Claude will ask for it when needed and hold it in memory only for that conversation.

The API uses HTTP Basic Auth: your key is the username, with an empty password.

```
Authorization: Basic <base64(YOUR_API_KEY + ":")>
```

**Security**: The skill instructs Claude to never write the key to files, display it in artifact UIs, or persist it beyond the current session.

## Usage Examples

### Simple Queries (Chat)

```
Show me the portfolio for 0x42b9df65b219b3dd36ff330a4dd8f327a6ada990
```

```
What's the current price of ETH and its 30-day change?
```

```
List the last 10 trades for vitalik.eth
```

```
What's the PnL for 0x42b9df65b219b3dd36ff330a4dd8f327a6ada990 on Ethereum?
```

```
Show NFT holdings for 0x42b9df65b219b3dd36ff330a4dd8f327a6ada990, sorted by floor price
```

### Dashboard Artifacts

```
Build a dashboard showing the full multichain portfolio and PnL for 0x42b9df65b219b3dd36ff330a4dd8f327a6ada990
```

```
Create a price chart artifact for ETH over the past 3 months
```

When building artifacts, Claude will:
1. Prompt you for your API key via a masked password input
2. Call the Zerion MCP through the Anthropic API (Claude-in-Claude pattern)
3. Parse the MCP response and render the data in a polished UI


## Links

- [Zerion API Docs](https://developers.zerion.io/reference)
- [Zerion API Dashboard](https://dashboard.zerion.io/)
- [Supported Blockchains](https://developers.zerion.io/reference/supported-blockchains)
- [MCP Server](https://developers.zerion.io/mcp)
