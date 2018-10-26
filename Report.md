[//]: # (Image References)

[image1]: https://github.com/schambon77/DRLND-Navigation/blob/master/rewards.JPG "Plot of Rewards"

# Project 1: Navigation

## Technical Details

### Learning Algorithm

#### Q-Network

The `QNetwork` class implements a fully connected neural network responsible to capture the trained `Module`
mapping an observed state to the optimal corresponding action to take.

| Input Size        | Layer           | Output Size |
| ------------- |:-------------:| -----:|
| 37      |  Fully Connected    | 64 |
| 64      | RELU     |   64 |
| 64 | Fully Connected     |    64 |
| 64      | RELU     |   64 |
| 64 | Fully Connected     |    8 |

#### Agent

The `Agent` class implements an agent as seen in the class material. It references internally a `QNetwork` instance 
and a memory buffer.

The `act` function is passed the current observed state and an epsilon value and returns an action 
chosen by the internal local `QNetwork` according to an epsilon-greedy policy parameterized with the 
epsilon argument value.

The `step` function is passed the past and new states from the environment once the action is taken, 
as well as the corresponding reward. This experience is stored in memory and the `QNetwork` retraining 
is triggered every 4 new experience points acquired. A discount rate of 0.99 is used for the retraining.

The `learn` function implements the `QNetwork` retraining. It uses an Adam optimizer to minimze the MSE
error loss function between expected and target `QNetwork` weights.

#### Training

The function `dqn` implements the training of the agent `Agent`.

The training requires 1000 episodes and takes a few minutes on a standard CPU.

Each episode can last a maximum of 1000 timesteps unless a final `done` state is achieved.

At each timestep, the current `state` is passed to the agent `act` function in order to select the next action 
according to an epsilon-greedy policy.

Upon taking the selected action, the environment provides a new state, a reward and the `done` status.

The new state and reward are passed to the agent `step` function in order for the agent to persist this experience
and learn from it.

A overall score is updated with the obtained reward, and an average of the last 100 scores is 
provided at the end of each episode to give indications of learning progress.

The epsilon parameter decays over the training process from 1 to a minimum of 0.01 with a decay rate of 0.995.

Once all episodes are finished, the model is persisted on disk for further use.

#### Play Demonstration

A short `play` function is implemented to demonstrate over 3 episodes of 200 timesteps max that the agent 
has learnt to collect yellow bananas and leave the blue ones. 

### Plot of Rewards

The diagram shows evolution of the score versus episodes. We can see it reaches a plateau after 500 episodes
around a value of 14.

![Plot of Rewards][image1]

### Ideas for Future Work

The agent training can be further shortened by reducing the number of episodes to 500, as well as 
training on GPU-enabled hardware.

As a future work, the optional proposed exercice of training the agent on pixel images should be looked at.