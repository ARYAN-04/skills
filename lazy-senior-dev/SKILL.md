---
name: lazy-senior-dev
description: "Use when user explicity calls the skill or when something is broken in the code and user is asking for fixes"
disable-model-invocation: true
---
Avoid overengineering and unnecessary complexity. Ask: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

Example: the user asks for a date picker. Instead of installing flatpickr, writing a wrapper component, adding a stylesheet, and starting a discussion about timezones, write:

<input type="date">

Before writing any code, stop at the first rung that holds:

    Does this need to be built at all? No? Skip it. (YAGNI)
    Does it already exist in this codebase? Reuse the helper, util, or pattern.
    Does the standard library do it? Use it.
    Does a native platform feature cover it? Use it.
    Does an already-installed dependency solve it? Use it.
    Can this be one line? Do it.
    Only then: write the minimum code that works.

The ladder runs after you understand the problem, not instead of it. Read the task and the code it touches, trace the real flow end to end, then climb.

Bug fix = root cause, not symptom. A report names a symptom. Before editing, grep every caller of the function you are about to touch. One guard in the shared function is smaller than one guard per caller, and patching only the path the ticket names leaves sibling callers broken. Fix it once, where all callers route through.

Rules:

    No unrequested abstractions.
    No avoidable dependencies.
    No speculative scaffolding.
    Prefer deletion over addition.
    Boring over clever.
    Fewest files possible.
    Shortest working diff wins once you understand the problem.
    Pick the edge-case-correct option when two standard-library approaches are the same size.

Complex request? Ship the lazy version and question it in the same response: "Did X. Y covers it. Need full X? Say so." Always tell the user what you skipped. If the user insists on the full version, build it, no re-arguing.

When not to be lazy:

    Do not cut validation, error handling, security, accessibility, data-loss protection, or real edge cases.
    Do not skip understanding. A small diff you do not understand is just laziness dressed up as efficiency.
    Non-trivial logic leaves one runnable check behind. Trivial one-liners need no test.
