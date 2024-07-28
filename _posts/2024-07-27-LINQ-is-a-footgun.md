---
layout: post
title: LINQ is a footgun
tags: software, csharp
---

Here's something that I didn't expect:

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

LINQ offers a number of helpful methods to `IEnumerable<T>` types. It can also be a giant ass footgun because, sadly, you have to be aware of it's implementation - every call re-initializes the enumerable!

Let's take some slightly fictious method:

```csharp
public IEnumerable<long> RestoreSomeItem( long itemId ) {
  // updates something in the database
  // returns ids in the database that changed as a result, as a byproduct of that update
  while ( results.HasMoreItems ) {
    long relatedItemIds = results.ReadRow()
    yield return relatedItemIds;
  }
}
```

I had to call this method, but in my method I had to return whether any items changed. "Simple!" I thought, incorrectly:

```csharp
IEnumerable<long> results = someClass.RestoreSomeItem( 1 );
bool hasChanged = results.Any();
// let others know that some items have changed
publisher.Publish( results );
```

But there was a bug! `RestoreSomeItem()` is not deterministic. If you restore the same item twice, only the first call will return results. The second one will return an empty list.

The call to `.Any()` ran the database query. When the publisher iterated over the results it got back an empty list.

Thankfully tests picked up my error. But this is when I learned these LINQ methods are generally not great to use - they have unintended side-effects, and honestly seem to defeat the purpose of using `IEnumerable<T>`. Unfortauntely I needed to convert this to a `List<T>`, which kinda sucks because the results could be tens of thousands of items.

So... uhhh.. [I wrote something](https://github.com/cdolivei/Miser) that I hope to use that will be less of a footgun
