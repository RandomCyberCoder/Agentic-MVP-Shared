# Agentic-MVP-Shared

Shared utilities for our project (created by Bob, edited by Emma).

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

### Example

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
