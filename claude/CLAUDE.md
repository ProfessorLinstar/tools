## Git
- For draft PRs or branches without a PR, always use `git -c commit.gpgsign=false ...` when making commits. For PRs that are ready for review, always sign commits.
  - This holds even when a CI check (e.g. in-toto attestation) needs a signed HEAD: report that failure as expected on drafts instead of signing.
- When making branches, name then "andywang/..." where ... is the intended change
- Always make sure that you're working with the right branch locally. If the user asks for changes to a particular PR, then you should check out that PR first locally before making your changes.
  - If there are untracked/unstaged changes, prompt the user for further instruction.
- You can and should make commits to the local branch without explicit permission.
- Only push changes to remote if there is not a PR open for the current branch or if the PR is a draft. In those cases push without asking.
- Once I've agreed to a plan, carry out every step (checking out the PR, follow-up draft PRs, pushes) without stopping to ask "should I …?". If a message has an obvious typo, act on the obvious intent instead of asking.

### Github PRs
- When iterating on an open or draft PR, add new commits instead of amending existing ones and force pushing
- Prefix the first commit message with \[PR-start <branch-name>\]
- Never add comments in github unless I say exactly to "reply" to a comment.
- Double check for permission before adding comments.
- Always create PRs in draft mode, never ready for review
- When marking a PR as ready for review, sign and rebase the PR if any commits are unsigned
- When retargeting a stacked PR (e.g. after a parent PR merges), update the stack list in the description accordingly.


## Code changes
- Make the smallest change that solves the problem. No incidental refactors, renames or cleanups of existing code; if one seems worthwhile, ask first or put it in a separate preflight PR.
- When the change itself would copy the same logic into several places, factor it into a shared helper in the same PR instead.
- Don't add defensive code (try/catch, env scrubbing, cleanup hooks, workarounds applied "everywhere just in case") unless you've confirmed it's needed. Prefer the simplest approach and measure before optimizing.

## Verification
- Before giving me a link you constructed, open it (e.g. with the browser tools) to check it works.
- Before claiming something is absent, impossible or untestable, exhaust the options (complete search, config overrides, custom permissions/policies) and say what you checked.

## Design
- Prefer the simplest, most idiomatic design. Before adding polling, generated files or complex awk/sed, offer a simpler alternative.
- Degrade gracefully (fall back to default behavior with a warning) rather than failing hard.
- Don't remove existing functions or behavior that aren't part of the ask.
- Don't write migration or compatibility code for old formats, markers or files unless asked; handle them case by case.

## Commenting
- You may author trivial comments yourself, as well as new comments that are straightforward and have strong precedent in the surrounding code for what they should look like.
- Otherwise, whenever something needs to be documented in code (e.g. javadocs), add a `TODO(andywang): add comment` instead.
- If an existing comment should be changed, add `TODO(andywang): update comment` instead, unless the change is trivial.
- You may copy comments verbatim, but if the comment needs to be adapted non-trivially, then add `TODO(andywang): update comment` instead.
- If some behavior deserves explanation, you may add a github comment IF the PR is in draft mode. Otherwise flag this to the user directly.

## Formatting
- Don't manually wrap markdown unless existing code already does it
- Wrap comments with a text width of 120 characters
