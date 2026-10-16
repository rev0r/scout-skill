# scout-skill

A Claude Code skill that tells you what you don't know yet, on any topic.

Run `/scout` and it does live web research, throws out hype and old news, checks every find at its
source, and returns a short briefing of developments and insights that are **real, new, useful and
not yet obvious**, each with who it affects and what to watch next.

## What you get

A two-minute briefing:

1. **The bottom line**: how many finds made it, and the most useful one.
2. **Each find**: what it is, what changed and why it matters (one line), who it affects, what to
   watch next (the next dated event, or "No date announced"), its maturity and confidence, and the
   source link.
3. **Watchlist**: promising but unproven items, and what would have to happen for them to graduate.
4. **Just outside the window**: strong finds that were only too old, with dates.
5. **Skipped**: a hyped thing it rejected and why.

If only two things are worth your time, you get two. It never pads the list. The briefing stays
under about 600 words before the sources.

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
/scout longevity research
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
| `--science` | Research turning into something usable: materials, energy, space, biology, climate. |
| `--health` | Medicine, public health, nutrition, fitness, mental health. |
| `--policy` | Laws, regulation, rulings and government programs. |
| `--business` | Companies, markets, industries, labor, consumer behavior. |
| `--focus <topic>` | Anything else, in your own words. Plain words after `/scout` work too. |

Presets combine (`--finance --ai`). With no topic, it sweeps all fields, not just tech.

| other flag | meaning |
| --- | --- |
| `--days N` | How far back "new" reaches. Default 60. |
| `--top N` | How many items to report. Default 5. |
| `--deep` | 15 to 25 searches in extended mode. Default is 8 to 12. |

## How it decides what's worth your time

Every candidate has to pass four tests:

- **Real**: usable today (code, docs, a product you can sign up for). A demo or press release is not enough.
- **New**: appeared or changed materially inside the window.
- **Useful**: you can name who is affected and what changes for them, or the decision it informs.
- **Non-obvious**: not already the lead story everywhere.

Each survivor is then verified at its primary source and labeled:

- **Confirmed**: the primary source was read and an independent source corroborates it.
- **Likely**: the primary source was read but nothing independent backs it yet, or the primary
  source could not be read and several independent professional sources agree (it says which).
- **Unverified**: a single secondary, vendor-only or trade-press source. Never makes the main list.

If a primary source is blocked, it looks for an official mirror, otherwise caps the item at Likely
and names the source it could not read. Vendor comparison pages count as leads, not evidence, and
it says so when a page ranks its own product. If an item involves the maker of the model running
the skill, it discloses that conflict.

An optional adjacent find outside your topic counts toward the item limit, not on top of it. Items
announced but not yet shipped go on the watchlist with a due date.

It is unbiased by design: it ignores your profile, preferences and memory, so only the flags you
type shape what it finds. That is an instruction to Claude, not a hard switch, so for a guaranteed
clean run, turn off your preferences and memory in Settings first.

## Running without approval prompts

In Claude Code, web tools normally ask before they run. The skill's frontmatter lists
`allowed-tools: WebSearch WebFetch Read Write`, which pre-approves web search and fetch plus
reading and writing the `.scout/seen.md` log for the turn that runs the skill. It does not override
your own deny or ask rules, and an organization's managed settings can ignore it. For fully
unattended runs, use a scheduled task and set its permission mode, or add allow rules in your
settings. If you would rather approve each request, delete the `allowed-tools` line.

## Memory

Reported items are logged to `.scout/seen.md` in your current directory, so the next run skips them.
Delete the file to reset. Add `.scout/` to your `.gitignore`. If file tools are unavailable, the
run skips logging and says so in one line.

## Make it weekly

Ask Claude to run `/scout` as a scheduled task and the briefing arrives on its own.

## Changelog

**1.5.0**: pre-approved log access, fallback ladder for blocked primary sources, redefined
confidence tiers, vendor comparison pages treated as leads, tighter briefing format (about 600
words), adjacent find counts toward the item limit, conflict-of-interest disclosure.

## License

MIT
