# Top Reinforcement Learning Algorithms

Reinforcement learning has several algorithms that take different approaches to give rewards to the machine.

One of the biggest **driving forces** in the recent **advancements** in AI has been reinforcement learning (RL). A simple definition of reinforcement learning is to train the machine to act as good as possible by giving it feedback for its action, which implies finding a policy that maximizes the expected return. [RL](https://analyticsindiamag.com/how-to-generate-recommendations-using-reinforcement-learning/) algorithms adopt slightly different approaches to train the agent for its actions. ​​However, to find the optimal policy and value, most of the RL algorithms follow a similar pattern with either a model-free or a model-based approach along with an on-policy or off-policy approach.

All RL algorithms have common terms that need to be understood before diving into the algorithms.

1. **Action** (A): Moves that the agent makes.
1. **State** (S): Current situation in the environment.
1. **Reward** (R): Return sent back from the state to evaluate the last action.
1. **Policy**: Strategy the agent employs for determining the action based on the current state.
1. **Q-value**: Often called the *action value*, it defines the estimation of how good the action taken by the agent is at the state.

Notably, the RL approach to AI was taken further by OpenAI when they introduced reinforcement learning with human feedback (RLHF) that led to the birth of [ChatGPT](https://analyticsindiamag.com/chatgpts-pricing-of-42-month-has-ultimate-question-of-life-the-universe-and-everythingchatgpt-for-42-month-has-answer-to-ultimate-question-of-life-the-universe-and-everything/). OpenAI powered RLHF with the [Proximal Policy Optimization](https://www.assemblyai.com/blog/how-chatgpt-actually-works/) (PPO) algorithm, which they released in 2017 as their baselines repository.

**Q-Learning**

Starting with Q-Learning, which is a model-free and off-policy RL algorithm that is based on the [Bellman Equation](https://www.deeplearningwizard.com/deep_learning/deep_reinforcement_learning_pytorch/bellman_mdp/). The algorithm uses a Q-table, which is a lookup table that stores the agent’s estimated utility or “quality” of taking a certain action in a given state. The agent updates the Q-values to maximise it in the table through trial and error and, eventually, it converges to the optimal policy.

Since it is a model-free algorithm, Q-Learning does not need any space to store all the combinations of actions and states. Furthermore, as this algorithm does not follow a single policy like SARSA (discussed below), it can select the best successor action, which is determined by another policy. This also allows one to incorporate additional influences.

**Q(s,a) ← Q(s, a) + α(r + γ maxₐ’ (s’, a’) — Q(s, a))**

**Q(s, a)** is the current estimate of the utility of taking action ‘**a**’ in state ‘**s’**.
**α** is the learning rate, a value between 0 and 1 that determines the relative weight of the current estimate and the new information.
**r** is the reward received after taking action ‘a’ in state ‘s’.
**γ** is the discount factor, a value between 0 and 1 that determines the importance of future rewards.
**s’** is the next state after taking action ‘a’ in state ‘s’.
**a’** is the action selected in state **s’.**

**SARSA**

[SARSA](https://analyticsindiamag.com/a-complete-intution-on-sarsa-algorithm/), or State Action Reward State Action, is similar to Q-Learning but the key difference is that it is an on-policy algorithm, and is often denoted as the ‘on-policy Q-learning’. This implies that through this algorithm, Q-value is derived from the action performed by the current policy, which is in contrast to the Q-learning algorithm that has no constraint over the next action.

The abbreviated name, SARSA, denotes a sequence that the algorithm starts in a state (S), takes action (A), and then the reward is generated (R). This updates the Q-function (value).

**Q(s,a) ← Q(s, a) + α(r + γ Q(s’, a’) — Q(s, a))**

Now, these obtained Q-values are stored in a table and the one with the highest values is chosen by the policy by observing its current state, leading to a new state, and it continues on for the following conditions. Q-values keep getting updated till we find a good policy. But it is constrained by a single policy, thus Q-learning offers more scope for value selection.

Both Q-learning and SARSA are tabular methods and, due to vast memory consumption and failure to visit all states and actions while training, do not scale well for large state and action spaces. This is where neural networks come in.

**Deep Q Network (DQN)**

DQN is an extension of Q-Learning that leverages neural networks to estimate the Q-value function. This enables it to move beyond the limitations of Q-learning, which cannot estimate value for the unseen states. In 2013, DeepMind even applied DQN to the [Atari Game](https://arxiv.org/pdf/1312.5602.pdf).

The neural network is trained based on the Q-learning update equation:

**Q\_θ(s, a) ← Q\_θ(s, a) + α((r + γ maxₐ’ Qₜₐᵣ(s’, a’)) — Q\_θ(s, a))**

The standard Q-learning technique finds the optimal values, which are the highest rewards, and then developers decide the optimal function. DQN allows direct approximation of the optimal value using two essential techniques:

1. **Experience Relay**: To solve the problem of high correlation and less data efficiency, experience relay allows the sample transitions (moves from one state to another by actions) to be stored. This allows the detection of trends, which are then randomly selected from the pool to update the knowledge.  
1. **Target Networks**: This help determine if the output reward is not already the best one. This is achieved by going back to the last updated output and considering Q-values as the target.

**Deep deterministic policy gradient (DDPG)**

The methods so far cover discrete action spaces with a fixed number of actions. But when the action space is continuous, tabular and neural network-based Q-learning algorithms fall short because finding the action that leads to the highest reward is challenging, if not impossible. DDPG is then considered a breakthrough.

DDPG is an actor-critic algorithm that also uses a neural network to approximate both the policy and the value function. It is particularly well-suited for continuous action spaces. DDPG also borrows the ideas of the target network and experiences replay from DQN.

### **Q\_θ(s, a) ← Q\_θ(s, a) + α((r + γ Qₜₐᵣ(s’, μₜₐᵣ(s’))) — Q\_θ(s,a))**

Instead of manually searching the best state–action pair and the Q-value, another neural network is introduced that learns the approximate maximiser and calculates the target. Here, μₜₐᵣ determines the best action that uses a slightly older version of the network.

**TRPO and PPO**

**Trust Region Policy Optimization (TRPO)** and **Proximal Policy Optimization (PPO)** are both on-policy algorithms that use a neural network to approximate the policy. TRPO uses a trust region method to ensure that the policy update is “conservative” while PPO uses a “clipped” objective function to ensure that the update is not too far from the current policy. Both algorithms are able to handle large, high-dimensional state spaces and continuous action spaces.

TRPO achieves great and consistent high performance, but the computation and implementation of the algorithm is increasingly complicated. [OpenAI released PPO](https://openai.com/blog/openai-baselines-ppo/) in 2017 and since then it has become their default as it got rid of computation problems created by constrained optimization by way of proposing a clipped surrogate objective function.
