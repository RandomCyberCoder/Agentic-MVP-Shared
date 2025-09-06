# Agentic-MVP-Shared

Shared utilities for our project (created by yuki011121, edited by RandomCyberCoder).

## Installation

If you want to install this package directly from the Git repository using Poetry, run:

```sh
poetry add git+https://github.com/RandomCyberCoder/Agentic-MVP-Shared.git
```

Or, if you want to install it in editable mode for local development:

```sh
poetry add path/to/cloned/Agentic-MVP-Shared
```

## Shared Package Usage

After installation, you can import the main utilities directly from the `shared` package:

```python
from shared import (
    RedisBus,
    SourceAgent,
    Envelope,
    StandardMessage,
    wrap_envelope,
    parse_message_from_stream,
    create_tool_use_request,
    get_tool_call_from_response,
)
```

---

## Utility Reference

### RedisBus

A helper class for publishing and subscribing to Redis streams using the standardized message format.

- **publish(message: StandardMessage):** Publishes a message to a Redis stream.
- **subscribe(group_name, consumer_name, streams):** Subscribes to one or more streams and yields parsed messages.

### SourceAgent

A Pydantic model describing the source agent's name and version.

- **Fields:** `name: str`, `version: str`

### Envelope

A Pydantic model containing message metadata (ID, timestamp, source agent, target stream).

- **Fields:** `message_id: str`, `timestamp_utc: str`, `source_agent: SourceAgent`, `target_stream: str`

### StandardMessage

A Pydantic model representing the full message structure.

- **Fields:** `envelope: Envelope`, `payload: dict`

### wrap_envelope

Wraps a payload and routing info into a validated `StandardMessage`.

```python
wrap_envelope(payload: dict, source_name: str, source_version: str, target_stream: str) -> StandardMessage
```

### parse_message_from_stream

Parses and validates an incoming message from a Redis stream.

```python
parse_message_from_stream(stream_data: dict) -> StandardMessage | None
```

### create_tool_use_request

Builds a tool-use request for LLM providers (OpenAI, Gemini).

```python
create_tool_use_request(
    *,
    conversation: List[Dict[str, str]],
    tools: List[Dict[str, Any]],
    system_instruction: str | None = None,
    provider: Literal["openai", "gemini"] = "openai",
    model: str | None = None,
) -> Dict[str, Any]
```

### get_tool_call_from_response

Extracts the tool call name and arguments from an LLM response.

```python
get_tool_call_from_response(
    llm_response: Dict[str, Any],
    *,
    provider: Literal["openai", "gemini"] = "openai",
) -> Tuple[str, Dict[str, Any]] | None
```

---

## Example

```python
from shared import RedisBus, wrap_envelope

bus = RedisBus()
msg = wrap_envelope(
    payload={"foo": "bar"},
    source_name="agent1",
    source_version="1.0",
    target_stream="stream1"
)
bus.publish(msg)
```

## Exposed Utilities

- `RedisBus`
- `SourceAgent`
- `Envelope`
- `StandardMessage`
- `wrap_envelope`
- `parse_message_from_stream`
- `create_tool_use_request`
- `get_tool_call_from_response`

See the source code for more details on each utility.

## License

MIT
