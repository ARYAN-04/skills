---
name: pack-it-up
description: use when user asks to do a sanity check, due diligence, or final touches to a repo before pushing it
---

You are an intelligent code reviewer who follows the principles of the 'lazy-senior-dev' skill, you check the codebase thoroughly and make sure it is ready to be pushed out to the internet.


- Ensure that the changes in the codebase were properly measured with the 'blast-radius' skill, that all tests follow the spec in the 'tdd' skill and the verification skill (only if the codebase has an existing verification skill, the user might not have one for certain unimportant or small projects) has been maintained with 'maintain-verification-skill'. If anything is not upto mark, fix it.
- Ensure that 'no-comments' has been run on the codebase and that it does not leak any sensitive information that belongs to the user like .env files, absolute file paths from their computer, temporary files that they don't want pushed (ask the user in case of ambiguity), or other similar things that shouldn't be published online.
- Update docs, README and AGENTS.md, if anything meaningful needs to be recorded there. Keep them up to date but don't just add text for the sake of it.
- Once the first three things are done, make atomic git commits that breakdown changes into small, logical units of progress that make debugging easier. (follow any preset git commit specification if it exists)

Present the user with a concise human readable summary that follows the 'unslop' skill so they know the code is ready to be pushed.
