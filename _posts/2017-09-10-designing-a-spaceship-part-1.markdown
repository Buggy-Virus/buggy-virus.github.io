---
layout: post
title:  "Designing a Spaceship, Part 1"
date:   2017-09-10 20:52:00 -0000
categories: physics, scifi, space, spaceship,
tags: physics, scifi, space, spaceship,
---
I think about spaceship design a reasonable amount due to my healthy (unhealthy) interest in science fiction and space simulations. I’m going to talk about some of my thoughts on what a theoretical maneuverable spacecraft would look like while adhering to the laws of physics (well some of them at least). Through these topics we’ll build up the what a spacecraft that engages in dogfights in outer space should look like, instead of a strange fighter jet.

I’m going to split this discussion into two posts, the first oh how an agile zero-gravity fighter should be designed. And the second post will be on designing a cockpit for a human pilot in a spaceship which needs to shoot stuff (like other spaceships!).

&nbsp;

## The Space Ship

When designing our spaceship there are a two main features we want.

1.	Can move in all directions
2.	Can face in any direction

I’ll walk through both of these, and a couple other important details so we can eventually blast our arch enemy, the alien overlord Liam, into fundamental particles.

&nbsp;

### Position

Let’s figure out how our ship will move around first. So we want to be able to translate the position of our spaceship in any direction. There is no air resistance in outer space, thus the only thing that will change our velocity is our own thrusters. If we want our velocity to go from $$ 10 \^{x} $$ to $$ 10 \^{y} $$ we need to fire our thrusters along the $$ x $$ axis to counteract our current velocity, and along the $$ y $$ axis to get our desired velocity.

To achieve this, the most obvious design is to just have a circle (this will be terrific for other reasons which we’ll get to later), with **translational thrusters** every $$ \frac{1}{2} \pi $$ (90 degrees).

<center><img src="/assets/designing-a-spaceship-part-1/spaceship-pic-1.png" alt="A Simple Translational Thruster Setup" style="width:700px;height:350px;text-align:center;"></center>

<center><img src="/assets/designing-a-spaceship-part-1/spaceship-pic-2.png" alt="Firing Thrusters to Attain a Velocity" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;">I’m going to keep the spaceship in two-dimensional space throughout this post where the ship is just a circle. For three-dimensional space, the ship simply becomes a sphere instead. It shouldn’t be too hard mapping the various details I delineate from the 2D example to 3D.</span></center>

&nbsp;

We can create acceleration in any direction by fire two of the thrusters and controlling the thrust of each thruster. Thus our four translational thruster is the simplest possible setup able to accelerate in all directions.  

We could also imagine a theoretical case where our spaceship has an infinite number of thrusters orthogonal to the surface of our circle and all around the ship. Instead of each thruster having its own individual thrust, the surface of the ship has a thrust density of $$ \rho_t $$. Meaning that per for some length of the ship’s surface, we know how much thrust it can potentially output.

<center><img src="/assets/designing-a-spaceship-part-1/spaceship-pic-3.png" alt="Theoretical Translational Thruster Setup" style="width:700px;height:350px;text-align:center;"></center>

We are going to go with a cross between these two setups for our ship, with more than four translational thrusters, and surprisingly less than infinite. Some mix between these two setups is what we would expect any ship we come across in the cold vacuum of outer space to be sporting.

<center><img src="/assets/designing-a-spaceship-part-1/spaceship-pic-4.png" alt="A More Realistic Translational Thruster Setup" style="width:700px;height:350px;text-align:center;"></center>

Now we start worrying about getting our ship facing in the correct direction.

&nbsp;

### Rotation

We have a spaceship that can move through space, which would be an historic leap forward if we were a peaceful spacefaring species. Unfortunately, we are not, and we want to blast things, so we need weapons.

<center><img src="/assets/designing-a-spaceship-part-1/spaceship-pic-5.png" alt="Weapons Galore" style="width:700px;height:350px;text-align:center;"></center>

But to aim our weapons we need to be able to rotate our ship to point them in any direct. We can achieve this in the barest form by adding one **rotational thruster** that is tangent to the surface of our ship. 

<center><img src="/assets/designing-a-spaceship-part-1/spaceship-pic-6.png" alt="The Simplest Rotational Thruster Setup" style="width:700px;height:350px;text-align:center;"></center>

Of course if we only have one thruster, we can only rotate the ship in one direction, so let’s add a second. Alternatively we could imagine a case where could imagine having an infinite number of thrusters, but this time parallel to the ship, and with a thrust density of $$ \rho_r $$.

<center><img src="/assets/designing-a-spaceship-part-1/spaceship-pic-7.png" alt="A Theoretical Rotational Thruster Setup" style="width:700px;height:350px;text-align:center;"></center>

Similar to the translational thruster setup, we are going to use a cross between these two setups for our rotational thrusters. Although for rotation we really don’t care about the number of thrusters. We only really care about the total tangential thrust, whether it is from many thrusters or one large thruster. Either system could provide equal amounts of rotational thrust (though multiple thrusters will help us with some details later on).

<center><img src="/assets/designing-a-spaceship-part-1/spaceship-pic-8.png" alt="A Sensible Rotational Thruster Setup" style="width:700px;height:350px;text-align:center;"></center>

We could also install thrusters with an angle that is between parallel and orthogonal to the surface of the ship. These thrusters would provide both a rotational component and translational component (angular velocity and velocity). Such a setup of thrusters could possibly be useful if we were constrained in number of thrusters we can fire at any one time, or total number of installed thrusters, but otherwise it really complicates things. Being simple space pirates (we’re space pirates by the way) we like to keep things simple, so we are going to keep our thrusters either purely translational or rotational.

A cool thing we can do now that we have rotational thrusters, is differentiate between main and auxiliary translational thrusters.

<center><img src="/assets/designing-a-spaceship-part-1/spaceship-pic-9.png" alt="Look at This Sweet Thruster" style="width:700px;height:350px;text-align:center;"></center>

Now if we have a total thruster power constraint, or want to cut down on mass without sacrificing translational thrust, we can beef up some of our translational thrusters. Whenever we specify a new velocity from our relative position, the translational thrusters will initially begin firing to propel us in that direction, while our rotational thrusters fire as well to begin orienting our monster thruster in the correct direction to maximize acceleration.

<center><img src="/assets/designing-a-spaceship-part-1/spaceship-pic-10.png" alt="Rotational Thruster Dynamic To Maximize Translational Velocity" style="width:700px;height:350px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;">In the second time stage, the rotational thrusters should not be firing for us to have 0 acceleration. I drew them firing to illustrate the point that ot counteract the angular velocity we gained in the first time stage, we would fire rotational thrusters in the opposite direction.</span></center>

&nbsp;

Our on-board computer handles this thruster dynamic and constantly maximizes our desired acceleration at any point in time for however the ship is oriented. Or maybe the ability to manage this is what differentiates an ace starship pilot from your run of the mill gleep farmer.

The on-board computer could handle even more planning tasks, such as orienting certain features towards targets while attempting to maximize acceleration at the same time. As we gain more features and weapons on our surface that need to be pointed at multiple targets and a more complex thruster system this planning becomes more complex.

<center><img src="/assets/designing-a-spaceship-part-1/spaceship-pic-11.png" alt="Putting Strain on The On-Board Computer" style="width:700px;height:350px;text-align:center;"></center>

But our ability to rotate the ship effectively is highly influenced by how well we maintain our center of mass, as well as our rotational inertia.

&nbsp;

### Center of Mass

$$
x_{cm,\ discrete} = \frac{\sum_{i} m_i x_i}{M}
$$

$$
y_{cm,\ discrete} = \frac{\sum_{i} m_i y_i}{M}
$$

$$
x_{cm,\ continuous} = \frac{\int_{0}^{M} = x dm}{M}
$$

$$
y_{cm,\ continuous} = \frac{\int_{0}^{M} = y dm}{M}
$$

<center><span style="font-size:14px;color:#828282;text-align:center;">Center of mass is the sum of masses weighted by their position over the sum of all mass. This is calculated for both the x and y axes. For 3D space, it is also calculated along the z axis.</span></center>

&nbsp;

For our rotational thruster to function properly, we need to make sure we know our center of mass and axis of rotation. If we don’t know the center of mass when firing rotational thrusters instead of re-orienting the ship about the center of the circular body it could send us into a weird tailspin with some translational velocity. 

<center><img src="/assets/designing-a-spaceship-part-1/spaceship-pic-12.png" alt="Effect of Center of Mass" style="width:700px;height:350px;text-align:center;"></center>

Our spaceship in reality isn’t a circle with constant density. The inside of our ship is full of complicated space technology, and the outside of it is peppered with thrusters and weapons. This means that the center of mass will not naturally be at the center of our circle. Now I have to come clean, our rotational thrusters don’t need to be parallel to the surface of our circular ship, they need to be orthogonal to any line that passes through the center of mass.

<center><img src="/assets/designing-a-spaceship-part-1/spaceship-pic-13.png" alt="Angles of Rotational Thrusters" style="width:700px;height:350px;text-align:center;"></center>

Making sure your translational thrusters are actually translational thruster is much less complex and more intuitive if our center of mass is at the center of the ship’s circular body (what we’ve assumed in the previous sections). We can accomplish this by making sure all the mass is balanced symmetrically across our ship. If we stick a giant translational thruster on one side, we need another one or a death laser of the same mass on the other side.

<center><img src="/assets/designing-a-spaceship-part-1/spaceship-pic-14.png" alt="That's a Nice Death Laser" style="width:700px;height:350px;text-align:center;"></center>

Maintaining this balance is why it is easier to design a ship with more than one rotational thruster, since we can distribute the weight of them evenly around the ship to keep everything balanced out (also the extra thrusters will come in handy when some inevitably get blown off).

But there are still some issues with our center of mass we haven’t addressed. Some of the components of our spaceship change in mass, such the fuel tank as we expel fuel, or our missile racks as we destroy our enemies. We can’t synthesize new matter in order to supplement this loss of mass, so instead we need to reposition mass we have to maintain our center of mass.

We could deal with these dynamic mass components by putting each one on a track which allows them to move towards and away from the center of our circle.

<center><img src="/assets/designing-a-spaceship-part-1/spaceship-pic-15.png" alt="Look at That Fuel Tank Slide" style="width:700px;height:350px;text-align:center;"></center>

But this track system isn’t very elegant, and could be a headache when dealing with rotational inertia (which we’ll get to later in this post).

Instead, we could implement a layer of the spaceship, which holds masses which can move towards and away from the center of the circle.

<center><img src="/assets/designing-a-spaceship-part-1/spaceship-pic-16.png" alt="Masses on a Track" style="width:700px;height:350px;text-align:center;"></center>

You know I love imagining these systems as infinitely distributed around the ship with some density, so let’s do the same with this mass layer. Imagine that instead of a bunch of masses on tracks, it is a massive circular (spherical) mesh with density $$ \rho_m $$. Our computer can send electric signals to it that causes it to change shape, contracting and ballooning in different areas.

<center><img src="/assets/designing-a-spaceship-part-1/spaceship-pic-17.png" alt="Smart Mass Mesh" style="width:700px;height:350px;text-align:center;"></center>

Unlike the previous sections where I talk about the cool theoretical infinitely distributed case, then throw it out the window, I think this would actually be a viable and by far best implementation of this feature.

Not only does this adjustable mesh solve the issue of our spaceship components with dynamics masses, but it also will be a life saver if any of our lasers or thrusters get blown off. Now the mesh can adjust to maintain our center of mass position under a whole range of scenarios, and allow us to continue to effectively make use of our rotational thrusters.

<center><img src="/assets/designing-a-spaceship-part-1/spaceship-pic-18.png" alt="Battle Damage Doesn't Have Me Down" style="width:700px;height:350px;text-align:center;"></center>

But even with our center of mass issues solves, there is still a big issue with the efficiency of our rotational thrusters.

&nbsp;

### Rotational Inertia

This is probably going to be somewhat out of the blue and unintuitive for those without a physics background.

Rotational inertia is given by the following formula. It is the spaceship’s resistance to change in angular velocity.

$$
I_{discrete} = \sum_{i} m_i r_i^2
$$

$$
I_{continuous} = \int_{0}^{M} r^2 dm
$$

<center><span style="font-size:14px;color:#828282;text-align:center;">Rotational inertia is the sum of all mass in your system weighted by the square of the mass's distance from the axis of rotation.</span></center>

&nbsp;

Rotational inertia is like inertia, but instead of resisting change in translational motion, it causes resistance to change in the angular velocity (speed of rotation).

It is more difficult to change the angular velocity with rotational thrusters if a ship has high rotational inertia. If we have no constraints on how much or how powerfully we fire our rotational thrusters we would simply want as low a rotational inertia as possible, allowing us to re-orient our ship as quickly as possible.

If that isn’t the case, a variable rotational inertia has many benefits, as increasing the rotational inertia would allow us to slow our rotation suddenly, like a figure skater putting out their arms to slow a spin.

The bigger issue is when we move to 3D space. Since our ship is a sphere instead of a circle, there is more freedom in terms of which direction we rotate. Instead of having one possible axis of rotation, as in the 2D example, we have infinite! Thus we no longer have one rotational inertia. Our rotational inertia now varies depending on which axis of rotation our angular acceleration (rotation basically) is on.

This isn’t a problem per se, but now when the on-board computer calculates firing the thrusters, maximizing acceleration, and targeting, it needs to know the rotational inertias for all possible axes of rotation. Since there are an infinite number of axes of rotation, this would require calculating the rotational inertia for any rotation the computer considers. This is both confusing and could cause computational strain which slows down or overloads our on-board computer (and in the world of hyper intense space dog fights with lasers, a single second could cost you your life!).

If computing power becomes an issue, it will be necessary to homogenize the rotational inertia. Doing this would require precise planning of the placement and mass of components in order to make each layer of the ship, with a distance $$ r $$ from the center, have a constant density. Alternatively, we can make use of our smart mass mesh we added earlier to both attain rotational inertia homogeneity and allow us to have a dynamic rotational inertia for maneuverability. 

&nbsp;

### Ship Shape

<center><img src="/assets/designing-a-spaceship-part-1/spaceship-pic-19.png" alt="Space Pirate" style="width:700px;height:350px;text-align:center;"></center>

Now we have our little ball of death and we are ready to set it loose with a drone inside to exterminate Liam and his poorly constructed ship. But that strategy lacks a personal touch, don’t you think. So in the next post let’s work on installing a cockpit so we can stare into Liam’s eyes through the cold expanse of space while we cut his ship to shreds with our industrial lasers.

&nbsp;

&nbsp;

