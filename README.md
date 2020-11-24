# secretary-problem-env
An environment compatible with open-AI gym for the secretary problem


## The problem definition

## The environment

The environment is devised for an agent with the following internal state (```time```, ```best-so-far```, ```current```) where:

* ```time``` -- represent the rescaled time-step, i.e the number of interviewed candidates divided by the total number of candidates (N),
* ```best-so-far``` -- the best score of the interviewed candidates, and
* ```current``` -- the score of the current candidate.

By each step, the environment is:
* changing the state to a new state,
* returns a reward,
* send a signal indicating whether the process is terminated or not.

In this implementation two actions are available to the agent:

0. Continue (action 0): In this case the current candidate is rejected:

 * the state changes:  (i) time is increased by 1/N, (ii) the "best-so-far" variable is changed to max(best-so-far, current), and (iii) the current state is updated to a random value in range [0, 1]

* the reward is zero,

* the process continues, i.e. done = False

1. Halt (action 1): For this action the current candidate is accepted:
  
  the state changes: (i) time is increased by 1/N. ..

...the reward is the score of the accepted candidate, and 

the process is terminated. Assigning a new state is meaningless here.



## Usage

First importing the secretary class

```
from secretary import secretary 
```

 Now instantiate an environment (with ```N``` candidates) with

```
env = secretary(N=20)
```
and reset it immediately:

```
env.reset()
```

Now you can call the common Open-AI Gym APIs: ```step, reset, render, close, and seed```.

Have fun and let me know if you started playing around with this env.
