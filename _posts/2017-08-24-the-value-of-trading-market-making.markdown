---
layout: post
title:  "The Value of Trading: Market Making"
date:   2017-08-24 15:50:00 -0400
categories: trading, finance,
tags: trading, finance,
---
A common question I've gotten from many of my friends is what value does trading add to society. I think the fact that trading doesn't have a physical product, in addition to the zero sum game traders play against each other, makes it seem to many people that trading is an activity that only enriches those who engage in it, possibly to the detriment to the rest of society. I hope I'll be able to explain why this isn't the case.

The simplest answer to this question is that trading makes markets more efficient. I'm sure you've heard this before, and it isn't exactly clear why we should care about market efficiency. The reason is efficient markets free up capital, which can then be used to create some tangible product. Below I'll explain some examples that illustrate this process, and how trading is beneficial to all non-traders in a market.

&nbsp;

### What I Mean When I Say Trader

Throughout this post, when I refer to traders I am not referring to anyone who makes trades on a financial market. I'm referring to actors in the market that have equal expectation that the price will go up or down for any security they trade. They are not dependant on the value of the security they are trading changing with respect to time.

These traders are market makers or trade arbitrage. They have no stake in whether security prices will go up or down, and their profitability is based on making securities' prices better reflect their true values.

Alternatively, what I would refer to as "investors" buy or sell a security at one point in time, hoping that the market value of the security will change, and then at a later point in time execute the other side of the trade and make a profit.

The definition of trader and investor I'm using here is by no means the correct or true definition of trader, and when other people say trader they likely are not referring to the definition I'm using here. I'm just using this definition for the purpose of clarity in this article, as I am only going to talk about those who fall in this definition of trader.

&nbsp;

&nbsp;

## Market Making

Before explaining how traders who function as market makers create value for society, or even what they are, let me build a hypothetical scenario.

Let's imagine we're at the intergalactic exchange. We're looking at the gleep market in particular, which trades in the currency blorgs. Currently the best bid for a gleep is 10 blorgs, meaning that someone is openly stating that they will pay 10 blorgs to anyone in exchange for a gleep. The best offer is 15 blorgs, meaning that someone is openly stating that if someone pays them 15 blorgs, they will give them a gleep. So the market looks like this:

<center><img src="/assets/the-value-of-trading-market-making/gleep-market-0.png" alt="The Renowned Gleep Market" style="width:500px;height:400px;text-align:center;"></center>

There are other bids and offers, but all other bids are for less than 10 blorgs, and all other offers are above 15 blorgs, so we won't worry about them for now.

But what is the [true value of a gleep][friendship]? There is no way to discern the true value, what we do know, is that it is somewhere between 10 and 15 blorgs, inclusive. Let's say it is actually 12.5 blorgs, and there are a bunch of gleep farmers that want to sell their gleeps at a price lower than 15, but are waiting for a more favorable bid above 10 blorgs to sell to. Similarly there are a bunch of gleep eaters (it's like, an alien food or something) who are willing to buy gleeps at a price above 10 blorgs, but not for 15 blorgs. (I'll talk about the reason why they don't put bids and offers of their own on the market later)

<center><img src="/assets/the-value-of-trading-market-making/gleep-market-1-1.png" alt="The Renowned Gleep Market 1.1" style="width:500px;height:400px;text-align:center;"></center>

Now enters you, the gleep market maker. You have zero interest in physical gleeps, in fact you're allergic, so the less gleeps you end up with, the better. You come into the gleep market, and make a bid at 11 blorgs **and** an offer at 14 blorgs. We call this making a market. So now the market looks like this:

<center><img src="/assets/the-value-of-trading-market-making/gleep-market-2-0.png" alt="The Renowned Gleep Market 1.1" style="width:500px;height:400px;text-align:center;"></center>

After doing this, all the gleep farmers, who are willing to sell gleeps between 10 and 11 blorgs, hit your bids. All the gleep eaters, who are willing to buy your gleeps between 15 and 14 blorgs, take your offers. We'll say there are *x* of these farmers and *y* of these eaters.

<center><img src="/assets/the-value-of-trading-market-making/gleep-market-2-1.png" alt="The Renowned Gleep Market 1.1" style="width:500px;height:400px;text-align:center;"></center>

Let's just say that *x = y*, this means you bought and sold equal amounts of gleeps, so you ended up net 0 gleeps. Since you bought each of these gleeps at 11 blorgs, and sold them at 14, this means you have a profit of 3*x* blorgs. In addition to your profit, we allowed a bunch of gleep farmers to sell their product, and a bunch of gleep eaters got their favorite food.

&nbsp;

### Effect on Society

The utility you created by making this market is at least your profit, since that is the utility you created for yourself by making a profit. Additional utility may be captured by any of the gleep farmers and eaters whom bought or sold gleeps at a price better than their personal valuation of gleeps. For example, let's say there are gleep eaters that think gleeps are worth exactly 14.5 blorgs to them. This means every gleep they bought at 14 blorgs netted them a utility of 0.5 blorgs.

<center><img src="/assets/the-value-of-trading-market-making/gleep-market-2-2.png" alt="The Renowned Gleep Market 1.1" style="width:500px;height:400px;text-align:center;"></center>

There are plenty of other gleep farmers and eaters who gained utility from trades in a similar way. Thus when market making is profitable, the trader gains utility, and at worst no utility is added to the rest of society (but it is not hurt), and at best some amount of utility is added equal to the amount of trades made multiplied by the margin between their offer or bid and the the best offer or bid before you made a market.

 
$$\text{your utility} = min(x, y) \times (your\ offer - your\ bid)$$

$$\text{gleep eater utility} = y \times (best\ offer - your\ offer)$$

$$\text{gleep farmer utility} = x \times (your\ bid - best\ bid)$$


<center><span style="font-size:14px;color:#828282;text-align:center;">I did gloss over the issue of when <i>x</i> and <i>y</i> are not equal. In that case, the trader needs to buy or sell gleeps to make up the difference, eating into their profits.</span></center>

&nbsp;

For a less utilitarian explanation, imagine the gleeps are instead wheat futures, and the blorgs are dollars. This means more wheat farmers are able to sell their crops, and continue supporting themselves. Bakers, who previously couldn't afford wheat to make their bread, now are able to buy wheat and bake bread. Additionally, all the wheat farmers and bakers, who were able to operate before, operate with much better margins, freeing up more capital for them to use. All the extra business that was enabled by more competitive prices of the market, is the product of the trader making markets. This is an example of trading translating directly into tangible products (in other situations, it's a lot more complicated).

&nbsp;

### The Zero Sum Nature of Trading

Market making is still a zero sum activity, but this zero sum game is played between traders. And this game is to the benefit to the rest of society.

The profit of a market maker is greater the bigger the margin between their bid and offer. In our earlier gleep example your 3 blorg profit per gleep was the difference between your 14 blorg offer and your 11 blorg bid. 

Now your galactic arch-enemy, the alien Liam, wants to muscle in on your profits. So he also makes a market of 12 blorg bid and 13 blord offer.

<center><img src="/assets/the-value-of-trading-market-making/gleep-market-3-0.png" alt="The Renowned Gleep Market 1.1" style="width:500px;height:400px;text-align:center;"></center>

Now all gleep trades go to Liam, and he makes all the profits. But his profit is only 1 blorg per hit bid and taken offer. Additionally, everyone who was making utility by buying and selling at your more competitive prices (than the original market), make even more utility.

To capture profits again, you make a market even more compeitive than Liam, and then he is incentivized to then do the same. This theoretically continues until you have the smallest possible margin around the true value of a gleep. If there was no limit on the smallest decimal of a blorg you can trade on (it's probably due to it being some weird alien cryptocurrency or something) then the gleep market's best bid and offer would be ~12.5 blorgs, reflecting the true price of the market.

<center><img src="/assets/the-value-of-trading-market-making/gleep-market-3-1.png" alt="The Renowned Gleep Market 1.1" style="width:500px;height:400px;text-align:center;"></center>

There is virtually no profit in the market for you or Liam at this point. But all the gleep farmers and eaters now derive the maximum utility they can by interacting with the market.

Thus in the long run, market making has made the market perfectly efficient, providing society with the most utility possible, and enabling as much gleep business as possible.

&nbsp;

### Why Doesn't This Happen Naturally

If there are farmers and eaters who are willing to make transactions at more competitive prices than listed, why don't they make their own bids and offers? Why did they wait for you to make a market for them?

This question doesn't actually show that market makers can have a negative impact on society, but rather poses the question why we have them at all. Theoretically the market could achieve efficiency without them, there is no explicit barrier. That being said, there are plenty of profitable market making firms, meaning that there are plenty of markets like our gleep market that are improved through them. This is proof enough as to the fact that market makers provide a value to society. That being said, I'll try to explain why marketn prices aren't naturally perfectly competitive.

There is risk in offering more competitive bids and offers than the existing ones in a market. This risk comes from various sources like adverse selection (an important concept that I'll talk about in a future post). A market maker eats this risk whenever they make their market, and make it more competitive for the gleep farmers and eaters.

Let's go back to the original gleep market before you did some market making. In this example, let's say the real price of gleeps is actually exactly 15 blorgs. This means that if any gleep farmer makes an offer below 15 blorgs, they will receive less blorgs than their gleep is actually worth. As such, they all set their offers at 15 blorgs, and perhaps slowly eaters are taking their offers.

Now you come in and make your market:

<center><img src="/assets/the-value-of-trading-market-making/gleep-market-4-0.png" alt="The Renowned Gleep Market 1.1" style="width:500px;height:400px;text-align:center;"></center>

None of the farmers hit any of your bids at 11 blorgs, since the true price is actually 15 blorgs. Gleep eaters start feverishly taking your offers at 14 blorgs, until you realize something is wrong, at which point you cancel all your listed bids and offers.

The market goes back to how it was before, and you're left short *z* gleeps, from all the trades you did. You must fulfill all these gleep orders, so now you need to go back to the market and buy some gleeps yourself from listed offers, until you have *z* gleeps to fill all your orders. This means you are buying gleeps for 15 blorgs (the price the farmers are offering at), and end up with a net loss of *z* blorgs at the end of the day.

From a utilitarian perspective, you lose *z* blorgs of utility. But importantly, no one aside from the trader lost any utility. In fact, all the gleep eaters who bought at your lower price gained utility by buying at your lower price. So society is at worst not harmed, and any harm is isolated to the trader.

&nbsp;

&nbsp;

## Afterword

There is no reason to prefer not having traders act as market makers in a market. As they don't harm non-traders who participate in markets in any situations, and may result in improving prices and providing utility to other market actors if they are profitable.

I hope this was a clear explanation as to how market makers fundamentally function, and how it provides value to society. If anything is unclear or you have any questions (or arguments) feel free to [contact][contact] me.

I meant to also talk about arbitrage traders in this post as well, but it ended up being much longer than I expected. I'll write a post about it and delve more into the idea of societal value from improving the accuracy of prices there.

&nbsp;

&nbsp;

[friendship]: /friendship
[contact]: /contact/