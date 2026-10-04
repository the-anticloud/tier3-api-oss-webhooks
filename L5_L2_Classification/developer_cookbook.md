# Developer Cookbook — api-oss-webhooks
**Stack:** Python 3.11, asyncio, httpx (local targets only), AIOSS_FORMAT
**Domain:** Sovereign webhook dispatcher: event-driven notifications for Anticloud events
**License:** Apache-2.0 | **IP:** USPTO pending 2026, Anticloud FZ LLE

## Core Usage

```python
from api_oss_webhooks import WebhookDispatcher
wh = WebhookDispatcher(aioss_chain='./webhooks.aioss')

# Register subscription (LAN targets only)
wh.subscribe(event='aioss.chain_updated', target='http://192.168.1.100:9000/hook',
             filter_pax=True, pax_model='./pax-27b-q4.gguf')

# Dispatch event
wh.dispatch('aioss.chain_updated', payload={'chain_hash': '8b4a8a4f...', 'module': 'PAX_INFERENCE_CORE'})
```

## AIOSS Chain Append

```python
import hashlib, time

def aioss_append(chain_path, payload: bytes, module_id: str):
    entry_hash = hashlib.sha3_256(payload).digest()
    ts = int(time.time_ns()).to_bytes(8, 'big')
    with open(chain_path, 'rb') as f:
        f.seek(-32, 2); prev_hash = f.read(32)
    new_hash = hashlib.sha3_256(prev_hash + entry_hash + ts).digest()
    with open(chain_path, 'ab') as f:
        f.write(ts + entry_hash + new_hash)
    return new_hash.hex()

# After every api-oss-webhooks output:
chain_hash = aioss_append("./api_oss_webhooks.aioss",
                           result_bytes, "api-oss-webhooks")
```

## Performance & Integration

Performance: profile with api-oss-devtools. Benchmark with api-oss-analytics. Integration: all api-oss-webhooks operations are logged to api-oss-logging and audited by api-oss-compliance.
