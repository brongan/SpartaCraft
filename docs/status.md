---
layout: default
title: Status
---
(put video here)

## Project Summary
Our original goal was to have the agent (Spartos) learn how to fight against three different types of mobs on the field, altering its battle stragegy according to the type of mob encountered (passive mobs, aggressive mobs, endless mobs)

This was scaled down due to feasibility issues. We decided that, out of all the possible battle strategies Spartos could learn from our previous idea, we wanted to prioritize a hyper-aggressive agent that values pursuing enemies as much as possible. Our updated problem formulation is as follows:

__Baseline__:<br>
Spartos learns to kill a single zombie in a small 5x5 arena. This is the simplest case reduction of the final agent we eventually want to train. From here we hope to scale up to a mob of zombies in a larger and potentially varied arena.

__Target__:<br>
After successfully training Spartos to hunt a single enemy, the next step will be to add the complexity of hunting and surviving multiple enemies at once. To accomplish this, we will increase the size of the arena to 20x20 and gradually add more zombies, with a max horde size of 5.

__Goal__:<br>
The ultimate goal for Spartos will be for it to either fight well against a variety of enemies, or in a complicated arena (or potentially both if time allows). We will start by adding different enemies and adding obstacles to the arena separately. If both work reasonably well, we will attempt to merge the 2 environments.

## Approach
We are using policy-based reinforcement learning with Deep Q-Learning to approximate Q values for a discrete action space.

To achieve our baseline goal, we've spawned the agent, equipped with an enchanted sword, and a single zombie in a flat 5x5 room with no obstacles.

### State
The algorithm receives as input the state, which is made up of:
- Health of the agent
- Coordinates of the agent
- Coordinates of the enemies
- Elapsed time of episode

### Actions
At any given state, the actions available to the agent are:
- Start moving forwards
- Start moving backwards
- Stop moving
- Start turning left
- Start turning right
- Stop turning
- Attack

### Rewards
The agent receives the following rewards for the following events:
- Agent lands successful hit/kill: +40
- Agent takes damage: -5
- Agent dies: -40
- Agent survives a state: +0.03
- Proximity reward (not yet implemented; may need to add to increase the aggressiveness of the agent)

## Evaluation

## Remaining Goals & Challenges
- Put Spartos against a variety of enemies, or a horde of one type of enemy
- Reduce strength of sword so Spartos has to go in for multiple hits
- Add verticality to the arena by adding obstacles and cliffs

## Resources Used
__RL Algorithms__:<br>
- http://incompleteideas.net/book/RLbook2018.pdf
- http://incompleteideas.net/tiles/tiles3.html

__Implementation Examples__:<br>
- https://medium.com/emergent-future/simple-reinforcement-learning-with-tensorflow-part-0-q-learning-with-tables-and-neural-networks-d195264329d0
- https://medium.freecodecamp.org/an-introduction-to-deep-q-learning-lets-play-doom-54d02d8017d8?gi=8d7e34546ac3
- https://adventuresinmachinelearning.com/reinforcement-learning-tensorflow/
- https://github.com/openai/gym/blob/master/gym/envs/classic_control/mountain_car.py
