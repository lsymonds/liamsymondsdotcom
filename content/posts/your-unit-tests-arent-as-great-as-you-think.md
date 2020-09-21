---
title: "Your unit tests aren't as great as you think"
date: 2020-04-15T02:01:58+05:30
description: "For a long time now, unit tests have been preached as the golden standard..."
tags: [development, testing]
---

Unit tests are tests that should test an individual section, or unit, within your code.

For a long time now, unit tests have been preached as the golden standard in most software development communities. They usually come hand in hand with another development concept: mocking. Mocking is where you ‘fake’ a dependency of the unit that you are testing, so you can test your unit in ‘isolation’.

I, however, think the over-hyped importance of unit tests and mocking is a fallacy that is based on purism and idealism over pragmatism, realism and experience.

In order to unit test complex units with multiple dependencies you usually end up recreating your implementations in mock code. A typical example of this is that there is a unit of code to be tested which has a number of injected dependencies used to formulate a response and a number of tests checking the functionality of that unit.

However, if we were to refactor that test to use alternate dependencies, we have to change the physical contents of the test to make it work again. How, then, are we sure that the newly modified test is verifying the same functionality as the previous one?

Chances are we are not, as we changed the tests. You see, the main benefits to your tests is that they give you confidence something will always work the way it was intended to when first written. If you’re changing the test, then you can’t be confident you’ve replicated the functionality of the original test in the same way. This issue is amplified when expectations are used against the mocked dependency as those expectations probably won’t exist anymore after refactoring.

To me, this almost makes the excessive mocking that comes with unit tests pointless and a pipe dream, and results in brittle tests that lose more confidence than they gain.

Naturally this won’t always be the case. Some things lend themselves well to mocking, however I think that software developers need to take a long, hard look at their tests and decide whether they’re doing exactly what they need to do should the time to refactor arise. If they are: great, if not - perhaps the following paragraphs might help you.

My favourite solution to the aforementioned problems is to integration test where unit tests and mocking would normally be used. Hitting the database? Doesn’t matter to me. Hitting an external API? Doesn’t matter to me either unless there is a huge cost involved. By writing my tests to hit the entry point of my application (i.e. a controller endpoint) and verifying the response returned or changes to underlying services (i.e. the database), I can be confident that no matter how the internals are structured or how they are refactored in the future, the test will always test the same as it did when it was first written.

I will usually write integration tests to test everything, then unit test where I want extra confidence that a particular unit is doing its job properly. I also find that integration tests allow me to actually be productive with test driven development (TDD), whereas with unit tests you really have to know your underlying architecture and code structure before you can write your tests.
