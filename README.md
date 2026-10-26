# bet-picker

A [Claude Code](https://claude.com/claude-code) skill that applies one person's rules for picking sports bets: European football and NFL, winner only, built for 2–3 game parlays.

You give it a date range. It finds the fixtures and odds on the web and screens them against the rules: team lists, odds ranges, league table gaps, opponent form, fixture congestion around European games, and NFL quarterback injuries. Then it returns every game that passes in one table:

| Game | Description | Pick | Odds | Date |
|---|---|---|---|---|
| Venezia v Inter | Serie A. Inter 1st, Venezia bottom and lost at Genoa on Sunday. Inter's next European game is 6 days later. | Inter | 1.36 | Wed 28 Oct |
| Eagles v Cowboys | NFL. Jalen Hurts is out for the season, so backup Tanner McKee starts. | Cowboys | 1.46 | Mon 26 Oct |

Under the table, one sentence gives the tokens the run used and what they would cost at Anthropic API rates. `scripts/run_cost.py` reads these from the Claude Code session transcript.

The rules are personal and opinionated. They're all in [SKILL.md](SKILL.md), so read them before you use the skill, and edit them to match your own.

## Install

Copy this folder into your Claude Code skills directory:

```
git clone https://github.com/escadesupremo/bet-picker ~/.claude/skills/bet-picker
```

## Use

In Claude Code, run `/bet-picker`, or just ask something like "what can I play this weekend?". If you don't give dates, it asks for them first. You can also paste in games with odds, table positions and form, and it checks them against the rules using your numbers.

Odds come from public comparison sites and move constantly. Always check the price at your own bookmaker.

## Tests

`evals/` holds the test cases used to develop the skill. Each case has a prompt and the checks a good answer must pass. With Claude Code you can run them from this folder:

```
claude plugin eval . --allow-tools Write,Edit,Bash
```

## Disclaimer

This is a personal betting system, not advice. It doesn't predict results, and no game it lists is a sure thing. Bet only what you can afford to lose.
