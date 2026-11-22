---
max_turns: 6
allowed_tools: [Skill]
---

Run the strict pass on this change.

```python
def load_config(path: str) -> dict:
    if not os.path.isfile(path):
        raise FileNotFoundError(path)
    return _parse(path)


def _parse(path: str) -> dict:
    try:
        with open(path) as f:
            return json.load(f)
    except (OSError, json.JSONDecodeError):
        return {}
```

`_parse` is private and `load_config` is its only caller in the repository.
You cannot run the tests here, so say what you would verify.
