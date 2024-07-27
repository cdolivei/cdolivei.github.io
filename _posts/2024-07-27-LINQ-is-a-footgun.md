---
layout: post
title: LINQ is a footgun
tags: software, csharp
---

```csharp
IEnumerable<int> list = Enumerable.Range(1,10);
Assert.That( list.Take(5), Is.EquivalentTo( new int[] { 1, 2, 3, 4, 5 }) );
Assert.That( list.Take(5), Is.EquivalentTo( new int[] { 6, 7, 8, 9, 10 }) );
```

```
  Error Message:
     Expected: equivalent to < 6, 7, 8, 9, 10 >
  But was:  < 1, 2, 3, 4, 5 >
```
