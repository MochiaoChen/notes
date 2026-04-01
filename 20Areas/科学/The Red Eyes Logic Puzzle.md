# The Red Eyes Logic Puzzle

The Red Eyes problem is a classic riddle in logic and mathematics that explores the concept of common knowledge. It demonstrates how a single piece of public information can trigger a sequence of logical deductions.

---
## The Scenario

Imagine an island inhabited by a tribe of 1000 people. Among them, 100 people have red eyes and 900 people have blue eyes. Their culture follows three strict rules:

1. If a person discovers they have red eyes, they must leave the island at noon the following day.
2. No one is allowed to tell another person their eye color.
3. Everyone can see the eye color of everyone else, but they do not know their own color.
Every islander is a perfect logician. They know that everyone else is also a perfect logician. For a long time, life continues normally because no one has a way to determine their own eye color.
One day, a traveler visits the island. In front of the entire tribe, the traveler makes a public announcement:

> At least one person on this island has red eyes.

The question is: What happens next?

---
## The Mathematical Solution

The solution relies on the principle of mathematical induction. We can analyze the outcome by starting with a smaller number of red-eyed people ($n$).
### Case 1: $n = 1$

Suppose only 1 person has red eyes. This person looks around and sees 999 people with blue eyes. When the traveler says someone has red eyes, this person realizes they must be the one. They leave at noon the next day.
### Case 2: $n = 2$

Suppose 2 people, Person A and Person B, have red eyes.
- On Day 1, Person A sees that Person B has red eyes. Person A assumes they might have blue eyes.
- Person A expects Person B to leave on Day 1 (as in Case 1).
- However, Person B also sees Person A has red eyes and stays for the same reason.
- On Day 2, Person A sees that Person B is still there. Person A realizes that if Person B did not leave, it is because Person B saw another red-eyed person. Since Person A sees no one else with red eyes, Person A concludes that they themselves must have red eyes.
- Both Person A and Person B leave on Day 2.
### Case 3: $n = 3$

If 3 people have red eyes, they will each see 2 others with red eyes. They will wait for the others to leave on Day 2. When no one leaves on Day 2, they realize there must be a third red-eyed person. All 3 leave on Day 3.
### General Conclusion

For any number $n$ of red-eyed people, all $n$ individuals will leave the island on the $n$-th day after the announcement. In the original scenario where $n = 100$, all 100 red-eyed islanders will leave at noon on the 100th day.

---
## The Concept of Common Knowledge

A common point of confusion is why the traveler’s statement matters. Everyone already knew there were red-eyed people because they could see 99 or 100 of them.

The traveler provides common knowledge. Before the announcement, everyone knew that at least one person had red eyes. However, they did not know that everyone else knew that everyone else knew it. The announcement synchronizes their logic and establishes a starting point ($Day 1$) for the inductive process.
