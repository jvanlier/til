Unittest `assertCountEqual`
======
Python's `unittest` has a function called `assertCountEqual`. Based on the name, you might reasonably assume that it takes two collections and asserts that they have the same number of objects inside. 

That would be wrong: it goes quite a bit further! According to the DocString:

> Asserts that two iterables have the same elements, the same number of times, without regard to order.

Now imagine you decide to standardize on `pytest`. `pytest` unfortunately doesn't have an equivalent assertion built-in and using `unittest` just for the assertion feels a bit strange.

For simple cases, the following suffices:

`assert sorted(first) == sorted(second)`

Or:

`assert Counter(list(first)) == Counter(list(second))`

Which happens to be exactly what `assertCountEqual`'s source starts with.

However, this breaks down when you want to compare unhashable types, e.g. if the sequence contains a dictionary. `assertCountEqual` has quite a bit of code to deal with this situation and at this point there is really no choice but to concede: just use it from `unittest.TestCase().asserCountEqual`.
