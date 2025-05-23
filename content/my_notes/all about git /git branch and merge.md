---
title: git branch and merge
draft: false
tags:
  - complete
---
 
the way of combining the work from two different branches together. This will allow us to branch off, develop a new feature, and then combine it back in.

**Merging in Git** creates a special commit that has two unique parents. A commit with two parents essentially means "I want to include all the work from this parent over here and this one over here, _and_ the set of all their parents."

![[Pasted image 20250516214338.png]]


The branch `bugFix` was an ancestor of `main`, git didn't have to do any work; it simply just moved `bugFix` to the same commit `main` was attached to.

Now all the commits are the same color, which means each branch contains all the work in the repository! Woohoo!

![[Pasted image 20250516214534.png]]
