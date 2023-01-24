---
tags: 
course: CS2109S
type: lecture
---
Date:: 2022-08-12 Friday
Links: [[CS2109S]]
- - -
## Questions/Cues
###### Question 1: Difference between performance measure and utility function?

Performance measure: Used by an outside observer to evaluate success. Functions from histories to real numbers.

Utility function: Used by the agent itself to evaluate how desirable states and histories are. Functions from states to real numbers.

They could be the same in some cases but it's not necessarily true. Also a performance measure exists always but a utility function might not.

###### Question 2: An agent with partial information about the states cannot be perfectly rational?

False. Perfect rationality refers to the ability to make good decisions *given the sensor information received.* So it CAN be perfectly rational.

###### Queston 3: Every agent is rational in an unobservable environment. 

False. Some actions are stupid—and the agent may know this *if it has a model of the environment*—even if one cannot perceive the environment state.

###### Question 4: Consider a task in which an agent plays rock-paper-scissors against a human multiple times with no clock. The task environment(s) is/are: 
a) Deterministic
b) Stochastic
c) Static
d) Discrete

ANS: b, c, d
## Notes

##### Turing Test: 
- Human has to decide if its a human or AI.
- If the human cannot tell reliably, AI passes the test.
- Example of a crazy AI: [[GPT-3]]

##### Intelligent Agent:
- Perceive environment through sensors
- Act on environmnent through actuators
- A **percept** refers to the agent's perceptual inputs at any given instant?

##### Function: 
`f: P -> A` (percept to action)

Transition funtion: `T(state, action) → Next state`. An example is  The Cannibal problem is tutorial 1.

##### Performance measure:
- Best for whom?
- Optimization
- Info
- Unintended effect
- Costs?
  
##### Rational agent: 
- Choose actions to *maximize performance measure*
- Sometimes agent may do sth *not optimal to learn more info for future* optimization → **Information gathering** and **exploration**
- Agent is *autonomous* if its behavior is determined by its own experience. It should learn what it can do to compensate for partial or false prior-knowledge.

##### PEAS 

**P**erformance Measure, **E**nvironment, **A**ctuator, **S**ensor

For self-driving car:
- **Performance Measure**: Safe, fast, legal, comfortable trip, maximize profits.
 - **Environment**: Roads, other traffic, pedestrians, customers.
 - **Actuators**: Steering, accelerator, brake, signal, horn, display.
 - **Sensors**: Cameras, sonar, speedometer, GPS, odometer, accelerometer, engine sensors, keyboard.

![[Pasted image 20220822190425.png]]

##### Characteristics of environment:
1. Fully/Partially *observable*
2. *Deterministic*/Stochastic (?)
	- Deterministic means nothing is by chance: a uniqueness in the agent’s current state completely determines the next state of the agent (eg: chess)
	- Stochastic means purely by probability and chance (rock paper scissor)
3. *Episodic*/Sequential 
	- Episodic: There is no dependency between current and previous states. In each state, agent receives inputs from env and perform corresponding actions → Pick and Place vacuum cleaner: if current room is dirty, suck.
	- Sequential:  Previous decisions can affect all future decisions → Chess
	- Do we care abt what happened the past? Yes then sequential, No then episodic → Really depends on how you define your goal
	- Sequential allows us to do [[Backtracking]]
4. *Static*/Dynamic
	- Unchanging while the agent is deliberating
	- Semi-Dynamic: env does not change but the agent's performance does (Blitz chess)
5. *Discrete*/Continuous
	- Discrete = a limited number of distinct, clearly defined percepts and actions
6. *Single*/Multi Agent

##### Agent Functions:

An agent is specified by the *agent function*. 

Table-lookup agent: 
- EG: Tic-Tac-To
- We just have to look up the states in the look-up table because the states are very little.
- Drawbacks:
	- Storage
	- No autonomy/Cannot react to change
	- Need a long time to compute/learn the table entries

##### Some Models for Agent organization (*increasingly complex*)

1. Simple reflex agent (suck robot, sus bro)
2. Model-based reflex agent (Some internal model shit to consider state of the env)
3. Goal-based agent (Actions based on goals)
4. Utility-based agent (no clear goal, just maximise utility)
5. Learning agent (theres a critic with constant feedback, the more info fed the more efficient the AI)

- A learning agent **may not** maximize performance measure! No one-size-fit-all ans
- Exploitation vs exploration?
	- When to maximize utility
	- When to gain info

## Summary
Agent, Agent model, PEAS

## PDF
![[Lecture+1-Introduction+to+CS2109S+and+AI.pdf]]