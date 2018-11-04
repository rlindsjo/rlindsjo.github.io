---
layout: post
title: Hurt by test
---

TDD, BDD, ATDD, Unit Tests, Integration Tests, System Tests, Manual Test and the list can go on and on and on. There are a myriad of test methodologies, patterns and frameworks. They are all adapted for different programming languages or situations, some taget developers whiting code, some target whoever tries to express a rule in a suitable domain language. Some run quickly with minimal fuss and limited dependencies while others helps brining a whole system with multiple servers, databases and loads of test data into a known state for realistic end-to-end testing. Testing helps us to know what we have, allows us to verify that changes does not have unintended consequences and prepare for new what-if scenarios. 

Most of us probably agree that tests are good, and we complain when we encounter code that does not have tests, especially if the code is complicated to understand. But, is there such a thing as bad tests? Tests that actually make the code harder to maintain? Tests that has taken time to write but does not actually help the next developer understand the code nor helps them avoid breaking changes? Surely that can't be so, why would someone ever write such code...

A discussion with a colleague the other week led us onto this track. We were writing the tests after the fact (yes, TDD and everything, but sometimes you are in projects where code is already written, seemingly working and now it appeared in your lap) and I was complaining that it was very hard to write the tests, and mainly for two reasons:

1. The code was not written to be testable, unhelpful interfaces and quite a high dependency between modules.
2. I did not really understand what the code did, I had knowlede gaps both in the domain was that the code solved the problem for as well as the domain language used.

I was very reluctant to "just test" to make sure that we had good coverage and after apologising for disturbing my colleague for the nth time that afternoon with yet another question of why the code did what it did I got the response: 

> "That's ok, we don't want to write tests as if we were pouring concrete over the code."

The comment got us talking a bit and we continued the discussion on and off for the next few days. Of course we shouldn't write tests as if we made a concrete (or plaster) cast of the code. That would probably be fine if we wanted to make sure that we could write the exact same code later. However, just as every one else we use CVS so there really shouldn't be a "next time" writing the same code. We are not building physical things, when we want a copy we just make one at zero cost. Or ten copies. Or millions. So, the tests are not there to make sure we write the samecode again, but rather to test that if we write slightly different code later, it behaves the same way we want it to. But everything about the code probably isn't important and among those thing that are important some are because of domain of the language and other are important because of the current implementation.

"What?!?" you might exclaim, "what would be a test that isn't important?" Well, I'll give a couple of examples:

1. Testing the implementation of a data interface. I have seen tests requesting a Set of data and verifying the data by verifying the specific iterated order. So, the contract says it will return A, B and C in any order and the tests verifies that it actually comes as A, B, C.
2. Testing implementation details that are not specified as important, such as which order methods are called even if they do not depend on each other. Say you have code that will call a weight method av multiple instances and return the sum of their value, and the tests verifies that they are called in a specific order.

Now, I don't say that these kinds of test are not useful, but I have seen many of them where tests were written a certain way because that made it easy to write the tests or alternatively easy to get get a high code coverage. But when the next developer (our your self at a later time, say the next day or so) breaks one of those tests either due to trying to add new functionality or just refactoring code to accomodate a functionality change will have to make the decision if the code protects 

1. features in the system
2. the current implementation
3. or is there "just because". 

Of course we don't want to test of type (#1) to break. However, tests of (#2) is ok to break if the new implementation does not have the same limitations. However, (#3) can be broken at any time with no consequence to the end system.

The problem is only that the tests are not labeled (#1), (#2), (#3) and if it was hard to understand what the domain code did without the tests it does not actually get easier with test (#3) sprinkled all over the place. And I think this easily happens when writing tests without understanding what the code is / should be doing.

If you are writing tests "after the fact" and there are parts that you do not understand why it behaves the way it does, I think I'd rather have no test than a test fixating random (or even incorrect) behaviour.

