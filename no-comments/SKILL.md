---
name: no-comments
description: Audit and strip unnecessary comments, dead code, and workaround justifications from the codebase while preserving essential contracts, legal headers, and required platform constraints.
---

# No Comments

Audit the codebase to eliminate unnecessary comments, remove commented-out dead code, and replace workaround justifications with clear, self-explanatory code and structural guarantees.

## Core Philosophy

Code should be clean, expressive, and self-documenting. Explanatory comments narrating what code does, or workaround rationalizations defending fragile code, often indicate underlying architectural issues, unclear naming, or missing types.

Instead of writing or preserving prose to explain confusing code, fix the code at its root cause.

## Scope

- Operate on files or diffs explicitly provided by the caller.
- If no scope is specified, operate on the current working tree diff against the base branch (default `main`).

## Comment Classification

### Comments to Remove
1. **Explanatory Narration:** Line-by-line commentary describing *what* the code is doing (e.g., `// loop through items`, `// set status to active`). The code must speak for itself.
2. **Commented-Out Dead Code:** Inactive code blocks, commented-out debugging statements, or legacy implementations. Version control preserves history.
3. **Banners and Section Dividers:** Visual clutter such as `// =====================` or `// ----- Helper Functions -----`.
4. **Workaround Excuses:** Comments rationalizing hacks or deferred fixes (e.g., `// fine for now`, `// too risky to touch`, `// hack for upstream bug`). Fix the root cause or remove the workaround.
5. **Redundant Paraphrasing:** Comments that merely rephrase function, variable, or type names without adding non-obvious context.

### Comments to Preserve (Exceptions)
1. **Legal and License Headers:** Copyright notices and licensing headers required by open-source licenses or organizational policies.
2. **External / Platform Constraints:** Documentation of non-obvious behavior forced by third-party dependencies, vendor APIs, OS quirks, or protocols that cannot be reshaped.
3. **Public API Contracts:** Formal doc comments (JSDoc, godoc, Python docstrings) defining contracts for external consumers of a public API.
4. **Issue or RFC Links:** Explicit references to issue tracker tickets, RFCs, or external specifications that explain constraints code cannot express.
5. **Legitimate Tooling Pragmas:** Strictly necessary directives (such as `// prettier-ignore` or pedantic style-only linter suppressions where the linter rule is faulty).

## Suppression Auditing

Inspect linter and compiler suppressions (`eslint-disable`, `@ts-ignore`, `@ts-expect-error`, etc.):
- If a suppression masks a real type error, correctness bug, or safety risk, **remove the suppression** and fix the underlying types or implementation.
- Only retain suppressions if the tooling rule is provably broken or enforcing an inapplicable stylistic convention.

## Constraint Encoding

Comments warning against changes (e.g., `// do not remove`, `// do not alter wording`, `// order matters`):
- Do not leave passive comment warnings in place if they can be enforced systematically.
- Convert them into **structural encodings**:
  - Strict type definitions (discriminated unions, branded types, readonly modifiers).
  - Runtime validation or assertions (`assert(condition)`).
  - Automated unit or integration tests that fail if the invariant is violated.
  - Linter rules or static checks.
- If an automated check cannot be implemented within scope, document the constraint in the summary report.

## Step-by-Step Workflow

1. **Establish Scope:** Identify target files from the user request or working tree diff against `main`.
2. **Audit Comments:** Scan all target files and classify each comment according to the Keep vs. Remove criteria above.
3. **Strip Prohibited Comments & Dead Code:** Delete all narrative comments, section banners, dead code, and redundant prose.
4. **Refactor Code Smells:** Where comments were masking awkward or confusing internal logic, refactor the code (extract functions, rename symbols, clarify branching) so that the behavior is obvious without commentary.
5. **Audit and Fix Suppressions:** Remove unjustified type/linter suppressions and resolve the underlying errors.
6. **Encode Constraints:** Convert load-bearing constraint comments into types, tests, or assertions.
7. **Report:** Output a concise summary listing:
   - Files inspected and touched.
   - Total comment deletions and dead code lines removed.
   - Retained comments with specific justification for each.
   - Refactorings performed to replace comments.
   - Structural encodings or remaining open constraints.
