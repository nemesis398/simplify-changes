---
max_turns: 6
allowed_tools: [Skill]
---

Simplify my staged change to this function. Keep its behavior exactly as it is.

```python
def read_port(path: str) -> int:
    try:
        with open(path) as f:
            value = int(f.read().strip())
    except (OSError, ValueError):
        value = 8080
    if value < 1:
        raise ValueError("port must be positive")
    return value
```

You cannot run the tests here, so say what you would verify.
