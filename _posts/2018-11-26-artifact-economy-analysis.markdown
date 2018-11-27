---
layout: post
title:  "Artifact Economy Analysis"
date:   2018-11-24 02:00:00 -0000
categories: artifact, esports, gaming, statistics, probability,
tags: artifact, esports, gaming, statistics, probability,
---

In the coming weeks, Valve's digital trading card game, [Artifact](https://playartifact.com/){:target="_blank"}, is slated for release. The game promises some of the most strategic and deep gameplay in the card game genre, and after Valve uncharacteristically marketing the game, featuring various other card games' professional players and streamers testing the beta and a reveal tournament, it seems to poised to fulfill that promise. Despite this, all news and discussion about the game has been overshadowed by one thing: the economy. The process by which you can gain cards, and the fact that it is purely through buying them, which is a point of consternation for many people in the age of free to play card games.

There are two main contentions. First, one of the main methods of play, draft mode, requires tickets you need to purchase in order to play. In draft, instead of using a deck you own, you draft a unique deck from a selection of presented cards, then go against players sporting similarly drafted decks until you lose twice. Depending on your number of wins you receive rewards. One complaint is this gates one of the main play modes behind a pay-wall. Further many complained the expected rewards for what you paid were necessarily going to be poor, as your opponent is determined through a sort of ELO matchmaking, thus you should expect a 50% win-rate. Since the beginning of the controversy, Valve has announced there will be a way to play draft for free with no rewards, but the cost of the draft with rewards still remain a source of discomfort for many considering the game.

The second contention is the fact packs can only be purchased with real money. Most other games provide some method to grind in order to build up virtual currency that can be spent on packs, in addition to being able to purchase them directly. But to alleviate these concerns, cards can be sold directly on the Steam user marketplace. Traditionally items sold on Valve market places have had extremely low cost if their supply is uncapped, but many gamers still hold reservations. These reservations are reasonable considering how other games with similar models such as Magic the Gathering have seen the price of the rarest cards sky rocket on secondary markets, and it isn't clear at first glance why the Valve market place will function differently.

### Introduction

In this article I'm going to provide some mathematical analysis on these topics. First, I'll cover various expectations for the draft rewards system, such as expected rewards and individual draft mode runs. Second, I'll calculate upper bounds for the price of a specific rare on marketplace. I'll derive general equations for both of these topics, as well as plug in numbers for the variables based on the available information.

Although this topic has been attacked mathematically by other in the Artifact community, I hope my article is a clear and rigorous read for those new or interested in the topic, one that goes into greater depth on certain topics, and can be used as a starting point for further discussion.

[//]: <> (My general findings were that draft rewards were a very comparable value to opening in expectation for players with 50% winrate. For players with a higher than average winrate playing draft has very high rewards compared to opening packs. Further going infinite is possible for feasibly high winrates depending on the rate at which packs can be recycled for tickets. For the upper bound and affordability of rares, I found that no singular card should be too expensive if all other cards aren't devalued. Also the upper bound on the average cost of a rare is much lower than even I expected, and points to the game being quite affordable.)

&nbsp;

### Notes On Notation

Throughout this article, I get a little wonky with my expectation notation. Generally when I use $$E[x]$$, it signifies the expected amount of $$y$$ (where $$y$$ is whatever value we are interested in) given that you go through the process of converting $$x$$ into $$y$$. For example, if we care about number of packs you would receive from one ticket of phantom draft where you recursively redeem won tickets for future runs, then $$E[d]$$ would be the number of packs you receive in expectation from recursively using the starting ticket, $$d$$.

$$C$$ is the set of all unique collectible cards in Artifact. Empirically the cardinality (or count) is $$\vert C \vert = 234$$. $$c$$ will refer to an arbitrary card in $$C$$, $$c \in C$$. $$R$$ is the set of unique collectible rares, thus $$R\subset C$$, $$\vert R\vert = 76$$, and similarly $$r$$ is an arbitrary rare in the set of rares, $$r\in R$$. Additionally I use $$v(c)$$ to denote the value or price of a card on the marketplace, and $$v'(c)$$ is the actual cost of getting the card through buying packs until it appears.

&nbsp;

## Expected Outcomes of Draft

There are two types of draft with different rewards. They both require some number of tickets, which need to be purchased with real money (or, as it was recently announced, can be acquired by recycling cards). One of these draft formats also requires packs to play. In both formats, after two losses with your deck you retire the deck and your ticket is forfeit. The two formats are listed below, along with their costs and rewards.

&nbsp;

 **1 Ticket Entry** (Expert Constructed & Phantom Draft):
* 3 Wins: 1 Event Ticket
* 4 Wins: 1 Event Ticket, 1 Pack
* 5 Wins: 1 Event Ticket, 2 Packs

&nbsp;

**2 Tickets + 5 Packs Entry** (Keeper Draft):
* 3 Wins: 2 Event Tickets, 1 Pack
* 4 Wins: 2 Event Tickets, 2 Packs
* 5 Wins: 2 Event Tickets, 3 Packs

&nbsp;

For both formats, getting 3 wins awards the players the ticket cost to replay whichever draft format they just played. Note that for the Keeper Draft, you keep the 5 packs worth of cards you drafted to play the mode, thus the extra cost. With this information we can derive the expectation for various values of interest.

## General Form Expectations

#### Expected Number of Packs Per Run

First, we can calculate the expected number of packs per run for a player with some probability $$p$$ of winning any given match. This expectation is simply the probability of ending with a specific number of wins times the number of packs you recieve for that many wins. First I give the formula for the probability of getting a specific number of wins for some $$p$$.

* $$P(0w)\ =\ \binom{1}{1}p^0(1-p)^2\ =\ (1-p)^2$$

* $$P(1w)\ =\ \binom{2}{1}p^1(1-p)^2\ =\ 2p(1-p)^2$$

* $$P(2w)\ =\ \binom{3}{2}p^2(1-p)^2\ =\ 3p^2(1-p)^2$$

* $$P(3w)\ =\ \binom{4}{3}p^3(1-p)^2\ =\ 4p^3(1-p)^2$$

* $$P(4w)\ =\ \binom{5}{4}p^4(1-p)^2\ =\ 5p^4(1-p)^2$$

* $$P(5w)\ =\ \binom{5}{4}p^5(1-p)^1 + \binom{5}{5}p^5(1-p)^0\ =\ 5p^5(1-p) + p^5$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 1: Probability of some number of wins given a probability of winning a match </span></center>

&nbsp;

The above block gives the probability of any specific number of wins, where wins is $$w$$. Generally it is the probability of winning raised to the power of the number of wins, multiplied by the probability of losing raised to the power of the number of losses, and multiplied by the number of ways the event can occur. It may seem that I under counted the amount of times each event can occur when calculating the probabilities, and that my binomial coefficients should be $$n$$ choose $$n-2$$ instead of $$n$$ choose $$n-1$$. But you need to consider the fact that for any time you get 2 losses, one of your losses will always be your last game. And similarly, if you ever end with less than 2 losses, your last game must be a win. You can plug in a number and verify these probabilities are unitary if you like, (I also do so myself in my [script](https://github.com/Buggy-Virus/artifact-analysis/blob/master/expectationGraphs.py){:target="_blank"} for generating graphs for this part of the article).

For the expected number of packs for Phantom Draft, we now just take the sum of each  event's probability multiplied by its number of packs.

$$E[d] = 0 P(0w) + 0 P(1w) + 0 P(2w) + 0 P(3w) + 1 P(4w) + 2 P(5w)$$

$$E[d] = P(4w) + 2 P(5w)$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 2: Expected number of packs from one Phantom Draft run </span></center>

&nbsp;

This gives us the expected number of packs for a single Phantom Draft run, $$E[d]$$, where $$d$$ denotes a phantom draft run. For Keeper draft, we can consider the 5 packs worth of cards as part of the rewards for a specific run, and we simply add 5 packs to get the expectation.

$$E[d'] = 5 + 1 P(4w) + 2 P(5w)$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 3: Expected packs from one Keeper Draft run </span></center>

&nbsp;

Thus we get the expected number of packs from a Keeper Draft run, $$E[d']$$.

&nbsp;

#### Expected Number of Runs Per Phantom Draft

Alternatively, some people are just interested in playing as much of the daft format as possible. In this case, we want to calculate the expected number of runs per Phantom Draft run given that the player always chooses to redeem tickets they are awarded for future runs, until they fail to reach 3 wins.

To get this expectation, we what to calculate the the expected number of runs $$d$$ given an initial ticket $$t$$. First, we note that regardless of the outcome of a run, the player experienced a run $$d$$, so in the expectation there is always a 1 term. Also if they get over 3 wins they get another ticket $$t$$ which they can redeem to play more runs. Thus the expectation is:

$$E[t] = 1 + t P(3w) + t P(4w) + t P(5w)$$

$$E[t] = 1 + t \big( P(3w) + P(4w) + P(5w) \big)$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 4: Expected number of runs from one ticket </span></center>

&nbsp;

If we always redeem each of the tickets $$t$$, we can consider rewards that give $$t$$ as instead the expected number of runs $$t$$ gives us, thus we get an equation we can use to solve for the expected number of runs given an initial $$t$$.

$$E[t] = 1 + E[t] \big( P(3w) + P(4w) + P(5w) \big)$$

$$E[t] - E[t] \big( P(3w) + P(4w) + P(5w) \big) = 1$$

$$E[t] \Big( 1 - \big( P(3w) + P(4w) + P(5w) \big) \Big) = 1$$

$$E[t] = \frac{1}{1 - \big( P(3w) + P(4w) + P(5w) \big)}$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 5: Expected number of runs from one ticket solved </span></center>

&nbsp;

At a basic level, this equation makes sense. The more likely you are earn a ticket as a reward, the more runs you are expected to have from a single ticket. As the probability of the event where you receive a ticket rises towards certain, your expected number of runs blows up to infinity.

&nbsp;

#### Expected Number of Packs Per Phantom Draft Ticket

Now we would like to see the number of packs you expect to get from a single Phantom Draft Ticket. The equation is similar to the equatoin for the expected number of runs. We drop the 1 term, as we are no longer tracking each run. Now each event awards a number of packs along with another ticket, so the probability of each event is multiplied by its awarded packs plus the expectation of another ticket. (Additionally we are going to be a little murky with our notation and reuse $$E[t]$$ to denote expected number of packs from one ticket (sorry)).

$$E[t] =  P(3w)E[t] + P(4w)\big( 1 + E[t] \big) + P(5w)\big( 2 + E[t] \big) \big)$$

$$E[t] =  E[t]\big( P(3w) + P(4w) + P(5w) \big) + P(4w) + 2P(5w)$$

$$E[t] \Big( 1 - \big( P(3w) + P(4w) + P(5w) \big) \Big) =  P(4w) + 2P(5w)$$

$$E[t] = \frac{P(4w) + 2P(5w)}{1 - \big( P(3w) + P(4w) + P(5w) \big)}$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 6: Expected number of packs from one Phantom Draft ticket </span></center>

&nbsp;

Note that this is the same result as if we simply multiplied our expected number of packs per run by our expected number of runs per ticket (funny how expecation works that way).

$$\big( P(4w) + 2 P(5w) \big) \times \frac{1}{1 - \big( P(3w) + P(4w) + P(5w) \big)} = \frac{P(4w) + 2P(5w)}{1 - \big( P(3w) + P(4w) + P(5w) \big)}$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 7: Also the expected number of packs from one Phantom Draft ticket </span></center>

&nbsp;

I actually scratched my head on how to describe how one aught interpret this result without basically saying, "it's the expected number of packs per run times the expected number of runs per ticket", again. Honestly, I don't think anything really describes it better than that. So, it's the expected number of packs per run times the expected number of runs per ticket. So again, as your probability of going infinite increases, your expected rewards blow up.

Given that packs are supposed to hold some real money value on the marketplace, this equation implies that players with high winrates would expect enormous value in terms of rewards from 1 ticket.

&nbsp;

#### Note On Keeper Draft

So for Keeper draft, calculating expected number of runs or packs per ticket is awkward as each new run requires five unopened packs. As such it is impossible to earn enough raw rewards from a single run for a second run.

If you make the assumption that you will be supplying the 5 pack cost independantly of your rewards for each run, then the derivation of general equations for the expectations become trivially similar to the derivation of the expectations for Phantom draft. So you'll have to forgive me for not including more on Keeper Draft. Generally if you are able to get very good rewards from Phantom Draft, then playing Keeper will reduce your ratio of rewards to cost, since there is a higher baseline cost and reward. Though it is possible you may value highly the ability to draft five packs over the better reward ratio.

&nbsp;

#### Expected Number of Runs Per Phantom Draft With Exchanging Packs For Tickets

Now let's consider the scenario where you are a draft purist. You have no interest in ever opening a single pack you earn, nor have you figured out the method to play Phantom Draft for free. You sell every pack you receive, and pour that money back into Phantom Draft tickets, a true draft fanatic.

To calculate the expected number of runs, we now introduce $$\gamma$$, the rate at which a pack can be exchanged for a ticket (via some process of presumably selling the pack of its cards and buying a new ticket). Now we use a similar equation as for the runs per ticket, but include card rewards in the form of some fraction of a new ticket determined by $$\gamma$$.

$$E[t] = 1 + P(3w) E[t] + P(4w)\big( E[t] + \gamma E[t] \big) + P(5w)\big( E[t] + 2 \gamma E[t] \big)$$

$$E[t] = 1 + P(3w) E[t] + P(4w)E[t](1 + \gamma) + P(5w)E[t](1 + 2\gamma)$$

$$E[t] = 1 + E[t] \big( P(3w) + P(4w)(1 + \gamma) + P(5w)(1 + 2\gamma) \big)$$

$$E[t]\Big(1 - \big( P(3w) + P(4w)(1 + \gamma) + P(5w)(1 + 2\gamma) \big) \Big) = 1$$

$$E[t] = \frac{1}{1 - \big( P(3w) + P(4w)(1 + \gamma) + P(5w)(1 + 2\gamma) \big)}$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 8: Expected number of runs from one Phantom Draft ticket when recycling packs </span></center>

&nbsp;

This equation looks similar to the vanilla expected number of runs per Phantom Draft ticket, but now we have all these weird $$\gamma$$s floating around. Intuitively, better the rate you can exchange packs for tickets, the more runs you will get to play.

The odd part about this equation, is when not exchanging, it was impossible to go infinite, as $$P(3w) + P(4w) + P(5w) < 1$$. So for a given win probability less than 1, you would always get a real positive number as your expected number of runs.

For the expectation with recyclying, depending on win probability and recycle rate, $$P(3w) + P(4w)(1 + \gamma) + P(5w)(1 + 2\gamma)$$ can be greater than 1. If this is the case, the general equation I wrote will equal a negative number, which may be confusing. What it's implying is the expectation of one ticket is greater than 1 ticket. The only way to reconcile this in the equation is a negative number, but what it is implying is that you are expected to have an infinite number of runs, as each run you end up with an equal or greater number of tickets than you started with.

&nbsp;

### Graphs And Stuff

For a baseline, let's consider the probabilities of achieving a certain number of wins in draft with a 50% win rate. If the matchmaking ranking of Artifact functions correctly, we can expect the majority of players to have a winrate that is about 50%.

* $$P(0w) = 0.25$$

* $$P(1w) = 0.25$$

* $$P(2w) = 0.1875$$

* $$P(3w) = 0.125$$

* $$P(4w) = 0.078125$$

* $$P(5w) = 0.109375$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 9: Probability of a certain number of wins with a 50% winrate </span></center>

&nbsp;

This may seem pretty bleak, with there being a 50% change a player gets at most one win, and less than 20% chance that they win any rewards in a run, but once we start taking into account the fact that you can recursively win more tickets, we'll see it isn't quite as unrewarding as it looks.

Next we look at the graph of expected packs per run against win probability.

<center><img src="/assets/artifact-economy-analysis/packsPerRun.png" alt="Graphing in Python is very conveniant" style="width:640px;height:480px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 2: Expected packs per run graphed against win probability</span></center>

&nbsp;

This is a fairly straightforward story, your expected packs per run goes up as your win probability goes up, with it tapering off at 2 packs as your winrate gets closer to 100%, at which point you will always win 2 packs. We see here your expected number of packs only becomes 1 around 70%, and only becomes 0.5 at 60%, where 0.5 is how much we should expected a ticket to be worth since it costs half as much as a pack.

Looking at expected number of runs per ticket:

<center><img src="/assets/artifact-economy-analysis/runsPerTicket.png" alt="The story is starting to come together" style="width:640px;height:480px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 3: Expected runs per ticket graphed against win probability</span></center>

<center><img src="/assets/artifact-economy-analysis/runsPerTicketBlowUp.png" alt="The story is starting to come together" style="width:640px;height:480px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 4: Expected runs per ticket graphed against win probability extended to 95% win probabilty</span></center>

&nbsp;

Here we see the inverse growth, where the expected number of runs blows up as you get closer to 100%. Around the more reasonable win rates, we see 1.5 to 3 runs per ticket. Getting to a really unheard 80% you see 5 runs. It only starts getting really ridiculous numbers and growth at 85%, which is an extremely difficult winrate to achieve.

<center><img src="/assets/artifact-economy-analysis/packsPerTicket.png" alt="Inverse functions behave like inverse functions" style="width:640px;height:480px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 5: Expected packs per ticket graphed against win probability</span></center>

<center><img src="/assets/artifact-economy-analysis/packsPerTicketBlowUp.png" alt="Things blow up to infinite, who knew" style="width:640px;height:480px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 6: Expected packs per ticket graphed against win probability extended to 95% win probabilty</span></center>

&nbsp;

Here we see a very similar story, where the number of expected packs blows up as the winrate increases. At 70% we see about 2.7 packs, at 60% you can expect about 1 pack, and at 50% you can expect about 0.43 packs. Considering that a ticket costs about half a pack, this makes phantom draft a very good alternative to opening packs if you have a winrate that is slightly higher than 50%, but even at 50% you are still almost getting as much value as just buying packs. As you hit 60% though, you are getting twice as much value as buying packs, and it starts growing rapidly from there. Looking at the extended graph we just see the power of inverse functions as expected packs grows to around 20 at 85% then skyrockets into the hundreds near 95%. Again maintaining these high winrates should be very difficult with a proper MMR system.

Now we'll move onto what I think is the most interesting result, runs per ticket with recycling.

<center><img src="/assets/artifact-economy-analysis/runsPerTicketRecycling.png" alt="3d plots are nice to look at, but difficult to interpret" style="width:640px;height:480px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 7: Expected runs per ticket with recycling graphed against win probability and recycle rate</span></center>

&nbsp;

This is a more difficult graph to interpret, and it is hard to see the growth in the expected number of runs. What is really interesting here though, is what looks like a gap running across the data. The gap is where there are points that suddenly blew up and are very high, or are very negative, and then all points to the right of it are actually negative numbers close to zero. This gap and the points to the right signify points where the player expects to go infinite with a single ticket. 

None of these data points use a winrate below 60%. The 2 tickets per pack recycle rate is based on the idea that a pack's cost is twice the cost of a ticket. It's more likely a pack or its cardss' values on the marketplace won't be near the value you can buy it at, thus a recycle rate of 1 or even lower seems more plausible. That being said this is a very optimistic result, as you can literally expect to go infinite with a winrate less than 60% if the recycle rate is higher than 1. Further with the incredibly optimistic recycle rate of 2, you can expect to go infinite with about a 50% winrate.

Thus, even if there isn't a free to play draft mode with matchmaking, if you are quite good at draft with a 55% to 60% winrate, and you literally only care about draft, you should be able to go infinite as long as the recycle rate doesn't drop too low. It is a distinct possibility that the contents of packs really will be devalued, especially as more and more players play draft and pump packs into the economy, making going infinite very difficult. But if this is the case, then constructed should become very affordable, reflected generally by the drop in the average value of a pack on the marketplace.

So we see that the ability to focus on only playing phantom draft trades off with the affordibility of constructed at a pretty extreme rate.

An addendum I'm adding right before posting: the details on recycling cards for packs has been announced, and 20 cards can be recycled for 1 ticket. This gives a lower bound on the recycle rate at rouchly 0.5 tickets per pack. This is still low enough that it would require a very high winrate to maintain, but in the theme of alot of this article, it gives a bound.

&nbsp;

## Upper Bound On Rare Card Costs

Here I'll be deriving upper bounds on the cost of rares. These upper bounds describe the highest a specific rare card's price can be on the marketplace under a set of assumptions. Although this doesn't attempt to directly predict the price of a specific card, it is still useful in that it narrows the range of what the price can be, and provides an idea of the order of magnitude of the cost of the more expensive cards. Generally I would expect a card's price to be very far from any upperbound, and I would be surprised if one card started encroaching on it. Then again I can't guarentee it won't encroach on the upper bound, only that it won't violate the upper bound under my assumptions (thus why it's called an upper bound I guess).

&nbsp;

### Upper Bound Through Unpacking Cards
 
Unlike most economies which are driven purely through supply and demand, where supply is dictated by agents selling goods at a variable price and demand by consumers looking to make transactions with these sellers, Artifact has another source of supply by the advent of it being a digital card game. Thus instead of the classic two function supply demand graph, we introduce another constant function, denoting the ability for consumers to purchase an infinite number of packs at a constant price directly through Artifact.

<center><img src="/assets/artifact-economy-analysis/supplydemand.png" alt="So so ugly" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 7: Supply and demand with a second supply curve from pack price (Let me know how noticeable it is that my photoshop key expired and that my drawing tablet is still packed (I'll update it to a prettier graphic once I stop being lazy and get a handle on my life))</span></center>

&nbsp;

This means regardless of the price of a card on the Steam Marketplace, you can always turn to opening packs to get a constant price in expectation. So if we are interested in the expected cost of getting a specific rare card from packs, we can easily calculate that cost based on the information that every pack will contain at least one rare.

$$E[q] = p(r)$$

$$E[q] \geq \frac{1}{\vert R \vert }$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 10: Expected number of a specific rare from a single pack </span></center>

&nbsp;

The expected number of the specific rare $$r$$ that you would get from some pack $$q$$ is simply the probability of pulling that rare from a pack. Since we know that you are guarenteed at least one rare per pack, that means the probability of pulling $$r$$ from $$q$$ is at least the inverse of the cardinality (or count) of the set of rares, $$\vert R\vert$$.

Thus we can calculate the number of packs necessary for you to pull at least one $$r$$ in expectation.

$$\vert R \vert  E[q] \geq \frac{\vert R \vert }{\vert R \vert }$$

$$E[\vert R \vert q] \geq 1$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 11: Number of packs where you would expect at least one of a specific rare </span></center>

&nbsp;

This is fairly straightforward, if you open as many packs as there are rares in the set of rares, in expectation you will recieve at least 1 of any specific rare. Here we'll introduce our first assumption: 

* **Assumption 1:** The value of all other cards in the set of all cards except for a specific rare, $$v(c), c\in C \setminus r$$, is zero, $$v(c)=0$$.

With this assumption, the expected cost of opening packs to get $$r$$ is simply the number of packs necessary to pull 1 $$r$$ in expectation times the cost of a pack. If we let the cost of a pack be $$g$$, then this is:

$$E[v'(r)] \leq g\vert R \vert$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 12: Expected cost of getting a specific rare from opening packs</span></center>

&nbsp;

Here we can get our first upper bound on $$v(r)$$ from under our next assumption:

* **Assumption 2:** No one will purchase a specific rare $$r$$ from the market place if it's cost on the marketplace, $$v(r)$$, is higher than the expected cost of getting it in a pack, $$E[v'(r)]$$.

$$v(r) \leq E[v'(r)] \leq g\vert R \vert$$

$$v(r) \leq g\vert R \vert$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 13: Upper bound 1, upper bound on the marketplace cost of a specific rare due to the expected cost of getting the rare from packs, uses assumption 1 and 2</span></center>

&nbsp;

This is a fairly intuitive upper bound, but I would argue a useful one that will probably empirically hold  even without the two assumptions being necessarily true. Generally, I imagine many players would obey assumption 2, due to the fact that they chose to play Artifact, a game with a high amount of chance. So they are probably not so risk adverse that they would prefer to pay a price that is higher than an expected price. Secondly, assumption 1 is super strong, and as you relax it, the value of all the packs you open while searching for $$r$$ can both have gameplay value, or be sold on the marketplace. Thus the value of the extra cards you open would offset the cost of all the packs, making the pack strategy much more attractive, but we'll do more specific analysis on relaxing assumption 1 later.

&nbsp;

#### Plugging In Some Numbers

Using the fact that $$\vert R \vert=76$$, and the cost of a pack is $$g = $2$$, the upper bound becomes:

$$v(r) \leq g\vert R \vert$$

$$v(r) \leq $152$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 14: Upper bound on marketplace cost of a specific rare due to the expected cost of getting the rare from a pack pack, with input numbers, uses assumption 1 and 2</span></center>

&nbsp;

Well it's a bound, but I imagine it's pretty scary for most people, as no one is excited by the idea of spending $152 on one card. But it's important to note again that this is an upper bound, and simply states a rare can't be more expensive than this. We shouldn't necessarily expect any rare to be anywhere near it's upper bound. 

What I find significant is that there is a bound at all, which isn't the case in non-digital trading card games where supply through packs is finite. Also this bound is based off the extremely strong assumption 1, and we will find lower upper bounds as we relax it later.

&nbsp;

### Upper Bound Enforced By Arbitrage

A much more interesting upper bound than the previous one using assumption 2, and one that is even more likely to hold empirically, is the upper bound enforced by arbitrage. Should the price of a specific rare, $$v(r)$$, rise too high, agents can engage in statistical arbitrage where they buy packs until they get get $$r$$, then recoup the the cost of the packs and make a profit through selling $$r$$ at $$v(r)$$.

This upper bound would be trivially the same as the last one, if it was not for the fact that Valve takes a percentage cut of all sales on the steam marketplace. If we denote this cut as $$(cut)$$ (creative I know), we let the fraction of a revenue a seller recieves from a sale to be $$1-(cut)=\delta$$. So now if one sells a card $$r$$ on the marketplace they recieve $$\delta v(r)$$.

Using this we can calculate the minimum price a specific rare, $$v(r)$$ must be on the market for an arbitrage opportunity to exist. Note here assumption 1 still holds.

$$\delta v(r) \geq E[v'(r)]$$

$$\delta v(r) \geq \vert R \vert g$$

$$v(r) \geq \frac{g\vert R \vert}{\delta}$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 15: Condition under which an arbitrage opportunity exists</span></center>

&nbsp;

But I argue that the marketplace should never exist in a state where an arbitrage opportunity exists, as it should immediately be executed, as it is just free money. As agents attempting to execute the arbitrage compete with each other, they drive down the price, since the agent with the lowest price gets the execution, incentivizing all agents to drop their prices. This continues until the $$v(r)$$ no longer fulfills the condition where an arbitrage opportunity exists. We add this as our third assumption.

* **Assumption 3:** Arbitrage opportunities cannot exist.

Thus, under assumption 1 and 3, we have an upper bound at the point where the arbitrage condition would become true.

$$v(r) \leq \frac{g\vert R \vert}{\delta}$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 16: Upper bound 2, upper bound on marketplace cost of a specific rare due to arbitrage, uses assumpitions 1 and 2</span></center>

&nbsp;

This is a weaker upper bound than the first one we derived, but I include it because it's more interesting, and I think there are plenty of people that feel assumption 3 is more valid than assumption 2. Discussing assumption 3 for a moment, empirically we see arbitrage opportunities in real markets all the time, but the point is they are usually quickly corrected at a high speed, such that anyone who isn't an agent specializing in capitalizing on arbitrage can't access them. In this way, even if arbitrage opportunities end up existing in the marketplace, I expect it will be so briefly that it won't affect normal players (if not good for you, and take get some free money when it happens).

What makes this upper bound especially useful is that the revenue fraction parameter $$\delta$$ can be changed and alter the meaning of the upper bound. If we let $$\delta = 1$$ we have our upper bound 1 using assumpition 2. So for future calculations we'll ignore whether we are considering the arbitrage versus the expectation upper bound, and just include the $$\delta$$ multiple.

&nbsp;

#### Plugging In More Numbers

We see a similar result as upper bound 1 when we plug in some numbers. Again $$\vert R \vert = 76 $$, $$g=$2$$, and now $$(cut) = 0.15$$, thus $$\gamma = 0.85$$.

$$v(r) \leq \frac{g\vert R \vert}{\gamma}$$

$$v(r) \leq \frac{2(76)}{0.85}$$

$$v(r) \leq 178.83$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 17: Upper bound 2, upper bound on marketplace cost of a specific rare due to arbitrage, with input numbers, uses assumpitions 1 and 2</span></center>

&nbsp;

As I said earlier, this is a weaker upper bound than the first one we calculated, but the assumptions required for it may be more palatable to some readers. Also again, this may seem very high, but you have to remember that it is using the very strong assumption 1, and we don't expect cards to necessarily be anywhere near these upper bounds.

&nbsp;

### Relaxing Assumption 1 For a Tighter Bound

Now we are going to relax assumption 1, to get a more realistic and tighter upper bound. So now we'll use assumption 1.1 instead of 1.

* **Assumption 1.1:** The value of all cards other than rares, $$c\in C\setminus R$$, is zero.

Now we have an enviroment that is closer to what the reality is, where all rares hold some value, rather than the very strong assumption that only one rare held value.

First we note that if an agent doezsn't recieve $$r$$ from a pack they open, they receive a card that is expected to be worth the average of all $$r'\in R\setminus r$$, which we will define as $$\alpha$$. Thus the new expected value from an opened pack is:

$$E[q] \geq \delta \Big(\frac{1}{\vert R \vert} r + \frac{\vert R \vert - 1}{\vert R \vert}\alpha \Big)$$

$$\vert R \vert E[q] = E[\vert R \vert q] \geq \delta \big( r + (\vert R \vert - 1)\alpha \big)$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 18: Expected value of a pack with assumption 1.1</span></center>

&nbsp;

Now if we consider the condition under which people would choose to buy packs to get a card or arbitrage is possible, (depending on which assumption and value for $$\delta$$ we use), we have:

$$\delta \big( v(r) + (\vert R \vert - 1)\alpha \big) \geq \vert R \vert g$$

$$v(r) + (\vert R \vert - 1)\alpha \geq \frac{\vert R \vert g}{\delta}$$

$$v(r) \geq \frac{\vert R \vert g}{\delta} - (\vert R \vert - 1)\alpha$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 19: Condition under which arbitrage exists or buying packs for a card is more attractive than the marketplace depending on assumptions and $$\delta$$</span></center>

&nbsp;

Under our assumptions this condition can never be true, we get another upper bound.

$$v(r) \leq \frac{\vert R \vert g}{\delta} - (\vert R \vert - 1)\alpha$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 20: Upper Bound 3, upper bound using average cost of rares with assumption 1.1 and either assumption 2 or 3</span></center>

&nbsp;

Now we see that as we relax assumption 1 to assumption 1.1, the price of $$r$$ becomes bounded by the cost of the packs to get $$r$$, minus the average cost of a rare times the number of packs you open without $$r$$. This uncovers an interesting relationship, the upper bound on the price of any individual rare linearly trades off with the average cost of all other rares. This may seem unintuitive, until we consider if we also threw out assumption 1.1, in which case all cards, $$c\in C\setminus r$$, have a value, and we consider the average of all these cards as $$\beta$$. In this new case if we went through a similar derivation and $n$ was the number of cards you get from a pack we would end up with:

$$v(r) \leq \frac{\vert R \vert g}{\delta} - (n\vert R \vert - 1)\beta$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 21: Upper Bound 4, upper bound using the average cost of all other cards</span></center>

&nbsp;

This simply says that the cost of your card is at most how much spent on all your packs minus the value of all the other cards you received. Which is a pretty trivial result that I imagine most people intuitively understand. But the implication is still interesting, as the upper bound of an individual card falls linearly as the average value of cards rises. This is because as the average rises, your cost of opening packs, while looking for a specific card, drops because you can easily resell cards. This is something we don't see in other digital card games lacking marketplaces as unnecessary cards don't hold a value apart from their gameplay value to the player, other than their recycle value, which is set by the developers to a constant.

&nbsp;

#### Plug In Those Numbers

<center><img src="/assets/artifact-economy-analysis/ass1ass2graph.png" alt="A linear graph, yay" style="width:640px;height:480px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 8: Upper bound using assumption 1.1 and assumption 2, graphed against the average cost of all other rares</span></center>

<center><img src="/assets/artifact-economy-analysis/ass1ass3graph.png" alt="It's alomst as if I could have just said it was linear and not bother graphing this" style="width:640px;height:480px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 9: Upper bound using assumption 1.1 and assumption 3, graphed against the average cost of all other rares</span></center>

&nbsp;

Here we see the nice linear relationship of both of these functions with regards to the average cost of other rares (it's almost as if a linear curve implies I only needed to graph 2 points, huh). It may be surprising to people to see how quickly it drops, with it being about half of upper bounds 1 and 2 once the average cost of other rares hits $1. As it heads towards $2, it drops below $10 under assumption 2. At $2 under assumption 3, the upper bound is still about $20, but it drops below $10 if the average rises just a couple cents above $2.

<center><img src="/assets/artifact-economy-analysis/ass2ass3noass1.png" alt="This is a no ass 1 type of graph" style="width:640px;height:480px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 10: Upper bound using assumption 2 (the lower one) and assumption 3 (the higher one), graphed against the average cost of all other cards</span></center>

&nbsp;

Looking at the graph where we calculate the upper bound of a rare using the average of all other cardsm, $$\beta$$, we see an even more dramatic decrease as the average rises. But having an extremely low average cost among all cards, something around $0.10 isn't that wild, nor is it being closer to $0.20, so I feel this graph is much less useful in understanding constraints on the economy, until we've seen empirical data in the future.

&nbsp;

### Upper Bound On Average Cost Of Rares

So now we have an upper bound that applies to every rare that depends on every other rare. Using this we can consider what the highest possible average cost of all rares without violating the upper bound for any individual rare. This would occur when all rares are at their upper bound, requiring all $$v(r)$$ to be equal.

If we had a case where only one rare, $$r'$$ wasn't at its upper bound, we could increase the value of $$r'$$ by some small amount, $$\epsilon$$, less than the difference between the current value, $$v(r')$$ and $$r$$'s upper bound. This would increase the $$\alpha$$ for every other rare by $$\epsilon / (\vert R \vert - 1)$$. Thus it the upper bound for these other rares would fall, but it doesn't fall by $$\epsilon / (\vert R \vert - 1)$$ across these $$\vert R \vert - 1$$ rares. This is because as all rares at their upper bound have their prices fall, $$\alpha$$ drops. Thus since one rare had its price rise by $$\epsilon$$ and $$\vert R \vert - 1$$ rares had their price fall by less than $$\epsilon / (\vert R \vert - 1)$$, the sum of all prices must have increased. Thus in this scenario, pushing the last rare to be at its upper bound raises the total sum, and thus raises the average price of all the rares.

Further the instance where one rare is not at its upper bound, is the insance where one rares price rising needs to be offset by the most amount of other rares price falling, as it has the most rares at their upper bounds. Since in the least advantageous case, the price still rises when pushing a rare's price to its upper bound, it must be the case that we always increase the total price across all rares by raising a the price of some rare which isn't at its upperbound towards its upperbound, and letting the price of rares at their upper bounds drop, while keeping the price of all other rares not at their upper bounds fixed. This implies that we have the highest possible average when all rares are at their upper bound, thus requiring all rares to be equal.

You can also show the above statements is true by running a linear program where the objective function is maximizing the average price, and the conditions are that all prices are greater than zero and obey the upper bound for each rare. I have this LP written up in the [script](https://github.com/Buggy-Virus/artifact-analysis/blob/master/ubGraphsAndLp.py){:target="_blank"} for generating the graphs for this part of the article, and you can run it to confirm my statements.

For all rares to be at their upper bound it must be the case that:

$$v(r) = \frac{\vert R \vert g}{\delta} - (\vert R \vert - 1)\alpha$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 22: Condition for all rares to be at upper bound</span></center>

&nbsp;

In order for this condition to be true across all $$r$$, it requires that all rares be the same price, thus the $$\alpha$$ for any $$r$$ will be equal to $$v(r)$$. Thus we can find the upper bound for the average cost of the rare cards, where $$u$$ the upper bound.

$$v(r) = \frac{\vert R \vert g}{\delta} - (n\vert R \vert - 1)\alpha$$

$$u = \frac{\vert R \vert g}{\delta} - (n\vert R \vert - 1)u$$

$$u + (n\vert R \vert - 1)u = \frac{\vert R \vert g}{\delta}$$

$$u\big(1 + (n\vert R \vert - 1)\big) = \frac{\vert R \vert g}{\delta}$$

$$u \vert R \vert = \frac{\vert R \vert g}{\delta}$$

$$u = \frac{g}{\delta}$$

$$\alpha \leq u = \frac{g}{\delta}$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 23: Upper Bound 5, uppder bound for the average cost of a rare using assumption 1.1</span></center>

So now we have a rather surprising result. The average cost of a rare is capped at the cost of a pack, times the inverse of $$\delta$$. If we consider assumption 2 to hold, then $$\delta$$ is simply 1, and then the average cost of a rare is capped at the cost of a pack. And if we only consider assumption 3 to hold, then it is capped at an amount slightly more than the price of a pack, and if assumption 3 does hold, some complicated arbitrage exists (somewhere).

Further this result is still assumes assumption 1.1 holds. I imagine there is a similar way to derive the upper bound on the average cost of a rare when not assuming all non-rare cards have 0 value. That upper bound should be even tighter than the one calculated above, but this is left as an exercise for the reader.

&nbsp;

#### Plugging In Numbers For The Last Time

So now if we plug in the cost of packs, we get:

$$\alpha \leq \frac{g}{\delta}$$

$$\alpha \leq $2$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 24: Upper bound 5 for the average cost of a rare, with inputs using, assumption 1.1 and assumption 2</span></center>

&nbsp;

The above bound is if we assume assumption 2 holds, and players will always choose to buy pack over go to the market place if the value of the rares they get from the packs exceeds the price of the number of packs required to get the a specific rare.

$$\alpha \leq $2.36$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 26: Upper bound 5 for the average cost of a rare, with inputs, using assumption 1.1 and assumption 3</span></center>

&nbsp;

If instead we consider asusmption 3 holds, and arbitrage opportunities cannot exist, we get a slightly higher upper bound.

These upper bounds are much more heartening, and point the the cost of rares being quite low. And again we need to remember, that these are upper bounds, but the average price of a rare will likely be much lower than the upper bound, though how much lower exactly is yet to be seen.

&nbsp;

## Conclusion

We can see that phantom draft is a reasonable value compared to opening packs at a 50% winrate, and as one's winrate increases, the number of packs and runs you can expect greatly increases. Even at just a 60% winrate one can expect about twice the value as just opening a pack. Further the idea of going infinite if one is willing to sell all their pack rewards, and packs don't become too devalued, doesn't not require that wild a winrate. Thus Phantom Draft is a great alternative to buying packs for any player that is able to maintain a higher than average winrate.

The upper bounds I derived without using averages doesn't bound the price at a very affordable number, but they mostly are a testament to bounds existing at all. Once you start considering the bounds as a function of the average cost of other cards, we begin to see bounds which have direct implications on the affordability of Artifact at relatively reasonable average prices. Further the bound on the average price of rares is quite low, and takes no inputs other than the number of rares and price of packs, although it requires either assumption 2 or 3.

Personally I expect assumptions 2 and 3 to be true, even if it isn't because of people actively making the calculus to buy packs instead when favorable, or people executing arbitrage opportunities. I'm not going to try to argue this here, as it is just a intuitive hunch from working with markets in the past, but seems like something that we are better off just waiting to observe when the game comes out (in less than a week).

When I started working on these problems, I already intuitively understood the first two upper bounds I presented here, and had a general idea about the expectation from the draft being a somewhat reasonable value compared to opening packs. But the result of being when one is able play draft infinitely and the upper bound on the average cost of rares greatly surprised me. So I'm pretty glad I went through all of these calculations, and I hope people find it helpful or are able to use it for further analysis and discussion. You can see my scratchwork code for calculating some values and generating the graphs [here](https://github.com/Buggy-Virus/artifact-analysis){:target="_blank"}. Thanks.

&nbsp;

&nbsp;

&nbsp;

&nbsp;