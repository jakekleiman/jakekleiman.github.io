---
layout: article
title: "They Saw It Coming: What Predictable Play-Calling Costs an NFL Offense"
description: "I built a model that calls run or pass like a defensive coordinator, then measured what being predictable actually costs an NFL offense."
date: 2026-11-10
tag: "Football analytics · R"
permalink: /play-calling-predictability/
---

Most of my work is in baseball, but I watch every New York Jets game, and through the first half of this season, one thing kept standing out. On 3rd and short and 4th and short, they seemed to go back to the same one or two plays, and they kept getting stuffed. I could see it coming from my couch, and clearly so could the defense. That's what got me wondering how much being predictable actually costs an offense.

Then I remembered an interview from this spring. Shortly after signing with the Chargers, fullback Alec Ingold [sat down for an interview](https://youtu.be/50L7YnfNB_g) about Mike McDaniel's offense. When he was asked to describe it, one of the first things he brought up was "the illusion of sophistication." The interviewer described it as window dressing that makes a play look more complex than the concept really is, and Ingold agreed: "That's it. You got it." The goal, he explained, is for everything to be trained from the beginning "so that it looks like it's crazy, but really you've been training it since April."

In other words, the goal is to keep the defense from knowing what's coming. That's especially relevant for the Chargers right now. By the model I built for this article, they were the fifth most predictable offense in the NFL in 2025, and then they went out and hired McDaniel. As I write this, they're 0-8. This season's formation data isn't out yet, so I can't say whether the offense actually got harder to read. But it's a good reminder of something this article keeps coming back to: disguise helps, but it doesn't replace winning your matchups.

We hear a version of this every Sunday. It's 3rd and 1, the offense comes out with two tight ends and a fullback, and the guy in the booth says something along the lines of "everybody in the stadium knows what's coming." But does that actually matter? If the defense knows it's a run, does it truly have a lesser chance of being successful?

To find out, I built a model that thinks like a defensive coordinator. It looks at every NFL play from 2016 through 2025 (**328,141 plays**) and tries to call run or pass using only what a defense would know before the snap. Then I compared how predictable plays performed against plays that caught the defense off guard. The answer ended up being more interesting than a simple yes or no.

## How it works

The model is built in three stages, each adding information a defense would have before the snap:

1. **The situation:** down, distance, field position, score, clock, and timeouts remaining.
2. **The look:** the formation (shotgun, under center, pistol, empty) and the personnel on the field.
3. **The scouting report:** how that team had been calling plays in its earlier games that season.

Each play gets a **predictability** score: how likely the model thought the offense's actual call was. If the model gave a run a 95% chance and the offense ran it, that play was 95% predictable. If the offense threw it instead, the play was only 5% predictable.

To keep the model honest, it never predicts a play it learned from. To predict the 2022 season, for example, the model learns the general rules (like "an empty backfield usually means pass") from the other nine seasons and never sees a 2022 play. That does mean some of those rules come from seasons after 2022, which a real defense in 2022 wouldn't have had. Most of these rules barely change from year to year, though, so I don't expect that to make much of a difference.

The scouting layer works differently. It only uses that team's earlier games from the same season. For a Week 10 game, the model only knows how that offense called plays in Weeks 1 through 9, which is the same scouting report a real defense would have that Sunday.

## A defense can call it 3 times out of 4

<figure class="ll-fig">
  <img src="{{ '/assets/img/predictability/01-accuracy.png' | relative_url }}" alt="Model accuracy by layer of information">
  <figcaption>Figure 1. Down, distance, score and clock alone get the model to 71%. Adding formation and personnel pushes it to 76%, and a team's tendencies from earlier games add almost nothing on top of that.</figcaption>
</figure>

If you just guessed pass on every snap, you'd be right 61% of the time. Give the model the situation and that jumps to 71%. Add formation and personnel and it hits **76%**. Its probabilities also line up with what actually happens: on plays it calls 80% pass, teams pass about 80% of the time.

The last layer added less than I expected. A team's tendencies from earlier in the season moved accuracy from 76.0% to 76.1%. That doesn't mean scouting doesn't matter. It means most of what a scouting report tells a defense already shows up in how the offense lines up. The formation is what gives the play away.

Some looks give it away completely:

| Look | How often it's a pass |
| --- | --- |
| Empty backfield, shotgun | 98% |
| Shotgun, 1 back, 1 TE, 3 WR (44% of all plays) | 78% |
| Under center, 1 back, 1 TE, 3 WR | 30% |
| I-formation, 2 backs, 1 TE, 1 WR | 9% |

## Predictable runs get hurt. Predictable passes mostly don't.

To keep the comparison fair, every run was measured only against other runs, and every pass against other passes, in the same down, distance and field position. Then I looked at how results changed as plays became more predictable.

<figure class="ll-fig">
  <img src="{{ '/assets/img/predictability/02-epa-vs-predictability.png' | relative_url }}" alt="EPA vs. predictability for runs and passes">
  <figcaption>Figure 2. Passes stay close to average no matter how predictable they are. Runs hold steady until the most obvious ones, which lose 0.08 EPA compared with similar runs in the same situation.</figcaption>
</figure>

Surprises paid off for both runs and passes. Plays the model gave less than a 35% chance gained about **+0.03 to +0.06 EPA** (expected points added, a measure of how much a play helps an offense's chances of scoring) more than a typical play in the same situation.

The big difference showed up on the predictable end. When the model was more than 90% sure a run was coming, that run averaged **0.083 EPA** less than the average run on the same down, distance and field position. It was also less likely to work. A play counts as a success when it has positive EPA, and these runs were successful **7 percentage points** less often. Passes the model saw coming didn't take that hit. They performed about the same as the average pass in the same situation.

I also ran a regression that holds the situation, score, clock, the offense's quality that year, and the defense's quality constant. Same story. Every 10 points of predictability costs a run **0.019 EPA**, about three times what it costs a pass (0.006). Predictability also drags down a run's success rate, but for passes the effect is so small it could just be noise.

Which made me wonder... why would knowing it's a run matter so much more than knowing it's a pass?

## It all comes back to the box

<figure class="ll-fig">
  <img src="{{ '/assets/img/predictability/03-box-reaction.png' | relative_url }}" alt="Stacked-box rate by run probability">
  <figcaption>Figure 3. When a run is least likely, defenses put eight or more in the box 0.7% of the time. When a run is most likely, they do it 51% of the time.</figcaption>
</figure>

When the model gave a play under a 10% chance of being a run, defenses had eight or more guys in the box **0.7%** of the time. When it was over 90%, that number was **51%**. The average box went from 5.6 defenders to 7.5.

Then I found the part that surprised me the most. If you compare runs against the same number of defenders, obvious runs don't do any worse than surprise runs.

<figure class="ll-fig">
  <img src="{{ '/assets/img/predictability/04-runs-by-box.png' | relative_url }}" alt="Run EPA by defenders in the box, obvious vs. surprise runs">
  <figcaption>Figure 4. From six defenders up, obvious runs do as well as or better than surprise runs against the same box. They only look worse overall because they see far more eight- and nine-man boxes.</figcaption>
</figure>

Against a seven-man box, obvious runs averaged −0.051 EPA and surprise runs averaged −0.086. Against eight, it was −0.097 vs. −0.132. Some of that edge is because obvious runs tend to be short-yardage plays where a couple yards goes a long way. But the main point holds. The run itself isn't the problem. The problem is the extra defender. Why passes don't suffer the same way is something this data can't fully answer. My guess is that defenses have a harder time cashing in on an obvious pass. They can drop extra players into coverage, but every one of them is a player who isn't rushing the quarterback.

## Breaking the tell

If obvious runs pull defenders toward the line, then throwing out of a run-heavy look should catch the defense in the wrong spot. And it does:

| Look | How often it's a pass | EPA per pass |
| --- | --- | --- |
| Shotgun, 1 back, 1 TE, 3 WR | 78% | +0.02 |
| Under center, 1 back, 1 TE, 3 WR | 30% | +0.13 |
| I-formation, 2 backs, 1 TE, 2 WR | 34% | +0.18 |
| Singleback, 1 back, 2 TE, 2 WR | 39% | +0.19 |

Passes out of looks that usually mean run were worth anywhere from six to nine times as much as passes out of the league's most common look: three receiver sets in the shotgun. This is the idea behind play-action. But it only works if the offense also runs the ball out of those looks. If it doesn't, the defense stops respecting the run, and the advantage goes away.

## Who's the hardest to read?

<figure class="ll-fig">
  <img src="{{ '/assets/img/predictability/05-teams.png' | relative_url }}" alt="Every team-season, predictability vs. EPA per play">
  <figcaption>Figure 5. Each dot is one team-season. The 2024 Lions were the hardest offense to read and one of the most efficient, but the 2018 Steelers show a predictable offense can still move the ball.</figcaption>
</figure>

The least predictable team-season in the whole data set was the **2024 Detroit Lions** at 61.7%. They also had the most efficient offense in the league that year at +0.170 EPA per play. Not far behind were the 2025 Packers, 2023 Eagles, 2024 Packers and 2025 Bears.

The data tags each team by its head coach, not its play-caller. With that in mind, over the full ten years, the hardest offenses to read belonged to Matt LaFleur, Nick Sirianni and Dan Campbell. The easiest belonged to Bruce Arians, Jim Caldwell and Doug Marrone.

But the head coach isn't always the one calling plays, and who calls the plays isn't something the public data tracks. Using ESPN's yearly play-caller rundowns and news reports on midseason changes, I went through all 320 team-seasons from 2016 to 2025 and recorded who called the plays, week by week. In 40 of those team-seasons, the call sheet changed hands during the year.

Grouping team-seasons by play-caller explains about **38%** of the differences in predictability, compared with about **27%** when grouping by head coach.

Thirty-four play-callers also ran offenses for more than one team in this span, which made it possible to see whether their tendencies traveled with them. They did, but only partly: how predictable a play-caller was at one stop correlated with his next stop at about 0.38. Ben Johnson is the cleanest example. His Lions offenses were among the hardest in the league to read, and his first Bears offense was almost exactly as hard.

Not every play-caller held that consistency. Josh McDaniels has been noticeably easier to read since leaving Bill Belichick, in Las Vegas and again in his return to New England. Even so, his 2025 Patriots were the league's most efficient offense.

Nathaniel Hackett's offenses in Jacksonville and Denver were about average or slightly harder to read than the rest of the league. Then his 2023 Jets were the most predictable offense in the NFL, at 70.3% predictable compared with a league average of 67.0%. That jump comes from a single season, and it came after the Jets lost Aaron Rodgers four snaps into the year. Most of it came from the Jets doing exactly what down, distance, and score called for, which makes sense for an offense relying on backup quarterbacks.

Bruce Arians is an interesting case. He called the plays himself in Arizona, then handed them to offensive coordinator Byron Leftwich in Tampa Bay, who had coached under him in Arizona, and his offenses were almost exactly as predictable in both places. That suggests what carries over may be the system a coach installs, not just whoever holds the call sheet.

In 2025, Green Bay, Chicago, the Rams, Indianapolis and Seattle were the least predictable offenses. Atlanta, Tennessee, Tampa Bay, Cleveland and the Chargers were the most. The league as a whole is slowly getting harder to read too, dropping from 69.0% in 2016 to 67.3% in 2025.

Still, being hard to read doesn't guarantee a good offense. Across all team-seasons, less predictable offenses did tend to be more efficient, but the relationship is weak (r = −0.18). The 2018 Steelers and 2017 Saints were two of the most predictable offenses I looked at, and they were still near the top of the league in efficiency. Great players can still win even when the defense knows what's coming. Being predictable one year also didn't really predict how an offense did the next year, which makes me think some of this goes the other way too. In other words, being bad can make an offense predictable, not just the other way around.

## What this can't tell us

Everything in this article comes from publicly available data through nflverse and nflfastR. That covers a lot, but NFL teams have player-tracking and charting data that the public doesn't, and several of these limits come from not having access to it:

- **Audibles blur cause and effect.** When a quarterback sees a light box and checks to a run, the model sees a surprise run that was also set up to succeed. The box-count results help, but I can't fully separate a smart audible from a smart play call.
- **The model only predicts run or pass.** It doesn't know the actual play: the direction, the route concept, or whether it was a screen or a shot. RPOs count as whatever the quarterback ended up doing.
- **Motion and play-action data only go back to 2022.** Public charting data flags motion, play-action and RPOs starting in 2022, so to keep all ten seasons on equal footing, I left them out. Since motion is one of the main ways offenses disguise what's coming, the model probably understates how well the least predictable offenses hide their intentions.
- **Box counts are measured at the snap.** They don't capture a safety rotating down after the ball is snapped.
- **Play-caller data had to be built by hand.** The public data only tags each team by head coach, so I put the play-caller list together myself from ESPN's yearly play-caller articles and news reports. Some situations are tough to analyze, like the 2021 Miami Dolphins, who used "Co-Offensive Coordinators". Both names appear in my dataset.
- **Pass protection and the actual play call aren't public.** Teams know how a play was blocked and what was called in the huddle. Both would help explain why some predictable plays still work and others don't.

## Why this analysis matters

Predictability is something coaches, players, and broadcasters talk about constantly, but almost always by feel. This analysis quantifies it, and the results point somewhere specific. Being predictable doesn't cost every play equally. It mostly costs runs, and it costs them through the extra defender. That tells an offense where disguise actually matters and where it can afford to be obvious.

I don't think a model like this should be calling plays. But it could be really useful in a few ways:

- **Weekly self-scouting.** Which formations and personnel groups are giving away the call more than league average this season, and how are defenses responding?
- **Spotting the most costly runs.** Flagging every predictable run the defense met with eight or more players in the box. Those are the plays where being predictable costs the most, so they're the first ones worth disguising or changing.
- **Picking shot plays.** The looks with the strongest run tendency are the best spots for play-action, as long as the run game is real enough to keep the defense honest.
- **Evaluating play-callers.** Since predictability follows the play-caller more than the head coach, a team hiring a coordinator can look at how readable his past offenses were, and whether that changed with different quarterbacks.

## What I learned

Predictability barely hurts a passing game, but it significantly hurts a running game, because the defense can commit an extra defender to the box. The best offenses still have tendencies, but they hide them. They run and throw out of the same formations, so the defense can't tell what's coming from their alignment.

Coming from baseball, this reminded me of a pitcher tipping his pitches. The pitch itself isn't any worse, but once the hitter knows what's coming, he can sit on it. A predictable run works the same way. The play doesn't change, but a safety walks down before the snap and the defense has an extra man in the box to stop it. The fix is the same too. A pitcher cleans up his mechanics so every pitch looks the same coming out of his hand, and the best offenses line up so every play looks the same before the snap.

**Sources**

- **Play-by-play, formation, personnel and defenders-in-the-box data:** nflverse (nflreadr), 2016–2025 regular seasons
- **EPA:** nflfastR model
- **Play-caller list:** compiled by me from ESPN NFL Nation's annual "Who calls plays for every NFL team" articles and news reports on midseason changes
- **Alec Ingold interview:** [YouTube](https://youtu.be/50L7YnfNB_g)
