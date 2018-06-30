Title: Shut up and use definitions
date: 2017-04-16 10:20
comments: true
slug: shut-up-use-definitions
tags: physics,irc,concepts,definitions,angular,momentum

# Shut up! And use the definitions

So today I had a discussion with some folks at this physics chat room about the 
concept of angular momentum and the ability to use it to describe a
particle's motion (particle understood as a point mass in the classical sense).

My discomfort started building up when one of them claimed, and I quote, that

> "\<userX\> Point has no angular momentum or ways to transfer it"

> "\<userX\> Without fields , a particle has no angular momentum. In it rotation or orbiting (because it cant orbit)"

which are just wrong statements.

I can understand the confusion, when you commonly talk about "angular momentum" or "angular velocity" or "angular \<put_whatever_here\>", you commonly think about something rotating around, either around its own axis or around some external axis.

Evidently, a point rotating around its "own axis" has no real sense and I don't think there's much more to be explained there.[^footnote] On the other hand, a particle moving with some linear momentum $p$ does have some angular momentum $L$, you just have to use the **definition** for angular momentum,

[^footnote]: Just in case it helps, a point has no dimensions - or zero dimensions - and an axis is a one dimensional thing.

$$
\mathbf{L} = \mathbf{p} \times \mathbf{r}
$$

So, as long as the quantity $\mathbf{r} \times  \mathbf{p}$ is different from zero then there is angular momentum. It's easy to see how a particle with linear momentum $p \neq 0$ does have an angular momentum, even if it's going in a straight line at a constant speed (doesn't need to be rotating around anything).

In my opinion that would've been the end of the discussion, it should be clear now how the original claims were wrong, and one can think that since this occurred in a physics chat room, people would take the "high way", accept the mistakes, learn from them and move on... hell, far from the true. You know how people just love to argue on Internet and hide behind a computer screen and the illusion of anonymity it provides to act as jerks. I may add that trying to justify wrong (or [not even wrong](https://www.scientificamerican.com/article/wronger-than-wrong/)) claims and trying to piss off the administrators (and I'm one of those) may be the favourite sport of this chat room.

What came afterwards was a lot of ad-hoc arguments, just the user desperately trying to justify his mistakes, and yet another user trying to justify that user's mistakes with the only intention to "prove me wrong" and not for contributing to the conversation. This latter user incorrectly tried to disprove me by saying that in polar coordinates (coordinate system that uses $r$ and $\varphi$ as coordinates, check figure below) the angular momentum is not well-defined for a particle at the origin $(0,0)$, because according to him "$\varphi$ is not defined at the origin".

![](https://upload.wikimedia.org/wikipedia/commons/d/d3/Examples_of_Polar_Coordinates.svg)

This claim was what made me wrote this post and you will see why. His claim about the lack of definition of $\varphi$ at the origin is not wrong, but angular momentum for a particle at the origin is still well-defined in polar coordinates, and in that case $\mathbf{L}=0$. Angular momentum for a particle of mass $m$ and linear momentum $p = mv$ in circular motion, can be written using polar coordinates as

$$
L(r,\varphi) = mr^2 \frac{d \varphi}{dt}
$$

You could claim that the $r$-dependence in the previous expression shows how $L=0$ if $r=0$, but there are still some mathematical subtleties to deal with, such as proving $d\varphi /dt$ is finite, problem is that we already know $\varphi$ is not well defined at the origin. This is the key point of this post, why using expression (2) when you can just use the definition (1) and since $r=0$ then $\mathbf{L}=\mathbf{r} \times \mathbf{p} = 0$. This is one of the main differences about doing physics or doing math. Definitions in physics tend to be as general as possible and tend to be independent of the reference frame or the chosen coordinate system, they exist for a reason... so use them! A mathematician would deal with all the subtleties in expression (2) and try to prove that $L=0$ in that very specific case, but a physicist would just embrace the simplicity of the definition on expression (1) without even having to think on the mathematical subtleties when clearly is not needed.

So, I hope this shows how you can look like a fool if you don't let your ego apart, embrace mistakes and just **use definitions** for physics purposes.
