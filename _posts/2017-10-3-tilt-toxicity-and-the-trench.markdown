---
layout: post
title:  "Tilt, Toxicity, and The Trench"
date:   2017-10-02 20:52:00 -0000
categories: dota2, esports, trench, statistics,
tags: dota2, esports, trench, statistics,
---

The Trench  refers to a phenomenon in team based games where a player feels the outcome of matches is often highly influenced by poor player behavior. This phenomenon manifests mainly in games with ranked matchmaking, and has the effect of making players feel they are unable to affect the outcome of matches. In this post I explain this phenomenon and its cause s with a simple mathematical model. I investigate this issue in the context of Dota 2, but I hope this post will give insight into the Trench for games with a similar match making system such as League of Legends, Overwatch, and others.
 
This post is meant to be descriptive rather than prescriptive, i.e. I’m not going to give a list of tips one can utilize to climb through the Trench, but rather explain why it feels like the Trench exists, why many players of varying skill will argue that it doesn’t exist, and why it gets reported at all skill levels.
 
As opposed to just asserting my opinion and what the Trench is, I’m going to justify by reasoning with some simple models and computation. Maybe in the future I’ll follow it up with some simulations, but for now I’ll get into my hypothesis.

&nbsp;

&nbsp;
 
## Player Model
 
In order to explain my analysis outside of a purely qualitative domain, I’m going to create a model for how we should think about players and matches in Dota 2.
 
Let’s say that when a Dota match occurs, each player contributes a numerical amount of skill to their team. The skill a player contributes is randomly sampled from the player’s skill probability distribution. So every match they randomly contribute skill based on some constraints specific to the player. We’ll get into what these distributions look like for a player later.
 
The skill is summed for each team, whichever has a higher skill sum wins.

&nbsp;

$$ player_{a, i}\ skill\ contribution\ for\ a\ given\ match = s_{a, i} $$

$$ team_a\ skill\ sum = \sum_{}^{players} s_{a, i} = S_a $$

$$ if\ team_a\ beats\ team_b\ \implies S_a \geq S_b $$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 1: Skill Model </span></center>

&nbsp;
 
This is a very simplistic model, and ignores a variety of possible factors, such as synergies or anti-synergies between teammates’ dominant play styles (like getting a team where each player is most comfortable in a laning position unique from their teammates’ preferences), or how opponents’ play styles may counter each other (like one player being incredibly mechanically strong, but lacking the decision making skills to handle rat strategies).
 
One important aspect that the model does capture is if a player’s skill probability distribution’s mean is greater than that of the aggregate skill distribution mean of the other players at his current MMR, then when he queues and before he is matched with a team, his expectation of winning is greater than 50%. In other words, if he is better than the average player at his MMR, then he is more likely to win than lose his next match when he queues.
 
The purpose of this model isn’t to perfectly simulate a matchmaking ecosystem, but rather to illustrate my argument about the Trench.

&nbsp;

&nbsp;
 
### Player Skill Probability Distribution
 
The **player skill probability distribution** is a curve that describes the likelihood of a player contributing any amount of skill to a match. Player $$i$$’s probability density function (pdf) is $$f_i (x)$$. The probability that player $$i$$ contributes between $$a$$ and $$b$$ skill in a match is given by the integral of their probability function from $$a$$ to $$b$$.

&nbsp;

$$ probability\ of\ x = p(x) $$
 
$$ player_i\ pdf = f_i (x) $$

$$ p(player_i\ contributes\ c\ skill) = f_i (c)\ \ (discrete) $$

$$ p(players_i\ contributes\ between\ a\ and b\ skill) = \int_{a}^{b} f_i (x) dx\ \ (continuous) $$

$$ \int_{- \infty}^{\infty} f_i (x) dx = 1$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 2: Player Probability Density Function </span></center>

&nbsp;
 
Tracing this probability function will give a player’s skill probability distribution.
 
<center><img src="/assets/tilt-toxicity-and-the-trench/graph-1.png" alt="A Normal Distribution" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 1: A normally distributed player skill probability distribution</span></center>

&nbsp;

This curve shows the likelihood of any skill contribution in a match. Thus by viewing this we can get an idea of how much skill a player generally contributes to a match.
 
We can assume that the mean of a player's skill probability distribution is their “true” skill. The reason we assume this, is that if they are queueing in a pool of players who similarly have the same mean, then their expectation of winning the match is 50%.
 
We are going to make skill numbers roughly correspond to MMR (This is the numerical representation of a player’s ranking of in Dota 2). This means players whose most accurate MMR is 8K will have a skill distribution mean of 8K, and the amount of skill they are expected to contribute to a match is 8K. Having skill numbers correspond to ranking will just help me clean up the numbers and make arguments more intuitive later. For instance, when I say a player contributes 2K skill to a match, they are playing with the same mean efficacy of a 2K ranked player.

&nbsp;

&nbsp;
 
## What is The Trench
 
There are two effects that mainly contribute to people feeling like they are in the Trench. The first effect is instances where the difference between one’s team and the opponents’ team skill sum excluding the player is greater than the upper bound of the player’s skill probability distribution. Thus the player is unable to affect the outcome of the match. I’ll refer to this as the **True Trench**.
 
The second phenomenon that causes people to feel that they are in the Trench are when players have a MMR near their mean skill. Their MMR may be oscillating, making them believe that they are gaining MMR as they should be, then losing it due to factors out of their control, but in reality they are within the band of MMR that we would expect them to sit in according to the variance of their skill probability distribution. I’ll refer to this as the virtual Trench.

&nbsp;

&nbsp;
 
### The True Trench
 
Basically this refers to players being in situations, where even if their mean skill is greater than or equal to their current MMR, regardless of how well they play, they can’t be expected affect the outcome of a large percentage of the games they play. They don’t lose these games, but the outcome is decided almost purely by which team has more toxic or tilted players.
 
These situations are due to difference between the teams’ skill sums, excluding the player in question, is greater than the player’s upper bound of their skill probability distribution (or greater than the range of skill that they could reasonably expect to contribute).

&nbsp;
 
$$ player_{a, 1}\ pdf = f_{a, 1} (x) $$

$$ team_a\ skill\ sum\ without\ player_{a, 1} = \sum_{2}^{5} s_{a, i} = S_{a \setminus 1} $$

$$ difference\ between\ teams\ = S_b - S_{a \setminus 1} = d $$

$$ \int_{d}^{\infty} f_{a, 1} (x) dx \leq 0\ or\ \epsilon\ where\ \epsilon\ is\ very\ small $$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 3: The Trench </span></center>

&nbsp;

&nbsp;
 
#### Constructing Better Player Skill Probability Distributions
 
If we assumed every player’s skill probability distributions are normal distributions, True Trench situations will still occur, but they would be extremely unlikely. But what we are interested in are cases where people systematically report this phenomenon, causing them to believe they are in the Trench. Thus we are particularly interested in player behavior that makes True Trench instances common in team games like Dota 2.
 
It’s likely that players’ don’t have a normal distribution for their skill probability distribution. Rather their distribution is skewed right.
 
<center><img src="/assets/tilt-toxicity-and-the-trench/graph-2.png" alt="Right Skewed" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 2: A right skewed distribution</span></center>

&nbsp;
 
The skew is due to that fact that there is a skill level they generally achieve in a game, and they tend to perform around it unless they are being affected by adverse factors. We could think of the apex of their curve as how good they are at the game in the vacuum of behavioral factors. Players likely don’t randomly over perform this range, and they don’t randomly play at a level mechanically worse than they usually play. We don’t live in an anime where 2K players remember their dead friend, unlock secret hidden potential, then play with 8K skill. So our normal 4K player tends to play in the upper range of their set of possible skill outputs around 4K, and there isn’t a small percentage of games where they suddenly play like a 10K player.
 
I still haven’t explained why this relates to the True Trench, further this model doesn’t seem like a particularly accurate representation of a Dota 2 player’s skill probability distribution. So we’ll introduce a new part of the curve, how they play when on **tilt**. Tilt describes a player underperforming mechanically and strategically due to being emotionally upset.
 
<center><img src="/assets/tilt-toxicity-and-the-trench/graph-3.png" alt="Getting Tilted" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 3: Introducing the effect of tilt and the tilt distribution</span></center>

&nbsp;
 
When the player is tilted they perform worse by a fixed amount of skill specific to them, we’ll call this amount the player’s **tilt delta**. Tilt delta represents that when a player is tilted they don’t suffer from a spectrum of being tilted, it’s a binary. People tend to have a breaking point where they suddenly are on tilt. You don’t sit around and feel that you are 50% tilted and your ability is getting continuously worse as things that tilt you occur more, rather it is discrete.
 
We are going to use this simple model that considers there to be a binary between being tilted and not being tilted, and there is some probability that they play any game on tilt. It is probably more accurate to use a system where each player has a discrete tertiary (like a binary, but with more than two states) of tilts and tilt deltas. In other words, there are a couple different levels of tilt for them, sometimes they might be pissed off, and other times they’ll be outright furious.
 
<center><img src="/assets/tilt-toxicity-and-the-trench/graph-4.png" alt="It's a Discrete Tertiary!" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 4: What it could have been if I had more time</span></center>

&nbsp;
 
The number of levels and tilt delta for each level would be unique for each player, but for the sake of simplicity, we are going to stick with our binary model.
 
The last piece I’m going to add to this model, is how the player’s skill distribution is affected by how toxic they are. We are going to consider toxicity to be similar to tilt, it’s a binary where some games players are toxic and others they are not, and there is some probability as to whether they will be toxic in any given game. When they are toxic, it lowers their skill probability distribution by a toxicity delta. In reality, they are actually lowering the skill probability distributions of their teammates in the game, but we isolate the effect to their skill probability distribution to show that they are directly lowering their team’s skill sum in a game by being toxic.
 
<center><img src="/assets/tilt-toxicity-and-the-trench/graph-5.png" alt="Toxic" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 5: Toxicity distribution and its effect</span></center>

&nbsp;
 
At this point, many probably think there is an issue with the cause and effect of this model, or the lack of it. In reality there aren’t simple probabilities governing whether one is on tilt or toxic in a game. I could make a much more complex model, where players have thresholds. If the team’s skill sum is below a threshold or a single player’s skill contribution is below a different threshold, they become toxic. Also when toxic, instead of applying a toxicity delta, they should instead activate other players’ tilt and cause them to lower their skill contributions by their tilt delta.
 
I didn’t use a more complex model like this for two reasons. Firstly, because it’s just very complicated. Secondly, I want to factor in toxicity as something that alters the toxic player’s skill probability distribution. Being toxic in a percentage of their games, whatever the cause, will lower the amount of games they are expected to win, thus they should have a lower mean skill and a lower true MMR, due to this. This is a simple way to capture this, instead of making the amount they lower their true MMR dependent upon other players susceptibility to toxicity (complicated).
 
Now I will redraw how we think their skill probability distribution curve looks when we combine all these different curves.
 
<center><img src="/assets/tilt-toxicity-and-the-trench/graph-6.png" alt="I Called This a Confluence of the Other Curves Before, I Don't Know Why" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 6: Putting all the curves together</span></center>

&nbsp;

&nbsp;
 
#### How Does This Cause The True Trench
 
Let’s work through an experiment. We are going to assume that all players with a specific MMR have a mean skill near that MMR (within a +/- 100 range), except for Liam, the specific player we are following. Let’s say Liam is currently sitting at 3500 MMR, but his mean skill is actually 3800, and he has a very low chance of being tilted or toxic (we are assuming it is 0 here). So we expect Liam to win any match he queues into, as he is expected to contribute more skill to his team than every other player in the match.

<center><img src="/assets/tilt-toxicity-and-the-trench/graph-7.png" alt="Liam Isn't This Good" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 7: Liam's skill probability distribution</span></center>

&nbsp;
 
Unfortunately all the other players in the match actually have a pure skill rating of around 3700, but their mean skill is 3500 MMR because their tilt delta is 1000 MMR, and their toxicity delta is 1500 MMR. So they have the following skill probability distributions.
 
<center><img src="/assets/tilt-toxicity-and-the-trench/graph-8.png" alt="Pretty Consistent Players" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 8: Other players' discrete probability distribution</span></center>

&nbsp;
 
This means that the outcome of the game is impacted by a player being tilted or toxic more often than Liam’s high skill mean. For Liam, the game becomes a dice-roll as to whether his team or the opponents’ team will have more toxic and tilted players.
 
If we assume that each player has a 5% chance of being tilted and a 5% chance of being toxic, then there is a 56% chance that the match will be purely decided by which team has less toxic or tilted players (this is assuming that the difference in skill sums of both teams is less than 500 when excluding the effects of tilted and toxic players).
 
&nbsp;

$$ \int_{d}^{\infty} f_{a, 1} (x) dx \leq 0\ or\ \epsilon\ $$ 

$$ the\ collective\ tilt\ delta\ of\ some\ group\ c = tilt_c = \sum_{}^{c} \Delta tilt $$

$$ probability\ of\ trench = p(tilt_{a \setminus 1} \neq tilt_b) \approx 56 \% $$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 4: Trench Calculation, <a href="https://docs.google.com/spreadsheets/d/1dOAfkb3SnAaC50lp5ZNSWAy02oHrCtWNg6LmkmJJ6Bs/edit#gid=0" target="_blank">Computation Sheet</a> </span></center>

&nbsp;
 
The other 44% of the time, they have a “normal” Dota 2 match, determined by who plays better rather than who is tilted or toxic (though in some of these matches there are players that are tilted or toxic, but both teams have an equal negative impact on their skill sums from tilted or toxic players). The chances of there being a match where no player is tilted or toxic is 40%, which isn’t terrible, but also probably doesn’t fill anyone with great confidence (the great news is that there is only a 3.44e-20 chance that all nine other players are both tilted **and* toxic, but this is just a model, Dota 2 players will know that this grossly underestimates reality).
 
<center><img src="/assets/tilt-toxicity-and-the-trench/piechart.png" alt="It's a Discrete Tertiary!" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 9: Possible outcomes</span></center>

&nbsp;
 
The dice rolling nature of games due to tilted and toxic players is what causes the Trench to manifest. It’s obviously very upsetting to queue into games which you should win, but are decided by random chance more than 50% of the time.
 
This also helps explain why players of differing ranks might report the Trench being at different MMR ranges. It’s possible that the chances of players tilting or being toxic doesn’t change very much as MMR rises, but tilt deltas and toxicity deltas grow as games are played at a higher level. It makes sense that lack of communication or inability to work together due to tilt would have a greater impact when it is a greater necessity at higher MMR.
 
A 5K player playing in the 3.5K bracket will encounter less game states which they cannot affect. But as they get closer to 5000 MMR, and their relative advantage over opponents shrinks, as well as the effect of tilt and toxicity rises, they are likely to experience the same dice-rolly situation Liam is currently having trouble with.

&nbsp;

&nbsp;
 
#### A Few Notes
 
There are a few things to note before we move on. First is that neither Liam nor the 5K player are actually capped in how much skill they can add to games. The skill probability distribution we present is from one snapshot in time, it doesn’t imply that Liam will never get better than his current upper bound. Liam could overcome the Trench to some degree by becoming a better player rather than focusing on MMR, this would cause less of his games to be dice rolls similar to the 5K player in 3.5K games. 
 
Second, as I mentioned before, tilt and toxicity are highly causal. Not only is the 5K player going to be able to affect a greater number of matches in the 3K bracket, but he is also less likely to trigger toxicity from 3K teammates in the first place. If we consider the more accurate model I posited before, where players become toxic if their team or an individual player perform below a threshold, having a 5K player will easily keep the team above this threshold reducing the number of players being toxic in the 5K player experiences in his 3.5K games (but it doesn’t reduce the number of toxic players). Further players are less likely to become frustrated and toxic when they feel they are going to win due to being carried to victory. 
 
There is probably also a toxicity domino effect, where one player being toxic causes more players in the match to be toxic (because it totally increases your chances of winning).
 
Third thing I want to talk about is that even if Liam is unable to affect the game state of 56% of games, that doesn’t mean he loses the other 44%, some he still wins due to his team having less tilted or toxic players, in fact he wins the majority of these games. The reason for this is because in our model Liam is never tilted or toxic (something I can assure you is not true). Thus his opponents’ team’s expected lost MMR due to tilt and toxicity is less than Liam’s team. In fact Liam has a 56% chance of winning matches which come down to tilt and toxicity dice rolls (with the numbers I used it was coincidental that the chance to win a dice roll game is similar to the chance to get a dice roll game (so he’s winning 56% of the 56% of matches that are dice-rolly (I’m sorry that this happened))).

&nbsp;

$$ p(favorable\ trench) = p(tilt_{a \setminus 1} \leq tilt_b) \approx 31 \% $$

$$ 31 \div 56 \approx 56 \% $$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 5: Favorable Trench </span></center>

&nbsp;
 
A 56% win rate is exceptional in Dota 2, where most players’ winrate sit within 3% of 50% (I actually made up that statistic, but I’d be willing to bet a fair amount that this is accurate), and this was achieved for 56% of all games by simply changing a feature that Liam is completely in control of: his behavior.
 
With this fact, any rational player who is in a Trench is advantaged by choosing not to get tilted or be toxic. So yeah, be less toxic in your matches.

&nbsp;

&nbsp;
 
### The Virtual Trench
 
The virtual Trench has less of a mathematical explanation, and instead requires more psychological assumptions. Because the idea that players’ MMR have variance isn’t a crazy or particularly interesting idea, but there seem to be various factors that cause players to reject the idea that their fluctuations in MMR is simply variance, and instead it’s the effect of the Trench.
 
This section is based on my observations and assumptions about how players tend to think, so I have to add a disclaimer that this isn’t nearly as concretely reasoned as the previous section, and I haven’t collected any data to back this up. This is just my take on the phenomenon.
 
The first thing I want to talk about is the strange belief of some players that, over time, playing more matches will slowly narrow down their MMR to exactly their true MMR according to their mean skill. This isn’t the case, because of variance. Even if a player’s skill level was perfectly stagnant and they weren’t improving at all, we don’t expect them to eventually hit an MMR, and if they win a match they will immediately then lose the next one, or vice versa. Clearly there is variance even if you are currently sitting at your true MMR.
 
If at a MMR all players had zero chance for tilt or toxicity, so they have simple right skewed skill probability distributions, it still presents a distribution and a variety of outcomes that could occur with different probabilities. So you will have players oscillate around their true MMR, and we simply expect their mean MMR over time to be their true MMR (expecting this does not mean that it will be the case, just that it is the expectation).
 
I’m sure at this point, anyone reading with a rudimentary grasp of probability are tired of me trying to convince you that variance is a thing. And even if you don’t believe me still that it is a thing, just trust me. And everyone else. Variance is a thing.
 
<center><img src="/assets/tilt-toxicity-and-the-trench/variance.png" alt="It Totally Is" style="width:297px;height:143px;text-align:center;"></center>

&nbsp;
 
So likely a large amount of players are mis-attributing their gained MMR to their playing well and blaming the games they lose to Trench dynamics, when in reality they sit in a range around their mean that we would expect from their variance. That being said, if they are around their correct MMR then they are most likely to experience Trench effects, but ignoring cases that come down to dice rolls right now.
 
There are a bunch of reasons players don’t recognize that they are sitting where they should be, and just admit that they are experiencing MMR volatility. The most obvious reason is that players generally feel they are a higher MMR than the one they are currently at. This is probably partially due to the fact that it would be somewhat depressing if you just believed you were where you should be, and didn’t believe you could get any higher. If a player did feel like this, their main motivation for playing ranked matchmaking, raising one’s MMR, would disappear. We would expect these players to then play much less or not at all, at which point they fall out of the matchmaking environment. With this being the case, we can assume most players in ranked matchmaking are playing because they believe when they queue that the next match is more likely to increase their MMR than decrease it (otherwise we don’t expect them to queue), thus they must necessarily believe their MMR is higher than whatever their current one is.

&nbsp;
 
$$ player_i\ perspective\ = per_i (x) $$

$$ if\ MMR_i \geq per_i (s_i) \implies per_i (E (\Delta MMR)) \leq 0 $$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 5: Why We Play </span></center>

&nbsp;

This perception is probably reinforced by the nature of snowballing team based games like Dota 2. Every once in awhile you will stomp a game due to a mix of factors, such as picks, the other team having players on tilt, or just random chance throughout the game. If a player ends up being the main beneficiary of the stomp, by having the most kills or by playing a core at the time, they might attribute this success to their play. The set of games that are stomps reinforces in the player’s mind that they are a higher MMR player. Conversely, whenever they lose, due to the fact that Dota 2 is often more a game of which team makes less mistakes than which team has better execution, they are offered a slew of excuses for blaming teammates for the loss in order to shield their ego.
 
Now literally everyone thinks they are better than their MMR, and those who really aren’t, are provided a nice excuse of the Trench to rationalize why their MMR sits around 3.3K generally, instead of 4.5K (something I used to do) (I’m not 4.5K now, I’m just, more realistic).

&nbsp;

&nbsp;
 
#### Prescriptive Advice
 
I know I said this post was going to be descriptive rather than prescriptive, but I lied. Hopefully this section doesn’t seem to long or preachy. Most importantly hopefully it doesn’t take away at all from the earlier better argued processes.
 
**1. Don’t Go on Tilt or be Toxic**
 
This is something everyone understands they shouldn’t do from a moral and social perspective, and many people already understand that it has an adverse effect on their MMR. Those who didn’t previously believe that it negatively impacted their win rate, I hope what I wrote in the post has convinced you.
 
Another issue is that people don’t really always understand what it means to be toxic. I think we should investigate two scenarios. The first one is when you still believe the game is winnable, but your teammates are making mistakes. Many people start pointing out mistakes, or dwell on them after they happen. Before you do this, you should consider, will my communication right now cause my teammate to be a better player for the rest of the match? If not, then doing this just carries a chance that you tilt them, so doing this is literally lowering your chances of winning. So don’t do it, unless you are really into playing ranked match making to explain to your teammates what they are doing wrong instead of winning.
 
The other scenario is when you think there is no chance to win, so you start flaming or carrying out other toxic behaviour. This may get me some flak from Reddit, but if a player knew with 100% certainty the game was going to be a loss, it makes alot of sense that they should engage in behavior to end the game faster, and flaming teammates doesn’t have a negative impact on them. Even if they knew there was a 90% chance the game would be a loss, it still seems pretty logical to just scrap the game and move onto the next one.
 
This issue with actually doing this is that there is a difference between **knowing** it is a 100% chance a game will result in a loss, and being a player who **thinks** there is a 100% chance that a game is a loss. No one truly **knows** the probability that a game will be a loss. They probably don’t have an accurate assessment of what the end of the game will be unless they are in an extremely severe situation (like being down 31-1 and a barracks at 15 minutes). Especially because people are really bad at factoring how comeback mechanics can affect the rest of the game. So in situations where the game seems highly unlikely to win, I would suggest continuing to attempt to maximize your chances of winning, because your assessment of probability of winning may be just wildly wrong, and also you should be more focused on improving your actual skill through practice than your MMR anyways.

&nbsp;
 
$$ probability\ of\ win = p(w) $$

$$ per_i (p(w)) \neq p(w) $$

$$ \mid per_i (p(w)) - p(w) \mid = much\ higher\ than\ you'd\ think $$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 7: A Simple Fact</span></center>

&nbsp;
 
I will say that I don’t think it’s that unreasonable when high level pro players give up on games mid way through and start doing things to speed up their opponent’s win. I think they probably have pretty accurate assessments of their probability winning, and so ending the match sooner improves their experience as well as their teammates as they can get to their next match faster. The issue is that this fosters the mentality in their stream viewers that this is a reasonable action, who as I described before, probably have a really poor understanding of when they should do this, and will likely just end up harming their own MMR and ruining games for other people. So I really wish pros wouldn’t do this. Not because they shouldn’t, but because it makes my pubs worse.

**2. Focus on Raising Your Mean Skill, Not Your MMR**
 
This is weird, because your MMR is a proxy for your mean skill, and the reason we want high MMR is because it communicates to others that we have high mean skill. So wanting to raise your MMR should be the same action as wanting to raise your mean skill.
 
In reality, this isn’t the case. The fact that people purchase accounts is evidence enough. Also there is an effective difference between focusing on whether your MMR is rising, and focusing on whether your game impact is rising. Any game you perform poorly, but you are carried to victory should be an equally poor signal as losing a match, because your game impact had low influence. Further reveling in MMR increases probably isn’t a good use of your time. It is hard for one to tell whether they actually are moving towards their true MMR when their MMR goes up, or if they are just experiencing MMR volatility.
 
So alternatively it’s much more productive to really focus on getting better in each match, and analyzing how to improve personal play and how your game impact could turn a loss into a victory, rather than analyzing your team as a whole and how a player who isn’t you could have possibly had more impact and changed the loss into a victory.

&nbsp;

&nbsp;
 
## Afterward

Last thing I want to note pertains to the example players I had Liam play with. I assumed their mean skill and true MMR was 3.5K. Anyone can quickly use the numbers I gave for their player skill probability distribution and see that 3.5K number was wrong. Let's find out what their mean skill actually is:

$$ 0.05 \times 2200 + 0.05 \times 2700 + 0.9 \times 3700 = 3575 $$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 6: Well That Wasn't Too Hard </span></center>

&nbsp;

This actually doesn't affect the above argument at all, since it is based solely on difference of tilt and toxicity deltas, but it's worth noting all the same (One could even ask why I don't edit the above paragraphs to reflect this (That's a good question friend)).
 
This post ended up being much longer that I expected it to be. I think I spent much more time explaining basic probability concepts than I necessarily needed to, but I guess increasing accessibility isn’t a terrible thing (though it directly trades off against people deciding not to read the post due to the entirety of it being too long (I guess maybe it is a terrible thing (rough))).
I plan to post a follow up in the near future where I create simulated matchmaking environments using a model for players and matches similar to the one in the post. Hopefully the simulations will generally agree with what I outlined here, otherwise I’ll look pretty stupid won’t I.
 
If you have any questions or disagreements send me a message to my email or any other service on my [contacts][contact] page, and I’ll either respond or talk about it in a follow-up post.

&nbsp;

&nbsp;

&nbsp;

&nbsp;
 
[contact]: /contact/

