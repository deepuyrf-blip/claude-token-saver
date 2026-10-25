---
name: token-saver
description: Use when the user asks to save tokens/credits, work cheaply, or "be efficient", and before exploring a codebase, reading large files, or doing a multi-step task. Enforces token-efficient habits so credits are not wasted.
---

# Token-efficient working rules

Goal: complete the task using the **fewest tokens**. Follow these rules whenever
this skill is active.

## Reading files
- Never read a whole file when you need one thing. Use `rg -n "pattern" <path>` to
  find the line, then read a **small range** around it.
- Do **not** re-read a file you already read in this session — recall it instead.
- For large files, read targeted ranges (offset/limit), not the whole file.
- Prefer `rg --files` / `rg -n` / `rg -c` over dumping file contents.
- Never `cat` big files or logs. Filter first: `tail -n 50`, `head -n 50`, `grep`.

## Searching
- Narrow with globs and types: `rg -n "X" -g '*.ts'`, `rg -n "X" -t py`.
- Cap every listing: `| head -n 50`.
- If a search returns nothing, refine the pattern — don't broaden to reading files.

## Doing the work
- Make the **smallest** change that satisfies the request. No drive-by refactors.
- Batch independent edits; avoid editing the same file over and over.
- Never run a command whose output you will not read.
- Don't narrate each step. Act, then report the result briefly.

## Responding
- **Answer first**, then only the detail that is needed.
- No restating the request, no filler, no repetition, no "Great question".
- Use short lists; skip long prose for simple answers.
- Do not paste back large blocks you just read — reference them by path/line.

## Output-size discipline
- Before any command that may produce huge output, add `| head`, `| tail`, or a
  grep filter.
- Avoid printing whole dependency trees, full logs, or entire directories.
- When you already know the answer, don't run a command to confirm it.

## Context hygiene
- Keep a short mental summary of what you've already learned; don't reload it.
- When the task is done, stop — don't keep exploring "just in case".
- If the user only asked for a plan/answer, give that; don't implement unasked.
