---
layout: post
title:  "MacOS使用 BeyondCompare 作为 MergeTool"
date:   2021-08-19 16:12:40
catalog:  true
tags:
  - Mac
  - Git
---

```shell
git config --global merge.tool bc
git config --global mergetool.bc.path "/usr/local/bin/bcomp"
```


