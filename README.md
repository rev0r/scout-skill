# scout-skill

A Claude Code skill that tells you what you don't know yet.

Run `/scout` and it does live web research, throws out hype and old news, checks every find at its
source, and returns a short briefing of technologies and insights that are **real, new, useful and
not yet obvious**, each with a first step you can try in under an hour.

## What you get

A two-minute briefing:

1. **The bottom line**: how many finds made it, and the most useful one.
2. **Each find**: what it is, why it matters and to whom, a first step to try, its maturity and
   confidence, and the source link.
3. **Watchlist**: promising but unproven items, and what would have to happen for them to graduate.
4. **Just outside the window**: strong finds that were only too old, with dates.
5. **Skipped**: a hyped thing it rejected and why.

If only two things are worth your time, you get two. It never pads the list.

## Install

**Plugin install (Claude Code):**

```
/plugin marketplace add rev0r/scout-skill
/plugin install scout-skill@scout-skill
```

Installed as a plugin, the skill appears as `/scout-skill:scout`.

**Manual copy, for plain `/scout`:**

```
git clone https://github.com/rev0r/scout-skill.git
cp -r scout-skill/skills/scout ~/.claude/skills/
```

**Project-local:** copy the `scout` folder into your repo's `.claude/skills/`.

Requires Claude Code with web search and fetch available. No other dependencies.

## Use

```
/scout
/scout --finance
/scout --technology --days 14
/scout --finance --ai --top 3
/scout --deep --focus "tokenized collateral"
```

| focus flag | what it hunts |
| --- | --- |
| `--technology` | New tools, platforms and infrastructure: software, hardware, developer tooling, automation, open source. |
| `--finance` | Valuation and modeling tools, FP&A and treasury, deal and diligence tooling, payments and market infrastructure, accounting automation, rule changes. |
| `--strategy` | Market and competitive intelligence, research and synthesis tooling, planning and decision methods. |
| `--ai` | New models, agents and AI tooling that are usable now, not announced. |
| `--data` | Databases, BI, pipelines, visualization, query tools. |
| `--focus <topic>` | Anything else, in your own words. |

Presets combine (`--finance --ai`). With no focus flag, it hunts broadly.

| other flag | meaning |
| --- | --- |
| `--days N` | How far back "new" reaches. Default 60. |
| `--top N` | How many items to report. Default 5. |
| `--deep` | 15 to 25 searches in extended mode. Default is 8 to 12. |

## How it decides what's worth your time

Every candidate has to pass four tests:

- **Real**: usable today (code, docs, a product you can sign up for). A demo or press release is not enough.
- **New**: appeared or changed materially inside the window.
- **Useful**: you can name who benefits, what they can now do, and a first step.
- **Non-obvious**: not already the lead story everywhere.

Each survivor is then verified at its primary source and labeled Confirmed, Likely or Unverified.
Unverified items never make the main list.

## Memory

Reported items are logged to `.scout/seen.md` in your current directory, so the next run skips them.
Delete the file to reset. Add `.scout/` to your `.gitignore`.

## Make it weekly

Ask Claude to run `/scout` as a scheduled task and the briefing arrives on its own.

## License

MIT
