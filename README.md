# claude-resources

A collection of reusable resources for working with Claude Code.

## Contents

- **[CLAUDE.md](CLAUDE.md)** — generic, project-agnostic context file. Drop into the root of any repo to give Claude Code a consistent baseline. Covers commit policy, doc sync, conflict handling, verification discipline, command discovery, dependency hygiene, and bug-repro practice, plus behavioral defaults for code quality.

More resources to come.

## Using CLAUDE.md

From the root of any repo:

```bash
curl -fsSL https://raw.githubusercontent.com/nsvirk/claude-resources/main/CLAUDE.md -o CLAUDE.md
```

Or copy `CLAUDE.md` manually. Claude Code loads it automatically into every session in that project. Layer project-specific instructions on top — this is the floor, not the ceiling.

The file has two sections with explicit priority:

- **Rules** — hard constraints.
- **Behavioral Guidelines** — defaults that yield to your explicit instructions when they conflict.

## Sizing & assessment

**749 words / ~1000 tokens.** Comfortably in the "mostly retained" attention band for in-context instructions (rough guide: <200 words = every rule lands; 200–800 = mostly retained; 800–2000 = softer rules drift; 2000+ = attention noise). Long enough to cover real failure modes, short enough that every rule gets weighed each turn.

**Assessment: solid.** No duplication with Claude Code defaults. Rules and Behavioral Guidelines have explicit priority (hard constraints vs. defaults that yield to user instructions). Each rule maps to a recurring class of LLM mistake. Drop-in portable across any project.

## Author

Navdeep Virk ([@nsvirk](https://github.com/nsvirk))

## License

[MIT](LICENSE)
