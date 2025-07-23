# Pathwise Commit Summaries

Pathwise Commit Summaries are a structured format for writing commit summaries that emphasize *location*, *precision*, and *reviewability*. Instead of leading with a verb or a vague prefix, each summary begins with a path--through the codebase or namespace hierarchy--to the exact subject of change. This syntactic discipline reinforces good commit hygiene and encourages commits to be independent, small, descriptive, and contextually scoped.

## Goals

- Maintain linear history
- Promote commit hygiene through syntactic constraint
- Encourage small, auditable deltas
- Emphasize precision of location, with namespace-, path-, or identifier-level specificity
- Maximize descriptive fidelity within the space of a single summary line
- Avoiding noisy prefixes (e.g., `fix:` or `feat:`) that dilute signal
- Preserve special characters (like `/`, `::`, `()` etc.) for code fragments in the message portion

Good Pathwise commit summaries should reshape how you approach version control: each commit becomes a small, reversible, and reviewable unit that stands on its own, yet contributes meaningfully toward a larger goal. This encourages breaking work into narrow, contextual deltas--easy to audit, cherry-pick, re-order, or revert--without losing sight of the broader feature or refactor. The format supports both novice and expert Git users and integrates smoothly into `rebase`-centric workflows across branches and collaborators.

## Non-goals

- Changelog generation
  - Changelogs should be written by humans for humans. That said, a list of Pathwise commits offers a great starting point for distilling code changes into human-readable release notes.
- Pull-request titles or squash commits
  - While similar heuristics can inform PR titles, Pathwise summaries are optimized for atomic commits, not aggregation.
- Merge commits or nonlinear history
  - This convention assumes that your Git workflow keeps development history in its entirety, and favors local rebasing for organization.

## Guidelines

Pathwise commit summaries begin with one or more *path segments*, delimited by colons (`:`), followed by a concise description of the change.

The segments are *semantic* and *hierarchical*, not strictly tied to the filesystem nor any module system. They should intuitively lead the reader to the locus of the change--be it a directory, module, identifier, or other logical location in the structure of the codebase.

### Path segments may refer to:

- Directories leading up to the change (using colons instead of slashes)
- File name(s) where they represent logical units, omitting extensions unless necessary to disambiguate
- Module identifiers (joined with colons; avoid language-specific syntax such as `::` or `.`)
- Type, function, macro identifiers (typically the last segment)
- Any other named entity that helps pinpoint the scope of change

Use the plus sign (`+`) to combine segments at the same hierarchical level when a change affects several similar paths.

### Naming and syntax rules

- The summary must include a short message after the final path segment to describe the nature of the change, preferably beginning with a verb.
- Separate path segments using a colon and a space (`: `).
- Do *not* wrap path segments (or any code) in quotes or backticks.
- Write summaries as plain text--GitHub's rendering is a distraction, not a target.
- Do *not* employ visual markup tricks, which waste space and can be misleading.
- Only include special characters in paths and messages when they are syntactically meaningful in the language.
- Prefer public API identifiers when viable. Internal details should only be referenced when the change is explicitly internal.

If you find it difficult to summarize a commit using this format, it's a strong sign that the change should be split into smaller, more focused commits--perhaps even re-ordered.

# Why not Conventional Commits?

- The verb-prefixes don't add meaningful value to the commit log and don't help with reviewability.
- Changelogs should start from a list of commits since the last tagged release and be curated by a human to communicate relevant information to consumers.
- The prefixes aren't used as part of a readable phrase, even though they could be incorporated more naturally.
- Conventional Commits don't encourage small, focused commits and may lead to sprawling changes being squashed or created as a single commit.
- The format prioritizes the developer's problem statement over the actual implementation detail or architectural change.
- Problems should be explained in pull-request descriptions, not shoehorned into commit summaries.
- Commit message bodies can explain why each change builds on the previous to achieve the intended result.
- Conventional Commit summaries rarely indicate *where* a change was made--likely because they're too broad.
- Ad-hoc scope identifiers in parentheses (`feat(foo):`) can conflict with past or future commits. Even when specific enough to be useful, they still introduce visual noise and consume precious space in the summary line.
