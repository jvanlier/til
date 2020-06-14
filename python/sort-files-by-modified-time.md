Sort Files By Modified Time
===========================

```python
from pathlib import Path

paths = Path("/some/location").glob("*")
paths_sorted = sorted(paths, key=lambda p: p.stat().st_mtime)
```

Another option is `st_ctime` (creation time).
