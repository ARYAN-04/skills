---
name: recall
description: Reconstruct recent working context, decisions, and progress from agent logs, conversation transcripts, and workspace state, then hand back a tight current-state brief and recommended next moves.
---

# Recall

Rebuild recent working context and hand back a tight, high-signal capsule of where things stand now and what to do next.

## Core Process

Context lives across agent session logs, live git state, and project history. This skill mines past agent transcripts and logs to restore working memory before resuming or starting work.

### 1. Identify and Request Agent Logs

Before analyzing, determine the log source:
- If the user provided the agent logs, file paths, transcript URLs, or session IDs in their prompt, use them directly.
- **If the user did not specify the log source:**
  - Ask the user directly which agent logs or conversation transcripts they want to recall (e.g., specific log file paths, session IDs, or exported transcript files).
  - Clarify the scope: ask for any specific topic, feature, or time window they want to focus on (default: last 7 days).

### 2. Mine Agent Logs and Transcripts

Once the logs are identified, parse them for actionable context:
- **User Goals:** The primary objectives requested and any subsequent course corrections.
- **Key Decisions:** Architecture, schema, library, or design choices made, and alternatives rejected.
- **Open Threads:** Tasks started but incomplete, pending verifications, or deferred steps.
- **Blockers and Struggles:** Errors encountered, flaky tests, tool failures, or user pushbacks.
- **Artifacts:** Branches created or checked out, commit hashes, pull requests, and modified file paths.

### 3. Verify Against Live Workspace State

Ground the log findings in the current live environment:
- Check `git status` for uncommitted modifications or untracked files.
- Check `git log -n 5 --oneline` and `git branch` to locate current branch position relative to main.
- Verify whether the changes discussed in the logs were merged, still in flight, or discarded.

### 4. Synthesize the Brief

Format the recalled context into the standard output contract below. Keep it tight, direct, and factual.

---

## Output Contract

Lead with the capsule, followed by threads, problems, and the next move:

- **Capsule:** At most 5 bullet points. What this work is and where it stands overall.
- **Threads:** One line per active work stream, prefixed with exactly one status tag:
  - `[merged #N]`
  - `[open PR #N]`
  - `[in flight <branch>]`
  - `[verified, uncommitted]`
  - `[reverted #N]`
  - `[planned, not started]`
- **Problems:** At most 5 recurring issues, user-reported symptoms, or regressions from prior attempts, so work begins where the last attempt stopped.
- **Next Move:** The single most useful, concrete next action to take.
