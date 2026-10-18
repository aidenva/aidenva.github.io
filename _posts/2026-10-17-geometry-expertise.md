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

This family also has a standard topological reading. For a generic smooth K (a Morse function), the topology of E(τ) can only change as τ passes a critical value of K: a new component appears when the bar drops below a peak, and two components merge at a saddle. Persistent homology records when each component appears and when it merges as τ decreases, which describes a learner's peaks (how many there are, and how far each stands above the saddles around it) without reference to any metric.

Comparing learners gets a little uncomfortable here. The natural way to say A knows more than B is that B's expertise set sits inside A's at every bar, which is the same as $$K_B \le K_A$$ everywhere--but that is only a partial order (an ordering in which some pairs simply can't be ranked), and most pairs of learners are simply incomparable, since each clears some bar somewhere the other doesn't. "Who knows more?" doesn't have an answer until you add more structure.

The domain question can now be restated, too, though there are two different ways a region can relate to an expertise set, and they need to be kept apart. A learner is an expert in a region D when $$D \subseteq E(\tau)$$: the region sits inside what it knows well. A learner's expertise is confined to a region N when $$E(\tau) \subseteq N$$: what it knows well sits inside the region. The first relation puts no constraint on D at all, since a single point can sit inside a large expertise set. The second is the relation behind statements like "my expertise is X," and it turns the domain question into a question about sets: which regions can contain the entire expertise set of an actual learner? If $$E(\tau)$$ is allowed to be a single point, any region can, and the distinction between domain and niche really is convention.

One caution, because we tend to picture all of this on flat 2D maps. A map is a projection, and projections never increase distances: two pieces of knowledge that look far apart on a map really are far apart, but two that look close may only be close in that particular slice, and far apart in the dimensions the map threw away. Maps flatter us; they make knowledge look more connected than it is.

## Can expertise be a spike?

Take a learner that knows electron hopping deeply. It is hard to picture one without some mechanics, some linear algebra, some chemistry sitting underneath, and so the natural question is whether a spike of competence with nothing around it can exist at all, or whether depth somehow drags its surroundings up with it.

I have this weird interest in fluid dynamics, borne out of doing well in a fluids class I did not expect to do well in. Fluids are interesting because they are everywhere yet elusive to capture; they require a natural elegance that is mathematically bulky. One such property has to do with physical continuity. A sharp discontinuity in a fluid isn't strictly forbidden, but it isn't natural either--it drives the system out of equilibrium, and diffusion and viscosity smooth it out until it's gone. Whether competence behaves similarly is something that can be stated precisely once it is written as an equation.

Written as a fluid person would write it, with $$u(x, t)$$ the effort put in, λ a forgetting rate and ν a coefficient for how much neighboring knowledge props each point up:

<div class="math-display">
$$\frac{\partial K}{\partial t} = \nu\,\Delta_g K \;-\; \lambda K \;+\; (1 - K)\,u$$
</div>

Read term by term: the first spreads competence into nearby knowledge, the second lets it fade when unused, and the third adds it wherever effort is spent. The Laplacian $$\Delta_g$$ in the first term is doing the interesting work, because on any Riemannian manifold it measures how a point compares with its surroundings,

<div class="math-display">
$$\Delta_g K(x) = \lim_{r \to 0} \frac{2n}{r^2} \left( \frac{1}{|\partial B_g(x,r)|}\int_{\partial B_g(x,r)} K \;-\; K(x) \right)$$
</div>

so the ν term pulls every point toward the average of its neighborhood, eroding peaks and filling gaps. (It should be read as support rather than conservation; studying chemistry does not drain physics.) The factor $$(1 - K)$$ is there so that competence can approach one but never reach it.

This is also where the idea of a peak "collapsing" can be made exact, and computational mathematics gives the cleanest way to see it. Discretize $$\mathcal{M}$$ as a mesh with spacing $$\Delta x$$. The Laplacian becomes a finite-difference stencil, in one dimension

<div class="math-display">
$$(\Delta_{\Delta x} K)_i = \frac{K_{i+1} - 2K_i + K_{i-1}}{\Delta x^2}$$
</div>

which is the mean-value formula above with the sphere replaced by the two neighboring nodes. Two standard facts about this setup carry over directly. The first is a maximum principle: with no effort ($$u = 0$$), the largest value of K can only decrease, both in the continuum and on the mesh (for a stable time step). A peak with nothing feeding it has no way to grow or hold its height. The second is spectral. Write K as a sum of eigenmodes of the Laplacian, $$K = \sum_k a_k \phi_k$$ with $$-\Delta_g \phi_k = \mu_k \phi_k$$. With no effort, each mode decays independently,

<div class="math-display">
$$a_k(t) = a_k(0)\, \exp\big(-(\nu \mu_k + \lambda)\, t\big)$$
</div>

and the eigenvalue $$\mu_k$$ grows with how oscillatory the mode is, like $$|k|^2$$ in flat space. A feature of width σ is built from modes with $$|k|$$ of order 1/σ or more, so it decays on a time scale of order $$\sigma^2/\nu$$. On a mesh, the narrowest representable feature, a spike at a single node, is dominated by the highest-frequency modes, and the largest eigenvalue of the one-dimensional stencil is $$4/\Delta x^2$$. The same scaling appears in practice as the stability limit for explicit time-stepping, $$\Delta t \le \Delta x^2/(2\nu)$$: the finer the features a mesh can represent, the faster they decay. So the statement that a peak without lower peaks around it collapses can be replaced by a precise one: under diffusion-type dynamics, the narrow part of any profile is carried by high-frequency modes, and those are the modes that decay first. (The modes with $$\mu_k = 0$$ are the ones the ν term never erodes, and they are topological: on a closed manifold, the number of such modes for functions equals the number of connected components, and Hodge theory extends the same statement to loops and higher-dimensional holes. The spectrum sees topology through its zeros and geometry through everything else.)

The first thing one might try, before any of this, is simply to demand that K be smooth. Smoothness can be kept, but it isn't enough on its own: it requires derivatives to exist, not to be small, so it allows peaks of any width. Near a point $$x_0$$, consider the dilations, which simply zoom the space in or out around that point by a factor s,

<div class="math-display">
$$\delta_s(x) = x_0 + s\,(x - x_0), \qquad s > 0$$
</div>

They form a group (zooms can be combined and undone), acting on competence functions by squeezing or stretching them about $$x_0$$, and smoothness is invariant under that action: if one smooth peak of height h exists, so does every squeezed copy of it, at the same height and as thin as you like. There are even smooth bump functions, which rise to a peak and fall to exactly zero within a tiny ball--islands with literally nothing around them. Continuity, smoothness of any order, even analyticity are all qualitative conditions with no length scale in them, and no condition invariant under dilations can ever impose a minimum width on expertise. Ruling out spikes requires something that breaks the symmetry.

The fluid equation does: ν and λ together define a length,

<div class="math-display">
$$\ell = \sqrt{\nu/\lambda}$$
</div>

and rescaling space changes the equation unless ℓ rescales with it. Several things fall out of that one length. Left alone, a peak of width σ decays on the $$\sigma^2/\nu$$ time scale from the spectral argument above, so narrowness becomes a maintenance cost. Under sustained, tightly focused effort, competence settles into a profile whose shoulders fall off like $$\exp(-r/\ell)$$, so focus finer than ℓ doesn't produce narrower expertise at all, only the same shoulders. And in such a profile the slopes are bounded, roughly by $$L \approx h/\ell$$, which gives a static shadow of the dynamics, what mathematicians call a Lipschitz condition: competence can change by at most L per unit of distance,

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

There is also a topological reading, and part of it needs no scale at all. If K is continuous, the set $$\{K > \tau\}$$ is open, so any point where the bar is cleared with room to spare already has a neighborhood (a small ball, room in every direction) where it is still cleared. A point, a curve, or a thin lower-dimensional slice of $$\mathcal{M}$$ has empty interior, so none of them can be the entire expertise set of a learner that clears the bar strictly anywhere. What the scale adds is size: under the Lipschitz condition that neighborhood has radius at least $$(h - \tau)/L$$, so it has to get bigger the deeper you go. The natural way to measure "thick enough" is the inradius, the radius of the largest geodesic ball a region contains. The ball and its radius are both measured in the ambient space $$(\mathcal{M}, g)$$, not inside the region, so the region does not need to be convex or have any particular shape; it only needs to enclose the ball:

<div class="math-display">
$$\rho_g(D) = \sup\{\, r : B_g(x, r) \subseteq D \text{ for some } x \,\}$$
</div>

This is where the question from the poset gets an answer. The inradius is monotone under inclusion, $$D \subseteq D' \Rightarrow \rho_g(D) \le \rho_g(D')$$, so it is an order-preserving map from the poset of regions to $$[0, \infty)$$. Walking down a chain of refinements--science, chemistry, physical chemistry, quantum dynamics, electron hopping--can therefore only shrink it, until at some point the boxes are too thin to contain a ball of the radius that depth demands. Everything below that point is a niche. A domain, then, would be a region that can confine a depth-h expertise set, which requires $$\rho_g(D) \ge r(h - \tau)$$; a niche is a region with less, and by monotonicity, refining past a niche can only produce more niches. Two consequences follow. First, the cutoff depends on depth: at shallow depth almost anything counts as a domain, and the deeper one wants to go, the coarser the boxes have to be. Second, because $$\rho_g$$ is measured with the learner's own metric, the same region can be a niche for one learner and a domain for another. The support length ℓ sets the grain, so to speak; it is the finest resolution at which any learner can usefully specialize.

So is electron hopping a domain or a niche? The framework turns that into a different question, which is whether it is a fat region of knowledge space or a thin slice through it. If it's a slice, then "my expertise is electron hopping" is shorthand for "my expertise is a region of quantum dynamics, and my peak sits on electron hopping." A niche would be where your summit is, not what your expertise is.

At the other extreme, a learner with finite time can only hold a bounded region above the bar, so there are also regions too large to sit inside any single learner's expertise set; call those fields. A domain sits between the two: its inradius is at least $$r(h - \tau)$$, and its volume is small enough for a single learner to cover at level τ.

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

Put the two together and the floor sets a minimum on depth and on breadth at the same time. Any learner with distinctive value must peak above c and must hold nonzero competence across a region at least c/L in radius, and both minimums rise as models improve. A generalist plateau fails the first condition; an unsupported spike fails the second. Under a floor, then, neither a pure plateau nor a pure spike has V > 0, and depth and breadth enter as two conditions of a single constraint rather than as alternatives.

A related property concerns cost. A learner of depth h has to hold at least the minimum profile $$m(x) = \max\big(0,\ h - L\, d_g(x, x_0)\big)$$ everywhere. Only the part of m above the floor counts toward V; the part beneath it is required but invisible, sitting in precisely the material the machine already covers. As c rises toward h, the total that m demands stays fixed while the part that counts shrinks toward zero, so a growing share of what depth requires lies below the floor.

Two caveats, in fairness. A real model isn't flat; it is another learner with its own competence function, $$K_{\mathrm{AI}}$$, and the distinctive set becomes $$\{K > K_{\mathrm{AI}}\}$$, which is no longer a superlevel set, though the logic about peaks and support carries over. And V only counts competence beyond the machine. It says nothing about what a learner can do with it, which may well depend heavily on that base.

## What I assumed away

All of the above rests on an assumption I made on purpose and am not at all sure about: that there is no emergence. Pieces of knowledge only interact through nearness, and the space itself never changes. In neural networks that is plainly false--abilities show up that no single parameter encodes, living instead in how the parameters co-vary, so that if you were handed the parameters without their correlations you would miss them entirely. I set that aside to see how much the plain geometry could say on its own, and it ended up being more than I expected, but it is worth being clear about what was held fixed.

Klein's Erlangen program offers a tidy way to say it: classify a geometry by the group of transformations that leave it unchanged. Read that way, the model has three layers. The competence function K, what a learner knows, is preserved by isometries (maps that keep every distance the same) and changed by learning and forgetting. Beneath it sits the metric g, which items are near each other <em>for that learner</em>, preserved by isometries but not by dilations, which is exactly where the scale ℓ lives. Beneath that sits the topology of $$\mathcal{M}$$, which items are adjacent at all and how many independent directions there are, preserved only by homeomorphisms (continuous deformations that can stretch the space but never tear or glue it). Everything so far has moved the top layer alone. One more thing is held fixed that is easy to miss: the competence scale itself. The order-level statements (nesting, the partial order, whether the distinctive set exists) survive any strictly increasing relabelling of K, but V, the Lipschitz constant and the diffusion equation depend on the actual numbers, so they inherit whatever choice was made in putting competence on [0, 1).

Which makes me wonder what moving the middle layer would look like. One candidate is to let the metric contract wherever competence runs deep, and the most modest way to do that is a conformal change: multiply the metric at every point by a positive factor, $$g = \exp(2\varphi)\, g_0$$, so that lengths near a point are scaled by $$\exp(\varphi)$$ while angles between directions are left untouched. It is the smallest change to the geometry that can still bring things closer together, since it rescales distance without twisting the space or touching its topology. The simplest version would be

<div class="math-display">
$$\frac{\partial \varphi}{\partial t} = -\kappa\, (K - \theta)_+, \qquad \theta \ge \tau$$
</div>

so that beyond some consolidation threshold θ, the items around a deep peak become cheaper to move between--the way experts chunk what novices see as separate steps. Because the change is conformal, nothing emergent sneaks in. What I find interesting is what this does to every other path. Shortest routes get drawn toward contracted regions, so a deep specialization S starts acting like a hub, and any pair of points whose geodesic passes near it can get closer. Once the contraction has reached $$\varphi \le -\Phi$$ on S (taking S to be geodesically convex, so that its diameter is measured by paths inside it), with d the old distance and $$d'$$ the new one,

<div class="math-display">
$$d'(x,y) \;\le\; \min\Big\{\, d(x,y),\;\; d(x,S) + \exp(-\Phi)\,\operatorname{diam}_g(S) + d(S,y) \,\Big\}$$
</div>

How much of the space benefits then depends on how central S is--on the fraction of all pairs whose geodesics cross it, a continuous cousin of betweenness centrality, which in a network counts the share of shortest paths passing through a given node. In a tree-like, negatively curved field, paths between different branches run through the trunk, so specializing in the trunk would reshape distances almost everywhere, while specializing in a leaf would reshape almost nothing outside its own branch. If capacity is something like this, then whether going deep builds anything general is less a property of depth than of where one happens to dig. (This version can only ever shrink distances, which means specialization never makes anything harder; catastrophic forgetting in neural networks suggests that is too generous, and letting φ rise elsewhere would be the obvious repair.)

Moving the bottom layer is a different kind of change. Dimension, connectedness and the number of independent loops in a space are topological invariants: no homeomorphism changes them, and no change of metric does either, because every metric g lives on the same underlying manifold. A metric can bring two points arbitrarily close, but distinct points always stay a positive distance apart, and every shortcut runs through space that already exists. So a new connection between two distant ideas (a new loop) or a new direction of thought (a new dimension) cannot come from a smooth evolution of g; it requires replacing $$\mathcal{M}$$ with a different manifold. If emergence means anything here, it is that kind of discontinuity, a point where the evolution of the space stops being continuous. If that were to be formalized, the standard tool is a cobordism: a manifold whose boundary consists of the old and the new space, along which the topology changes only at isolated critical points.

I don't know yet whether either of these is right, and I suspect the answer is "sometimes." If specialization only ever moves the field, then the argument about floors and peaks is more or less the whole story, and depth is mostly a way of standing above the machine. If going deep in one place can change the geometry--or even the topology--of everything else, then specialization is something stranger and more interesting than that, a way of changing the space you learn in.

## So what?

Suppose, for the sake of argument, a learner that is currently a generalist: a plateau of competence at some level p over a wide region, and no peak to speak of. It wants to develop something specialized, either to exceed the floor set by grade-X machinery at some target, or without a particular target in mind. Under the assumptions above, both motives run through the same three quantities, and each of them has an upper bound.

The first is transfer. If effort goes into one region and the payoff is wanted somewhere else, at distance d, then in the field equation the marginal effect of a unit of effort at y on competence at x is bounded by the Green's function of the operator $$\lambda - \nu\Delta_g$$, which at large distances decays exponentially in units of the support length:

<div class="math-display">
$$\frac{\delta K(x)}{\delta u(y)} \;\le\; G_\ell(x, y) \;\sim\; \exp\big(-d_g(x,y)/\ell\big)$$
</div>

Each additional ℓ of distance divides the possible transfer by a fixed factor. This is a standard property of the equation, so it is only as good as the equation, but within the model the effect of learning in one region on competence far away is small and decays with distance.

The second is the cost of depth at the target itself. Under the Lipschitz condition, a peak of height h at $$x^*$$ needs at least the cone $$\max(0,\ h - L\, d_g(x, x^*))$$ beneath it, and the marginal cost of raising h is the volume of the region where that cone still sits above existing competence. For a generalist with plateau p around $$x^*$$, that region is a ball of radius $$(h - p)/L$$ rather than $$h/L$$:

<div class="math-display">
$$\frac{\partial h}{\partial (\text{effort})} \;\le\; \frac{1}{\mu_g\big(B_g(x^*,\ (h - p)/L)\big)}$$
</div>

Three things follow from this one inequality. The plateau acts as base that has already been paid for, so breadth near the target lowers the marginal cost of depth there. Breadth farther than $$(h - p)/L$$ from the target contributes nothing to it. And because ball volumes grow polynomially with radius in flat regions and exponentially in negatively curved ones, returns on depth fall off polynomially in fields whose ideas interlock and exponentially in fields that branch.

The third is capacity. If specializing on a region S contracts the metric there by a factor $$\exp(-\Phi)$$, then for any pair of points (taking S geodesically convex, with shortest paths entering it once),

<div class="math-display">
$$d_g(x,y) - d'(x,y) \;\le\; \big(1 - \exp(-\Phi)\big)\,\operatorname{diam}_g(S) \;<\; \operatorname{diam}_g(S)$$
</div>

No two topics get closer by more than the size of the specialization, and the gain is zero for pairs whose detour through S costs more than that. Which pairs benefit depends on centrality, as before.

Read alongside the floor from earlier, the bounds describe the two kinds of learning in different terms. Learning aimed at exceeding c at a particular target is an optimization of the field at that target: push $$K(x^*)$$ above c. The bounds say this pays off locally, within $$(h - p)/L$$ of the target for depth and within a few ℓ for transfer, and that the payoff is a moving target, since c rises and the distinctive set shrinks along the filtration. Learning for its own sake, read in the same terms, does two other things: it raises the plateau p over wide regions, and, if the metric-contraction picture holds, it reshapes distances. Neither shows up in V, which is computed from the field alone and only above the floor. But both lower the cost of the next peak: a higher p shortens the radius in the second bound, and contraction shrinks the volume of the ball being paid for while pulling distant targets closer.

That difference matters because the target is rarely known in advance. Which problems remain above grade X depends on where c rises next, and no learner controls that. If $$x^*$$ is effectively unknown, the relevant quantity is the cost of building a peak wherever one is needed, and that cost is governed by the base and the geometry, which are the two things learning for its own sake builds and V cannot see. In the model's terms, the two differ in what they act on: one acts on the field at a known point, the other on the base and geometry that set the cost of reaching any point. Under a rising floor and an unknown target, the second determines the cost of the first.

The bounds also say where this stops working. Every one of them is finite and decays with distance, so within the model neither motive buys unlimited reach. The only unbounded gains are the ones the model cannot describe: non-local couplings and changes of topology. The model has nothing to say about those beyond the fact that they sit outside it.

## Self-reflection

This was made possible with the help of Claude, who (?) is shockingly competent. I think that in my current state of knowledge, it would have taken me a lot more time to develop this post, despite a long-running interest in topology that has not manifested in any formal capacity (besides one final project in Statistical Mechanics).

As of this writing, OpenAI and the likes have ruffled many feathers across math and applied math communities, some of which reaches me as a committed learner in anything fluids-related. I have never had a strong opinion towards the kind of intelligence or capacity that silicon-based beings develop, or at least any opinion that is borne out of ethical or social must-haves. A lot of scientists and engineers are tool-builders, who engage in this feigned praxis of agnosticism toward their own craft. Sometimes that conviction builds the character for the work; over-aligning can be exhausting and unproductive.

What that then means is that the job of aligning is left to the people who specialize in alignment; one must dedicate oneself to AI Safety and the hypotheticals that it purports. Or, you care so much that you reject its intrusion into your space, by holding anything generated through a machine at bay and curating your consumption around how provably human it is. Is either approach right? I don't know; it is a choice. I generally do not condemn anyone for any practice that is rooted in coherent self-perception (here, referring to the relationship that a person should cultivate with knowledge, or with machine).

But I think science suffers from under-discovery, perhaps because it is really expensive. Ask any scientist(-in-training), and you will learn how much gaining any kind of knowledge costs. Pure math, for instance, can develop debilitatingly eccentric traditions because math departments are small, underfunded, and require a devout commitment to the most removed-from-reality abstractions. No one thinks that they are unimportant, but the degree of importance is apparent through the assigned dollar value that, let's say, the NSF gives. Money attracts talent and knowledge, which is not good or bad, but the way things are.

I don't think generative AI models will replace mathematicians, but they will give mathematicians more to work with, and I have never met an academic who is not behaviorally turned on by a harder problem.