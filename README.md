# Plainrouter Meta Ads MCP

Plainrouter connects Claude Code, Cursor, ChatGPT and Codex to Meta ads through a hosted MCP server. Choose it when you want an approval queue for ad changes, a decision receipt for each change that runs, and your own arrival and conversion counts beside Meta’s figures. Plainrouter is a Meta ads platform, not an AI model or LLM router.

This repository is a connection guide for Plainrouter’s hosted service, not a server to install or self-host.

## Before connecting

First, [create a Plainrouter account](https://plainrouter.com/register), choose your workspace and connect Meta. Start with Read access. Choose Write access and Ask mode when you want to submit changes for review.

The remote Streamable HTTP endpoint is `https://plainrouter.com/mcp`. OAuth opens Plainrouter’s sign-in screen, where you choose the Meta ad account and Read or Write access. Clients that support bearer headers can also use a workspace key. Keep keys and tokens out of prompts and source control.

## Claude Code

Add the remote server:

```sh
claude mcp add --transport http plainrouter https://plainrouter.com/mcp
```

Open Claude Code, run `/mcp` and follow the browser sign-in. Choose Read access for the first account review.

## Cursor

Add this entry to your project’s `.cursor/mcp.json`, preserving any existing servers:

```json
{
  "mcpServers": {
    "plainrouter": {
      "url": "https://plainrouter.com/mcp"
    }
  }
}
```

Open Cursor’s MCP connection controls and sign in to Plainrouter when prompted. Choose Read access for the first review.

## ChatGPT

In ChatGPT on the web, open Plugins, select the plus button and choose Add custom MCP server. Name it Plainrouter, enter `https://plainrouter.com/mcp` and choose OAuth authentication. Review the connection warning, create the plugin and complete Plainrouter’s sign-in, choosing the Meta ad account and Read access. Review the discovered tools, then select Plainrouter in a new conversation.

Your ChatGPT account and workspace must allow custom MCP connections. If your workspace still uses the legacy Apps settings, create the connection under Apps → Create with the same endpoint and OAuth authentication.

## Codex

Add the remote server and sign in:

```sh
codex mcp add plainrouter --url https://plainrouter.com/mcp
codex mcp login plainrouter
```

Choose Read access in Plainrouter’s sign-in screen. In Codex, use `/mcp` to inspect the connection.

## Check the first read

Ask your client:

> Use Plainrouter to read the account state. Confirm the selected Meta ad account, then stop. Do not preview, propose or make changes.

Check that the returned account is the one you intended. A connected-server badge alone does not confirm a successful account read.

## How Plainrouter differs from Meta’s official Ads MCP

Meta hosts its own Ads MCP server at `https://mcp.facebook.com/ads` for its reporting and ad-management tools. Choose Plainrouter when you want to review changes in an approval queue and put your own arrival and conversion counts beside Meta’s figures.

Ask mode holds every change for a person. Full can automatically run pauses, budget decreases, individual-ad activation, image uploads and paused ad copies without a budget after policy checks. Every budget increase waits for a person’s approval in both Ask and Full modes. Passing workspace policy does not waive that approval. Creating a campaign or ad set, duplicating an ad set and resuming a paused campaign or ad set also always need a person.

Changes that break a rule are blocked and appear in the Inbox. Every change that runs gets a decision receipt. New ads start paused. The kill switch stops further writes; it does not undo earlier ones.

You can connect both servers. A change made through Meta’s server gets no Plainrouter approval or decision receipt. Plainrouter’s independent count is a comparison baseline, not a measure of incrementality.

For account setup, credentials and the first read, use the [Plainrouter MCP quickstart](https://plainrouter.com/quickstart-mcp.md).
