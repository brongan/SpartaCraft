---
layout: default
title: Proposal
---

## Summary of the Project
Our idea is to create a gladiator arena for Spartos(our agent) to fight against multiple mobs. We plan to have 3 mission types: 
- fighting against passive mobs,
- fighting against hostile mobs,
- fighting against an endless horde of enemies.

### Main Idea
The battle will occur in a destructible arena. We have goals corresponding to our 3 mission types:
- Passive Mobs: The goal is for Spartos to kill all enemies as fast as possible. 
- Hostile Mobs: The goal is for Spartos to kill all enemies as fast as possible while losing as little health as possible.
- Endless Horde: The goal is for Spartos to survive as long as possible. 

### Input/Output Semantics
As input the agent will receive a grid view of the surrounding world, as well as the agent's current heatlh and inventory.
Actions for the agent will be generated as output.
At present, we are deciding between 2 different methods for representing the environment space:
- The actions will be the optimal move for the agent to make given the current environment, e.g. move away or build shelter to evade attack, attack the enemy, switch weapons, etc.
- The action space will be a reasonable subset of Malmo's HumanLevelCommands.

### Applications

Our application would be entertainment on a Minecraft Server or for a Youtube video. 

<!-- ### Instructions
In a paragraph or so, mention the main idea behind your project. Focus on the problem setup, not the solution, i.e.
what is your goal? At the very least, you should have a sentence that clearly explains the input/output semantics
of your project, i.e. what information will it take as input, and what will it produce. Mention any applications, if
any, for your project. -->

## AI/ML Algorithms
Policy-based reinforcment learning with a neural function approximator for a discrete action space.

 <!-- In a single sentence, mention the AI and ML algorithm(s) you anticipate using for your project. It does not
have to be a detailed description of the algorithm, even the sub-area of the field is sufficient. Examples of this
include “planning with dynamic programming”, “reinforcement learning with neural function approximator”,
“deep learning for images”, “min-max tree search with pruning”, and so on. -->

## Evaluation Plan

<!-- Paragraph 1: Quantitative evaluation: what are the metrics, what are the baselines, how much do you expect your approach to improve the metric by, what data will you evaluate on, etc.

Paragraph 2: Describe what qualitative analysis you will show to verify the project works; what are the sanity cases; what's the "moonshot case?" -->

- Mission 1(Passive) Metrics:
    - Time to Kill All Enemies:
        - Baseline: The time for a naive agent(doing random actions) to complete the mission will be ~infinity.
        - Human Score: The team will each do 10 runs of the mission and compute how fast a human can kill all enemies.
        - Improvement: We expect the agent to lower time to kill all enemies to within an order of magnitude of a human.

- Mission 2(Aggressive) Metrics:
    - Time to kill
        - Baseline: Infinity. We expect a naive agent to die.
    - Health lost
        - Baseline: We expect a naive agent to lose all health.
        - Human Score: The team will each do 10 runs of the mission and compute on average how much health is lost per battle.
        - Improvement: We expect the agent to survive a round of battle.    

- Mission 3(Endless) Metrics:
    - Survival Time
        - Baseline: We expect a naive agent to die with in ~5 seconds depending on our enemy and environement specifics.
        - Human Score: The team will each do 10 runs of the mission and compute long a human can survive in our gladiator arena environment.
        - Improvement: We expect the agent to lower the time to kill all enemies to within an order of magnitude of a human depending on the environment.

For qualitative analysis, we would like to get close/surpass Human Score levels for each mission type.


## Appointment
Monday, April 22
10:45AM - 11:00AM
