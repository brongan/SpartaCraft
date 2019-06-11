---
layout: default
title: Final Report
---
## Spartos Video
(embed vid here)

## Project Summary
Our ultimate goal for this Project in AI course was to create a Minecraft fighter bot, dubbed Spartos, whose survival instincts and tactical skills in the battle arena surpassed all others. In the original planning stages, we had envisioned a bot that was able to conquer 3 types of mobs in the arena: passive mobs, aggressive mobs, and endless mobs.

### Progress Iterations
Over the course of the quarter, we narrowed and refined our problem specifications to create the final iteration of Spartos: a fighter bot who specializes in the efficient eradication of aggressive mobs, specifically an aggressive mob of zombies.

To achieve this goal Spartos, we first distilled the problem to its simplest terms and built up from there. We began with a random agent in a small arena, with a single, non-pursuing zombie as its enemy. As Spartos adapted to this simple environment, we increased the difficulty: increasing the size of the arena, allowing the zombie to pursue Spartos, and increasing the number of zombies spawned.

### An AI Problem
Just on pure observation of the random agent alone, it is clear why AI/ML algorithms are needed for this problem. Even when we broke our problem down to its simplest terms, the random agent struggles with simply locating its opponent (see our Status video for a demonstration of this). And when we scaled our problem up to its final iteration (pursuant enemies in a large field), a random agent could not conceivably or consistently survive. Machine learning is necessary to solve our proposed problem in any significant way; the agent must learn to seek out its enemies, swing its sword when in range, and, if necessary, evade their attacks. (Please see below for specific details of our implementation approach.)

## Approaches
### Algorithm
We are using Vanilla Policy Gradient as our reinforcment learning algorithm. We've experimented with observing position and position + velocity. Currently, we have position and velocity represented as floats for the x and z dimensions.

In our Baseline scenario, the agent receives as its observation solely it's current position. The Vanilla Policy Gradient algorithm predicts action probabilities and an action is selected based on those probabilities. Notably, it observes nothing related to the location of the zombie in the room. Weights are updated every 5 episodes based on the discounted rewards over each episode. 

#### Vanilla Policy Gradient:
We restructured Arthur Juliani's implementation of Vanilla Policy gradient to work with any environment and save checkpoints etc.

Gradient Calculation and Update Equation:

{% raw %}
$$ \nabla_\theta J(\pi_\theta) = E_{\tau \sim  \pi_\theta} \left[\sum^T_{t=0} \nabla_{\theta}\log \pi_{\theta}(a_t|s_t)A^{\pi_\theta}(s_t,a_t)\right]$$
$$ \theta_{k+1} = \theta_k + \alpha \nabla_{\theta}J(\pi_{\theta_k}) $$
{% endraw %}

#### MDP
Using Malmo's "HumanLevelCommands", our agent selects actions analogous to human key presses. It then receives an observation after 4 Minecraft ticks. We discretized time and our action space this way as our goal is to have the agent appear to act as humanly as possible.

### Environment Representation
To achieve our baseline goal, we spawned the agent, equipped with an enchanted sword, and a single zombie in a flat 5x5 room with no obstacles. Both the agent and the zombie consistently appear at the same location. Notably, the location of the zombie isn't represented anywhere in the agent's observation of the environment.

To achieve our final goal, we increased the size of the arena to 30x30, spawned a horde of 12 aggressive zombies and 5 passive cows. We  represent these observations with multiple enemies as gridworlds and added convolutional layer(s) to our neural network.

### State Representation
The algorithm receives as input the state, which is made up of:
- Coordinates of the agent
- Health of agent
- Total health of enemies in a given tile

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
- Agent lands successful hit/kill: +400 (this reward is given to the agent based on damage dealt)
- Agent takes damage (per damage taken): -5
- Agent dies: -1000
- Agent runs out of time: -100
- Agent doesn't run out of time: 200
- Time(per agent tick): -1.0

## Evaluation
We are using the same evaluation metrics as described in the Status Update to evaluate the progress of our improved agent:

Quantitatively, we are evaluating our agent by the total rewards they generate, and by the amount of time it takes for them to complete an episode. Our rewards are simple and clearly imply how many enemies died, and whether the agent died/took damage. We are using a random agent as a baseline, and comparing the random agent with these metrics to the “perfect” agent.

Qualitatively, our goal is for the agent to appear intelligent and behave similarly to a human. We want it to appear to be as close to an efficient killing machine as possible. This means not wasting time attacking nothing, not walking towards enemies, and taking damage. Realistically, this can only be measured by a person watching a video of the agents in action. The “perfect” agent clearly demonstrates a strategy it is using. Please see our video for reference.

(insert graphs here)

## References
### RL Algorithms:
- http://incompleteideas.net/book/RLbook2018.pdf
- http://incompleteideas.net/tiles/tiles3.html
- https://medium.com/@awjuliani/super-simple-reinforcement-learning-tutorial-part-2-ded33892c724
- https://spinningup.openai.com/en/latest/algorithms/vpg.html

### Implementation Examples:
- https://medium.com/emergent-future/simple-reinforcement-learning-with-tensorflow-part-0-q-learning-with-tables-and-neural-networks-d195264329d0
- https://medium.com/@awjuliani/super-simple-reinforcement-learning-tutorial-part-2-ded33892c724
- https://medium.freecodecamp.org/an-introduction-to-deep-q-learning-lets-play-doom-54d02d8017d8?gi=8d7e34546ac3
- https://adventuresinmachinelearning.com/reinforcement-learning-tensorflow/
- https://github.com/openai/gym/blob/master/gym/envs/classic_control/mountain_car.py
