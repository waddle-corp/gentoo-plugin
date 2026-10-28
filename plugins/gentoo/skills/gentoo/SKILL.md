---
name: gentoo
description: Manage a Shopify store's Gentoo Growth Agent Goal, Opportunities, Actions, Tools, Performance, Credits, Sidekick, and Shop settings using the Gentoo remote MCP tools.
---

# Gentoo Merchant Skill

Use this skill when the user wants to inspect or manage their Shopify store's Gentoo Growth Agent, including Store Goals, Opportunities, Action previews and approvals, Merchant Tools, Performance campaigns, Credit usage, Sidekick conversations, or Shop deploy settings.

## Authentication and Setup

The user connects their store through the remote MCP OAuth flow (`https://mcp.gentooai.com/mcp`) using a one-time store connection key (`gt_pat_...`) generated in **Shopify Admin > Gentoo > Settings > Connectors**.

- Never ask the user to paste passwords or Shopify Admin tokens in chat.
- Every tool call is automatically scoped on the server to the authenticated Shopify store.

## Core Operating Rules (Mandatory)

1. **Two-Step Action Approval Protocol**:
   - Never approve an Action (`gentoo_action_approve`) without first inspecting its preview.
   - Step 1: Call `gentoo_action_preview` with `actionId` to retrieve the Before/After comparison states, screenshot capture URLs, credit cost, and `reviewFingerprint` (or `approvalViewFingerprint`).
   - Step 2: Present the concrete Before/After summary and credit cost to the user and obtain explicit approval.
   - Step 3: Only after explicit user confirmation, call `gentoo_action_approve` with `actionId` and `expectedReviewFingerprint`.
2. **Preserve BIGINT Identifiers as Strings**:
   - Always treat `blockerId`, `actionId`, `runId`, `jobId`, and `proposalId` as decimal strings. Never coerce them to floating-point numbers.
3. **Non-Blocking Long Runs**:
   - `gentoo_tool_run` and `gentoo_action_bulk_approve` enqueue background work and return `runId` or `jobId` immediately. Poll progress with `gentoo_tool_status` or `gentoo_action_bulk_approval_status`.
4. **Confirmation Before Credit-Consuming or Storefront Writes**:
   - Always obtain explicit user confirmation in the current task before calling write tools (`gentoo_action_approve`, `gentoo_action_rollback`, `gentoo_action_pause`, `gentoo_action_restore`, `gentoo_action_bulk_approve`, `gentoo_goal_propose`, `gentoo_goal_select`, `gentoo_tool_run`, or shop auto-approve updates).
