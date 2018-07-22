
[//]: # (Image References)
[image1]: ./images/reward_plot.png "Reward Plot"

### Project Overview

The goal of this project is to  train an agent to navigate (and collect bananas!) in a large, square world.

A reward of +1 is provided for collecting a yellow banana, and a reward of -1 is provided for collecting a blue banana. Thus, the goal of your agent is to collect as many yellow bananas as possible while avoiding blue bananas.

The state space has 37 dimensions and contains the agent's velocity, along with ray-based perception of objects around the agent's forward direction. Given this information, the agent has to learn how to best select actions. Four discrete actions are available, corresponding to:

0 - move forward.
1 - move backward.
2 - turn left.
3 - turn right.
The task is episodic, and in order to solve the environment, your agent must get an average score of +13 over 100 consecutive episodes.

### Environment Setup

This project makes use of Unity ML Framework for training and visualisation. The README has detailed instructions for installing dependencies ad setting up the environment.

### Implementation

The reinforcement learning agent is implemented using Agent class. It contains the methods to interact with the environment and learn from the environment.

Deep Q Network Learning Algorithm has been used to train the agent. Deep Q Network works as a function approximator that maps agent's states to action. The reinforcement learning agent uses Deep Q Network to predict next set of action based on the current state. DQN learning makes the use of epsilon greedy policy selection to explore the environment or exploit the already learned Q-values by selecting theactions that maximises Q value. The epsilon probability is decreasing suggesting the agent exploits more in the later episodes. During the inference, epsilon value needs to be zero because the agent is not suppose to explore the environment space. DQN is meant to solve discrete action space. It also stabilises the prediction utilising a replay of previous experiences stored in memory utilising ReplayBuffer class.

#### DQN Algorithm
The `dqn()` function contains the implementation of the following DQN Learning Algorithm:
1. Fill the Replay Buffer
2. For each episode
    - Find an action using Epsilon Greedy Policy
    - Evaluate the next state and reward by performing the action on the environment
    - Add the Action-State pair in replay buffer
    - Update the prediction QNetwork, and for every fourth run update the traget QNetwork.
    - Repeat steps till the game is over (done = true)

#### Deep Q Network
The Deep Q Network approximates the value function. It has been implemented as `QNetwork` class.  The implementation contains a simple three layered feed forward network. The input layer has 37 units, the two hidden layers have 64 units each and the output layer has 4 units, one for each action.

#### Training Hyperparameters
Follwing hyperparameters were used to train the network using dqn algorithm

Replay Buffer size: 100000. It will be used to intially store the random game and then teach the network by choosing random samples from it.
Batch size: 64. The number of samples taken at a time for training.
Discount Factor: 0.99. Relative importance the network gives to the future rewards. A large value means the agent will choose the actions which maximize the future rewards sometime even sacrificing the current reward.
Learning rate: 0.0005 It is a very slow learning rate to ensure stability. It is used by the network to update the weights via back propagation.
Update every: 4. Episodes elapsed between updates to the target QNetwork.

#### Reward Plot

Training with the above QNetwork implementation and chosen hyperparameters solved the environment in 656 episodes with an average score of 15.03
![Reward Plot][image1]

### Future Ideas
As a next evolutionary step to the implementation of the simple DQN, It would be great to try out Duelling DQN and Double DQN to see its impact on performance and stability. It would also be interesting to use prioritized experience replay, so as to replay important transitions more frequently, and therefore learn more efficiently as mentioned [here](https://arxiv.org/abs/1511.05952)






