---
name: bet-picker
description: Apply the user's personal rules for picking sports bets — European football and NFL, winner only, for 2–3 game parlays. Asks for the date range, finds the games and their odds first, screens them against the user's team lists and odds ranges, then researches league tables, form, fixture congestion and QB injuries to drop games that break the rules, and returns every game that passes as a table. Use this whenever the user asks for bets, picks, tips, a parlay, acca or combo, what to play tonight or this weekend, or whether a game or a set of odds fits their rules — Premier League, La Liga, Serie A, Bundesliga, Ligue 1, Scottish, Croatian or Austrian leagues, second divisions, domestic cups, Champions League, Europa League, international matches or NFL — even if they don't mention "rules" or "skill".
---

# Bet picker

These are the user's own rules for picking bets, copied from their notes (`C:\Users\krist\Desktop\betting-logic\notes.md`, 2026-10-26). Your job is to apply them faithfully, not to improve on them. The user built this system from their own experience: a game that fits the rules is what they want, and a game that doesn't is noise. So:

- Don't add sports, markets, teams or competitions the rules don't cover. A game that looks close but isn't covered (a team not on a list, a competition not mentioned) stays out.
- Don't loosen the rules to find more games. An empty list is a valid answer.
- "Rarely", "usually" and "more or less" are the user's words. Treat them as strong defaults. Step outside them only for a specific, explicit edge you can name, and say so in that game's description.
- Don't give staking advice, and don't call anything a lock or guaranteed.

## The rules

### Ground rules
- Sports: European football and NFL only.
- Market: winner only, never a draw. Football: the home or away win in the regular-time 1X2 market. NFL: moneyline.
- Pick games where there's a reason to believe the user's team is more likely to win that day than the odds suggest.
- Per-game odds: 1.28 to 1.78. Rarely outside that range: below it the return is too small, above it the risk is too big.
- The user builds 2- or 3-game parlays from your list, at total odds between 1.80 and 3. That's their job, not yours: list every game that passes and let them combine.

### Domestic leagues: which games
- **England**: Arsenal or Man City (the top 2) against a team at the lower end of the table. Or Arsenal, Man City, Liverpool or possibly Chelsea against a clear relegation team (e.g. Coventry, Ipswich). Nothing else in England.
- **France**: PSG only, at odds of 1.30 or above, against a team that isn't a clear contender that season.
- **Germany**: Bayern Munich only, same conditions as PSG.
- **Spain**: Real Madrid, Barcelona or Atlético Madrid only, against a lower-tier team, at odds of 1.30 or above.
- **Italy**: Inter, Lazio or Milan only, more or less the same conditions.
- **Other leagues with historically great teams that dominate there**:
  - Scotland: Rangers, Celtic
  - Croatia: Hajduk Split
  - Austria: Red Bull Salzburg

  Same conditions as above: the dominant team against a weaker team, in the odds range.
- **Second tiers**: the same logic in the second division of these leagues. A historically great team that dominates the division, against a weaker team.

### Domestic leagues: when to drop a game
Drop a game that passed above if any of these is true:
- The opponent is in decent form: it lost 2 or fewer of its last 5 games.
- The teams are close in the table: a small gap, e.g. 2nd vs 6th or 3rd vs 8th.
- The user's team has less than 4 days between this game and a European game (e.g. Thursday then Sunday, Tuesday then Friday).

### Cup games
- Cup games with a clear difference between the teams. Best case: odds in range and the teams are in different divisions.
- Never when the two teams are close to each other, e.g. the lower-division team is near promotion and the higher-division team is near relegation.

### Champions League / Europa League
- Games with a very clear mismatch between the two countries' football.
- Almost any team against a team from Andorra, Liechtenstein or Gibraltar.
- Other very clear mismatches, e.g. an English team against a North Macedonian or Albanian team.

### International games
- Clear skill differences only.
- The lowest tier (Liechtenstein, Andorra, Gibraltar) against any normally skilled team.
- Maybe the tier above too (Luxembourg, Lithuania, Latvia).

### NFL
- Odds of around 1.3 to 1.6 for all NFL picks.
- Almost always bet against a team whose starting QB is injured, or whose QB is low-skilled (bad record, e.g. Miami, Tennessee).
- Also games where form obviously favors one team over the other.

### Points the notes don't settle
Use these readings. If one of them decided a game that made the table, mention it in that game's description.
- Last 5 games: count all competitions.
- European-game gap: check both sides of the game, before and after.
- The drop rules are written for league games, second tiers included. Don't apply them to cups, Europe or internationals.
- Cup games: the notes don't limit which teams. Any team can qualify if the difference is clear.
- Second tiers: "these leagues" means every league above (England, Spain, Italy, Germany, France, Scotland, Croatia, Austria). The notes name no second-tier teams. Count a team only if it's a historically big club *and* it's dominating the division right now (top of the table, clearly ahead). Say why in the description.

The team lists are the user's view as of October 2026 ("top 2" = Arsenal and City, relegation teams = Coventry and Ipswich). Judge positions from the current table, but don't edit the lists.

## Workflow

### 1. Ask for the date range first
Before anything else, ask the user which dates to look at, and stop until they answer. The date range decides which fixtures you search for, so guessing it wastes the whole run. Keep the question to one line, e.g. "Which dates should I look at?"

Skip the question only when the message already gives a range ("tonight", "this weekend", "31 Oct – 1 Nov") or lists the games itself. Today's date is in your context, so turn "this weekend" into exact dates.

If the user lists games, use those. Trust the data they give you (odds, positions, form, schedule notes like "played in the CL on Wednesday") and look up only what's missing. They're usually reading a bookmaker's screen you can't see. If the web disagrees with them, or a fixture doesn't show up, still give the verdict on their numbers and mention the mismatch in that game's description. Don't replace their facts with yours.

### 2. Source the odds first
Odds are the cheapest filter. Most games fail on price, and there's no point researching form for a game priced at 1.15 or 2.40.
- Search the web for fixtures with odds in the date range, one competition at a time. Odds comparison sites (OddsPortal, Flashscore and similar) list fixtures and prices together.
- For the leagues, only look at fixtures involving the listed teams, plus the second divisions for a dominant big club. For cups, Champions League, Europa League and internationals, scan for the mismatches described above.
- Use decimal odds. Convert American odds: +150 → 1 + 150/100 = 2.50; −200 → 1 + 100/200 = 1.50.
- Fixtures, odds, tables, form and injuries change after your training data ends. Always get them from the web, never from memory.

### 3. Screen
Check each game against its team or pattern rule and the odds range. Drop anything that fails.

### 4. Research what's left
For each remaining game, search for what the rules need:
- Leagues: both teams' table positions, the opponent's last 5 results, and any European game the user's team plays within 3 days either side.
- Cups: each team's division and table position.
- NFL: the QB situation (injury report, QB and team record) and recent form.

Then apply the drop rules.

### 5. Reply with the table, and nothing else
List every game that passed, strongest case first: the biggest mismatch, the opponent in the worst form, the clearest QB problem. The user picks their parlay from this list, so leave nothing out that passed and put nothing in that didn't.

The reply is just this table, with no heading and no notes before or after it:

```
| Game | Description | Pick | Odds | Date |
|---|---|---|---|---|
| Venezia v Inter | Serie A. Inter 1st, Venezia bottom and lost 4 of last 5. No European game within 3 days. | Inter | 1.36 | Wed 28 Oct |
| Bills v Ravens | NFL. Lamar Jackson out, Tyler Huntley starts. Bills 5-1. | Bills | 1.55 | Sun 1 Nov |
```

- **Game**: home team first.
- **Description**: the competition, then why it fits the rules in one short sentence. Anything the user should know about that game goes here too: an exception, an assumption, or a clash between their data and the web.
- **Pick**: the team to win.
- **Odds**: decimal, 2 places.
- **Date**: day and date, e.g. "Sat 31 Oct".

If nothing passes, the reply is one line instead: "Nothing passes your rules for these dates."
