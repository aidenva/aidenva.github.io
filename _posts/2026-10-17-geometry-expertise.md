---
layout: post
title: "Sandbag or Sad Dog"
author: "Linh Le"
categories: journal
tags: [documentation,random]

---
A question the machines force on us

I think that, given how shockingly proficient generative models have been at replacing a lot of us, there has been an echoing sentiment about what we should do. <em>Are we harnesses for AI, rather?</em> Some of the more bullish takes revolve around the inability of AI to develop domain expertise--or rather, they call attention to the void that AI leaves behind for humans to fill.

The argument usually goes something like this. A generalist, someone who is good at a lot of things, has competence spread out over many fields; if you draw it as a curve over everything one could know, it is low and wide, while a specialist's curve is narrow and tall (and nobody promises that the two enclose the same area--some people simply know more, and that's fine). If a model already holds grade-X knowledge in most fields, then a person spread to roughly grade X across those same fields is doing something a machine does faster and for pennies. Models don't hold grade X + 5 in all of those things (yet), though, so perhaps the reasonable move is to go and build domain expertise somewhere.

That sounds right to me, mostly. But it leans on two words, domain and expertise, that are surprisingly slippery when we try to define more rigorously. Here, I am trying to borrow the language of geometry to make more sense of it (perhaps I have math envy).

## Boxes inside boxes

People used to consider "science" a domain, which nowadays sounds absurdly broad; a chemist does not understand the same things a physicist does. Then again, chemistry itself is too broad, since organic and inorganic chemists are very different people with very different lives, and they hold quite different pictures of how the world fits together. A domain can be a field, a discipline, a department, a topic you happen to be obsessed with--but it can also be an arbitrarily drawn box that you've decided to call a domain, and the boxes keep getting smaller.

There is a little structure hiding in that, which is that domains nest:

$$\text{quantum hopping} \;\subset\; \text{inorganic chemistry} \;\subset\; \text{chemistry} \;\subset\; \text{science}$$

Collect every candidate domain and order them by inclusion, and you get a partially ordered set. Choosing a "level" of specialization amounts to choosing a partition of knowledge into boxes, and partitions are themselves ordered by refinement--one refines another if each of its boxes sits inside a box of the other--which makes the collection of partitions a lattice. The history of academic departments looks, from here, like a slow walk down that lattice toward finer and finer partitions.

The order is tidy, but it doesn't seem able to tell us when to stop. Is quantum hopping events a domain, or a niche? At some point a domain becomes so constricted that it stops sounding like a field and starts sounding like a hobby, yet a poset has no notion of size: every link in the chain above looks the same to it, and in a continuum of knowledge you could keep refining all the way down to single points. Whether there is any principled place where refining a domain turns it into a niche, or whether the line is pure convention, seems to need something order alone can't provide--some idea of nearness and size, which means putting knowledge in a space.

## A landscape of competence

What kind of space, though? Knowledge is many-dimensional, and the things we want to say about it--how quickly competence falls off as you move away from what you know, how it spreads, what the shortest route from one topic to another looks like, how fast a neighbourhood grows--are, rather conveniently, exactly the things a Riemannian manifold is built to talk about. So let (𝓜, g) be a smooth, connected manifold of dimension n with a metric g. A point is a piece of knowledge at the finest resolution we care about; the length of a curve is the effort it takes to carry mastery along it; and from g we inherit, for free, a geodesic distance d_g, a volume μ_g, a gradient, a Laplacian Δ_g, and curvature. (One thing I like about this is that g doesn't have to be the same for everyone: two people can face the same things to know and still find different things close together.)

A person, in this picture, is a competence function on that space,

$$K : \mathcal{M} \to [0, 1)$$

where zero means no competence and one stands for complete, infinite knowledge of a point--a limit nobody actually reaches, hence the open interval.

Expertise needs a bar, and the bar is admittedly somewhat arbitrary. Pick a threshold τ, call anything at or above it "good," and your expertise is the set of places where you clear it:

$$E(\tau) = \{\, x \in \mathcal{M} : K(x) \ge \tau \,\}$$

These sets nest, which is a small thing but turns out to matter. Raise the bar and the set can only shrink,

$$\tau \le \tau' \;\Longrightarrow\; E(\tau') \subseteq E(\tau)$$

so a person's expertise isn't really one set at all, but a decreasing family of sets indexed by how strict you are being--a filtration, if you want the word. That gives generalists and specialists a description that is purely about shape: the generalist's sets are large at low bars and vanish early, while the specialist's are small but survive to much higher bars.

Comparing people gets a little uncomfortable here. The natural way to say A knows more than B is that B's expertise set sits inside A's at every bar, which is the same as K_B ≤ K_A everywhere--but that is only a partial order, and most pairs of people are simply incomparable, since each clears some bar somewhere the other doesn't. "Who knows more?" doesn't have an answer until you add more structure.

The domain question can now be restated, too. Being an expert in a domain D just means D ⊆ E(τ), so asking which boxes deserve to be called domains becomes asking which sets can actually sit inside the expertise set of a real person. If any set at all can--if E(τ) is allowed to be a single point--then the distinction between domain and niche really is convention.

One caution, because we tend to picture all of this on flat 2D maps. A map is a projection, and projections never increase distances: two pieces of knowledge that look far apart on a map really are far apart, but two that look close may only be close in that particular slice, and far apart in the dimensions the map threw away. Maps flatter us; they make knowledge look more connected than it is.

## Can expertise be a spike?

Take someone who knows quantum hopping deeply. It is hard to picture them without some mechanics, some linear algebra, some chemistry sitting underneath, and so the natural question is whether a spike of competence with nothing around it can exist at all, or whether depth somehow drags its surroundings up with it.

I have this weird interest in fluid dynamics, borne out of doing well in a fluids class I did not expect to do well in. Fluids are interesting because they are everywhere yet elusive to capture; they require a natural elegance that is mathematically bulky. One such property has to do with physical continuity. A sharp discontinuity in a fluid isn't strictly forbidden, but it isn't natural either--it drives the system out of equilibrium, and diffusion and viscosity smooth it out until it's gone. It seems plausible that competence does something similar: a high peak without lower peaks around it collapses and smears into its neighbours, and we lose exactly the property we wanted to describe.

Written as a fluid person would write it, with u(x, t) the effort you put in, λ a forgetting rate and D a coefficient for how much neighbouring knowledge props each point up:

$$\frac{\partial K}{\partial t} = D\,\Delta_g K \;-\; \lambda K \;+\; (1 - K)\,u$$

The Laplacian is doing the interesting work here, because on any Riemannian manifold it measures how a point compares with its surroundings,

$$\Delta_g K(x) = \lim_{r \to 0} \frac{2n}{r^2} \left( \frac{1}{|\partial B_g(x,r)|}\int_{\partial B_g(x,r)} K \;-\; K(x) \right)$$

so the D term pulls every point toward the average of its neighbourhood, eroding peaks and filling gaps. (It should be read as support rather than conservation; studying chemistry does not drain your physics.) The factor (1 − K) is there so that competence can approach one but never reach it.

The first thing one might try, before any of this, is simply to demand that K be smooth. That doesn't work, and the reason why ends up being the most useful idea in the post. Near a point x₀, consider the dilations

$$\delta_s(x) = x_0 + s\,(x - x_0), \qquad s > 0$$

They form a group, acting on competence functions by squeezing or stretching them about x₀, and smoothness is invariant under that action: if one smooth peak of height h exists, so does every squeezed copy of it, at the same height and as thin as you like. There are even smooth bump functions that are exactly zero outside a tiny ball--islands with literally nothing around them. Continuity, smoothness of any order, even analyticity are all qualitative conditions with no length scale in them, and no condition invariant under dilations can ever impose a minimum width on expertise. Ruling out spikes requires something that breaks the symmetry.

The fluid equation does: D and λ together define a length,

$$\ell = \sqrt{D/\lambda}$$

and rescaling space changes the equation unless ℓ rescales with it. Several things fall out of that one length. Left alone, a peak of width σ spreads on a time scale of order σ²/D, so the narrower it is the faster it erodes; narrowness becomes a maintenance cost. Under sustained, tightly focused effort, competence settles into a profile whose shoulders fall off like e^(−r/ℓ), so focus finer than ℓ doesn't produce narrower expertise at all, only the same shoulders. And in such a profile the slopes are bounded, roughly by h/ℓ, which gives a static shadow of the dynamics:

$$|K(x) - K(y)| \;\le\; L \, d_g(x, y)$$

I don't want to insist that knowledge obeys this particular equation or this particular inequality; the specific forms hardly matter. What matters is the structural property underneath both, that the constraint respects isometries--rearrangements of knowledge that keep neighbours as neighbours--and breaks dilations. Everything after this uses only that.

## What a scale buys

Suppose you clear the bar at some point x₀ with room to spare, K(x₀) = h > τ. Competence can only fall off at a bounded rate, so it can't drop below τ immediately; it has to stay above the bar on a whole geodesic ball around x₀, and the radius of that ball grows with h − τ:

$$h > \tau \;\Longrightarrow\; B_g\big(x_0,\, r(h - \tau)\big) \subseteq E(\tau), \qquad r \text{ increasing}$$

Someone who barely clears the bar can be an expert at a single point, but someone far above it can't. Running the same argument with a lower bar gives a larger ball on which K is still comfortably above zero, so a deep peak forces two nested regions--an expertise region where you clear the bar, and a support region underneath where you don't, but aren't at zero either. The supporting lower peaks from the fluid picture show up here as a consequence, rather than something that had to be assumed.

How expensive that support region is depends on curvature, which I find one of the more suggestive parts of the picture. Curvature controls how fast geodesic spheres grow as you move away from a point, and comparison theorems (Günther–Bishop on one side, Bishop–Gromov on the other) turn that into bounds on the volume of the balls above. In negatively curved regions spheres grow exponentially, and negatively curved spaces happen to be the ones that hold trees with little distortion, which is why hierarchies embed so well in hyperbolic space. So a field whose prerequisites branch like a taxonomy behaves as if negatively curved: the base under a peak fans out quickly. A field whose ideas interlock, where everything uses everything else, behaves more like a positively curved space, and going deep there is comparatively cheap.

There is also a topological reading. Deep expertise sets have non-empty interior, and that interior has to get bigger the deeper you go, which quietly rules out a whole class of sets: a point, a curve, a thin lower-dimensional slice of 𝓜 all have empty interior, so none of them can be the entire expertise of someone deep. The natural way to measure "thick enough" is the inradius, the radius of the largest geodesic ball a region contains,

$$\rho_g(D) = \sup\{\, r : B_g(x, r) \subseteq D \text{ for some } x \,\}$$

and this is where the question from the poset finally gets an answer. Walk down a chain of refinements--science, chemistry, inorganic chemistry, quantum hopping--and the inradius shrinks, until at some point the boxes are too thin to contain a ball of the radius that depth demands. Everything below that point is a niche. A domain, then, would be a region with ρ_g(D) at least r(h − τ), and a niche one with less; refining past a niche can only produce more niches. Two things follow that I didn't expect. The cutoff depends on depth: at shallow depth almost anything counts as a domain, and the deeper you want to go, the coarser your boxes have to be. And because ρ_g is measured with the learner's own metric, the same region can be a niche for one person and a domain for another. The support length ℓ sets the grain, so to speak; it is the finest resolution at which anyone can usefully specialize.

So is quantum hopping a domain or a niche? The framework turns that into a different question, which is whether it is a fat region of knowledge space or a thin slice through it. If it's a slice, then "my expertise is quantum hopping" is shorthand for "my expertise is a region of physical chemistry, and my peak sits on quantum hopping." A niche would be where your summit is, not what your expertise is.

At the other extreme, a learner with finite time can only hold a bounded region above the bar, so there are also regions too large to sit inside anyone's expertise set; call those fields. A domain lives somewhere in between, thick enough to hold depth and small enough to hold at all.

## Back to the machine

Where does the model from the opening fit into all this? As a very rough first pass, treat a general-purpose AI as a flat level of competence c across the whole space--grade X everywhere. The part of your knowledge that is distinctively yours is then wherever you beat it,

$$\{\, x : K(x) > c \,\}$$

which is just one of your own superlevel sets, a member of the same nested family from before. The machine doesn't seem to introduce any new structure at all; it raises the bar. As models improve, c creeps upward, and everyone's distinctive set shrinks along a family of sets they already had.

If you want a single number for how much sticks out, the natural one is the volume of competence above the floor,

$$V = \int_{\mathcal{M}} \big(K - c\big)_+ \, d\mu_g$$

and it behaves in a way I found clarifying. At c = 0, V is just total competence, and any two people with the same total are worth the same whatever their shape; the generalist and the specialist are simply different. As c rises, the generalist's low, wide sets are the first to sink beneath it, while the specialist's tall, narrow ones survive longest. So shape only starts to matter once there is a floor, and it is the arrival of a competent generalist machine that makes it matter at all.

The previous section complicates the obvious conclusion, though. Every point above the floor sits on a forced support region, and much of that support lies below the floor, in precisely the material the machine already covers. It looks redundant, and it is tempting to skip it for exactly that reason. But it is what holds the peak up; take it away and the peak loses the neighbourhood it needs to exist at all. Under a rising floor, distinctive value requires a peak and a peak requires a base, so the breadth a model makes look worthless turns out to be the price of the depth that still counts--and the higher the floor goes, the larger the share of what you know that ends up as invisible base. Perhaps the opening question was slightly mis-posed, then. It was never really a choice between being a generalist and being a specialist.

Two caveats, in fairness. A real model isn't flat; it is another competence function, K_AI, and your distinctive set becomes {K > K_AI}, which is no longer a superlevel set, though the logic about peaks and support carries over. And V only counts what you know beyond the machine. It says nothing about what you can do with it, which may well depend heavily on that base.

## What I assumed away

All of the above quietly rests on an assumption I made on purpose and am not at all sure about: that there is no emergence. Pieces of knowledge only interact through nearness, and the space itself never changes. In neural networks that is plainly false--abilities show up that no single parameter encodes, living instead in how the parameters co-vary, so that if you were handed the parameters without their correlations you would miss them entirely. I set that aside to see how much the plain geometry could say on its own, and it ended up being more than I expected, but it is worth being clear about what was held fixed.

Klein's Erlangen program offers a tidy way to say it: classify a geometry by the group of transformations that leave it unchanged. Read that way, the model has three layers. The competence function K, what you know, is preserved by isometries and changed by learning and forgetting. Beneath it sits the metric g, which items are near each other for you, preserved by isometries but not by dilations, which is exactly where the scale ℓ lives. Beneath that sits the topology of 𝓜, which items are adjacent at all and how many independent directions there are, preserved only by homeomorphisms. Everything so far has moved the top layer alone.

Which makes me wonder what moving the middle layer would look like. One candidate is to let the metric contract wherever competence runs deep. Restricting to conformal changes, g = e^(2φ) g₀, the simplest version would be

$$\frac{\partial \varphi}{\partial t} = -\kappa\, (K - \theta)_+, \qquad \theta \ge \tau$$

so that beyond some consolidation threshold θ, the items around a deep peak become cheaper to move between--the way experts chunk what novices see as separate steps. Conformal changes rescale distances but keep angles and topology intact, so nothing emergent sneaks in. What I find interesting is what this does to everyone else's paths. Shortest routes get drawn toward contracted regions, so a deep specialization S starts acting like a hub, and any pair of points whose geodesic passes near it can get closer. Once the contraction has reached φ ≤ −Φ on S, with d the old distance and d′ the new one,

$$d'(x,y) \;\le\; \min\Big\{\, d(x,y),\;\; d(x,S) + e^{-\Phi}\operatorname{diam}_g(S) + d(S,y) \,\Big\}$$

How much of the space benefits then depends on how central S is--on the fraction of all pairs whose geodesics cross it, a continuous cousin of betweenness centrality. In a tree-like, negatively curved field, paths between different branches run through the trunk, so specializing in the trunk would reshape distances almost everywhere, while specializing in a leaf would reshape almost nothing outside its own branch. If capacity is something like this, then whether going deep builds anything general is less a property of depth than of where you happen to dig. (This version can only ever shrink distances, which means specialization never makes anything harder; catastrophic forgetting in neural networks suggests that is too generous, and letting φ rise elsewhere would be the obvious repair.)

Moving the bottom layer is stranger still. Two distant ideas suddenly becoming adjacent, or a new direction of thought appearing that the space didn't have before, is a change of topology, and no smooth reshaping of distances can produce it; it needs the space itself to change. Perhaps that is what emergence would mean here.

I don't know yet whether either of these is right, and I suspect the answer is "sometimes." If specialization only ever moves the field, then the argument about floors and peaks is more or less the whole story, and depth is mostly a way of standing above the machine. If going deep in one place can change the geometry--or even the topology--of everything else, then specialization is something stranger and more interesting than that, a way of changing the space you learn in.

## Self-reflection

This was made possible with the help of Claude, who (?) is shockingly competent. I think that in my current state of knowledge, it will take me a lot more time to develop this post, despite a long-running interest in topology that has not manifested in any formal capacity (besides one final project in Statistical Mechanics).

As of this writing, OpenAI and the likes have ruffled many feathers across math and applied math communities, some of which reaches me as a committed learner in anything fluids-related. I have never had a strong opinion towards the kind of intelligence or capacity that silicon-based beings develop, or at least any opinion that is borne out of ethical or social must-haves. A lot of scientists and engineers are tool-builders, who engage in this feigned praxis of agnosticism toward their own craft. Sometimes that conviction builds the character for the work; over-aligning can be exhausting and unproductive.

What that then means is that the job of aligning is left to the people who specialize in alignment; one must dedicate oneself to AI Safety and the hypotheticals that it purports. Or, you care so much that you reject its intrusion into your space, by holding anything generated through a machine at bay and curating your consumption around how provably human it is. Is either approach right? I don't know; it is a choice. I generally do not condemn anyone for any practice that is rooted in coherent self-perception (here, referring to the relationship that a person should cultivate with knowledge, or with machine).

But I think science suffers from under-discovery, perhaps because it is really expensive. Ask any scientist(-in-training), and you will learn how much gaining any kind of knowledge costs. Pure math, for instance, can develop debilitatingly eccentric traditions because Math departments are small, underfunded, and require a devout commitment to the most removed-from-reality abstractions. No one thinks that they are unimportant, but the degree of importance is apparent through the assigned dollar value that, let's say, the NSF gives. Money attracts talent and knowledge, which is not good or bad, but the way things are.

I don't think generative AI models will replace mathematicians, but it will give them more to work with, and I have never met an academic who is not behaviorally turned on by a harder problem.