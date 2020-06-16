# Markov Decision Process

## Markov Processes

### Introduction to MDPs

-   Markov devision processes (MDPs) formally describe an environment for reinforcement learning
-   The environment is fully observable (i.e., the current state completely characterizes the process)
-   Almost all RL problems can be formalized as MDPs
    -   Optimal control primarily deals with continuous MDPs
    -   Partially observable problems can be converted into MDPs
    -   Bandits are MDPs with one state

### Markov Property

"The future is independent of the past given the present"

>   **Definition**
>
>   A state $S_t$ is Markov if and only if
>   $$
>   \mathbb{P}\left[S_{t+1} | S_{t}\right]=\mathbb{P}\left[S_{t+1} | S_{1}, \ldots, S_{t}\right]
>   $$

-   The state captures all relevant information from the history
-   Once the state is known, the history may be thrown away (i.e., the state is a sufficient statistic of the future)

#### State Transition Matrix

For a Markov state $s$ and successor $s^\prime$, the state transition probability is defined by
$$
\mathcal{P}_{s s^{\prime}}=\mathbb{P}\left[S_{t+1}=s^{\prime} | S_{t}=s\right]
$$
State transition matrix $\mathcal{P}$ defines transition probabilities from all states $s$ to all successor state $s^\prime$,
$$
\mathcal{P}=\left[\begin{array}{ccc}
\mathcal{P}_{11} & \dots & \mathcal{P}_{1 n} \\
\vdots \\
\mathcal{P}_{n 1} & \dots & \mathcal{P}_{n n}
\end{array}\right]
$$
where each two of the matrix sums to 1 (with each row representing the probabilities of state $i$ transitioning to state $j$).

### Markov Process (Markov Chains)

A Markov process is a memoryless random process (i.e., a sequence of random states $S_1, S_2, ...$ with the Markov property.

>   **Definition**
>
>   A Markov Process (or Markov Chain) is a tuple $\langle\mathcal{S}, \mathcal{P}\rangle$
>
>   -   $\mathcal{S}$ is a (finite) set of states
>   -   $\mathcal{P}$ is a state transition probability matrix, $\mathcal{P}_{s s^{\prime}}=\mathbb{P}\left[S_{t+1}=s^{\prime} | S_{t}=s\right]$

## Markov Reward Processes

### Markov Reward Processes (MRPs)

A Markov reward process is a Markov chain with values.

>   **Definition**
>
>   A Markov Reward Process is a tuple $\langle\mathcal{S}, \mathcal{P}, \mathcal{R}, \gamma\rangle$
>
>   -   $\mathcal{S}$ is a finite set of states
>   -   $\mathcal{P}$ is a state transition probability matrix, $\mathcal{P}_{s s^{\prime}}=\mathbb{P}\left[S_{t+1}=s^{\prime} | S_{t}=s\right]$
>   -   $\mathcal{R}$ is a reward function, $\mathcal{R}_{s}=\mathbb{E}\left[R_{t+1} | S_{t}=s\right]$
>   -   $\gamma$ is a discount factor, $\gamma \in[0,1]$



## Markov Decision Processes

## Extentions to MDPs

