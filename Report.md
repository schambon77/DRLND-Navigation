[//]: # (Image References)

[image1]: https://github.com/schambon77/DRLND-Navigation/blob/master/rewards.JPG "Plot of Rewards"

# Project 1: Navigation

## Technical Details

### Learning Algorithm

#### Q-Network

#### Agent

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



### Plot of Rewards

![Plot of Rewards][image1]

### Ideas for Future Work