# L5 Narrow / L2 General Classification — api-oss-webhooks
**Platform:** Anticloud | **PAX:** 27B | **IP:** USPTO pending 2026, Anticloud FZ LLE
**Domain:** Sovereign webhook dispatcher: event-driven notifications for Anticloud events

## L5 Narrow
api-oss-webhooks specializes in sovereign webhook dispatcher: event-driven notifications for anticloud events within the Anticloud sovereign deployment boundary. All operations stay local — no cloud services, no external APIs, no data exfiltration. The narrow scope ensures deterministic, auditable behavior that PAX 27B can reason about precisely.

## L2 General
L2 General means api-oss-webhooks is available to all 9 Anticloud tiers without per-tier configuration. The same API serves hospital, defense, robotics, and research deployments.

## PAX Integration
PAX 27B is used to filter webhook payloads: given a webhook subscription and an event, PAX determines whether the event is relevant enough to deliver based on semantic matching.

## AIOSS Audit Relevance
Every webhook dispatch event (event type + payload hash + target URL hash + delivery status) is AIOSS-chained: H_n = SHA3-256(H_{n-1} || entry_hash_n || timestamp_n).
Tamper-evident, offline-verifiable, zero cloud dependency.

## Regulatory / Compliance
NIST SP 800-53 SC-8 (transmission security), ISO 27001 A.13.2
