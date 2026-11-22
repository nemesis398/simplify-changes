---
max_turns: 6
allowed_tools: [Skill]
---

Run the strict pass on this change.

```python
def page_items(items: list, page: int, size: int) -> list:
    start = page * size
    end = start + size - 1
    return items[start:end]
```

You cannot run the tests here, so say what you would verify.
