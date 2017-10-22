---
layout: post
title:  "Game Board Light Propagation Algorithm"
date:   2017-10-22 02:00:00 -0000
categories: daedalus, algorithms, light, lightsys,
tags: daedalus, algorithms, light, lightsys,
---

In my free time I’ve been trying to come up with a good $$O(n^2)$$ algorithm for propagating light across a $$ 2D $$ game-board of with side length of $$n$$, thus $$n^2$$ tiles. We can think of this game board as  a $$ 2D $$ array, and we’ll call it *B*, where each cell represents a specific square, and can keep track of various variables related to the square. 

The motivation behind this was to design a system I could use for **Daedalus**. I haven’t introduced what Daedalus is on my blog yet, but basically it uses a game-board with square tiles for turn based combat, and I want to be able to simulate things like light and sound in a reasonable amount of time. The game-board can have a variety of things on it that produce or obstruct light, and we need to deal with all of these in $$O(n^2)$$ time.

<center><img src="/assets/game-board-light-propagation-algorithm/fig-1.png" alt="Candle" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 1: Game board with light </span></center>

&nbsp;

The reason we are after an $$O(n^2)$$ runtime is that it’s our lower bound for possible runtime since we want each square to always calculate its illuminance, $$ E $$, and hold it. This requires that we do some amount of computation for each square, thus at least $$ O(n^2) $$ operations. 

We could theoretically have a better runtime if we just wanted each square to be able to access its illuminance if asked, in which case we theoretically wouldn’t have to do some sort of computation for every square. But since this is going to be used for a game board that may eventually be represented graphically, we want to each square to know its illuminance such that when it is rendered we know how to represent it.

$$ E = \frac{I}{r^2} $$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 1: Inverse square low calculation of illuminance </span></center>

&nbsp;

The main difficulty with a simple dynamic programming algorithm for this system is that light propagation obeys the inverse square law. Thus light dies out at a squared rate, rather than a linear one. I’ll go through my preliminary thoughts on how to design this system, and what was the issues with each one before revealing my solution. If you want to skip ahead and just read the actual solution, you can just <a href="#identifier">click here</a>.

&nbsp;

## The Naive Solution

For the naive solution consider we have a source of light at square $$B(k, l)$$ with an intensity $$I$$. The intensity, $$I$$, is the light value an unobstructed square next to the light source would have. We define $$I$$ this way because our units of measurements are squares, so the center of an adjacent square is 1 away. Thus according, to the inverse square law, unobstructed adjacent squares have illuminance equal to the intensity.

$$ E_{adjacent} = \frac{I}{1^2} = I $$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 2: Illuminance of adjacent squares </span></center>

&nbsp;

Say we want to find the light intensity for an arbitrary square $$B(i, j)$$. We could just calculate the distance between $$B(i, j)$$ and the source, $$r_{i, j}$$. Then we use $$r_{i, j}$$ to calculate the light intensity for $$B(i, j)$$ using the inverse square law.

$$ r_{i, j} = \sqrt{ \mid i - k \mid^2 + \mid j - l \mid^2 } $$

$$ E_{i, j} =  \frac{I}{r_{i, j}^2} $$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 3: Illuminance of an arbitrary square </span></center>

&nbsp;

Every square uses constant work to calculate its light intensity, thus since we have $$n^2$$ squares we have an $$ O(n^2) $$ algorithm.

&nbsp;

### Naive Issues

The issue with this is that it ignores anything that could be in between our source and $$B(i, j)$$. We don’t want a square to be illuminated by a lantern that has a wall between them. What if there is a slit in the wall between a lantern and a square? We want some amount of light to reach our square then, but not all of it.

To deal with these concerns we need a slightly more complex model. First we give any square on our board has some value for transparency, $$t$$ where $$ t \in [0,1] $$. 1 means there is nothing obstructing light, and a 0 means that it is completely opaque. Now to calculate the the value of $$B(i, j)$$, we need to find the product of the transparencies of all squares between the source, $$ T $$ and $$B(i, j)$$, then multiply the value we originally calculated by this aggregate transparency.

<center><img src="/assets/game-board-light-propagation-algorithm/fig-2.png" alt="Obstructing Light" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 2: Naive solution with obstructions </span></center>

$$ T = \prod_{i}^{obstructing\ cells} t_i $$

$$ E_{i, j} =  T \times \frac{I}{r_{i, j}^2} $$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 4: Illuminance accounting for obstructions </span></center>

&nbsp;

For every cell we need to calculate its unobstructed density, then look at every cell between it and the source to get the aggregate transparency. Since the length of our board is $$ n $$, our algorithm now takes $$ O(n^3) $$ time. 

This also raises further questions. If $$B(i, j)$$ doesn’t have a straight line of cells between it and the source, how do we decide which squares are blocking the light?

<center><img src="/assets/game-board-light-propagation-algorithm/fig-3.png" alt="Who Do We Use" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 3: Light line from source to square </span></center>

&nbsp;

We could draw a line between $$B(i, j)$$ and the source, and just say every intersecting square is a potential obstruction. If we do that, it raises the question as to which cells are greater obstructions, as the line does not pass as directly through some squares compared to others. If the line is at an angle, and it barely clips through the edge of one square, it shouldn’t have apply the same amount of obstruction as a square the line passes directly through the center of. This is a conundrum, and there are a bunch of other issues, such as if we want light to spill into squares next to them even if they aren’t directly exposed to light, and how should this phenomenon function? 

<center><img src="/assets/game-board-light-propagation-algorithm/fig-4.png" alt="Not All Intersections Are Created Equal" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 4: Light line clipping some squares </span></center>

&nbsp;

We could try to create an even more complicated model to solve these issues, but we already have a $$O(n^3)$$ time complexity, so we are going to abandon this solution. Parts of it will be useful later, but for now we’ll move on.

&nbsp;

## The Naive Dynamic Solution

The obvious direction to head in is dynamic programming. Our game board is already a $$ 2D $$ array, so now we just need to find a way to propagate light square by square. The naive approach to this is to imagine light flowing from square to square.

<center><img src="/assets/game-board-light-propagation-algorithm/fig-5.png" alt="Propagating Light Dynamically" style="width:700px;height:350px;text-align:center;"></center>

<center><img src="/assets/game-board-light-propagation-algorithm/fig-5-2.png" alt="Weird Dynamics" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 5: Naive dynamic programming algorithm passing light </span></center>

&nbsp;

So the light in an arbitrary square $$ B(i, j) $$ is dependant on the squares adjacent to it. The adjacent squares pass some amount of light to $$ B(i, j) $$ equal to their own $$ I $$ discounted by some value $$ \delta $$ to account for the light dying out the further away from the source we get.

$$ E_{i, j} = \delta t_{i, j - 1} E_{i, j - 1} + \delta t_{i - 1, j} E_{i - 1, j} + \delta t_{i - 1, j - 1} E_{i - 1, j - 1} $$

$$ E_{i, j} = \delta( t_{i, j - 1} E_{i, j - 1} + t_{i - 1, j} E_{i - 1, j} + t_{i - 1, j - 1} E_{i - 1, j - 1} ) $$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 5: Naive dynamic programming recurrance </span></center>

&nbsp;

This solution has some of the features we want, such as placing an obstacle between the source and square $$ B(i, j) $$ will cause the square to get darker along with all other squares behind the object, as these squares no longer are passed the light from the obstruction.

<center><img src="/assets/game-board-light-propagation-algorithm/fig-6.png" alt="Not Super Intuitive" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 6: Naive dynamic programming algorithm with obstructions </span></center>

&nbsp;

This also better reflects that light doesn’t just flow in a straight line through squares between $$ B(i, j) $$ and the source, but passes through more than one square adjacent to $$ B(i, j) $$ before hitting it. This is why we calculate $$ B(i, j) $$ by looking at all adjacent squares which are intersected by any line segment we can draw that begins somewhere in $$ B(i, j) $$ and ends in $$ B(k, l) $$.

Additionally this is very easy to understand, calculate and implement. We just fill the table starting from the source, doing constant time at each square, giving us a runtime of $$ O(n^2) $$.

&nbsp;

### Naive Dynamic Issues

There are two main issues with this implementation. The first is that it ignores the inverse square law. Instead of the light dying out at a rate dependant on how far it is from the source, it always loses the same percentage. Thus if we calculated the light in a square $$ x $$ to the right of our source it would simply have the brightness of:

$$ B(k, l + x) = I * \delta^x $$

As opposed to:

$$  B(k, l + x) = \frac{I}{x^2} $$

When using the inverse square law, the percentage of the light lost from square to square is directly dependant on the distance from the source. We can see this by comparing three adjacent squares for some arbitrary $$ I $$.

$$ I = 100 $$

$$ E_{k, l + 1} = \frac{100}{1^2} = 100 $$

$$ E_{k, l + 2} = \frac{100}{2^2} = 25 $$

$$ E_{k, l + 3} = \frac{100}{3^2} = 11 $$

$$ E_{k, l + 4} = \frac{100}{4^2} = 6 $$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 6: Illuminance decay over four squares </span></center>

&nbsp;

As we can see, there is a 75% drop in intensity from the first square to the second, and then a 56% drop in intensity from the second to third. Thus the further we get away from the light source, the slower the change in light (you can also trivially show this fact by taking the derivative of the inverse square law ($$ \frac{dB}{dr} = - \frac{I}{r^3} $$ haha formating!)).

<center><img src="/assets/game-board-light-propagation-algorithm/fig-7.png" alt="Not How Light Works" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 7: Board showing light dying out </span></center>

<center><img src="/assets/game-board-light-propagation-algorithm/plot.png" alt="Light Decay Curves" style="width:700px;height:525px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 8: Rate at which light dies out </span></center>

&nbsp;

So with this dynamic implementation we would see light values staying far too high in the vicinity around the source, and then dying our far too quickly as we moved away from the source. This has negative effects as we eventually want to implement a lighting system for a game, so we want light sources to effectively illuminate entire areas realistically. An unobstructed lantern in a dim room should make the entire room much easier to see in, not just create a super bright spot around the lantern that completely dies out a few squares away.

The second major issue is that this algorithm causes light to flow too much. In other words, it wraps around corners and doesn’t act like light emanating from a source. Instead we could get situations like this:

<center><img src="/assets/game-board-light-propagation-algorithm/fig-6-2.png" alt="Not Good At All" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 9: Light flowing like water </span></center>

&nbsp;

There is no reason we should have any light from the source at square $$ W $$, but this solution ignores the actual location of the source once we start filling it in causing us to end up with situations like the one above.

What we really want is for our squares to reflect that light must pass through squares adjacent to it if it hits a specific square, while not having to keep track of everything in between. We achieve this by combining these two naive solutions.

<a id="identifier">&nbsp;

## Real Solution 

For the real solution we make use of both of our previous solutions. We calculate the illuminance for the square $$ B(i, j) $$ with no obstructions using the inverse square law. Then to determine what fraction of that light actually reaches that square, we look at the adjacent squares in between it and the source. If $$ B(i, j) $$ is down and to the right of the source, this means we are looking at the squares one to the left, $$ B(i, j - 1) $$, and one up, $$ B(i - 1, j) $$, from $$ B(i, j) $$.

Now we recognize that all light which hits  $$ B(i, j) $$ after passing through  $$ B(i, j - 1) $$ comes through $$ B(i, j) $$’s left border. This means depending on our orientation to the source, more of the light passing through $$ B(i, j - 1) $$ will pass through $$ B(i, j) $$. We can think of this as the horizontal component of $$ B(i, j) $$’s total light, since it propagates in horizontally. If $$ B(i, j) $$ was directly right of the source, then all light that hits $$ B(i, j) $$ passes directly through $$ B(i, j - 1) $$ and thus all of our light is from the horizontal component. If $$ B(i, j) $$ is at angle $$ \frac{7 \pi}{4} $$ from the source, the horizontal component accounts for half of the total light. And if $$ B(i, j) $$ is directly below the source, then the horizontal component contributes nothing to our total light at $$ B(i, j) $$.

<center><img src="/assets/game-board-light-propagation-algorithm/fig-10.png" alt="Vertical and Horizontal Components" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 10: Horizontal and vertical components </span></center>

&nbsp;

This intuitively tells us that we should use $$ sin(\theta) $$ and $$ cos(\theta) $$, where $$ \theta $$ is the angle of line segment connecting the source and $$ B(i, j) $$. Specifically we’ll calculate the fraction of our total light contributed by the horizontal component with $$ cos^2 (\theta) $$ and the vertical component with $$ sin^2 (\theta) $$. We used the squared values as they always add to one, so they always present the two fractions of our total illuminance.

So now we know how much of our maximum total light passes through $$ B(i, j - 1) $$ and $$ B(i - 1, j) $$, but how do we handle light being blocked by obstacles? We can only look at the two adjacent squares, so we don’t know where obstacles might be. What we do know is that all the light contributed through the horizontal component is from $$ B(i, j - 1) $$, thus if $$ B(i, j - 1) $$ is missing illuminance then that is light that can’t be passed on to $$ B(i, j) $$ via the horizontal component. So we only use the fraction of the horizontal component equal to the ratio of $$ B(i, j - 1) $$ actual illuminance over its maximum possible illuminance when there are no obstructions. 

By lastly multiplying our horizontal component by the permittivity of $$ B(i, j - 1) $$, we have our final recurrence relation.

$$ B(i, j)_{max\ E} = \frac{I^2}{r_{i, j}} $$

$$ B(i, j)_{hor} = t_{i, j-1} \times cos^2 (\theta) \times B(i, j)_{max\ E} \times \frac{E_{i, j - 1}}{B(i, j - 1)_{max\ E}} $$

$$ B(i, j)_{ver} = t_{i - 1, j} \times sin^2 (\theta) \times B(i, j)_{max\ E} \times \frac{E_{i - 1, j}}{B(i - 1, j)_{max\ light}} $$

$$ E_{i, j} = B(i, j)_{hor} + B(i, j)_{ver} $$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 7: Solution dynamic programming recurrance </span></center>

&nbsp;

Note that if the square lies in a different quadrant of the graph centered at the light source, the two adjacent squares we access change. This is because depending on our orientation, the light passes through different cells before hitting $$ B(i, j) $$. If $$ B(i, j) $$ is up to the left for example, we access cells $$ B(i + 1, j) $$ and $$ B(i, j + 1) $$. This means when filling out our table, we spiral out from wherever our source is. With this we have a rough model to calculate the light due to a single source for our entire board.

<center><img src="/assets/game-board-light-propagation-algorithm/fig-11.png" alt="Order of Propagation" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 11: Order of propagation, compute each straight line, then each ring around the source emanating outwards </span></center>

&nbsp;

### Results

This implementation doesn’t perfectly calculate the amount of light that hits an arbitrary square, but it’s a good approximation, and has many of the features we were seeking for our light propagation system.

If we have a completely unobstructed board, then every square have the light of the sum of $$ cos^2(\theta) $$ and $$ sin^2(\theta) $$ multiplied by the light for the square calculated by the inverse square law, which is just the inverse square law. Thus light will die out at a realistic rate, and have all the nice possible gameplay implications.

<center><img src="/assets/game-board-light-propagation-algorithm/fig-1.png" alt="Reusing Assets Is a Solid Strategy" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 12: atmospheric </span></center>

&nbsp;

Although we still get the weird effect of light propagating to squares that have a partially unobstructed path between them and the source, and then it flowing into adjacent squares. This phenomenon is much less pronounced than with our naive dynamic solution. Horizontally propagating light is dependant on $$ cos^2(\theta) $$, so for scenarios where we consider a square next to an illuminated square, but completely obstructed, necessarily its $$ cos^2(\theta) $$ is very small if the illuminated square is directly above the source, and its horizontal component passes zero light, thus it ends up having very little light. If the $$cos^2(\theta)$$ or $$sin^2(\theta)$$ of some square is not low, this implies that a large amount of light will pass through its horizontal or vertical border respectively, and so if they are not obstructed on a border next to a highly illuminated square then it should receive the light.

<center><img src="/assets/game-board-light-propagation-algorithm/fig-12.png" alt="Looks A Little Better" style="width:700px;height:350px;text-align:center;"></center>

<center><img src="/assets/game-board-light-propagation-algorithm/fig-12-2.png" alt="Much Better" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 13: Light flowing less like water </span></center>

&nbsp;

Lastly calculating the light for all squares of the board takes $$ O(n^2) $$ time. It takes constant time to access all the needed values of the two adjacent squares, and again constant time to calculate the illuminance of $$ B(i, j) $$. We have $$ n^2 $$ squares, so it naturally becomes $$ O(n^2) $$.

&nbsp;

## Afterword

This gives a description of a $$ 2D $$ light propagation algorithm on a board of squares in $$ O(n^2) $$ time. In a future post I’ll post a java implementation of this algorithm along with a demo. Additionally I’ll write a post about the problem where we have an arbitrary number of light sources, and we want to achieve an effective implementation in $$ O(n^2) $$ time. When I write those two, I’ll be sure to include their links here.

Also if you see any errors, have criticism, or a better algorithm feel free to send me an email, or contact me through any other means. You can find my contact info on my [contact page][contact].

&nbsp;

&nbsp;

&nbsp;

&nbsp;

[link to bot]: /contact/
[contact]: /contact/

