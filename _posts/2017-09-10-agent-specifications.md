---
layout: post
title: Agent Specifications
categories: 'ai'
---

Now that the blog intro post is out of the way, let's go onto one last boiler plate post before diving into technical work. Here I'll focus on defining the high level specifications of the first agent I'll be making. This includes what the the problem even is, what kind of environment our agent will be looking at, and how our agent will actually perform its job.

## Problem Context
I'm not naive enough to try to tackle the _huge_ problem of creating a Starcraft agent in an actual 1v1 game, so I'm first focusing on a tiny toy problem to get a feel for the development environment and creating my first rational agent. This will be a pretty straightforward mini game, released along with the official library called "Defeat the Roaches". This map presents a super simplified approach to Starcraft, removing any need for significant strategy. There are no bases, no unit building, and nor is there any actual terrain that needs to explored. Instead, a small area of land is generated and you're dropped in there with 9 Marine units to control, with your goal being to destroy the other 4 enemy units, all Zerg Roaches.

{:.image-with-caption}
![Initial state]({{ site.url }}/assets/defeat_roach_start.png){: width="500px"}
_The initial state of the Defeat the Roach Minimap. There are 9 units our agent will control and 4 units to destroy. Note that there is no space beyond what is shown to explore, nor any bases or resources._

## Task Environment
There's a great checklist defined in [Artificial Intelligence: A Modern Approach][ai-book] for describing the context and goals of our rational agent:

**Performance Measure**: how do we measure the success of our agent\\
**Environment**: what does the agent's world look like and how do its actions affect it\\
**Actuators**: how will the agent interact with the world\\
**Sensors**: how does the agent perceive the world

### Performance Measure
The agent's first performance measure will just be to ensure that it wins consistently over a period of 10 games. After I reach a good measurement here, I'll probably re-visit this measure and make it slightly harder, adding an additional parameter of how many Marine units survived the encounter as well as the time taken for each simulation.

### Environment
This is a **fully-observable**, **stochastic**, **sequential** (with a major **episodic** component), **dynamic**, **discrete**, **multi-agent**, **known** environment. Breaking that down further and how this may differentiate from a "normal" SC2 game, the minimap makes a number of simplications that dramatically alters the type of environment our agent will play under.

The biggest change is probably that our environment is fully-observable, where a typical SC2 game involves a huge component of exploration and deducing your opponent's state and resources. The partial observability of a typical SC2 game is a pretty huge component of what makes RTS AI interesting, especially in comparison to some high profile games that AI has "solved" such as chess and Go, but it also poses a host of challenges that I'm not ready to deal with yet.

And, while SC2 is largely deterministic, there are stochastic elements that become important at a micro level, which is where this mini-game will be focusing on. Most importantly, the attack speed of the individual units has a small random component to it. This is mostly due to graphical concerns since it would look super primitive for all units of a group to have their attack animations completely in sync, but because of this, the result of a battle involving a small number of units can vary.

The rest of the environment categorizations are as one would expect in almost any RTS game. The agent's environment is sequential in that it will make a series of choices that affect its performance, and each action depends on previous ones. The "episodic component" refers to the fact that the agent's performance measure is actually based on the outcome of 10 games rather than an individual one, and the state is completely reset between each game.

The environment is dynamic in that the agent's choices will happen in real-time (spoiler alert: this is a real time strategy game), so our computations will need to be fast enough such that our agent is not sitting and getting wrecked while calculating an optimal action.

Our agent will be playing against the scriped AI that ships with SC2, so it will be pitted in a multi-agent, adversarial battle against a hard-coded bot. Luckily our agent has more than double the number of units that the enemy has, but it will still require formulating a strategy against an adversarial agent that mostly knows what it's doing.

And finally, the environment is known in that the agent knows what the outcomes of its actions will be. The rules of the game are well-defined, although I'm not so sure yet how to separate between hard-coding knowledge into the agent versus having all of that abstracted away for the agent to figure that out. This will come more into play as the tactics will need to become more sophisticated when dealing with the full game.

### Actuators
The agent will influence its environment strictly through the control of the 9 Marine units. The Marine units can be controlled as a lump group of 9, or be controlled with the granularity of any possible subset of surviving Marines. As one would expect, as a Marine unit is destroyed, it is no longer able to be controlled. Importantly, SC2's API has a Actions Per Minute (APM) limiter on it, such that the agent will not be able to perform inhuman levels of control as is possible with other RTS AI research environments. This fact is part of what makes the SC2 research environment particularly interesting -- the focus of our agent should be on discovering solid strategies and adapting to its opponent's rather than being able to technically outmatch its enemies. I've played way too many matches against Super Smash Bros AI that have perfect shield and dodge reflexes to know that this is sooo cheap, boring to play against, and computationally uninteresting.

### Sensors
The SC2 API is pretty clean to pull symbolic information from as there's no need for low-level decoding, and we can directly poll high level information from the API. This means that we'll be able to find the info of our and the enemy's units. We'll be able to read information such as the coordinates, HP, unit types, upgrades, etc. What will be interesting is how the API handles reading from the game state in a larger map. Will it only show information that's currently on camera? Hopefully that's the case so that it will more closely simulate a human playing the game, but I'm sure I'll find out soon enough.

{:.image-with-caption}
![Sensors]({{ site.url }}/assets/defeat_roach_sensors.png){: width="500px"}
_Interpretation of the high level game state the API is seeing (provided by the official library)._

Alright, next up is actually making this damn thing -- it took long enough to write up all of the boiler plate introduction. Stay ready for some updates as I try a bunch of different approaches and fail!

{:.image-with-caption}
![Defeat]({{ site.url }}/assets/defeat_roach_loss.png){: width="500px"}
_tl;dr of the blog. A whole lot of this._

[ai-book]: https://www.amazon.com/Artificial-Intelligence-Modern-Approach-3rd/dp/0136042597
