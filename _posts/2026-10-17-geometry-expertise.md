---
layout: post
title: "The Geometry of Expertise"
author: "Linh Le"
categories: journal
tags: [documentation,random]
math: true

---

I think that, given how shockingly proficient generative models have been at replacing a lot of us, there has been an echoing sentiment about what we should do. <em>Are we harnesses for AI, rather?</em> Some of the more bullish takes revolve around the inability of AI to develop domain expertise--or rather, they call attention to the void that AI leaves behind for humans to fill.

The argument usually goes something like this. A generalist, someone who is good at a lot of things, has competence spread out over many fields; if you draw it as a curve over everything one could know, it is low and wide, while a specialist's curve is narrow and tall (and nobody promises that the two enclose the same area--some people simply know more, and that's fine). If a model already holds grade-X knowledge in most fields, then a person spread to roughly grade X across those same fields is doing something a machine does faster and for pennies. Models don't hold grade X + 5 in all of those things (yet), though, so perhaps the reasonable move is to go and build domain expertise somewhere.

That sounds right to me, mostly. But it leans on two words, "domain" and "expertise," that are surprisingly slippery when we try to define them more rigorously. Here, I am trying to borrow the language of geometry to make more sense of it (perhaps I have math envy).

## Boxes inside boxes

People used to consider "science" a domain, which nowadays sounds absurdly broad; a chemist does not understand the same things a physicist does. Then again, chemistry itself is too broad, since organic and inorganic chemists are very different people with very different lives, and they hold quite different pictures of how the world fits together. A domain can be a field, a discipline, a department, a topic you happen to be obsessed with--but it can also be an arbitrarily drawn box that you've decided to call a domain, and the boxes keep getting smaller.

There is a little structure hiding in that, which is that domains nest:

<div class="math-display">
$$\text{electron hopping} \;\subset\; \text{quantum dynamics} \;\subset\; \text{physical chemistry} \;\subset\; \text{chemistry} \;\subset\; \text{science}$$
</div>

Collect every candidate domain and order them by inclusion, and you get a partially ordered set. Choosing a "level" of specialization amounts to choosing a partition of knowledge into boxes, and partitions are themselves ordered by refinement--one refines another if each of its boxes sits inside a box of the other--which makes the collection of partitions a lattice. The history of academic departments looks, from here, like a slow walk down that lattice toward finer and finer partitions.

The order is tidy, but it doesn't seem able to tell us when to stop. Is "electron hopping events" a domain, or a niche? At some point a domain becomes so constricted that it stops sounding like a field and starts sounding like a hobby, yet a poset has no notion of size: every link in the chain above looks the same to it, and in a continuum of knowledge you could keep refining all the way down to single points. Whether there is any principled place where refining a domain turns it into a niche, or whether the line is pure convention, seems to need something order alone can't provide--some idea of nearness and size, which means putting knowledge in a space.

## A landscape of competence

What kind of space, though? Knowledge is many-dimensional, and the things we want to say about it--how quickly competence falls off as you move away from what you know, how it spreads, what the shortest route from one topic to another looks like, how fast a neighborhood grows--are, rather conveniently, exactly the things a Riemannian manifold is built to talk about. It is worth being explicit about what that setup asks for, since each piece is doing a job. A manifold of dimension n is a space in which every point has a neighborhood that can be given coordinates in $$\mathbb{R}^n$$; for knowledge, this says that around any given item there are n independent ways to vary it slightly, and that between nearby items there are always intermediate ones. Making the manifold smooth means those coordinates fit together differentiably, which is what lets us talk about rates of change at all. A Riemannian metric g then assigns an inner product to the directions at each point, varying smoothly from point to point, and from that single object come lengths of paths, distances, angles, volumes and curvature. A bare metric space would give us distances but no derivatives; a graph would give us distances but no natural notion of averaging over a neighborhood or of curvature in the classical sense. A Riemannian manifold is the least structure that supplies all of these at once, which is the real reason to use it. The cost is that it assumes knowledge is locally finite-dimensional and has no gaps at small scales. So let $$(\mathcal{M}, g)$$ be a smooth, connected manifold of dimension n with a metric g. A point is a piece of knowledge at the finest resolution we care about; the length of a curve is the effort it takes to carry mastery along it; and from g we inherit, for free, a geodesic distance $$d_g$$ (the length of the shortest path between two points), a volume $$\mu_g$$ (how much knowledge a region holds), a gradient, a Laplacian $$\Delta_g$$, and curvature. (One thing I like about this is that g doesn't have to be the same for every learner: two of them can face the same things to know and still find different things close together.)

Now take a learner, by which I mean any unit of competence: a person, a research group, a model. In this picture it is nothing more than a competence function on that space,

<div class="math-display">
$$K : \mathcal{M} \to [0, 1)$$
</div>

where zero means no competence and one stands for complete, infinite knowledge of a point--a limit nobody actually reaches, hence the open interval.

Expertise needs a bar, and the bar is admittedly somewhat arbitrary. Pick a threshold τ, call anything at or above it "good," and the learner's expertise is the set of places where it clears the bar, what mathematicians call a superlevel set of K:

<div class="math-display">
$$E(\tau) = \{\, x \in \mathcal{M} : K(x) \ge \tau \,\}$$
</div>

These sets nest, which is a small thing but turns out to matter. Raise the bar and the set can only shrink,

<div class="math-display">
$$\tau \le \tau' \;\Longrightarrow\; E(\tau') \subseteq E(\tau)$$
</div>

so a learner's expertise isn't really one set at all, but a decreasing family of sets indexed by how strict you are being--a filtration, if you want the word. That gives generalists and specialists a description that is purely about shape: the generalist's sets are large at low bars and vanish early, while the specialist's are small but survive to much higher bars.

Comparing learners gets a little uncomfortable here. The natural way to say A knows more than B is that B's expertise set sits inside A's at every bar, which is the same as $$K_B \le K_A$$ everywhere--but that is only a partial order (an ordering in which some pairs simply can't be ranked), and most pairs of learners are simply incomparable, since each clears some bar somewhere the other doesn't. "Who knows more?" doesn't have an answer until you add more structure.

The domain question can now be restated, too. Being an expert in a domain D just means $$D \subseteq E(\tau)$$, so asking which boxes deserve to be called domains becomes asking which sets can actually sit inside the expertise set of an actual learner. If any set at all can--if $$E(\tau)$$ is allowed to be a single point--then the distinction between domain and niche really is convention.

One caution, because we tend to picture all of this on flat 2D maps. A map is a projection, and projections never increase distances: two pieces of knowledge that look far apart on a map really are far apart, but two that look close may only be close in that particular slice, and far apart in the dimensions the map threw away. Maps flatter us; they make knowledge look more connected than it is.

## Can expertise be a spike?

Take a learner that knows electron hopping deeply. It is hard to picture one without some mechanics, some linear algebra, some chemistry sitting underneath, and so the natural question is whether a spike of competence with nothing around it can exist at all, or whether depth somehow drags its surroundings up with it.

I have this weird interest in fluid dynamics, borne out of doing well in a fluids class I did not expect to do well in. Fluids are interesting because they are everywhere yet elusive to capture; they require a natural elegance that is mathematically bulky. One such property has to do with physical continuity. A sharp discontinuity in a fluid isn't strictly forbidden, but it isn't natural either--it drives the system out of equilibrium, and diffusion and viscosity smooth it out until it's gone. It seems plausible that competence does something similar: a high peak without lower peaks around it collapses and smears into its neighbors, and we lose exactly the property we wanted to describe.

Written as a fluid person would write it, with $$u(x, t)$$ the effort put in, λ a forgetting rate and ν a coefficient for how much neighboring knowledge props each point up:

<div class="math-display">
$$\frac{\partial K}{\partial t} = \nu\,\Delta_g K \;-\; \lambda K \;+\; (1 - K)\,u$$
</div>

Read term by term: the first spreads competence into nearby knowledge, the second lets it fade when unused, and the third adds it wherever effort is spent. The Laplacian $$\Delta_g$$ in the first term is doing the interesting work, because on any Riemannian manifold it measures how a point compares with its surroundings,

<div class="math-display">
$$\Delta_g K(x) = \lim_{r \to 0} \frac{2n}{r^2} \left( \frac{1}{|\partial B_g(x,r)|}\int_{\partial B_g(x,r)} K \;-\; K(x) \right)$$
</div>

so the ν term pulls every point toward the average of its neighborhood, eroding peaks and filling gaps. (It should be read as support rather than conservation; studying chemistry does not drain physics.) The factor $$(1 - K)$$ is there so that competence can approach one but never reach it.

The first thing one might try, before any of this, is simply to demand that K be smooth. That doesn't work, and the reason why ends up being the most useful idea in the post. Near a point $$x_0$$, consider the dilations, which simply zoom the space in or out around that point by a factor s,

<div class="math-display">
$$\delta_s(x) = x_0 + s\,(x - x_0), \qquad s > 0$$
</div>

They form a group (zooms can be combined and undone), acting on competence functions by squeezing or stretching them about $$x_0$$, and smoothness is invariant under that action: if one smooth peak of height h exists, so does every squeezed copy of it, at the same height and as thin as you like. There are even smooth bump functions, which rise to a peak and fall to exactly zero within a tiny ball--islands with literally nothing around them. Continuity, smoothness of any order, even analyticity are all qualitative conditions with no length scale in them, and no condition invariant under dilations can ever impose a minimum width on expertise. Ruling out spikes requires something that breaks the symmetry.

The fluid equation does: ν and λ together define a length,

<div class="math-display">
$$\ell = \sqrt{\nu/\lambda}$$
</div>

and rescaling space changes the equation unless ℓ rescales with it. Several things fall out of that one length. Left alone, a peak of width σ spreads on a time scale of order $$\sigma^2/\nu$$, so the narrower it is the faster it erodes; narrowness becomes a maintenance cost. Under sustained, tightly focused effort, competence settles into a profile whose shoulders fall off like $$\exp(-r/\ell)$$, so focus finer than ℓ doesn't produce narrower expertise at all, only the same shoulders. And in such a profile the slopes are bounded, roughly by $$L \approx h/\ell$$, which gives a static shadow of the dynamics, what mathematicians call a Lipschitz condition: competence can change by at most L per unit of distance,

<div class="math-display">
$$|K(x) - K(y)| \;\le\; L \, d_g(x, y)$$
</div>

I don't want to insist that knowledge obeys this particular equation or this particular inequality; the specific forms hardly matter. What matters is the structural property underneath both, that the constraint respects isometries--rearrangements of knowledge that keep neighbors as neighbors--and breaks dilations. Everything after this uses only that.

## What a scale buys

Suppose a learner clears the bar at some point $$x_0$$ with room to spare, $$K(x_0) = h > \tau$$. Competence can only fall off at a bounded rate, so it can't drop below τ immediately; it has to stay above the bar on a whole geodesic ball around $$x_0$$, and the radius of that ball grows with $$h - \tau$$:

<div class="math-display">
$$h > \tau \;\Longrightarrow\; B_g\big(x_0,\, r(h - \tau)\big) \subseteq E(\tau), \qquad r \text{ increasing}$$
</div>

A learner that barely clears the bar can be an expert at a single point, but one far above it can't. Running the same argument with a lower bar gives a larger ball on which K is still comfortably above zero, so a deep peak forces two nested regions--an expertise region where the bar is cleared, and a support region underneath where it isn't but competence is still above zero. The supporting lower peaks from the fluid picture show up here as a consequence, rather than something that had to be assumed.

How expensive that support region is depends on curvature, which I find one of the more suggestive parts of the picture. Curvature controls how fast geodesic spheres grow as you move away from a point. For intuition: on a sphere, which is positively curved, lines that start out parallel drift together and the area within a given radius grows more slowly than on a flat sheet; on a saddle, which is negatively curved, they drift apart and area grows faster. Comparison theorems (Günther–Bishop on one side, Bishop–Gromov on the other), which compare balls in a curved space with balls in a space of constant curvature, turn that into bounds on the volume of the balls above. In negatively curved regions spheres grow exponentially, and negatively curved spaces happen to be the ones that hold trees with little distortion, which is why hierarchies embed so well in hyperbolic space. So a field whose prerequisites branch like a taxonomy behaves as if negatively curved: the base under a peak fans out quickly. A field whose ideas interlock, where everything uses everything else, behaves more like a positively curved space, and going deep there is comparatively cheap.

There is also a topological reading. Deep expertise sets have non-empty interior (they contain at least a small ball, some room in every direction), and that interior has to get bigger the deeper you go, which quietly rules out a whole class of sets: a point, a curve, a thin lower-dimensional slice of $$\mathcal{M}$$ all have empty interior, so none of them can be the entire expertise of a deep learner. The natural way to measure "thick enough" is the inradius, the radius of the largest geodesic ball a region contains,

<div class="math-display">
$$\rho_g(D) = \sup\{\, r : B_g(x, r) \subseteq D \text{ for some } x \,\}$$
</div>

and this is where the question from the poset finally gets an answer. Walk down a chain of refinements--science, chemistry, physical chemistry, quantum dynamics, electron hopping--and the inradius shrinks, until at some point the boxes are too thin to contain a ball of the radius that depth demands. Everything below that point is a niche. A domain, then, would be a region with $$\rho_g(D)$$ at least $$r(h - \tau)$$, and a niche one with less; refining past a niche can only produce more niches. Two things follow that I didn't expect. The cutoff depends on depth: at shallow depth almost anything counts as a domain, and the deeper one wants to go, the coarser the boxes have to be. And because $$\rho_g$$ is measured with the learner's own metric, the same region can be a niche for one learner and a domain for another. The support length ℓ sets the grain, so to speak; it is the finest resolution at which any learner can usefully specialize.

So is electron hopping a domain or a niche? The framework turns that into a different question, which is whether it is a fat region of knowledge space or a thin slice through it. If it's a slice, then "my expertise is electron hopping" is shorthand for "my expertise is a region of quantum dynamics, and my peak sits on electron hopping." A niche would be where your summit is, not what your expertise is.

At the other extreme, a learner with finite time can only hold a bounded region above the bar, so there are also regions too large to sit inside any single learner's expertise set; call those fields. A domain lives somewhere in between, thick enough to hold depth and small enough to hold at all.

## Back to the machine

Where does the model from the opening fit into all this? As a very rough first pass, treat a general-purpose AI as a flat level of competence c across the whole space--grade X everywhere. The part of a learner's competence that is distinctively its own is then wherever it beats that floor,

<div class="math-display">
$$\{\, x : K(x) > c \,\}$$
</div>

which is just one of the learner's own superlevel sets, a member of the same nested family from before. The machine doesn't seem to introduce any new structure at all; it raises the bar. As models improve, c creeps upward, and every learner's distinctive set shrinks along a family of sets it already had.

If you want a single number for how much sticks out, the natural one is the volume of competence above the floor,

<div class="math-display">
$$V = \int_{\mathcal{M}} \big(K - c\big)_+ \, d\mu_g$$
</div>

and it has two properties worth stating plainly. At c = 0 it is shape-blind: V is just total competence, so two learners with the same total score the same however their competence is distributed. For c > 0 it vanishes on anything that stays below the floor: a learner whose competence never exceeds c anywhere has V = 0, however broad that competence is. So shape only starts to matter once there is a floor, and it is the arrival of a competent generalist machine that makes it matter at all.

Which learners have V > 0, then? The earlier properties answer this almost mechanically. The distinctive set is non-empty exactly when the peak clears the floor,

<div class="math-display">
$$\{\, x : K(x) > c \,\} \neq \varnothing \iff \sup_{\mathcal{M}} K > c$$
</div>

which is a statement purely about depth; no amount of breadth below the floor can help. But the Lipschitz condition says that a peak of height h at $$x_0$$ forces $$K(x) \ge h - L\, d_g(x, x_0)$$, so competence stays positive on a ball of radius h/L around the peak. Since h > c, that ball always contains one of radius c/L:

<div class="math-display">
$$\sup_{\mathcal{M}} K > c \;\Longrightarrow\; B_g\big(x_0,\ c/L\big) \subseteq \{\, x : K(x) > 0 \,\}$$
</div>

Put the two together and the floor sets a minimum on depth and on breadth at the same time. Any learner with distinctive value must peak above c and must hold nonzero competence across a region at least c/L in radius, and both minimums rise as models improve. A generalist plateau fails the first condition; an unsupported spike fails the second. Neither pure strategy survives a floor, which is why I think the opening question was mis-posed: it was never really a choice between being a generalist and being a specialist, because depth and breadth are two sides of a single constraint.

There is a quieter cost hiding here too. A learner of depth h has to hold at least the minimum profile $$m(x) = \max\big(0,\ h - L\, d_g(x, x_0)\big)$$ everywhere. Only the part of m above the floor counts toward V; the part beneath it is required but invisible, sitting in precisely the material the machine already covers. As c rises toward h, the total that m demands stays fixed while the part that counts shrinks toward zero, so a growing share of what depth requires is breadth that looks worthless and isn't.

Two caveats, in fairness. A real model isn't flat; it is another learner with its own competence function, $$K_{\mathrm{AI}}$$, and the distinctive set becomes $$\{K > K_{\mathrm{AI}}\}$$, which is no longer a superlevel set, though the logic about peaks and support carries over. And V only counts competence beyond the machine. It says nothing about what a learner can do with it, which may well depend heavily on that base.

## What I assumed away

All of the above rests on an assumption I made on purpose and am not at all sure about: that there is no emergence. Pieces of knowledge only interact through nearness, and the space itself never changes. In neural networks that is plainly false--abilities show up that no single parameter encodes, living instead in how the parameters co-vary, so that if you were handed the parameters without their correlations you would miss them entirely. I set that aside to see how much the plain geometry could say on its own, and it ended up being more than I expected, but it is worth being clear about what was held fixed.

Klein's Erlangen program offers a tidy way to say it: classify a geometry by the group of transformations that leave it unchanged. Read that way, the model has three layers. The competence function K, what a learner knows, is preserved by isometries (maps that keep every distance the same) and changed by learning and forgetting. Beneath it sits the metric g, which items are near each other <em>for that learner</em>, preserved by isometries but not by dilations, which is exactly where the scale ℓ lives. Beneath that sits the topology of $$\mathcal{M}$$, which items are adjacent at all and how many independent directions there are, preserved only by homeomorphisms (continuous deformations that can stretch the space but never tear or glue it). Everything so far has moved the top layer alone.

Which makes me wonder what moving the middle layer would look like. One candidate is to let the metric contract wherever competence runs deep, and the most modest way to do that is a conformal change: multiply the metric at every point by a positive factor, $$g = \exp(2\varphi)\, g_0$$, so that lengths near a point are scaled by $$\exp(\varphi)$$ while angles between directions are left untouched. It is the smallest change to the geometry that can still bring things closer together, since it rescales distance without twisting the space or touching its topology. The simplest version would be

<div class="math-display">
$$\frac{\partial \varphi}{\partial t} = -\kappa\, (K - \theta)_+, \qquad \theta \ge \tau$$
</div>

so that beyond some consolidation threshold θ, the items around a deep peak become cheaper to move between--the way experts chunk what novices see as separate steps. Because the change is conformal, nothing emergent sneaks in. What I find interesting is what this does to every other path. Shortest routes get drawn toward contracted regions, so a deep specialization S starts acting like a hub, and any pair of points whose geodesic passes near it can get closer. Once the contraction has reached $$\varphi \le -\Phi$$ on S (taking S to be geodesically convex, so that its diameter is measured by paths inside it), with d the old distance and $$d'$$ the new one,

<div class="math-display">
$$d'(x,y) \;\le\; \min\Big\{\, d(x,y),\;\; d(x,S) + \exp(-\Phi)\,\operatorname{diam}_g(S) + d(S,y) \,\Big\}$$
</div>

How much of the space benefits then depends on how central S is--on the fraction of all pairs whose geodesics cross it, a continuous cousin of betweenness centrality, which in a network counts the share of shortest paths passing through a given node. In a tree-like, negatively curved field, paths between different branches run through the trunk, so specializing in the trunk would reshape distances almost everywhere, while specializing in a leaf would reshape almost nothing outside its own branch. If capacity is something like this, then whether going deep builds anything general is less a property of depth than of where one happens to dig. (This version can only ever shrink distances, which means specialization never makes anything harder; catastrophic forgetting in neural networks suggests that is too generous, and letting φ rise elsewhere would be the obvious repair.)

Moving the bottom layer would be a different kind of change altogether, and the reason is a basic fact about topology. Some properties of a space, such as its dimension, whether it is connected, and how many independent loops run through it, are topological invariants: no homeomorphism changes them, and so no change of metric does either, however drastic, because every metric g lives on the same underlying manifold. A metric can make two points very close but never newly adjacent; distinct points always stay a positive distance apart, and every shortcut has to run through space that was already there. So if learning ever creates a genuinely new connection between two distant ideas (in effect, a new loop through the space) or opens a new direction of thought (a new dimension), it cannot be a smooth evolution of g. It has to be a jump to a different manifold. Geometric analysis has a precise version of this. In Ricci flow, a well-studied way of evolving a metric, the topology can change only at singularities, moments where the smooth evolution breaks down and the space has to be cut and reglued; that surgery is the heart of Perelman's proof of the Poincaré conjecture. If emergence corresponds to anything in this picture, it is to singularities of that kind: points where continuous learning stops being continuous.

I don't know yet whether either of these is right, and I suspect the answer is "sometimes." If specialization only ever moves the field, then the argument about floors and peaks is more or less the whole story, and depth is mostly a way of standing above the machine. If going deep in one place can change the geometry--or even the topology--of everything else, then specialization is something stranger and more interesting than that, a way of changing the space you learn in.

## Self-reflection

This was made possible with the help of Claude, who (?) is shockingly competent. I think that in my current state of knowledge, it would have taken me a lot more time to develop this post, despite a long-running interest in topology that has not manifested in any formal capacity (besides one final project in Statistical Mechanics).

As of this writing, OpenAI and the likes have ruffled many feathers across math and applied math communities, some of which reaches me as a committed learner in anything fluids-related. I have never had a strong opinion towards the kind of intelligence or capacity that silicon-based beings develop, or at least any opinion that is borne out of ethical or social must-haves. A lot of scientists and engineers are tool-builders, who engage in this feigned praxis of agnosticism toward their own craft. Sometimes that conviction builds the character for the work; over-aligning can be exhausting and unproductive.

What that then means is that the job of aligning is left to the people who specialize in alignment; one must dedicate oneself to AI Safety and the hypotheticals that it purports. Or, you care so much that you reject its intrusion into your space, by holding anything generated through a machine at bay and curating your consumption around how provably human it is. Is either approach right? I don't know; it is a choice. I generally do not condemn anyone for any practice that is rooted in coherent self-perception (here, referring to the relationship that a person should cultivate with knowledge, or with machine).

But I think science suffers from under-discovery, perhaps because it is really expensive. Ask any scientist(-in-training), and you will learn how much gaining any kind of knowledge costs. Pure math, for instance, can develop debilitatingly eccentric traditions because math departments are small, underfunded, and require a devout commitment to the most removed-from-reality abstractions. No one thinks that they are unimportant, but the degree of importance is apparent through the assigned dollar value that, let's say, the NSF gives. Money attracts talent and knowledge, which is not good or bad, but the way things are.

I don't think generative AI models will replace mathematicians, but they will give mathematicians more to work with, and I have never met an academic who is not behaviorally turned on by a harder problem.