# secretary-problem-env
An environment compatible with open-AI gym for the secretary problem


## The problem definition

The secretary problem (also known as the marriage problem, the sultan's dowry problem, the fussy suitor problem, and secretary problem) is a problem that demonstrates a scenario involving optimal stopping theory.

The basic version of the problemn can be stated as follows [[1]](https://en.wikipedia.org/wiki/Secretary_problem): 

* There is a single position to fill.
* There are n applicants for the position, and the value of n is known.
* The applicants, if seen altogether, can be ranked from best to worst unambiguously.
* The applicants are interviewed sequentially in random order, with each order being equally likely.
* Immediately after an interview, the interviewed applicant is either accepted or rejected, and the decision is irrevocable.
* The decision to accept or reject an applicant can be based only on the relative ranks of the applicants interviewed so far.
* The objective of the general solution is to have the highest probability of selecting the best applicant of the whole group. This is the same as maximizing the expected payoff, with payoff defined to be one for the best applicant and zero otherwise.
* A candidate is defined as an applicant who, when interviewed, is better than all the applicants interviewed previously. Skip is used to mean "reject immediately after the interview". Since the objective in the problem is to select the single best applicant, only candidates will be considered for acceptance. The "candidate" in this context corresponds to the concept of record in permutation.

In this project a python code is developed to find the optimal stopping point (stopping point refers to how many applicant are rejected immediately). The method used here is simple Monte-Carlo method.

## The environment

Here we developed an environment compatible with OpenAI Gym environments. The environment is devised for an agent with the following internal state (```time```, ```best-so-far```, ```current```) where:

* ```time``` -- represent the rescaled time-step, i.e the number of interviewed candidates divided by the total number of candidates (N),
* ```best-so-far``` -- the best score of the interviewed candidates, and
* ```current``` -- the score of the current candidate.

By each step, the environment is:
* changing the state to a new state,
* returns a reward,
* send a signal indicating whether the process is terminated or not.

In this implementation two actions are available to the agent:

**Continue (action 0)**: In this case the current candidate is rejected:

   * the state changes:  (i) time is increased by 1/N, (ii) the "best-so-far" variable is changed to max(best-so-far, current), and (iii) the current state is updated to a random value in range [0, 1] 
   * the reward is zero,
   * the process continues, i.e. done = False

**Halt (action 1)**: For this action the current candidate is accepted:

  * the state changes: (i) time is increased by 1/N.
  * the reward is the score of the accepted candidate, and 
  * the process is terminated. Assigning a new state is meaningless here.



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

## requirements
```
python3
numpy
gym
```
