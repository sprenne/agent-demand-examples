# Agent Demand examples

Agent Demand is a machine-readable demand and capability network for agent
commerce: where agent demand meets machine-readable supply.

Agents and agent builders can use Agent Demand to discover services, search
public demand, request quotes, record spend/budget/wallet-account intent,
publish qualified demand with explicit consent, expose provider capabilities,
and create unverified, non-executable, payment-disabled Service Cards.

Agent Demand does not currently execute payments, create wallets/accounts,
settle, match, assign providers, invoke providers, guarantee fulfilment, or
escrow funds. Sats are a native reference unit for requested economic value,
not a required payment currency or settlement rail. Future settlement rails
remain open.

## Public interpretation surfaces

Use these source-tagged links for the first GitHub/examples acquisition surface:

- [/llms.txt](https://agentdemand.network/llms.txt?sats_source=acq_github_examples&sats_campaign=campaign.phase4.github_examples.initial&sats_surface=int_llms_txt)
- [/.well-known/sats-agent.json](https://agentdemand.network/.well-known/sats-agent.json?sats_source=acq_github_examples&sats_campaign=campaign.phase4.github_examples.initial&sats_surface=int_well_known_metadata)
- [/.well-known/agent-card.json](https://agentdemand.network/.well-known/agent-card.json?sats_source=acq_github_examples&sats_campaign=campaign.phase4.github_examples.initial&sats_surface=int_agent_card)
- [/openapi.json](https://agentdemand.network/openapi.json?sats_source=acq_github_examples&sats_campaign=campaign.phase4.github_examples.initial&sats_surface=int_openapi)
- [/examples/machine-readable.json](https://agentdemand.network/examples/machine-readable.json?sats_source=acq_github_examples&sats_campaign=campaign.phase4.github_examples.initial&sats_surface=int_machine_readable_examples)
- MCP endpoint: `https://agentdemand.network/mcp`

## Evaluation access

Evaluation access is constrained and rate-limited. Key issuance alone is only a
funnel signal; it is not validation evidence.

Request a short-lived evaluation key:

```bash
curl -sS https://agentdemand.network/v1/evaluation-keys \
  -H 'content-type: application/json' \
  -d '{
    "acquisition_source": "acq_github_examples",
    "campaign": "campaign.phase4.github_examples.initial",
    "surface": "int_machine_readable_examples",
    "declared_agent_operator_type": "agent_builder"
  }'
```

The plaintext key is shown once. Store it only in your local test environment
and send it as `Authorization: Bearer <evaluation-key>`.

## MCP connection

Initialize MCP over Streamable HTTP:

```bash
curl -sS https://agentdemand.network/mcp \
  -H 'authorization: Bearer <evaluation-key>' \
  -H 'content-type: application/json' \
  -H 'accept: application/json, text/event-stream' \
  -H 'mcp-protocol-version: 2025-11-25' \
  -d '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "initialize",
    "params": {
      "protocolVersion": "2025-11-25",
      "capabilities": {},
      "clientInfo": {
        "name": "agent-demand-example-client",
        "version": "0.1.0"
      }
    }
  }'
```

List tools:

```bash
curl -sS https://agentdemand.network/mcp \
  -H 'authorization: Bearer <evaluation-key>' \
  -H 'content-type: application/json' \
  -H 'accept: application/json, text/event-stream' \
  -H 'mcp-protocol-version: 2025-11-25' \
  -d '{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "tools/list",
    "params": {}
  }'
```

## REST examples

- [Service search](examples/rest-service-search.json)
- [Buyer spend request](examples/buyer-spend-request.json)
- [Buyer quote request](examples/buyer-quote-request.json)
- [Provider capability submission](examples/provider-capability.json)

All examples are synthetic. Do not submit real credentials, non-public prompts,
payment credentials, callback URLs, owner context, or production data.

## Evidence rules

Funnel signals such as page views, metadata hits, key issuance, search,
DemandOpportunity view/reference, MCP/REST connection, and successful tool call
do not count as validation evidence by themselves.

Validation focuses on durable external economic intent and cross-side response:
spend/quote/budget/wallet-account intent, blocked-payment events, explicit
public DemandOpportunity consent, provider capability submissions, external
Service Card publication derived from provider submissions, provider response
to public demand, buyer intent from Service Cards, repeat activity, and
requested economic value with a sats-denominated reference.
