---
layout: post
title: 'Playing Starcraft for Science'
categories: ai
---

Just last month, Google DeepMind and Blizzard Entertainment jointly released a set of tools which opened up Starcraft 2, an immensely popular RTS game, as an AI research environment. This includes APIs that directly hook into the game itself which allows developers to directly read the symbolic game environment and issue commands, as well as a huge trove of game replays. I'm a huge nerd, and though I've never been very deep into RTS games or Starcraft for that matter, I knew that this could be a great potential project to experiment with AI and solidify some of the theoretical approaches that I'm learning in my current UIUC class.

There's a couple of other popular game AI environments these days, each with their own pros and cons of course. Leading in the pack by a wide margin is [OpenAI Gym][openai-gym], an environment created by the non-profile research led backed by some of Silicon Valley's most famous celebrities. This environment provides a collection of Atari-like games for developers to deploy their agents on and allows them to share their accomplishment and review others'. Recently, Facebook Research released their [ELF][elf] (Extensible, Lightweight, and Flexible) environment which has the huge advantage of not requiring a ton of resources like the other environments. For modern approaches to game AI, this is extremely important as it's very computationally expensive to train these algorithms, and factors like access to GPU computing power and time can often be a huge, if not the main, barrier. And notable to anyone looking to write Starcraft AI, there's a long-running [project][bwapi] to integrate developer-created AI agents into the original Starcraft Brood War. This project is great because it's got a huge community following already, which means there's great resources being passed around as well as an organized, annual tournament.

Ultimately though, I'm choosing to start my first AI project in the SC2 environment due to the fact that I don't want to deal with low-level issues such as representing the symbolic state of the environment from pixels as well as the hella basic fact that SC2 is just an immensely popular game. As of right now at least, I'm more interested in dealing with the logic used in playing the game with optimal strategy rather than how a computer might "see" a pixel stream and interpret that into symbolic knowledge. Additionally, the official API for SC2 seems to be easy enough to use, and so I hopefully won't even have to worry about sending events, navigating menus, etc. And while SC2 seems to be less popular than its predecessor, it has a following on a global scale, has tournaments held every year wtih a cumulative prize pool in the millions, and has a ton of information floating out there on the internet on gameplay mechanics, strategy, metagame, etc. As an avid PC gamer, I feel like this was a very natural choice.

I'm not too sure what the format of this journal will look like, whether it will lean towards being more technical or just a stash for personal retrospection, but I hope you check back on this every now and then.

[openai-gym]: https://gym.openai.com/
[bwapi]: https://github.com/bwapi/bwapi
[elf]: https://github.com/facebookresearch/ELF
