---
name: monthly-summary
description: Generate a concise per-day Git activity report for the current calendar month by inspecting the current user's commit diffs in the current repository.
---

# Monthly Summary

Generate a Markdown report of the authenticated user's Git activity for the
current calendar month.

1. Confirm the current directory is inside a Git worktree with
   `git rev-parse --is-inside-work-tree`. If it is not, explain the
   precondition and stop.
2. Read the author name with `git config user.name`. If it is empty, explain
   that `user.name` must be configured and stop.
3. Determine the first day of the current month and its last day at
   `23:59:59`. Use the local calendar month and keep the resulting `YYYY-MM`
   value for the output filename.
4. Collect every matching commit from all refs during that date range with
   the configured author, retaining each short hash and its calendar date:

   ```text
   git log --all --since="YYYY-MM-01" --until="YYYY-MM-DD 23:59:59" --author="<author>" --pretty=format:"%h %ad | %s" --date=short
   ```

5. Group the commits by date. For every commit, inspect its actual patch with
   `git show` or an equivalent `git diff`; do not infer the day's work from
   commit subjects alone. Use those patches to write one concise paragraph
   per active day, no longer than 500 characters, describing the work that
   was actually done.
6. Write `monthly-summary-YYYY-MM.md` in the current directory with this
   structure:

   ```markdown
   # Git Activity Summary - Month YYYY

   ## YYYY-MM-DD

   Summary paragraph (at most 500 characters).

   Commits:
   - `abc1234`
   ```

   Include one `## YYYY-MM-DD` section per active day and list every commit
   hash for that day. If there are no matching commits, still create the
   file and clearly state that no activity was found for the month; do not
   invent activity or add empty day sections.
7. Report the path to the created file when finished.
