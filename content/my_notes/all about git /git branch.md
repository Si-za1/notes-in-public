---
title: git branch
draft: false
tags:
  - complete
---
 
Branches in Git are incredibly lightweight as well. They are simply pointers to a specific commit -- nothing more. This is why many Git enthusiasts chant the mantra:


`branch early, and branch often`

Because there is no storage / memory overhead with making many branches.

we want to checkout the branch with

```
git checkout <name>
```

This will put us on the new branch before committing our changes.

If you want to create a new branch AND check it out at the same time, you can simply type `git checkout -b [yourbranchname]`

