# Dependency Graph Template

Use this template to define how service dependencies are discovered, classified, and stored.

This should be backed by automation. Do not rely only on manually written markdown.

---

## 1. Goal

Produce a dependency map that answers:

- which services call which other services
- which dependencies are confirmed by runtime traffic
- which dependencies exist only in code or contracts
- which APIs, topics, and data stores are involved

## 2. Data Sources

Build the graph from three sources.

### A. Runtime Sources

- OpenTelemetry traces
- AWS X-Ray service map
- CloudWatch Application Signals
- access logs or API gateway logs

Output:

- confirmed caller -> callee edges
- operation frequency
- latency and error indicators

### B. Static Sources

- HTTP client classes
- gRPC stubs
- Kafka/SNS/SQS producers and consumers
- config-based endpoint references
- repository and database usage
- shared library references

Output:

- potential edges inferred from code and config

### C. Contract Sources

- OpenAPI
- AsyncAPI
- protobuf
- database schema ownership definitions

Output:

- schema coupling and published/consumed interface edges

## 3. Edge Classification

Each edge should be tagged with one of:

- `runtime-confirmed`
- `static-only`
- `contract-only`
- `multi-source-confirmed`

Recommended confidence scoring:

- `0.9` for runtime-confirmed
- `0.7` for multi-source-confirmed
- `0.5` for contract-only
- `0.4` for static-only

## 4. Suggested Output Schema

```json
{
  "source_service": "orders",
  "target_service": "payments",
  "interaction_type": "http",
  "operation": "POST /payments/authorize",
  "evidence": ["otel", "openapi", "code"],
  "classification": "multi-source-confirmed",
  "confidence": 0.7,
  "source_locations": [
    "src/main/java/com/acme/orders/client/PaymentsClient.java"
  ],
  "contract_locations": [
    "contracts/openapi/payments.yaml"
  ],
  "notes": "Invoked during order placement flow"
}
```

## 5. Per-Service Dependency View

For each service create a focused dependency sheet.

### Service: `[service-name]`

- Inbound callers:
- Outbound calls:
- Published topics/events:
- Consumed topics/events:
- Datastores:
- Shared libraries:
- Critical edges:
- Unknown edges requiring review:

## 6. Visualization Outputs

Generate at least these views:

- full platform graph
- per-domain subgraph
- per-service neighborhood graph
- API-only graph
- event-driven graph

Useful formats:

- JSON
- CSV edge list
- Graphviz DOT
- Neo4j import CSV
- Backstage catalog annotations

## 7. Refresh Strategy

- runtime data: daily or hourly
- static scan: on merge to main
- contract extraction: on contract change
- published graph artifact: versioned per release

## 8. Validation Rules

Review these edge types manually:

- static-only critical dependencies
- newly introduced cross-domain dependencies
- dependencies with no contract owner
- dependencies that bypass approved client layers

## 9. Codex Usage Guidance

When asking Codex to change a service, attach or reference:

- the service knowledge file
- the per-service dependency view
- impacted contracts
- the exact flow being changed

Prompt Codex to inspect only the local neighborhood of the graph unless cross-service work is requested.
