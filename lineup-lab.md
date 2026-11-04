---
layout: article
title: "The Nine Are Picked. Now What? Grading How MLB Teams Order Their Lineups"
description: "I built an app that grades how well every MLB team ordered its lineups in 2026."
date: 2026-11-04
tag: "Baseball strategy · R Shiny"
permalink: /lineup-lab/
---

<a class="ll-button" href="https://01a1a807-7a57-1cec-3b91-855db5405ced.share.connect.posit.cloud/" target="_blank" rel="noopener">Launch Lineup Lab ↗</a>

Every day, a big league manager writes nine names on a lineup card. Fans debate it, broadcasters dissect it, and most of us have yelled at the TV about it at least once. We know batting order matters, but how much? Holding those same nine hitters constant, how many more runs could a team expect to score simply by rearranging them? And are some teams leaving more runs on the table than others?

Big league managers take plenty of blame for their lineup decisions. So I built **Lineup Lab**, an R Shiny app that takes the nine starting hitters from any 2026 game and estimates how changing their batting order would affect expected runs. The goal was simple: once a manager picks his nine, how much is he getting out of the order he puts them in? After analyzing every game of the 2026 regular season, the results surprised me.

## How it works

First, I want to be clear about what this app does NOT do. It never questions who plays. Rest days, injuries, platoons, and defense are the manager's call, and he knows things no public model ever will. Lineup Lab takes the nine names as given and only asks one thing... where should each of them hit?

You pick a team and a game, and the app shows you the starting nine, the opposing starter, and the final score. Then it projects how many runs that lineup should have scored. Drag a hitter to a new spot in the order and the number updates right away.

<figure class="ll-fig">
  <img src="{{ '/01-main-view.png' | relative_url }}" alt="Lineup Lab main view with the lineup and run tiles">
  <figcaption>The main view. Drag any hitter and the run tiles compare the new order to the real one.</figcaption>
</figure>

To get that number, the model estimates each hitter's chances of every result, from a walk to a home run to a strikeout. It builds that from eight inputs:

1. **The hitter:** how he has hit overall.
2. **The pitcher:** how the starter has pitched overall.
3. **Lefty/righty:** how the hitter does against that hand, and how the pitcher does against that side.
4. **Similar pitchers:** how the hitter has done against pitchers with a similar arm angle, velocity and pitch mix.
5. **Head-to-head:** how the hitter has done against that exact pitcher.
6. **Ballpark:** whether the park helps or hurts each type of hit.
7. **Times through the order:** hitters get a boost the third time they see a starter.
8. **The bullpen:** once the starter is projected to leave, hitters face the team's relievers instead.

### How the model decides what to trust

Small samples lie, so the model trusts a stat more when there's more data behind it. A hitter's full season counts a lot. His four career at-bats against today's starter barely count at all.

Recent seasons count more too. Every 2026 plate appearance counts in full, 2025 counts half, and 2024 counts a quarter.

Next, the app plays the game out one batter at a time, using real MLB data to decide how far runners advance on each hit or out. It plays that game 10,000 times, and the expected runs number is the average runs that lineup scores across those games. Those same games show how often it gets shut out or scores five or more. Then the app tests thousands of orders to find the best one.

All of this runs on every pitch thrown from 2024 through 2026, pulled from Baseball Savant and checked game by game against the official MLB box scores. And every projection only uses data from **before** that game. If I'm looking at a game on September 10th, the model has no idea what happened that day or any day after it.

<figure class="ll-fig">
  <img src="{{ '/02-hitter-breakdown.png' | relative_url }}" alt="Hitter breakdown tab">
  <figcaption>How one hitter's projection gets built, from league averages all the way to today's matchup.</figcaption>
</figure>

The Hitter breakdown tab is probably my favorite part. It shows how one hitter's projection gets built, step by step, so instead of just saying "the model says so," you can actually point to why.

## One game up close

Take Arizona at San Diego on September 27th. The Diamondbacks lost 9-4 at Petco Park against Randy Vásquez. Their lineup that day projected for **4.62 runs**, with a 5.2% chance of getting shut out and a 46.1% chance of scoring five or more. The model expected Vásquez to face about 21.2 batters before handing it to the bullpen... and he faced exactly 21.

<figure class="ll-fig">
  <img src="{{ '/03-optimal-lineup.png' | relative_url }}" alt="Optimal lineup tab for Arizona at San Diego">
  <figcaption>The best order the app found for Arizona at San Diego on September 27th, compared to the one they actually used.</figcaption>
</figure>

The best order the app found was worth **0.05** more runs per game, or about **8.1** runs if you played that exact game 162 times. Most days, the right order is only a few hundredths of a run better, and there are usually several orders that are almost equally good.

## Grading all 30 teams

Once one game worked, I wanted to run every game of the 2026 season and see which teams ordered their lineups best.

My first idea was simple. For each game, I compared the real order to the best order the app could find and counted how many runs the team left on the table. Fewer runs lost meant a better grade. Little did I know that this was quietly punishing the best teams. With a deep lineup, there's a bigger gap between the best and worst possible orders, so there are more runs to lose. A great team could set a smart lineup and still lose more runs than a weak team that barely thought about it.

So I changed the question. Instead of asking how far each order was from perfect, I started with a baseline: what if you just pulled the nine names out of a hat? For every game, the app scores the average random order, the best order, and the real order. The gap between random and best is how much a manager could possibly add by setting the order. Then I asked how much of that gap the real order actually covered. Say a random order projects for 4.30 runs and the best order for 4.50. If the real order projects for 4.40, the team captured 50% of the possible gain. No better than random is 0%, and matching the best order is 100%. That puts every manager on the same scale, no matter how good their hitters are.

I still kept the runs lost number, though, because the two answer different questions. Gain captured tells you how well a team ordered the nine guys it had. Runs lost tells you what that actually cost them.

<figure class="ll-fig">
  <img src="{{ '/04-season-chart.png' | relative_url }}" alt="Season chart of gain captured by team">
  <figcaption>How much of the available gain each team captured in 2026. Cincinnati led, Milwaukee finished last.</figcaption>
</figure>

The middle team was right around 52%, and only about 6% of all games had an order that was basically optimal. The biggest thing I took from this is how small the stakes are. The best team and the worst team were separated by a handful of runs over 162 games.

## The Milwaukee paradox

Then I saw who was at the very bottom... the Milwaukee Brewers. The same Brewers who won 103 games, swept the Dodgers in the NLCS, and beat Tampa Bay in 5 games to win the World Series.

At first I thought I broke something. But the more I looked at it, the more it made sense. Seven runs over a full season is less than one win, and Milwaukee clearly made up for it everywhere else. That doesn't mean it's nothing, though. Teams pay millions of dollars in free agency for a single win, and a better batting order costs nothing. It's free value, just the kind a 103-win team can afford to leave on the table. It is also possible that Pat Murphy knows something my model doesn't. Maybe a guy hits better in a certain spot, or maybe keeping the same order every day matters to the clubhouse. Baseball is inherently great because there are human elements that most models can never predict.

So I don't read this as "the Brewers were wrong." I read it as the model and the manager disagreeing, and the cost of that disagreement being really small. Honestly, that might be the most useful thing the project taught me.

## How a front office could use it

I don't think a tool like this should make the lineup card. I think it should start a conversation. A few ways I could see it helping:

- **Before a game**, checking the planned order against today's starter and ballpark, and flagging when a change is worth more than usual.
- **Explaining a recommendation**, using the Hitter breakdown to show the coaching staff exactly why the model likes a hitter in a certain spot.
- **Looking back**, seeing which kinds of games (lefty starters, certain parks, short outings) are where the order matters most.

<figure class="ll-fig">
  <img src="{{ '/05-model-check.png' | relative_url }}" alt="Model check tab">
  <figcaption>Testing the model on games it hadn't seen. Projected runs line up closely with what actually happened.</figcaption>
</figure>

## Can you trust it?

I wanted to know if the model was actually any good, so I tested it on games it had never seen. Across the season, it projected **4.43 runs per game** compared to the real average of **4.35**, and it predicted plate appearance outcomes about **1.3% better** than just using league averages. That may not sound like a lot, but plate appearances are very hard to predict, so any real improvement matters.

That said, like any model, it has limits:

- **It's a second opinion, not the truth.** Managers know about injuries, rest, who's hot and the clubhouse. A low ranking can mean a team knew something the model didn't.
- **Small differences can be noise.** The order is usually worth a tenth of a run per game or less, so two orders a few hundredths apart are basically a tie.
- **The bullpen is one average group.** Real managers save their best relievers for close games and bring in lefties to face lefties.
- **Every starter is treated the same way late in games.** His exit is based on his usual workload, not how he's pitching that day, and every pitcher gets the same third-time-through drop-off even though some fade much more than others.
- **No in-game moves.** There are no pinch hitters, defensive subs, steal decisions or extra innings. A runner is just fast or not fast.
- **Defense, weather and umpires aren't included.**
- **Rookies look average.** With little MLB history, a top prospect and a fringe call-up look about the same.
- **Park factors aren't split by handedness.** A short right field porch helps lefties and righties equally here.

If I keep building on it, the next things I'd add are a smarter bullpen, better starting points for rookies using minor league stats, and park factors split by handedness.

## What I learned

Batting order is one of the most argued about decisions in baseball, and most of that arguing happens without any numbers behind it. Now there's a way to put a number on it for every game of the season. Some teams captured twice as much of the available gain as others, and while the runs are small, they're free. The most valuable part isn't one perfect lineup. It's being able to see exactly where a manager and the data disagree, and how much that disagreement costs.

The hardest part wasn't the math. It was building something anyone could open, see why the model likes one order over another, and understand in thirty seconds.

This is just version one. Next, I want to bring in Triple-A Statcast data so rookies and call-ups don't all look like league average hitters. I also want to add bat tracking data like bat speed and swing length to better match hitters with the pitchers they handle best, plus game-day weather, since a hot day in Cincinnati plays very differently than a cold night in San Francisco. Each one should make the model a little sharper, and I'm excited to see how much they change the rankings in Lineup Lab 2.0.

If you want to try it yourself, pick your favorite team and a game you remember, and see if you can beat the manager. I'd love to hear what you find!

<a class="ll-button" href="https://01a1a807-7a57-1cec-3b91-855db5405ced.share.connect.posit.cloud/" target="_blank" rel="noopener">Try Lineup Lab ↗</a>

**Sources:** Pitch and Plate Appearance data from [Baseball Savant](https://baseballsavant.mlb.com/) and Lineups/Box Scores from the [MLB Stats API](https://statsapi.mlb.com/)
