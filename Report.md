# Introduction
The goal of this project is to train agents so that the are reaches to the moving target.

[image1]: https://github.com/sunilnandihalli/drnld-p2/blob/master/ddpg_algo.jpg

# Implemention

This is a off-policy actor-critic method. Both the actors and critics are trained simultaneously. In order to stabilize the training,
we use a target network for both actor and critic. The network that is being learnt is identical to the one that is serving as the target
in terms of architecture of the network. The weights of the network that is being learnt are gradually mixed with those of the target 
network to move the learning forward. The critic network is simply the action value function and the critic drives the learning of the
policy network.

![DDPG algorithm][image1]

## Hyperparamters

Various hyper parameters were tried before settling on the following values
Hyperparameter | Value
--- | ---    
batch_size | 128
gamma | 0.99
tau | 1e-3
lr_actor | 1e-3
lr_critic | 1e-3
update_every | 10

## Network Structures

### Actor

Layer | Dimension
--- | ---
Input | N x 33
Linear Layer, Relu, batch normalization | N x 400
Linear Layer, Relu | N x 300
Linear Layer, Tanh | N x 4

### Critic

Layer | output Dimension | input Dimension
--- | --- | ---
Input | N x 33 | 
Linear Layer, Relu, batch normalization | N x 400 | N x 24
Linear Layer, Relu | N x 300 | N x ( 400 + 4 )
Linear Layer, Leaky Relu | N x 4 | N x 300

## Training Results
The goal was achieved in 104 episodes. The graph is embedded in the ipython notebook.


# Ideas for future work
1. Should implement n-step td-learning to reduce bias.
2. Implement D4PG (distributed distributional deep deterministic policy gradient). This could significantly improve the performance and stability of the algorithm.
