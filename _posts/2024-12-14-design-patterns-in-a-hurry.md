---
layout: post
title: "design patterns in a hurry"
date: 2024-12-14
categories: tech
---

humans -> pattern recognition during problem solving -> repeatability over time -> ✨ design patterns ✨.`<br />`
first came about in architecture, where a language was made using patterns as its units. it was later picked up by software engineers.

kind of a double edged sword, because if used correctly, it makes things a lot easier, if not, it's creates technical debt.

> if all you have is a hammer, everything looks like a nail.

in my experience, some design patterns are frequently used within the same codebase, while others are rarely utilized. this is likely because some given problem space would have a limited number of patterns that fit the solution naturally, and these patterns are repeated over time.

it is beneficial to be aware of such patterns, as they help create a good structure for information flow. startups focus on speed, whereas larger companies focus on code maintainability and scalability - utilise patterns accordingly, as everything is a tradeoff.

this post is a a quick refresher on design patterns, i learned from [this repo](https://github.com/kamranahmedse/design-patterns-for-humans) and [this website](https://refactoring.guru/design-patterns/what-is-pattern).

### types of design patterns

there are three main categories of design patterns:

- [creational patterns]({% post_url 2024-12-14-creational-patterns %}) : related to object(s) instantiation
- [structural patterns]({% post_url 2024-12-14-structural-patterns %}) : related to object(s) composition, how entities can use each other. think "components".
- [behavioral patterns]({% post_url 2024-12-14-behavioral-patterns %}) : related to object(s) responsibilities, how they can interact with each other.
