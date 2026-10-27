---
name: bet-picker
description: Applies the user's personal rules for picking sports bets (European football and NFL, winner only, for 2–3 game parlays). Asks for a date range, finds fixtures and odds first, screens them against the user's team lists and odds ranges, researches tables, form, fixture congestion and QB injuries, and returns every game that passes as one table. Use it whenever the user asks for bets, picks, tips, a parlay, acca or combo, what to play tonight or this weekend, or whether a game or a set of odds fits their rules, in any competition they play: Premier League, La Liga, Serie A, Bundesliga, Ligue 1, the Portuguese, Scottish, Croatian, Austrian, Hungarian, Danish, Polish, Greek and Serbian leagues, second divisions, domestic cups, Champions League, Europa League, internationals or NFL. Use it even if they don't say "rules" or "skill".
---

# Bet picker

These are the user's rules for picking bets, copied from their notes (`C:\Users\krist\Desktop\betting-logic\notes.md`, October 2026). Apply them faithfully; don't improve on them. The user built this system from experience: a game that fits the rules is what they want, and anything else is noise.

- **Stay inside the rules.** No sports, markets, teams or competitions the rules don't cover. A game that looks close but isn't covered stays out.
- **Don't loosen them to find more games.** An empty list is a valid answer.
- **Respect the hedges.** "Rarely", "usually" and "more or less" are the user's words: treat them as strong defaults. Break one only for a specific edge you can name, and say so in that game's description.
- **No staking advice**, and nothing is ever a lock.

## The rules

### Ground rules
- European football and NFL only.
- Winner only, never a draw: the home or away win in football's regular-time 1X2 market, the moneyline in the NFL.
- The team you pick must be at least a better-known second-division club, such as a former top-flight side. A lesser-known second-division pick: rarely. A pick from below the second division: never. The opponent can come from any level.
- In lower-level games, the team you pick must also be in good form: drop the game if it lost 3 or more of its last 5.
- Only games where there's a reason to think the user's team is more likely to win that day than the odds suggest.
- Odds per game: 1.28 to 1.78. Rarely outside that: below it the return is too small, above it the risk is too big.
- The user combines your games into 2- or 3-game parlays at total odds of 1.80 to 3. That's their job, so list every game that passes.

### Leagues: which games
The user plays these countries' leagues and no others: England, Spain, France, Germany, Italy, Portugal, Scotland, Croatia, Austria, Hungary, Denmark, Poland, Greece and Serbia.
- **England:** Arsenal or Man City (the top 2) against a team at the lower end of the table. Or Arsenal, Man City, Liverpool or possibly Chelsea against a clear relegation team (e.g. Coventry, Ipswich). Nothing else in England.
- **France:** PSG only, at odds of 1.30 or above, against a team that isn't a clear contender that season.
- **Germany:** Bayern Munich only, on the same terms as PSG.
- **Spain:** Real Madrid, Barcelona or Atlético Madrid only, at odds of 1.30 or above, against a lower-table team.
- **Italy:** Inter, Lazio or Milan only, on more or less the same terms.
- **Portugal:** Porto, Sporting or Benfica, the user's usual picks there, and sometimes Braga as a fourth. Same terms: against a weaker team, within the odds range.
- **Scotland, Croatia, Austria:** the historically great teams that dominate there: Rangers and Celtic, Hajduk Split, Red Bull Salzburg. Same terms: the dominant team against a weaker one, within the odds range.
- **Hungary, Denmark, Poland, Greece, Serbia:** the same logic. The historically great teams that dominate there, against a weaker team, within the odds range.
- **Second divisions** of all these leagues: the same logic. A historically great club that dominates the division, against a weaker team.

### Leagues: when to drop a game
Drop a league game if any of these is true:
- The opponent is in decent form: it lost 2 or fewer of its last 5 games.
- The teams are close in the table, e.g. 2nd v 6th or 3rd v 8th.
- The user's team plays a European game less than 4 days before or after (e.g. Thursday then Sunday, Tuesday then Friday).

### Cups
- Games with a clear difference between the teams. The best case is odds in range and the teams in different divisions.
- Never when the teams are close, e.g. the lower-division team is near promotion and the higher-division team is near relegation.

### Champions League and Europa League
- Only very clear mismatches between the two countries' football.
- Almost any team against a team from Andorra, Liechtenstein or Gibraltar.
- Other very clear mismatches too, e.g. an English team against a North Macedonian or Albanian one.

### Internationals
- Clear skill differences only.
- The lowest tier (Liechtenstein, Andorra, Gibraltar) against any normally skilled team.
- Maybe the tier above too (Luxembourg, Lithuania, Latvia).

### NFL
- Odds of around 1.3 to 1.6.
- Almost always bet against a team whose starting QB is injured, or whose QB is low-skilled (bad record, e.g. Miami, Tennessee).
- Also games where form obviously favors one team.

### Where the notes are unclear
Use these readings. When one of them decides whether a game makes the table, say so in a few words in its description.
- Last 5 games: all competitions.
- European-game gap: it counts on either side of the game.
- The drop rules apply to league games, second divisions included, but not to cups, Europe or internationals.
- Cups: the domestic cups of the countries in the league list, league cups included (e.g. Portugal's Taça da Liga). Any team can qualify, not just the listed ones, if the difference is clear and the team you pick meets the team-level rule.
- Hungary, Denmark, Poland, Greece, Serbia: the notes name no teams. Count a club only if it's historically one of that league's dominant teams, and say which in its description.
- Lower-level games: any game where either team is from the second division or below. That covers cup ties against lower-division sides and second-division league games.
- Team level: "better-known" is a judgement call. Count former top-flight clubs and big names; when it's borderline, say so in the description. The rule is about club divisions, so it doesn't apply to internationals.
- Second divisions: the notes name no teams, so count a club only if it's historically big *and* clearly top of its division right now. Say why in its description.

The team lists reflect the user's view in October 2026: Arsenal and City are the top 2, Coventry and Ipswich the relegation teams. Check positions against the current table, but don't change the lists.

## Workflow

### 1. Get the date range
If the message gives no date range and lists no games, introduce the skill and ask for the range in two short lines, then stop until the user answers:

> This skill helps you find high-confidence football and NFL odds to complement your parlay.
> Which dates should I look at?

The range decides which fixtures you search for, so a guess wastes the whole run.

If the message gives a range ("tonight", "this weekend", "until Friday morning"), turn it into exact dates using today's date.

If the user lists games, check those. Trust their data (odds, positions, form, notes like "played in the CL on Wednesday") and look up only what's missing; they're usually reading a bookmaker's screen you can't see. If the web disagrees, or a fixture doesn't show up, judge the game on their numbers and mention the clash in its description.

### 2. Find the odds first
Price is the cheapest filter. Most games fail on it, so don't research form for a game priced at 1.15 or 2.40.
- Search one competition at a time for fixtures and odds in the date range. Odds comparison sites such as OddsPortal list both.
- In the leagues, only look at fixtures involving the listed teams, plus second-division games for a dominant big club. In cups, check every domestic cup and league cup of the league-list countries that has games in the range. In cups, Europe and internationals, scan for the mismatches described above. Skip any cup tie where both teams are below the second division straight away, without looking up its odds: there's no team you could pick.
- Comparison sites often lack cup prices. Try betting previews and tipster sites. If you still can't find a price, leave the game out.
- Use decimal odds. Convert American odds: +150 is 1 + 150/100 = 2.50; −200 is 1 + 100/200 = 1.50.
- Fixtures, odds, tables, form and injuries all change after your training data ends. Get them from the web, never from memory.

### 3. Screen
Check each game against its rule and the odds range, and drop whatever fails.

### 4. Research what's left
Look up what the rules need for each remaining game:
- Leagues: both teams' table positions, the opponent's last 5 results, and any European game for the user's team within 3 days either side.
- Cups: each team's division and table position.
- Lower-level games (cups and second divisions): the last 5 results of the team you'd pick.
- NFL: the QB situation (injury report, QB and team record) and recent form.

Then apply the drop rules.

### 5. Reply with the table, and nothing else
List every game that passed, strongest case first: the biggest mismatch, the opponent in the worst form, the clearest QB problem. The user builds their parlay from this list, so leave out nothing that passed and add nothing that didn't.

Reply with this table, then the cost sentence from step 6, and nothing else: no heading, no notes.

```
| Game | Description | Pick | Odds | Date |
|---|---|---|---|---|
| Venezia v Inter | Serie A. Inter 1st, Venezia bottom and lost 4 of last 5. No European game within 3 days. | Inter | 1.36 | Wed 28 Oct |
| Eagles v Cowboys | NFL. Jalen Hurts out for the season, backup Tanner McKee starts. | Cowboys | 1.46 | Mon 26 Oct |
```

- **Game:** home team first.
- **Description:** the competition and, in one short sentence, why the game fits. Anything else the user should know about this game goes here too: an exception, an assumption, or a clash between their data and the web.
- **Pick:** the team to win.
- **Odds:** decimal, 2 places.
- **Date:** day and date, e.g. "Sat 31 Oct".

If nothing passes, reply with one line instead: "Nothing passes your rules for these dates." The cost sentence still follows it.

### 6. Close with the cost
Once the analysis is done, run `python scripts/run_cost.py` from this skill's base directory and put the sentence it prints on its own line under the table. It adds up the real token usage of every model call since the skill was invoked, from this session's transcript, and prices it at Anthropic API rates. Don't estimate the numbers yourself: if the script fails, say in one line that the cost couldn't be measured.
