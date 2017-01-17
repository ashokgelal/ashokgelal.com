---
title: Opening a new copy of an app on MacOS
date: 2017-01-06 11:11:11
tags:
- MacOS
- terminal
- tips
---

Mac doesn’t like you to open multiple copies of an application. If you try to open a new copy, it will switch to the running copy. If you want to open a new copy, this is what you need to do from your terminal:

```bash
open -n /Applications/<name of application>.app
```

See that little `-n` switch? That’s the one that tells Mac to open a new copy.