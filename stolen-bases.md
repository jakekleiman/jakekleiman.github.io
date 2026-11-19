---
layout: article
title: "When to Attempt a Stolen Base"
description: "A breakdown of MLB's 2026 running game: five questions to ask before giving the steal sign, answered with every stolen base attempt from 2026."
date: 2026-11-19
tag: "Baseball strategy · R"
permalink: /stolen-bases/
---

<p class="dek">A breakdown of MLB's 2026 running game</p>

Top of the 9th, tie game. Your leadoff hitter walks. Nobody out. Do you give the steal sign?

On paper, yes. Think of the steal as a bet. If he makes it, your chances of winning go up about 10 percentage points. If he's thrown out, they drop about 14. Because getting caught costs more than making it gains, he needs to be safe more often than not, and in this spot the bet breaks even at **59%**. If your runner beats that, sending him wins you more games than it loses over time. For comparison, across all of MLB in 2026, runners who tried to steal second were safe about 74% of the time. That's every attempt from first base, in every inning and every score. So the average base stealer clears the 59% bar easily.

But neither number tells the whole story. The 59% is only true for this exact spot. Add an out, fall behind by two or get to a full count, and the break-even rate can jump. And that 74% is the average for every runner in baseball, against every pitcher and catcher. It doesn't tell you whether this pitcher is hard to run on, or whether this runner is really as good as his numbers say.

So instead of one answer, this article breaks the decision into five questions to ask before giving the sign, each answered with every stolen base attempt from 2026 (4,303 of them) and every pitch where a runner could have gone. First, though, a quick look at the math behind all five.

## First, what is a base worth?

Almost every answer in this article starts from one table. It's called a run expectancy matrix, and it shows how many runs MLB teams scored, on average, from each situation to the end of the inning in 2026. Every possible combination of runners and outs gets its own number.

<table class="re-table">
  <thead>
    <tr><th>Runners on</th><th>0 outs</th><th>1 out</th><th>2 outs</th></tr>
  </thead>
  <tbody>
    <tr><td>Empty</td><td>0.50</td><td class="hl">0.27</td><td>0.10</td></tr>
    <tr><td>1st</td><td class="hl">0.89</td><td>0.53</td><td>0.23</td></tr>
    <tr><td>2nd</td><td class="hl">1.18</td><td>0.68</td><td>0.32</td></tr>
    <tr><td>3rd</td><td>1.44</td><td>0.92</td><td>0.38</td></tr>
    <tr><td>1st &amp; 2nd</td><td>1.56</td><td>0.92</td><td>0.45</td></tr>
    <tr><td>1st &amp; 3rd</td><td>1.78</td><td>1.17</td><td>0.52</td></tr>
    <tr><td>2nd &amp; 3rd</td><td>2.00</td><td>1.37</td><td>0.53</td></tr>
    <tr><td>Loaded</td><td>2.49</td><td>1.65</td><td>0.76</td></tr>
  </tbody>
</table>

A stolen base attempt moves a team from one box in this table to another. Let's use the highlighted boxes, a runner on first with nobody out, worth 0.89 runs. If he steals second, the team moves down one row to a runner on second with nobody out, worth 1.18. That's a gain of 0.29 runs. If he's thrown out, the team moves to the bases empty with one out, worth just 0.27. That's a loss of 0.63 runs.

So a successful steal gains 0.29, and a caught stealing costs 0.63. Because the loss is about twice the gain, the runner has to be safe about **68%** of the time for the attempt to pay off. That's the break-even rate: the success rate where the runs you expect to gain and the runs you expect to lose cancel out.

One limit: this table counts runs, and it treats every inning the same. Early in a game, that works fine. But late in a close game, what matters is winning, and one run can matter much more (in a tie game in the 9th) or much less (down by four). Question 2 redoes the math in terms of wins for those spots. First, though, Question 1 uses this table to show how much the number of outs changes the answer.

## 1. How many outs are there?

In the last section, a runner on first with nobody out had to be safe at least **68%** of the time for a steal to be worth it. That number is the break-even rate. Do the same math with one or two outs and the break-even rate rises to about **73% to 74%**. With more outs, getting to second is worth less, but getting thrown out still costs a lot.

The chart below compares those break-even rates (red diamonds) with how often runners were actually safe (blue dots). The blue line around each dot is the margin of error. If the line doesn't reach the red diamond, the difference is real and not just luck.

<figure class="ll-fig">
  <img src="{{ '/assets/img/stolen-bases/01-breakeven-by-outs.png' | relative_url }}" alt="Break-even vs. actual success rate for stealing second, by outs">
  <figcaption>Figure 1. Runner on first stealing second, 2026.</figcaption>
</figure>

- **Nobody out:** runners beat the break-even rate easily. Across the league, it was worth about 44 runs.
- **One out:** right at the break-even rate. No real gain.
- **Two outs:** right at the break-even rate too.

One more thing stands out: the one situation where stealing clearly paid off is the one teams used least. With a runner on first, teams ran less often with nobody out than with one or two outs. And it wasn't because teams were saving those steals for their best chances. The runners who went with nobody out were just as fast, faced the same kinds of pitchers and had the same predicted chance of success as the runners who went with two outs. They were safe at almost the same rate, too: 75.2% with nobody out, 73.5% with one out and 74.3% with two outs. The only thing that changed was the break-even rate, and it was lowest with nobody out. That's a strong sign teams could run more in that spot.

## 2. What's the score, the inning and the count?

Late in a game, not every run is worth the same. A run that breaks a tie in the 9th can decide the game. A run that cuts a four-run deficit to three barely changes anything. So for this question, I built a win probability model from the same season. It estimates each team's chance of winning from any inning, score, outs and runners on base. Then I redid the break-even math in terms of wins instead of runs.

<figure class="ll-fig">
  <img src="{{ '/assets/img/stolen-bases/02-win-probability.png' | relative_url }}" alt="Win probability break-even by inning and score">
  <figcaption>Figure 2. Break-even rate for a runner on first stealing second, by inning, score and outs, with the visiting team batting.</figcaption>
</figure>

For the first six innings, the lines barely move. The break-even rate stays between about 64% and 77% no matter the score. From the 7th inning on, the lines split apart:

- **Tied:** the break-even rate falls. By the 9th with nobody out, it's just **59%**. One run could win the game, and a runner on second is the easiest way to get it. (For the home team in the bottom of the 9th, it's even lower: 55%.)
- **Down one:** it barely changes. A single run ties the game, so the steal is about as useful as it is early on.
- **Down two:** the break-even rate shoots up, to **92%** in the 9th with one out and 98% with two outs. You need two runs, so one runner on second doesn't help much, and an out is a disaster.

Down three or more in the 9th with two outs, almost no success rate makes a steal worth it.

The count matters too, but mostly once there are outs. With nobody out, almost every count keeps the break-even rate in the 60s. With one or two outs, three-ball counts push it into the high 80s. The reason: ball four would send the runner to second anyway, so the steal only helps if the pitch is a strike.

<figure class="ll-fig">
  <img src="{{ '/assets/img/stolen-bases/03-count.png' | relative_url }}" alt="Break-even by count and outs">
  <figcaption>Figure 3. Break-even for stealing second by count and outs, runner on first only. These come from smoothed estimates, so read the pattern more than any single box.</figcaption>
</figure>

One box to ignore: the 92% for a full count with two outs. In that spot, the runner should always be moving with the pitch. Ball four sends him to second anyway. A ball in play gives him a head start, so he can score on a double or reach third on a single. And on strike three, the inning is over whether he's safe or not. It isn't really a steal decision.

The number is there because the math treats every count like a normal steal decision: go or stay. With a full count and two outs, there's no real choice to make, so the math gives a misleading answer.

## 3. Who's on the mound?

There's an old baseball saying: you steal off the pitcher, not the catcher. Of all five questions, this one turned out to matter most, and the data backs up the saying.

I estimated how many attempts every pitcher *should* have faced, given the runners, catchers and situations he saw, and compared that to how many he actually faced.

<figure class="ll-fig">
  <img src="{{ '/assets/img/stolen-bases/04-pitchers.png' | relative_url }}" alt="Actual vs. expected steal attempts against pitchers">
  <figcaption>Figure 4. The eight pitchers runners avoided most and the eight they ran on most, relative to expectations (minimum 300 chances for a runner to go). Grey dots are expected attempts; blue dots are actual attempts.</figcaption>
</figure>

The gap between pitchers is huge. Michael McGreevy faced just 3 attempts when about 22 were expected. Luke Weaver and Kai-Wei Teng didn't face a single one. On the other end, runners went 35 times against Dylan Cease when about 14 were expected, 28 times against Eury Pérez when about 9 were expected and 14 times against José Alvarado when fewer than 5 were.

The pitcher doesn't just decide whether runners go. He decides whether they make it. Holding everything else equal, a pitcher one standard deviation worse at holding runners raised a runner's chance of being safe by about **7 points**. A slower catcher pop time added about 4 points. A runner being one standard deviation faster added about 3. On a stolen base attempt, the man on the mound mattered more than the catcher's arm and more than the runner's legs.

And unlike most of what's in this article, it repeats. Across four seasons (2023 to 2026), pitchers who kept runners from going one year did it again the next, with a year-to-year correlation of 0.52. That makes it the most repeatable skill in this whole study.

## 4. Has he already stepped off twice?

Under the current rules, a pitcher gets two disengagements (pickoff throws or step-offs) per plate appearance. A third one that doesn't get the runner is a balk.

Runners know it, and the chart below shows how much it changes their behavior.

<figure class="ll-fig">
  <img src="{{ '/assets/img/stolen-bases/05-disengagements.png' | relative_url }}" alt="Attempt and success rates by pickoffs or step-offs already used">
  <figcaption>Figure 5. How often runners took off, and how often they were safe, by how many pickoff throws or step-offs the pitcher had already used in the plate appearance.</figcaption>
</figure>

**Left side: how often runners went.** When the pitcher hadn't stepped off or thrown over yet, runners took off on 1.0% of pitches. After one, that rose to 3.8%. After two, it jumped to **7.3%**, about seven times as often as when he hadn't used any. Nothing else I looked at moved runners like that.

**Right side: how often they made it.** Runners were safe only slightly more often after two disengagements: 77%, compared with 74% to 75% before. That's partly because so many more runners went. Once the pitcher ran out of throws, runners who'd normally stay put took off too, and the bigger, less selective group kept the success rate from climbing much.

**What it means for the decision:** runners treat two step-offs as a signal to go, and they go seven times as often. But they only make it slightly more often. Running in that spot isn't a mistake, since they were still safe 77% of the time. It just isn't the edge it looks like. The step-off count is a small nudge at best. The outs, the score and the pitcher matter much more.

## 5. Should you trust last year's numbers?

The first four questions are about the moment. This one is about planning: when a team decides who gets to run next season, it usually looks at last season's stolen bases and success rate. Those two numbers say less about next year than you'd think.

To answer it, I split every steal into two parts. A model estimated each runner's chance of being safe before the pitch, based on his speed, the pitcher, the catcher, the base, the count and the outs. Then I separated:

- **Decision:** what the attempt was worth before the pitch. Did he pick a good spot?
- **Execution:** how the attempt actually turned out compared with what was expected. Did he beat the odds, or fall short of them?

<figure class="ll-fig">
  <img src="{{ '/assets/img/stolen-bases/06-runners.png' | relative_url }}" alt="Best and worst base stealers by runs added, split into decision and execution">
  <figcaption>Figure 6. The ten best and ten worst base stealers of 2026 (minimum 10 attempts), split into decision and execution.</figcaption>
</figure>

Otto Lopez led baseball at +4.2 runs (28-for-33), followed by Pete Crow-Armstrong, José Ramírez and Bryson Stott, who went 21-for-21. But look at how they got there. Most of the leaders were beating the odds. Nasim Nuñez was the exception: almost all of his +2.9 came from picking good spots.

That difference matters, because only one of the two carries over more consistently. I ran the whole analysis for 2023, 2024 and 2025 too, and checked whether runners who were good at each part one season were good at it again the next. A correlation near 1 means the skill repeats. Near 0 means it was mostly luck.

| What I measured (runners) | Year-to-year correlation (2023 to 2026) | Repeats? |
| --- | --- | --- |
| Picking good spots (decision) | 0.41 | Partly |
| Beating the odds (execution) | 0.15 | Barely |
| Success rate | 0.18 | Barely |

As a rough guide, 0.4 or higher means a real skill with some noise, and under 0.2 means mostly luck.

A runner who picks good spots tends to keep picking good spots. A runner who beats the odds usually doesn't do it again, and neither does his success rate. So Nuñez's season is the one I'd trust going forward. José Caballero is the other side of the same coin: his decisions were good (+1.5 runs), but his execution cost him 3.2. His bad luck on execution should even out, and his good decisions should stick. That's a runner I'd keep running. Over time, his success rate should move toward what his decisions predict.

Teams are a different story. A runner's knack for picking good spots carries over, but a team's doesn't. How picky a team was one season told you almost nothing about how picky it was the next (a correlation of 0.10), and its total runs from stealing didn't carry over either (0.06). The likely reason is that the skill belongs to the runners, not the team. The players doing the running change every year through trades, injuries and call-ups, and their judgment leaves with them. What a team *does* keep is its philosophy: teams that ran a lot one season usually ran a lot again the next (0.52).

<figure class="ll-fig">
  <img src="{{ '/assets/img/stolen-bases/07-year-to-year.png' | relative_url }}" alt="Two scatter plots of teams, one season vs. the next. How often teams ran carries over; how well they picked their spots barely does.">
  <figcaption>Figure 7. Each dot is one team, comparing one season with the next (2023 to 2026).</figcaption>
</figure>

**What it means for the decision:** when you decide who gets the green light next year, look at where a runner chose to go, not just how often he made it. Picking good spots repeats. Success rate mostly doesn't.

## One play worth more than the rest

Everything above is about one runner going. When two went at once, the numbers looked very different:

| Play | Plays | Runs per play | Total runs |
| --- | --- | --- | --- |
| Standard steal (one runner) | 3,386 | +0.02 | +74.0 |
| Double or triple steal | 161 | +0.28 | +45.6 |
| First-and-third steal of 2nd | 546 | +0.03 | +14.3 |

In just 161 plays, double steals added more than half as many runs as the 3,386 standard steals combined. Per play, they were worth more than ten times as much. So with two runners on, sending both may be worth a look more often than teams think.

## So when do you give the green light?

Every steal decision comes down to one comparison: **is this runner's chance of being safe, right now, higher than the break-even rate for this spot?** The five questions are just the way to fill in both sides of that comparison.

**Step 1: Find the break-even rate.** Start with the outs. Stealing second needs about 68% with nobody out and about 73% to 74% with one or two outs. Late in a close game, adjust for the score: a tie game pulls it down toward 55% to 60%, and trailing by two or more pushes it into the 80s or 90s. With one or two outs and three balls on the hitter, it climbs into the high 80s too.

**Step 2: Estimate this runner's chance of being safe.** The league average is about 74%. Then adjust for the matchup. The pitcher matters most: a pitcher who's bad at holding runners is worth about 7 points, more than a slow catcher (about 4) or an extra step of speed (about 3). Judge the runner by where he's chosen to go in the past, not by last year's success rate, because the first repeats and the second mostly doesn't.

**Step 3: Compare the two.** If his chance clears the break-even rate by a comfortable margin, the steal is usually a good bet. If it's close, small things can tip it, like a pitcher who has already stepped off twice. If it falls short, the odds say to hold him, though there are times a team needs a run badly enough, or knows something about the matchup the numbers don't, to take the chance anyway. Either way, last year's stolen base total alone shouldn't be what decides it.

No single factor makes the call on its own. A runner who's safe 80% of the time can clear the bar in almost any situation, while a slow runner against a pitcher who holds runners well might not clear it even in a perfect one. The situation sets the bar. The runner, the pitcher and the catcher decide whether he can clear it.

If there's one place teams are leaving value on the table, though, it's with nobody out. In 2026, that's where stealing paid off most, and it's where teams ran least, even with the same kinds of runners they sent in other spots.

## Where this falls short

The main results use every pitch and steal attempt from 2026. The checks on what carries over from one year to the next add 2023, 2024 and 2025. Nothing goes back further than 2023, because that's when the disengagement limit and today's bigger bases took effect. Seasons before then were played under different rules, so mixing them in would compare two different running games. Even so, public data only goes so far. Here's what this can't see, and what would make it better:

- **What happened on each pitch.** Runner jumps and pitcher holds come from season averages, not the individual play. Pitch-by-pitch tracking of each runner's lead, jump and speed, plus each pitcher's time to the plate, would sharpen the success estimates a lot. Teams have this. The public doesn't.
- **The catcher's throw on each play.** Pop time is also a season average. Knowing each throw's exchange time, accuracy and arm strength would separate a good catcher from a lucky one.
- **Who made the call.** On about 15% of attempts, the batter swung, so some were hit-and-runs or designed plays, not the runner's choice. Knowing which steals were called from the dugout would show whether it's runners or coaches who pick good spots.
- **Less data in rare spots.** Most of the numbers in this article come from thousands of steal attempts. But steals late in close games, or on three-ball counts, are only a small share of those. With fewer plays to learn from, those numbers are less certain. Adding the 2023 to 2025 seasons to those parts of the analysis would give them more plays to go on. I kept them to 2026 on purpose, though. This article is about how the running game looked this season, and earlier years include seasons when teams and pitchers were still adjusting to the new rules.
- **Only a few seasons to compare.** The year-to-year checks compare 2023 with 2024, 2024 with 2025 and 2025 with 2026. For teams, that's about 90 comparisons, so a number like 0.10 could reasonably be a bit higher or lower. Each new season will help, and minor league data would help judge young runners with little MLB history.

**Sources:** [MLB Stats API](https://statsapi.mlb.com/) and [Baseball Savant](https://baseballsavant.mlb.com/)
