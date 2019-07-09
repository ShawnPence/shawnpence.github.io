---
layout: post
title: Lines of Code
subtitle: A Misleading Measurement
social-title: Lines of Code - A Misleading Measurement
social-description: Lines of Code are a poor choice to measure developer performance.
---

Some employers desire a way to quantify the performance of their developers, and may turn to lines of code (LOC) as one such measurement. Countless blog posts and online comments have lamented this choice already, so why am I adding my voice to the chorus of opposition? Unfortunately, despite all the advice to the contrary, it keeps coming up as a way of measuring the value of a developer.

On more than one occasion, I've seen developers bragging about the amount of code they've written, or complaining that another developer who wrote fewer LOC is receiving too much credit. For experienced developers, most of this post is familiar material, but for the sake of new developers or non-developers, I'll explain in multiple ways why lines of code as a measure of developer performance is a poor choice.

## Code Repetition

The most verbose way of solving a problem is rarely the best. Take, for example, a very simple request: print the numbers 1 to 10. Using Python as an example, here are two snippets that would both accomplish the task:

Example 1:
```

for i in range(1,11):
    print(i)

```

Example 2:
```

print(1)
print(2)
print(3)
print(4)
print(5)
print(6)
print(7)
print(8)
print(9)
print(10)

```

While both examples print the same output, the first is efficient and would scale to printing 1 to 1,000,000 with a simple change and could still be accomplished with 2 lines of code. The second example does not scale well, but would give a developer credit for five times more LOC than the first example when printing from 1 to 10. This is an exaggerated case, but I've seen (and embarrassingly, in my early days of software development, even been responsible for) copy/paste chunks of the same code used in multiple places throughout a program instead of creating a single method and using it everywhere the chunk of code is needed.

## Auto-generated Code

Depending on the tools/framework used, something as simple as dragging a control into a GUI editor may generate many lines of code behind the scenes. If one part of a team is responsible for a GUI created with large amounts of auto-generated code and another group is responsible for a project requiring mostly hand-typed code, the developers with auto-generated code will have more lines than the developers typing each line even if they have similar levels of effort and ability.

## Different Roles

A team lead may spend as much or more time either guiding junior developers or in meetings discussing a project's direction as they do writing code. The contributions of an individual may be significant in terms of team leadership, but small in lines of code. Team members more skilled at debugging may spend a week tracking down a difficult to reproduce bug while others spend that same time adding new code in other areas. The relative contributions of those team members should not be measured by the number of lines each has written.

## Closing Thoughts

Developers should be evaluated by their contributions to the team: their knowledge, ability to lead, diversity of viewpoints they can add to discussions, ability to both teach and learn from others, quality of their code, teamwork, etc. Quantitative measurement of developer skill is difficult at best, and LOC is not a substitute for knowing the team and understanding how the individuals contribute to team success.
