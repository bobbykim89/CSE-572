# Markov Decision Process
You can think of an oil rig system, which is critical and has many components that can go wrong.
- Lots of step to mitigate fire due to a lot of resources and people.
- If spillage and leakage, then also risk to the environment.
- Need strict policies to contain fire.
- Limited resources and you have multiple criticalities need policies that have maximum impact.
- **Define impact** that needs to maximize:
  - saving lives
  - reducing the damage
  - saving resources
- **Define policies** (over time) that maximize impact:

This is a complex probabilistic decision process, so you use markov decisions.

## why markov?
s1' only depends on current state s1 and action a1. It does NOT depend on past states.

## MDP
You need 4 things:
- S: set of states
  - The current status of the system
  - V &rarr; set of variables
  - each state is a valuation of the variable
  - one example of state: fire alarm true, inminent danger true, non-tenable path true, asst required true
- A: set of actions that you can take (in a particular state)
  - On the example, then you can give asssistance.
  - On each state you can have different actions.
- T: transition matrix (function)
  - T is a function that goes from SXA to S
  - Deterministic transition matrix
    - SXA &rarr; S
    - (s1,a1) &rarr; s1'
  - Probabilistic transition matrix
    - SXA &rarr; P(S)
    - (s1,a1) &rarr; p(s1')
  - To can be probabilistic in case things did not get fixed
- R: set of rewards
  - R is a function that goes from SXA to the real set
  - SXA &rarr; R
  - R(s1,a1) belongs to real set R
  - Reward encourages/discourages certain actions

## AIM
- To define policies $\pi$ 

$\pi: S \rightarrow A$ 

$\pi: (s_1,a_1),(s_2,a_2),(s_3,a_3),...(s_p,a_p)$

Pi is a collection of tuples... given a state what action should we take.
Pi is a policy of mapping states to actions

- to evaluate policies
We use policy so that it has max impact. On oil rig you follow path as you successfully execute step one by one.
Even if you execute it may or not be succesful, hence probability.
  1. calculate the reward (accumulate reward over time)
  2. Choose initial state $s_i$
  3. perform action $pi(s_i)$
  4. use T to go to the current state $s_i'$
  5. Repeat 3.

## problems
You can take two policies and see which one gives best reward.

Execute a policy for infinite time and compare cumulative rewards.
- infinite time == infinite rewards, how to compare?
Solutions:
1. finite horizon analysis (set a point to stop... but when to stop?)
2. discounting reward (if too long in past discount reward), USED VERY OFTEN.
3. Expected reward (instead of cummulative)

## Value function
$V_\pi(s)$ &rarr; total discounted reward if we start from state s and follow policy $\pi$

For a different policy we may have a different:
$V'_\pi(s) \ne V_\pi(s)$

The trick is to find the policy that gives the best value $V_*(s)$


## calculating the value function
Bellman equations : recursive way of evaluating fcns

$$V_\pi(s)=R(s,\pi(s))+\sum_{s'\epsilon s}T(s,\pi(s),s')\gamma V_\pi(s')$$

where

$0 < \gamma < 1$

1. You follow a policy and state to get a reward..
2. then you go to a state s' and use the transition function to get probability to get to s'.
3. Then you can calculate the total expected probability from s' 
4. discount value using discounting factor gamma. Typically gamma is <1.
5. Sum this up for all s' belonging to s.. All the s's that you can go from s.

Then you want to find $\pi$ such that $V_\pi$ is maximized.

## MDP modeling... with markov
1. You fix a policy
2. Execute it for a long time
3. outome is markov chain
