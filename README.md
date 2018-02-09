# Deep-Q-Learning-Self-Driving-Car

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
