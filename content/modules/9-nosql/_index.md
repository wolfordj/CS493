---
title: "Non-Relational Databases"
description: "This week goes over the concept of non-relational databases. They have some limitations and abilities that are rather different from a typical relational database."
categories: ["Module"]
weight: 45
---

{{< title >}}
## Introduction
Relational databases enforce a number of rules to make sure that all the operations that occur are OK and that data remains consistent. This causes some issues where it can be difficult to distribute computations between different computers. It can also slow down processing. Non-relational databases may operate similarly in 99.9% of cases, but it is the edge cases under high load or where timing is important that things can get funny. And it depends a lot on the implementation of the database engine exactly how they get funny.

## Key Questions
- What is the difference between a relational and non-relational database?
- What happens when a database isn't consistent?
- What happens when a database uses eventual consistency?

## Explore the Topics
<!--- An automatically generated list of explore topics from the same directory as this overview. Generated from the frontmatter, make sure to fill in the title, description and include "Exploration" in the categories! -->
{{< explorelist >}}

## Additional Resources
[Brewers CAP Theorem](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.20.1495&rep=rep1&type=pdf)
: This paper looks at Brewer's CAP theorem in a good bit of theoretical details. A good bit has changed since this was originally conceived, but it gives you a good understanding of the original conjecture.

## Review
The important take away from this is that databases handle things like delays in signals or down nodes in very different ways. Traditional relational databases will do everything they possibly can to keep your data consistent and reject attempts that might cause problems. Other databases which have fewer relational constraints will do everything they can to make sure transactions get processed. Even it it means that things don't make sense for a moment in the database. And this is something of a spectrum. There are databases that end up somewhere in the middle. Understanding the sorts of limitations you might encounter and understanding how to deal with them are important when learning a new database system.