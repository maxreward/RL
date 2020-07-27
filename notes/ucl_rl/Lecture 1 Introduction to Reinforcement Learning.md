This is the 1st lecture of David Silver's #reinforcement-learning course.

Lecture video: https://youtu.be/2pWv7GOvuf0

## About Reinforcement Learning
### Faces of Reinforcement Learning
<img src="https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fchrisliu%2F8p26AtVBXq.png?alt=media&amp;token=34e13552-a10b-4aad-907f-f823ae283da2" style="zoom:33%;" />

### Branches of Machine Learning
<img src="https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fchrisliu%2FwVgUc5_SWZ.png?alt=media&amp;token=5a9e87a9-9012-41d3-b80e-17670fbac1b6" style="zoom:33%;" />

### Characteristics of Reinforcement Learning
-   There is no supervisor, only a reward signal

- Feedback is delayed, not instantaneous
- Time really matters (sequential, non i.i.d. data)
- Agent's actions affect the subsequent data it receives

## The Reinforcement Learning Problem
### Reward
- A reward $$R_t$$ is a scalar feedback signal indicating how well agent is doing at step $$t$$
- The agent's job is to maximize cumulative reward
- Reinforcement learning is based on the **reward hypothesis**
    - Definition: All goals can be described by the maximization of expected cumulative reward

### Sequential Decision Making
- Goal: select actions to maximize total future reward
- Actions may have long term consequences
- Reward may be delayed
- It may be better to sacrifice immediate reward to gain more long-term reward

### Agent and Environment
<img src="https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fchrisliu%2F7CSt-lTtsn.png?alt=media&amp;token=a5766dfb-afff-4486-a310-adc29e6a1284" style="zoom:33%;" />

- At each step $$t$$ the agent
    - executes action $$A_t$$
    - receives observation $$O_t$$
    - receives scalar reward $$R_t$$
- The environment
    - receives action $$A_t$$
    - emits observation $$O_{t_1}$$
    - emits scalar reward $$R_{t+1}$$
- $$t$$ increments at environment step

### History and State
- History is the sequence of observations, actions, and rewards
$$H_{t}=O_{1}, R_{1}, A_{1}, \ldots, A_{t-1}, O_{t}, R_{t}$$
- What happens next depends on the history:
    - The agent selects actions
    - The environment selects observations/rewards
- State is the information used to determine what happens next
Formally, state is a function of the history: $$S_{t}=f\left(H_{t}\right)$$

### Environment State
- The environment state $$S^e_t$$ is the environment's private representation
- The environment state is not usually visible to the agent
- Even if $$S^e_t$$ is visible, it may contain irrelevant information

### Agent State
- The agent state $$S^a_t$$ is the agent's internal representation
- It can be any function of history: $$S_{t}^{a}=f\left(H_{t}\right)$$

### Information State
- An information state (a.k.a. Markov state) contains all useful information from the history
- Definition: A state $$S_t$$ is Markov if and only if $$\mathbb{P}\left[S_{t+1} \mid S_{t}\right]=\mathbb{P}\left[S_{t+1} \mid S_{1}, \ldots, S_{t}\right]$$
- "The future is independent of the past given the present"
$$H_{1: t} \rightarrow S_{t} \rightarrow H_{t+1: \infty}$$
- Once the state is known, the history may be thrown away
- The environment state $$S^e_t$$ is Markov
- The history $$H_t$$ is Markov

### Fully Observable Environments
- Full observability: agent directly observes environment state
$$O_{t}=S_{t}^{a}=S_{t}^{e}$$
- Agent state = environment state = information state
- Formally, this is a Markov Decision Process (MDP)

### Partially Observable Environments
- Partially observability: agent indirectly observes environmen
- Agent state $$\neq$$ environment state
- Formally this is a partially observable Markov Decision Process (POMDP)
- Agent must construct its own state representation $$S^a_t$$

## Inside An RL Agent
### Major Components of and RL Agent
- An RL agent may include **one or more** of these components
    - Policy: agent's behavior function
    - Value function: how good is each state and/or action
    - Model: agent's representation of the environment

### Policy
- A policy is the agent's behavior
- It is a map from state to action
- Deterministic policy: $$a = \pi(s)$$
- Stochastic policy: $$\pi(a \mid s)=\mathbb{P}\left[A_{t}=a \mid S_{t}=s\right]$$

### Value Function
- Value function is a prediction of future reward
- Used to evaluate the goodness/badness of states
- And therefore to select between actions, e.g.
$$v_{\pi}(s)=\mathbb{E}_{\pi}\left[R_{t+1}+\gamma R_{t+2}+\gamma^{2} R_{t+3}+\ldots \mid S_{t}=s\right]$$

### Model
- A model predicts what the environment will do next
- Transitions: $$\mathcal{P}$$ predicts the next state
- Rewards: $$\mathcal{R}$$ predicts the next (immediate) reward, e.g.
$$\begin{aligned} \mathcal{P}_{s s^{\prime}}^{a} &=\mathbb{P}\left[S_{t+1}=s^{\prime} \mid S_{t}=s, A_{t}=a\right] \\ \mathcal{R}_{s}^{a} &=\mathbb{E}\left[R_{t+1} \mid S_{t}=s, A_{t}=a\right] \end{aligned}$$

### Categorizing RL Agents
- Value based
    - No policy (implicit)
    - Value function
- Policy based
    - Policy
    - No value function (implicit)
- Actor Critic
    - Policy
    - Value function
- Model-free
    - Policy and/or value function
    - No model
- Model-based
    - Policy and/or value function
    - Model

### RL Agent Taxonomy
<img src="https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fchrisliu%2FlsyUV4qnMN.png?alt=media&amp;token=62961704-03a3-4658-a677-5170b1b23ed2" style="zoom:33%;" />

## Problems within Reinforcement Learning
### Learning and Planning
- Two fundamental problems in sequential decision making
    - Reinforcement learning
        - The environment is initially unknown
        - The agent interacts with the environment
        - The agent improves its policy
    - Planning
        - A model of the environment is known
        - The agent performs computations with its model (without any external interaction)
        - The agent improves its policy

### Exploration and Exploitation
- Reinforcement learning is like trial-and-error learning
- The agent should discover a good policy
- From its experiences of the environment
- Without losing too much reward along the way
- **Exploration** finds more information about the environment
- **Exploitation** exploits known information to maximize reward
- It is usually important to explore as well as exploit

### Prediction and Control
- Prediction: evaluate the future given a policy
- Control: optimize the future (find the best policy)