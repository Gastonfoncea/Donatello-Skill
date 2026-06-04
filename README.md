# Donatello

A Claude Code skill that judges the visual taste of a landing page using a personal rubric — in Spanish, first-person, with strong opinions. It detects AI slop, template clichés, and a lack of editorial criterion. It returns a structured critique with detected syndromes, negative and positive signals, a section-by-section analysis, and suggested fixes.

It's not a performance analyzer or an accessibility auditor. It's a taste judgment — the kind of critique a senior designer would give looking at the landing without anesthesia.

## What it returns

Every critique follows the same structure:

1. **First impression** — gut reaction within the first 2 seconds.
2. **Category and target audience** — what the landing is measured against.
3. **Verdict** — one of `excelente`, `bueno`, `decente`, `mediocre`, `slop`, with justification.
4. **Detected syndromes** — recognizable clusters (AI Tool slop, SaaS template slop, Framer template slop, Web3/Crypto slop, Agency/studio slop).
5. **Negative signals** ordered by severity, with a concrete location and a verbatim quote when applicable.
6. **Positive signals** when there are any — without forcing positives if there aren't.
7. **Section-by-section analysis** (hero, features, pricing, testimonials, footer).
8. **Suggested fixes** — one per problem, one line each.

## Hard requirement: it needs pixels

This skill **does not work with HTML alone**. 70% of the rubric lives in color, typography, spacing, visual hierarchy, and component treatment — things that can't be evaluated from markup. Judging taste by reading HTML is like critiquing a painting by reading the list of materials.

For the skill to work you need one of these two pixel sources:

1. **A screenshot** pasted into the chat (ideal: desktop + mobile).
2. **A browser MCP** installed in Claude Code. The most direct one is Microsoft's Playwright:

   ```sh
   claude mcp add playwright npx '@playwright/mcp@latest'
   ```

   With Playwright available, the skill navigates the URL on its own and takes the screenshots before applying the rubric.

If all you have is a URL and no browser MCP is installed, the skill will stop and ask you for one of the two options above. It does not improvise a critique from WebFetch.

## Installation

The skill is a single `SKILL.md` file. Claude Code loads it from `~/.claude/skills/donatello/`.

```sh
git clone git@github.com:Gastonfoncea/Donatello.git ~/.claude/skills/donatello
```

Restart Claude Code and the skill becomes available globally.

If you prefer to keep the repo elsewhere and symlink it:

```sh
git clone git@github.com:Gastonfoncea/Donatello.git /path/wherever/you/want
ln -s /path/wherever/you/want ~/.claude/skills/donatello
```

## How it activates

The skill triggers when you ask Claude for a landing critique with phrases like:

- "critica esta landing"
- "qué opinás de esta página"
- "analizá esta landing page"
- "is this AI slop?"
- "review this landing"

Or simply by pasting a screenshot or a landing URL and asking for a visual judgment.

## Language and tone

The skill always responds in **Spanish**, in **first person**, with dry humor and no filler. It doesn't use empty words ("modern", "clean", "elegant", "polished", "flawless"): if it needs one of those, it reformulates with something concrete. If it sees slop, it says so. If it sees good criterion, it says that too — without hedging.

## The rubric

The heart of the skill is the full rubric inside `SKILL.md`: categories, syndromes, hard rules, per-section criteria, and the central principle behind it all — *does it look like someone decided this, or did it come by default?*

## License

MIT — see [LICENSE](LICENSE).
