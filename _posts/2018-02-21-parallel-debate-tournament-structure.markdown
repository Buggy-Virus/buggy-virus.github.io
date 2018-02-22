---
layout: post
title:  "Parallel Debate Tournament Structure"
date:   2018-02-21 02:00:00 -0000
categories: debate, mechanism-design, simulation, debate-tournament-simulator,
tags: debate, mechanism-design, simulation, debate-tournament-simulator,
---

The American Parliamentary Debate Association is basically a series of weekly tournaments at various colleges across the United States, which various other colleges travel to and compete. Tournaments generally last two days and are comprised of two parts:

1. A five round Swiss-system tournament. Teams are paired against other teams with the same win loss record, so a 4-0 team will hit another 4-0 team, and a 2-2 team hits a 2-2 team. Teams that have the same record are then paired such that the highest rated team with a record, hits the lowest rated team, and then this is repeated with the next highest team (the rating of a team is a cumulative sum of individual ratings given by judges each round).

<center><img src="/assets/parallel-debate-tournament-structure/img-1.png" alt="Swissy" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 1: Swiss tournament structure.</span></center>

&nbsp;

2. A handful of teams with the best records **break** to a single elimination bracket, seeded by team ratings.

<center><img src="/assets/parallel-debate-tournament-structure/img-2.png" alt="Your everyday tournament" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 2: Single elimination bracket for breaking teams.</span></center>

&nbsp;

In this post we are mainly concerned with the first part of these tournaments. It’s a reasonable tournament structure for events that can have upwards of 100 teams. Unfortunately, despite debaters generally being able to communicate clearly and occasionally say intelligent things, they have shown themselves to be empirically poor event organizers.

Tournaments budget about 9 hours to run five ~50 minute debate rounds. These five rounds often end up taking around 12-15 hours. 15 hours isn’t even the upper bound with some tournaments experiencing catastrophic events which cause the tournament to creep on late into the night, such as pairing software crashing, losing debate judges mid tournament, entire schools of teams dropping out, and organizers simply losing tournament data. The main bottleneck is the process of pairing that occurs between rounds. A mix of issues, from judges coming in late and general incompetence, will often make what could theoretically be a 10 minutes process into 2 hours.

In this post I propose an alternative system, which both drastically reduces the amount of time it takes to pair and run subsequent rounds, without sacrificing the accuracy of the tournament. By accuracy I’m referring to the likelihood that the results of a tournament reflect the true ordering of team’s ability. I’ll go more in depth on accuracy and comparing accuracy between tournament systems later.

&nbsp;

## Parallel Tournament System

We improve the tournament my running different parts of it in parallel, meaning we have different parts of the tournament run at the same time. Currently a tournament’s swiss system simply alternates between running rounds, pairing the next round based on all previous results, then running another round. It’s intuitive and straightforward, and is for the most part functional. I'll refer to tournaments of this type as standard APDA tournaments.

<center><img src="/assets/parallel-debate-tournament-structure/img-3.png" alt="Sleek, efficient, historied" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 3: Standard APDA tournament structure.</span></center>

&nbsp;

But debate rounds and pairing could potentially occur at the same time, as debaters don’t do anything during pairing, and those generating the pairings pairing, or **Tab**, aren’t necessarily doing anything while the debate round is happening. Recognizing this, we could restructure the tournament to look like this:

<center><img src="/assets/parallel-debate-tournament-structure/img-4.png" alt="Confusing, strange, unintuitive" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 4: Parallel tournament structure.</span></center>

&nbsp;

I'll refer to tournaments of this type as parallel tournaments. Instead of alternating between rounds and pairing, they happen at the same time. The first two rounds are pre-paired before the start of the tournament. For these two rounds teams are paired randomly, except teams containing a debater qualified for nationals are seeded and cannot hit another seeded team. This pairing scheme for the first two rounds is the same one used for the standard APDA tournament's first round.

During the second round, the tab receives the results of the first round, and uses it to pair round three. Then round four is paired during round three, using the results of round one and two, and all subsequent rounds are paired during the previous round. Teams are still only paired against other teams with the same record, but now it's their record from two rounds ago instead of their record after the last round. In other words, round pairing information lags behind all available information by one round at the start of a round.

The power of this system is that whichever takes less time, pairing or the round, occurs while the other activity is ongoing. Thus we save a significant amount of time per round and pairing.

To quickly illustrate how much time this would potentially save, let’s assume it takes $$50$$ minutes to run a round, and $$100$$ minutes to pair. If this is the case then a normal five round APDA tournament would take $$650$$ minutes. On the other hand, a five round parallel tournament would take $$400$$ minutes, $$50$$ minutes for the first and last round, and $$100$$ minutes for the pairing that takes place during rounds 2-4. Running an additional round only takes $$100$$ more minutes, adding 2 more rounds would still only take $$600$$. Thus, with these assumptions a seven round parallel tournament is still $$50$$ minutes shorter than 

$$ \text{Average Standard Tournament Time}=t_{round} + (i-1)(t_{pair} + t_{round})$$

$$ \text{Average Standard Tournament Time}(5\ \text{rounds})=50m + 4(100m + 50m) = 650m$$

$$ \text{Average Parellel Tournament Time}=t_{round} + (i-2)max(t_{pair},t_{round}) + t_{round}$$

$$ \text{Average Parellel Tournament Time}(5\ \text{rounds})=50m + 3(100m) + 50m=400m$$

$$ \text{Average Parellel Tournament Time}(7\ \text{rounds})=50m + 5(100m) + 50m=600m$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 1: Rough calculation of potential time saved.</span></center>

&nbsp;

These results rely heavily on my earlier assumptions about the length of rounds and pairings. Variance for these two amounts and other factors could make perfect parallelization impossible or cause other issues to occur. On the other hand there are many times when pairings take much longer than $$100$$ minutes at a tournament, in which case we would see the full possible speed up. One can’t be certain of of how much time a parallel tournament structure until it is actually tested, but it seems reasonable to assume it would be much faster for five rounds, and it’s feasible that a seven round parallel tournament could take about as long as a five round standard APDA tournament.

The other strength of this system is, regardless of whether the tournament’s accuracy increases by running more rounds in the time saved, everyone gets to debate more. I’ll assume most of everyone who decides to spend their entire weekend at another school, sit in classrooms all day, then sleep on the floor, is doing it because they intrinsically enjoy debate, and would enjoy being able to get more rounds in at a tournament. Further, it gives everyone more practice at tournaments, thus we can expect the level of debate throughout the league to increase. This extra practice is especially valuable for non-breaking debaters who don’t access as many rounds at tournaments their breaking counterparts. 

One could easily argue that this system allowing everyone to debate more even outweighs an increase in tournament results accuracy, and should be our primary concern as long as we are able to maintain a reasonably accurate break. I won’t attempt to convince you way or another as to what you should care more about. But I will show through simulation that we can expect a parallel tournament structure, running a number of rounds we reasonably expect can be run during the standard five round APDA tournament, will both have more rounds and more accurate tournament results. 

&nbsp;

## Tournament Simulation

### Hypothesis

I expect to see that, although parallel tournaments may have lower accuracy of results according to various metrics when compared against a standard APDA tournament with the same number of rounds, with the addition of a number of rounds, that we expect could occur within the amount of time necessary to run a five round standard APDA tournament, parallel tournaments would have better expected accuracy of results than a standard APDA tournament.

&nbsp;

### Introduction

Before I go into detail about how I simulated tournaments in order to compare their accuracy I’ll speak at greater length on what exactly the accuracy of a tournament’s results is. We could conceptualize of a tournament as a means to discover the ranking among participants at some activity. For debate, this means the results of a tournament should helps us discover who is the best debate team. Thus a tournament is some mechanism which creates an ordering between the teams based on their competitive success. 

What makes tournament design difficult is variance. We expect the very best team to have a greater than 50% probability of beating any other team, but there is still some chance that they could lose, and then even though they are statistically better than the other team, the tournament outcome may not align with the true ordering of the teams. In the real world we don’t know the true ordering of teams so comparing the accuracy of real tournaments versus other tournaments is difficult. We can use statistics from past events to make statements about who should have won, but it is always possible that it wasn’t a fluke, and at the point of time of the tournament the under dog was legitimately the better competitor.

For my simulations though, I know the true orderings of the teams, because I generated the teams. I then run these teams through a series of simulated tournaments and record the the results of the tournaments. Afterwards I did some analysis on the differences between the orderings of teams based on the results and what the true ordering. Generally the greater divergence from the true order, the less accurate a tournament is. There are various metrics we could use to measure this divergence, and there are specific kinds of divergences he may care about more than others, such as the difference between which teams break to out rounds according to the simulation results versus the true ordering. I’ll go more in depth about the different metrics for scoring results in the results section (surprise surprise), if you’re not interested in reading about how I generated the results you can <a href="#identifier">skip the method section and jump directly to metrics and results</a>.

You can see the code for the simulations at it’s [project’s Github page](https://github.com/Buggy-Virus/debate-tournament-simulation){:target="_blank"}. The code is generally split between two main files. [`debate_functions.py`](https://github.com/Buggy-Virus/debate-tournament-simulation/blob/master/debate_functions.py){:target="_blank"} contains all the individual functions for different parts of a tournament and the means to simulate a tournament. [`tournament_simulator.py`](https://github.com/Buggy-Virus/debate-tournament-simulation/blob/master/tournament_simulator.py){:target="_blank"} generates teams, runs tournaments, computes accuracy metrics and aggregate the results. I’ll first go through the processes `debate_functions.py` uses to run a tournament, then go through the parameters and structure of `tournament_simulator.py`.

&nbsp;

### Generating Teams

`make_debaters`, takes in the desired number of debaters,  the debaters’ mean mean, standard deviation of the mean, mean standard deviation, and standard deviation of the standard deviation. That last sentence was nonsense, but the idea is to generate many very diverse debaters. Each debater is going to end being a normal distribution that is sampled to determine how well they perform in any specific round. In order to generate distinct normal distributions for each debater, we sample a normal distribution with the mean of the mean mean and the standard deviation of the standard deviation of the mean to determine a debater’s mean. Then we sample a second distribution with the mean of the mean standard deviation and a standard deviation of the standard deviation of the standard deviation to determine the same debater’s standard deviation. Again, these sentences probably read like a bunch of nonsense, the important thing to note is that each debater is now a normal distribution which has a mean and standard deviation sampled from two normal distributions common amongst all debaters. The debater with the highest mean has the highest expected performance in any round, thus is considered the best debater, and generally we use this mean to order debaters from best to worst.

<center><img src="/assets/parallel-debate-tournament-structure/img-5.png" alt="The mean mean of your standard deviation's distribution" style="width:700px;height:400px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 5: Sampling distributions to build distributions.</span></center>

&nbsp;

Now we generate teams of two debaters. I could have randomly paired all the debaters, but that’s neither flavorful nor a very good model of reality. Instead the `make_teams` function considers the best unpaired debater then randomly pairs them with a random debater from the top ten percentile of unpaired debaters, then removes the two from the pool. The member of team $$i$$ that was the top of the unpaired pool before pairing is denoted $$\alpha_i$$ and the other is $$\beta_i$$. This process is repeated until the unpaired pool is exhausted.

<center><img src="/assets/parallel-debate-tournament-structure/img-6.png" alt="Pick your most competitive friend" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 6: Pictured above, common dynamics in debate teams: elitism and uniform distributions. .</span></center>

&nbsp;

The idea behind this implementation is that the best debaters get to choose who they debate with, and so they would generally decide to debate with their best possible choice. Unfortunately for them, they generally have to pick someone from their school, and so they may not have access to the second best available debater, but we assume there will be someone within the top ten percentile also at their school whom they pair with.

Generated teams are ordered by ability determined by the sum of the two teammates’ means. Similar to the individual case, the team with the highest sum of means has the highest expectation of combined performance in any round. Additionally, teams whose mean is higher than a sample from the normal distribution with a mean of 3 times the mean mean and standard deviation 2 times the standard deviation of the mean are given a seed.

&nbsp;

### Pairing

The function `pair_teams` takes in the current round number, the set of teams which includes the teams’ records, whether the round is seeded, and lastly whether it is a Dutch tournament (We’re going to ignore the Dutch parameter for now and talk about it later).

If it’s a seeded round, we run through the list of seeded teams and pair them with a random unseeded teams. Once one of these pools is exhausted, we pair leftover teams at random.

If it is an unseeded round, then we consider each set of teams with the same number of wins. The team with the highest aggregated performance assigned by judges so far is considered the top of the bracket, paired with the bottom of the bracket, and two teams are removed from the pool. This is continued until the bracket is exhausted, then move onto the next bracket with one less number of wins. 

<center><img src="/assets/parallel-debate-tournament-structure/img-7.png" alt="Super annoying to code" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 7: Standard process for pairing a bracket.</span></center>


In cases where there is an uneven number of teams in a bracket we pulled up the lowest ranked of the next highest bracket to participate in the current bracket. This annoyingly can create a chain of odd brackets and pull ups which eventually culminates in a bye for the lowest ranked team from the bottom bracket and forces me to write up a disgusting set of conditionals.

```python
if push_down != None and len_ordered_teams % 2 == 1:
	ordered_teams.insert(0, push_down)
	push_down = None
	len_ordered_teams += 1
elif push_down != None and bracket != brackets[-1]:
	new_push_down = ordered_teams[0]
	del ordered_teams[0]
	ordered_teams.insert(0, push_down)
	push_down = new_push_down
elif push_down != None:
	bye = ordered_teams[-1]
	ordered_teams.insert(0, push_down)
	del ordered_teams[-1]
elif len_ordered_teams % 2 == 1 and bracket != brackets[-1]:
	push_down = ordered_teams[0]
	del ordered_teams[0]
	len_ordered_teams -= 1
elif len_ordered_teams % 2 == 1:
	bye = ordered_teams[-1]
	del ordered_teams[-1]
	len_ordered_teams -= 1
```

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 2: Absolutely disgusting. </span></center>

&nbsp;

But now there is a set of tuples with all teams represented. This set is the pairings for a round based on the teams’ given records.

&nbsp;

### Running a Round

The function `run_round` takes a set of pairings generated pair_teams, the set of teams, and a judge bias parameter. It then goes through each pair, samples the distributions of each debater in the round, and assigns each team the value of the sum of its two debaters’ samples.

At this point it might be obvious to pick the team with the higher value as the winner, but anyone who has debated before knows it’s not that simple. Instead we sample each team’s score in the round from a normal distribution with a mean equal to their team value and a standard deviation equal to the judge bias. This simulates how there is additional variance on outcomes of rounds outside of just debater performance due to judge bias.

$$\text{Team Value}_i=N(\mu_{\alpha,\ i}, \sigma_{\alpha,\ i}^2) + N(\mu_{\beta,\ i}, \sigma_{\beta,\ i}^2)$$

$$\text{Team Score}_i=N(\text{Team Value}_i, \sigma_{judge}^2)$$

$$\text{Winner}=max_{i\in\1,2}(\text{Team Score}_i)$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 3: You would be surprised how little of debate is actually speaking, and how much of it is just sampling normal distributions. </span></center>

&nbsp;

Now we compare the two team scores and pick the team with the higher score as the winner. We then add the two teams to the set of results, which keeps track of whether each team won or loss and their score.

&nbsp;

### Updating Results

The final function necessary to run a tournament is `update_teams`. `update_teams` takes the set of teams and a set of results. It goes through each team and based on the corresponding result updates their record and adds their score from the last results to their aggregate score.

&nbsp;

### Tournament Functions

There are two functions for simulating a tournament. `apda_tournament` which simulates a standard Apda tournament, and `para_tournament` for a parallel tournament. Both take in the number of rounds to run, a set of teams, judge bias value, and whether it is a Dutch tournament. These functions output the set of teams at the end, but with a their records updated to reflect the results of the rounds.

You can see both functions below:

```python
def apda_tournament(num_rounds, teams, judge_bias, dutch):
	for i in range(1, num_rounds + 1):
		pairings = pair_teams(i, teams, [1], dutch)
		results = run_round(pairings, teams, judge_bias)
		teams = update_teams(teams, results)
	return teams
```

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 4: Old busted. </span></center>

&nbsp;

```python
def para_tournament(num_rounds, teams, judge_bias, dutch):
	rec_results = {}
	old_results = {}
	for i in range(1, num_rounds + 1):
		teams = update_teams(teams, old_results)
		pairings = pair_teams(i, teams, [1, 2], dutch)
		old_results = rec_results
		rec_results = run_round(pairings, teams, judge_bias)
	teams = update_teams(update_teams(teams, old_results), rec_results)
	return teams
```

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 5: New Hotness. </span></center>

&nbsp;

### Running Simulations

Now we turn our attention to `tournament_simulator.py`, which is poorly named because it doesn’t run one tournament, but rather one hundred thousand tournaments. Each tournament used the following set of parameters:

```python
team_sims = 100
tourn_sims = 1000

dbtr_num = 512
team_num = dbtr_num // 2
break_num = team_num // 8
dbtr_mn_mn = 1000
dbtr_mn_std = 300
dbtr_mn_mn_std = 0
dbtr_std_mn = 250
dbtr_std_std = 250
dbtr_std_mn_std = 0
judge_std = 800
judge_std_std = 0
```

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 6: Copying your parameters from the code, a great trick for when you don’t want to Latex them. </span></center>

&nbsp;

One might notice that the standard deviation of debaters and judge bias (called judge standard deviation here because it is a much more accurate description) are very high relative to the expected difference between debaters’ means. The reasoning behind this was to make the outcome of rounds very volatile. If we ran a tournament with relatively low standard deviations for the debater distributions, debaters would generally perform around their mean, and thus it would be very rare for a team with a lower sum of means to beat another team with a higher sum of means. Thus regardless of the tournament structure we would get a result very close to the true ordering. So I jacked up volatility in order to better differentiate different tournament systems from the true ordering, allowed them to be better differentiated from each other.

The actual process of running the simulations involved generated 100 unique sets of teams, for each set of teams I ran 1000 Apda tournaments and 1000 parallel tournaments. From each set of tournament results I collected the following metrics, and averaged them over all 100,000 simulated tournaments of each type.

&nbsp;

#### Distance from the true ordering

$$x_i = \text{rank of the }ith\text{ team of the true ordering}$$

$$\forall\ i,\ \sqrt{\sum_{i} (x_i - i)^2}$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 7: Distance of results from true ordering.</span></center>

This is the distance between the vector of the ordering of teams based on a simulations results and the vector of the true ordering. This distance represents general divergence from the true ordering, and thus overall accuracy of a tournament’s results. Thus the lower the distance the better. 

The issue with this metric is that it takes into account parts of the results that we may care much about. For example, we could have a tournament structure which always outputs a correct break, but does horribly at ordering the bottom half of teams, and thus receives a high distance. We may actually really like this tournament since we care greatly about which teams break, but if we only looked at the distance it would look very bad compared to other tournament structures.

&nbsp;

#### Distance from the true ordering of breaking teams

$$\forall\ i\ \in\ \text{break},\ \sqrt{\sum_{i} (x_i - i)^2}$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 8: Distance of breaking teams.</span></center>

This metric is similar to the previous one, but now the vectors that are compared have been truncated to just the breaking teams. This gives us a better idea of whether a tournament structure is likely to produce a break containing the top teams of a tournament seeded correctly.

&nbsp;

#### Number of Teams Missing Out of The Break

$$\forall\ i\ \text{break},\ \sum_{i}
\begin{cases}
    0, & \text{if }x_i \in \text{break}\\
    1,              & \text{otherwise}
\end{cases}$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 9: Number of teams from the true ordering that missed the break.</span></center>

This metric simply counts the number of teams that should be in the break according to the true ordering that are not represented somewhere in the break. This metric’s advantage over the previous one is that it is unbiased about the ordering of teams in the break, and only pays attention to if a team that should have be in the break is in it anywhere. This metric is useful because may would prefer a break containing everyone who should break over a break that misses some teams, but otherwise is well ordered.

&nbsp;

#### Break Score

$$\forall\ i\ \text{break},\ \sum_{i}
\begin{cases}
    0, & \text{if }x_i \in \text{break}\\
    x_i - i,              & \text{otherwise}
\end{cases}$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 10: Difference of teams missing the break from their true position.</span></center>

Break score is for every team that should have broken, but didn’t, the total number of breaking teams minus their expected position. Thus higher ranked teams, such as the team expected to get first, would contribute more if they missed the break than if the team on the edge of the break missed it. Again this is another metric that we want to minimize.

<a id="identifier">&nbsp;

## Results

Below we can see the results for 100,000 simulation for the various metrics.

<center><img src="/assets/parallel-debate-tournament-structure/img-8.png" alt="What a nice curve" style="width:481px;height:289px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 8: Results distance plotted against number of rounds run.</span></center>

&nbsp;

<center><img src="/assets/parallel-debate-tournament-structure/img-9.png" alt="Wait. . ." style="width:481px;height:289px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 9: Break results distance plotted against number of rounds run.</span></center>

&nbsp;

<center><img src="/assets/parallel-debate-tournament-structure/img-10.png" alt="What. . ." style="width:481px;height:289px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 10: Number of teams missing from break plotted against number of rounds run.</span></center>

&nbsp;

<center><img src="/assets/parallel-debate-tournament-structure/img-11.png" alt="Is even happening" style="width:481px;height:289px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 11: Break score plotted against number of rounds run. </span></center>

&nbsp;

The total distance graph is unsurprising, with both tournament structures getting better and distance falling as more rounds are added. We’ll note here that adding only one more round to the parallel tournament gave it a better distance than the standard five round Apda tournament, and adding a second additional round gave it an eighth less distance than the standard five round Apda tournament.

Considering the other metrics, things get much more complicated. The first most striking feature is shape of these curves. As number of rounds increases there is a general trend downwards, but adding another rounds seems to alternate between being highly effective and not helping very much. In some instances adding another round at certain points gives a worse score, such as if we look at the break score of a five round parallel tournament against a six round parallel tournament. 

At first I was very confused by these results, and reran the 100,000 simulations for each number of rounds a couple more times, but never saw a greater than 0.08% change in any of the numbers. This amount of change also never changed any of the relative results nor the general shape of these curves.

After a rather productive conversation with [Jack Glaser](/assets/parallel-debate-tournament-structure/glaser.png){:target="_blank"}, he informed me that there is an odd effect where adding rounds could cause accuracy to oscillate. The higher brackets are the most competitive, and half of each bracket loses, and then ends up in a weaker bracket. This causes teams to enter a cyclic process. They are continually bounce between a better bracket where they consistently lose, and worse bracket where they consistently win. This effect isn’t very pronounced when looking at the entire set of results, but when we are isolated to a small number of debaters, such as the breaking teams, an extra round can have this effect of inadvertently swapping out the bottom half of the break for the top half of the next highest bracket. This sudden swap is quickly rectified by adding another round. Thus we end up with oddly shaped oscillating curves like the ones above.

Based on this we can clearly see that by these three metrics a six round parallel tournament is always worse than a standard five round Apda tournament and even worse than at five round Parallel tournament. We should note though that a five round Parallel tournament is actually very close to a standard Apda tournament by these metrics, though it is worse by the general distance metric.

If instead we consider a seven round Parallel tournament against a standard five round Apda tournament, we see improvement across all these metrics, and it’s pretty drastic. Most of these metrics are quite abstract, but pointing to the metric of number of teams missed in the break, we see that on average a seven round Parallel tournament will miss 1.5 less teams, a directly quantifiable effect (and one anyone who was the team just out of the break should care about). So based on this we can conclude that a seven round Parallel tournament is preferable to a standard five round Apda tournament if tournament accuracy is all we care about.

&nbsp;

## Conclusion

Based on the results of the simulation we have that a seven round parallel tournament will yield more accurate results than the standard five round Apda tournament. Thus if it is the case that a seven round parallel tournament takes less or equal time as a standard Apda tournament, we ought prefer it for this reason. Further it also provides a greater number of rounds so everyone gets to debate more, and this should also be weighed when deciding between parallel and standard tournaments. 

In fact the increased accuracy of results and increased number of rounds debated could make a seven round parallel tournament preferable to a standard five round Apda tournament even it took more time on average. Though based on my loose calculations earlier and intuition I expect a seven round parallel tournament would generally take less time than the standard five round APDA tournament. So there should at least be experimentation with implementing seven round parallel tournaments.

An additional thing to note is that the five round parallel tournament yields very similar results to a standard Apda tournament if we just look at the break. Considering this, there could be an argument to running five round parallel tournaments in place of standard Apda tournaments to just save time. Though I expect this idea to be less popular. It would be a seemingly drastic change, and top debaters (who generally decide upon tournament structure changes) could fear it potentially affecting their results, while the only gain would be saving a couple hours (and considering they commit every weekend to this great and only fun activity, it’s hard to gauge how valuable a couple extra hours would be to them).

&nbsp;

## Notes and Concerns

### That’s Not Why Pairings Take So Long

A parallel tournament structure decreasing the total time of the tournament was based on the two assumptions that pairing teams took a long time, and this process could occur while teams were debating. The assumptions don’t seem that unreasonable, but it ignores a major issue that contributes to pairings taking a long time,the fact that tab has to wait for the last judge’s ballot to come in before a pairing algorithm can be run. 

This means individual judges can hold up the entire tournament. While some ballot processing can occur while waiting on judge ballots, people have claimed to me that pairing is actually very quick once all ballots are in.

This throws a wrench into the parallel tournament structure, because even if a round’s pairings aren’t based on the pairings of the previous round, all judges need to be free and not still filling out their ballot from last round to run the next round. This means that if the major bottleneck on pairings are judges taking a long time, a parallel tournament wouldn’t be able to solve it, though it would still reduce some time, due to all pairing processes after ballot collection still occuring during a round.

<center><img src="/assets/parallel-debate-tournament-structure/img-12.png" alt="Judges cause all the problems" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 12: Structure of parallel tournament taking into account judge ballot issue.</span></center>

&nbsp;

Waiting on slow judge’s ballots may not actually be the largest time sink of pairings, but I feel it is worth mentioning its potential impact when recommending tournament structures. Additionally we can think of some fixes to the judge issue to reduce its effect on a parallel tournament.

&nbsp;

#### Get More Judges

By simply having more judges, you could immediately run the next round once the number of outstanding ballots was equal to the number of reserve judges. This is because as the group of slow judges continue to fill out their ballots, the reserve judges sub in for them and the next round goes off immediately.

This is an elegant solution, and, while it works for parallel tournaments, it doesn’t work for standard Apda tournaments, which is a plus for parallel tournaments.

The issue with this fix is that Apda tournaments already suffer from a dearth of judges relative to teams wanting to attend tournaments. This is such a problem that the idea of having a large number of reserve judges seems as fantastical as the people on side opp being true friends.

&nbsp;

#### Impose Ballot Deadlines

If deadlines were imposed on judges, after which their judge rankings were tanked or the outcome was decided arbitrarily, it would probably incentivize the slowest judges to speed up a bit. This isn’t that wild an idea, and could in fact be implemented in standard Apda tournaments in the same manner.

The concern with deadlines is that judges may be too rushed to come to a conclusion about a round, and end up awarding the wrong team the victory. This would be a serious concern if the deadline was too soon after the round ended, but I believe there is a reasonable threshold where this becomes less of a concern.

We can think of the probability a judge selects the correct winning team (barring different judging paradigms (but really no competitive activity should have multiple legitimate outcomes based on who is officiating so I feel secure in saying we should ignore the idea of different judging paradigms (this aside will probably make someone very upset))) as a function dependant on time. Intuitively the more time the judge has to adjudicate the higher the probability is. I would argue that after a certain amount of time the gains diminish significantly, and for some judges more time after a threshold causes the probability to actually decrease.

<center><img src="/assets/parallel-debate-tournament-structure/img-13.png" alt="Fuck the red judge" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 13: Theoretical judge curves.</span></center>

&nbsp;

We can easily imagine the situation where after exhaustively reviewing the arguments on the flow, more time probably wouldn’t help better inform the judge as the outcome. Further we can imagine in some cases the longer and more a judge thinks about the round, beyond exhaustively reviewing the arguments on a flow, the more they are actually bringing their bias about the topic into the decision. The idea is that the more time passes since the round, they could begin to disassociate the round with the topic they have been reviewing, and their recollection of the true context of the arguments they wrote down in the flow could become warped. All this makes me reasonably comfortable in encouraging the one judge who always takes forty minutes to put together the reason for decision to hurry it up. I don’t believe that telling people to write up their decision after 15-20 minutes would drastically differ from the decision they would make given more time.

So my thinking right now, based on the reasoning a went through above, is that a deadline for ballots would be pretty rad. But I wouldn’t go so far as to say that tournaments ought implement or experiment with them. 

&nbsp;

### Dutch Tournaments Suck

I mentioned something about the Dutch earlier in this post. To clarify, a Dutch tournament is a tournament structure where the top team in a bracket hits the top of the second half of the bracket instead of the bottom.

<center><img src="/assets/parallel-debate-tournament-structure/img-14.png" alt="High quality work right here" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 14: Look at this! It makes no sense! Unless you’re Dutch.</span></center>

&nbsp;

Basically we flip the bottom half of each bracket before pairing.

The reasoning behind a Dutch tournament is that you could have a situation where a mediocre team ends up at the top of a bracket, and is never displaced as they continually hit the worst of the bracket, while there are alot of people in the middle of the bracket that are better than them. The Dutch tried solving this issue (Or I presume they did based on the name of these tournaments) by more heavily testing the top of the bracket against better teams within the bracket. If they are truly the best team we would still expect them to beat these slightly better teams.

This ends up being a hairy decision, as we would expect the top team of the bracket to be more deserving of a spot in the bracket than the lowest team in the top half of the bracket. So perhaps we should prefer to more heavily testing the lower end of the top half by pitting them against better teams. It’s pretty hard to weigh which is more preferable.

Luckily I have a tournament simulator that can be configured to run Dutch tournaments, and luckily I did just that! I ran 100,000 Dutch tournaments of both standard and parallel form for various number of rounds! And it was always worse than the non-Dutch counterparts! Much much worse. So much so that I don’t feel motivated to do more thoughtful analysis or post the results here.

So yeah, the Dutch suck.

&nbsp;

### Future Work And Wrap Up

To be more thorough I could go back and run the simulations with changing mean and variance and plot the results, but I’m not sure what those results would show. Also some preliminary messing around with the simulation parameters didn’t reveal anything interesting other than a reduction in differentiation between tournament structure results when there was less variance, although relative positions of results were preserved. So it’s unclear to me whether there is much to be gained by further pursuing the simulation side of this. Additionally I don’t see many future applications a debate tournament simulator would have, so I’ll probably just focus on simulators of more complex leagues and tournaments such as Dota 2.

Otherwise if you have any thoughts or questions feel free to contact me through any means on my [contact page](/contact/){:target="_blank"} and I’ll try to respond in a timely fashion.

&nbsp;

&nbsp;

&nbsp;

&nbsp;