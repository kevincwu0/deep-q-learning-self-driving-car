# Deep Q-Learning Self Driving Car

### 1. Plan of Attack
  - What is Reinforcement Learning?
  - Bellman Equation (Q-Learning fundamentals)
  - The "Plan" -> How AI Navigate environments
  - Markov Decision Process (MDP) - More sophistication to Bellman Equation
  - Policy vs. Plan - Differences
  - Adding a "Living Penalty" -> add complexity
  - Q-Learning intuition
  - Temporal Differnece -> How do AI agent learn and update
  - Q-Learning Visualization

### 2. What is Reinforcement Learning?
  - Example. Maze -> representation of environments, AI agent will beat (win) against the  environment
  - Agent performs certain actions -> state (params) -> rewards based on it
  - Environments don't have to be mazes, anything in life (e.g. omelette making - (certain actions, taking in states and get rewards))
  - Stock Market -> Environments, Driving Car (Police, leads to negative award)
  - AI -> Simplest example (dog -> biscuits for treat, state is the command, reward) -> AI not that complicated (+1 vs -1) 
  - Robot Dog -> RL no hard-coded programs, RL algorithm, not nothing anything (certain actions you can take, degree of freedom, rewards) 
    - Fall down -1, randomly going forward, more of it by taking right forward, better than pre-programmed dogs.
  - Very different from if and else etc. 
  - Further readings:
    - https://medium.com/emergent-future/simple-reinforcement-learning-with-tensorflow-part-0-q-learning-with-tables-and-neural-networks-d195264329d0
    - http://citeseer.ist.psu.edu/viewdoc/summary?doi=10.1.1.32.7692

### 3. The Bellman Equation
  - Quite complex, slowly to gradually understand it
  - Key Concepts
    - s - State
    - a - Action (action important in a state action combination)
    - r - Reward (for entering into a state)
    - γ - Discount
  - Richard Ernest Bellman (1953 Dynamic Programming inventor)
  - Agent in a maze 
    - grey is a wall
    - green in the finish (R=+1)
    - fire is the firepit (R=-1)
    - Actions (up and down and forward, left)
    - trigger algorithm ("cool I got rewarded, what was the preceding state to get the award, and how did I that state is valuable")
    - V=1 (white square -> right before green square) -> "How do I get to this square?" -> No difference to win
    - Iterate over squares that leads pathway
    - Reward <-> preceding state
    - What if agent -> assigned background (in-between values gets confused)
    - Doesn't work 
  - Bellman Equation
    - V(s) = max(R(s,a) + γV(s'))
      - s current state
      - s' following state you'll be in
      - max is for the many actions you can take
      - R is reward + get into new state
      - Optimal state why we use max
      - γ solves issue where to go
  - Agent in a maze
    - Every white square is a state
    - Discounting (V=0.81, V=0.9, V=1)
    - Discounts further away (time-value of money $5 today vs $5 10 days later)
    - Further away V will be least, artificially creating through gamma, to inspire agents to be closer to goal
    - Three possible values (V=0.9) 
    - Synthetically more valuable state is as closer to goal (sounds basic)
  - Further Reading: https://www.rand.org/content/dam/rand/pubs/papers/2008/P550.pdf

### 4. The "Plan"
  - The "Plan" - Like a treasure map (replace with arrows vs values)
  - Plan vs Policy (similar but there's a trick, they're stochastic)

### 5. Markov Decision Process (MDP)
  - Deterministic vs Non-Deterministic search
  - Deterministic Search -> must go up 100%
  - Non-deterministic search -> 80%, 10%, 10%, stochastic search -> simulate real-world env. randomness not under control with agent
  - MDP: a stochastic process has the Markov property -> future states depending on where you are now not how you got there, we don't care how the agent got there, only matter the present state
  - Framework to do in this environment (MDP) to make decision where to go, just an add on of Bellman equation
  - V(s) = max(R(s,a) + γV(s')) -> V(s) = max(R(s,a) + γΣP(s, a, s')V(s'))
  - Probability of s, a, s' -> Stochastic Non-Deterministic Search -> Represent real-world problems.
  - Applied real-world and really impressive: (fish) http://www.cs.uml.edu/ecg/uploads/AIfall14/MDPApplications3.pdf
  
### 6. Policy vs. Plan
  - Entering the world Stochastic Non-Deterministic Search
  - Random effects in environment that will effect 
  - All numbers go down because of randomness (hit walls etc.)
  - Fire -> 0.9 to 0.39 (because hit the wall or fire pit)
  - Policy is smarter (moves away from fire, rather hit the wall and have a chance to go left or right, 0% fire)
  
### 7. "Living Penalty" 
  - +1 or -1 (simplistic)
  - negative reward no matter where agent goes execept (goal + fire pit) incentive to finish game
  - Policy 0 vs. -0.04. vs. -0.05, -2.0 (so bad, it'll just jump into firepit as less penalty)

### 8. Q-Learning Intuition
  - V(s) = max(R(s,a) + γΣP(s, a, s')V(s'))
  - Why is it called Q-Learning?  
  - Q(s0, a1) -> quality of each action -> Quality vs. Value
  - Quantifiable value of Q, action leads to state
  - Q(s,a) = R(s,a) + γΣ(P(s, a, s') max Q(s', a')) 
  - γΣ(P(s, a, s')V(s')) expected value 
  - discounted value time, expected value, very similar to V but through possible actions rather than values, find optimal one
  - One powerful bellman equation
  - Mathematics: Q-Learning and Q-value Markov Decision Processes: Concepts and Algorithms -> https://pdfs.semanticscholar.org/968b/ab782e52faf0f7957ca0f38b9e9078454afe.pdf

### 9. Temporal Difference
  - Heart and soul of the Q-Learning algorithm
  - Lots of recursion going on
  - TD(a,s) = R(s,a) + γmaxQ(s',a') - Q(s,a)
  - After (R(s,a) + γmaxQ(s',a')) - Before (Q(s,a)
  - Ideally should be the same, empirical evidence, no guarantee due to randomness
  - How to use TD? and why called TD?
  - Difference is time (before and after) is their a shift in time
  - Q(s,a) = Q(s,a) + αTD(a, s)
  - α is alpha, learning rate, how quickly algorithm learning
  - Q(s,a) = Q_t-1(s,a) + αTD_t(a, s)
  - What should've been the Q-Value
  - Q_t(s,a) = Q_t-1(s,a) + α(R(s,a) + γmaxQ(s',a') - Q_t-1(s,a))
  - alpha if 1 negates Q value, 0 just Q-value
  - hopefully converge, closely to 0, new calculated value will equal to previous
  - continue updating Q-Value if environment is changing, optimal policy changes with environment
  - TD helps agent learn about environment slowly
  - https://link.springer.com/article/10.1007/BF00115009

### 10. Q-Learning Visualization
  - Q-values and Policy, CS188 Intro to AI UC Berkeley Pacman Project
  - GridWorld - Q-Value
 

## Deep Q-Learning

### 1. Plan of Attack
  - Deep Q-Learning Intuition (Learning)
    - Neural Networks Learn, update weights based on input, and Q-Learning
    - Temporal Difference concepts into Deep Q-Learning
  - Deep Q-Learning Intuition (Acting)
    - Decide what action to take depending on state
  - Experience Replay
    - Very important addition on top of Deep Q-Learning 
    - Enable Deep Q-Learning to work properly
  - Action Selection Policies
    - Deep Learning agents are able to combine exploration with exploitation
### 2. Deep Q-Learnig Inuition - Learning
  - Q-Learning -> Agents, State, Reward, Environment, Feedback loop, Non-Stochastic Policies
  - Deep Learning -> Add two axis (x1, x2), every state can be described by axis
  - Now we can feed states into Neural Networks (input layer) process through hidden layer, 4 values (Q1, Q2, Q3, Q4)
  - Q-Learning -> gets reward from moving, new state -> empirical Q value, ideally be the same, alpha learning rate
  - Deep Q-Learning -> NN will predict four values (up left, down, right) compare in the previous step, predictive value
  - Deep learning, NN learn from updating weights -> Q-Target1, Q-Target2, Q-Target3 -> Loss = Σ(Q-Target - Q)^2
  - Loss to be as close as possible, stochastic gradient descient to take the loss and backpropagated Loss = Σ(Q-Target - Q)^2, update weight of synapses
  - more and more descriptive of environment (actual q-value, q-target actually observes)
### 3. Deep Q-Learning Intuition - Acting
  - pass through softmax function (from output layer) 
  - best selection best action, highest Q-Value 
  - Feed in RL Neural Network
  - Learning from Q-Values backprop
  - Acting - Softmax and keeps happening
  - https://medium.com/@awjuliani/simple-reinforcement-learning-with-tensorflow-part-4-deep-q-networks-and-beyond-8438a3e2b8df
  - Convolution looks at the image, encoding environments state agent as vector (one-hot encoding), encoding
### 4. Experience Replay
  - Learning -> new state -> updates weights to get etter
  - Acting -> Softmax
  - Experience Replay 
  - False perception -> Neural Network (turns) -> every consecutive states, biases interdependent states
  - Experience Replay -> saved into memory before neural network, randomly selects uniformly distributed sample from experiences and learn from (state, action, reward,etc.) passes through network to break sequential nature of bias
  - valuable rare experience (sharp turns) -> simple neural network, experiences in batches (rolling window)
  - experience replay gives you more experiences (learn faster)
  - breaking pattern of sequential experiences, save rare experiences, learn faster in environments with shortage of experience
  - Google DeepMind - Why are we using a uniform distribution to learn from our batch https://arxiv.org/pdf/1511.05952.pdf
### 5. Action Selection Policies
  - Why wouldn't we take the highest Q-Value
  - Action Selection ϵ-greedy, ϵ-soft(1-ϵ), Softmax
  - Boils down to exploration vs. exploitation - core of reinforcement learning
  - Agent keep learning
  - ϵ-greedy -> select one with best Q-value, except ϵ percent of time (random action, 10% of time for example), less for exploration
  - ϵ-soft (1-ϵ) -> 10% taking Q-value, 90% random
  - softmax -> CNN softmax function, got these values 
  - softmax will take lots of values and squash them between 0 and 1, regardless and will always add up to 1
  - softmax is useful (Q-value some numbers), range of 0 and 1, probabilities add up to 1, now when action is selected
  - apply softmax to preserve exploration, softmax can combine the two, distribution (e.g. 90% take Q2, 5% Q1, 2% Q3, 3% Q4)
  - http://tokic.com/www/tokicm/publikationen/papers/AdaptiveEpsilonGreedyExploration.pdf
