---
layout: default
title: Status
---
(put video here)

## Project Summary
Our original goal was to have the agent (Spartos) learn how to fight against three different types of mobs on the field, altering its battle strategy according to the type of mob encountered (passive mobs, aggressive mobs, endless mobs)

This was scaled down due to feasibility issues. We decided that, out of all the possible battle strategies Spartos could learn from our previous idea, we wanted to prioritize a hyper-aggressive agent that values pursuing enemies as much as possible. Our updated problem formulation is as follows:

__Baseline__:<br>
Spartos learns to kill a single zombie in a small 5x5 arena. This is the simplest case reduction of the final agent we eventually want to train. From here we hope to scale up to a mob of zombies in a larger and potentially varied arena.

__Target__:<br>
After successfully training Spartos to hunt a single enemy, the next step will be to add the complexity of hunting and surviving multiple enemies at once. To accomplish this, we will increase the size of the arena to 20x20 and gradually add more zombies, with a max horde size of 5.

__Goal__:<br>
The ultimate goal for Spartos will be for it to either fight well against a variety of enemies, or in a complicated arena (or potentially both if time allows). We will start by adding different enemies and adding obstacles to the arena separately. If both work reasonably well, we will attempt to merge the 2 environments.

## Approach
We are using Vanilla Policy Gradient to predict actions based on the observation. We've experimented with observing position and position + velocity.


### Vanilla Policy Gradient:
We restructured Arthur Juliani's implementation of Vanilla Policy gradient to work with any environment and save checkpoints etc.

{% raw %}
$$ \nabla_\theta J(\pi_\theta) = \max_{\tau \sim  \pi_\theta} \left[\sum^T_{t=0} \nabla_{\theta}\log \pi_{\theta}(a_t|s_t)A^{\pi \theta}(s_t,a_t)\right]$$ \\
$$ \theta_{k+1} = \theta_k + \alpha \nabla_{\theta}J(\pi_{\theta_k}) $$ \\
{% endraw %}

To achieve our baseline goal, we've spawned the agent, equipped with an enchanted sword, and a single zombie in a flat 5x5 room with no obstacles. Both the agent and the zombie consistently appear at the same location. Notably, the location of the zombie isn't represented anywhere in the agent's observation of the environment.

### State
The algorithm receives as input the state, which is made up of:
- Coordinates of the agent
- Velocity of the agent (sometimes)

### Actions
At any given state, the actions available to the agent are:
["forward 1", "back 1", "left 1", "right 1", "attack 1", "attack 0"]
- Start moving forward
- Start moving backward
- Start moving left
- Start moving right
- Start attacking
- Stop attacking

### Rewards
The agent receives the following rewards for the following events:
- Agent lands successful hit/kill: +400
- Agent takes damage: 
- Agent dies: -1000
- Agent runs out of time: -100
- Time(per agent tick): -1.0

## Evaluation
To evaluate our learning model, we developed two agents that we can compare agent to:  
1. Agent taking random actions (same action space as our agent) throughout an entire duration of an episode.
2. Agent following an algorithm that can form the zombies into a train, and take the ones that get close. This algorithm consists of scoring the importance of each zombie based on their distance to the player, and then using that score to determine which direction the player needs to turn to. In addition to turning, the agent moves backward with a probability of 65%, and for the remaining 35%, the agent decides to strafe left or right with equal probability. 

## Remaining Goals & Challenges
- Put Spartos against a variety of enemies, or a horde of one type of enemy
- Reduce strength of sword so Spartos has to go in for multiple hits
- Add verticality to the arena by adding obstacles and cliffs

## Resources Used
__RL Algorithms__:<br>
- http://incompleteideas.net/book/RLbook2018.pdf
- http://incompleteideas.net/tiles/tiles3.html
- https://medium.com/@awjuliani/super-simple-reinforcement-learning-tutorial-part-2-ded33892c724
- https://spinningup.openai.com/en/latest/algorithms/vpg.html

__Implementation Examples__:<br>
- https://medium.com/emergent-future/simple-reinforcement-learning-with-tensorflow-part-0-q-learning-with-tables-and-neural-networks-d195264329d0
- https://medium.com/@awjuliani/super-simple-reinforcement-learning-tutorial-part-2-ded33892c724
- https://medium.freecodecamp.org/an-introduction-to-deep-q-learning-lets-play-doom-54d02d8017d8?gi=8d7e34546ac3
- https://adventuresinmachinelearning.com/reinforcement-learning-tensorflow/
- https://github.com/openai/gym/blob/master/gym/envs/classic_control/mountain_car.py
