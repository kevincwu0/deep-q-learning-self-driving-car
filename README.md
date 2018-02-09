# Deep-Q-Learning-Self-Driving-Car

1. Plan of Attack
  - What is Reinforcement Learning?
  - Bellman Equation (Q-Learning fundamentals)
  - The "Plan" -> How AI Navigate environments
  - Markov Decision Process (MDP) - More sophistication to Bellman Equation
  - Policy vs. Plan - Differences
  - Adding a "Living Penalty" -> add complexity
  - Q-Learning intuition
  - Temporal Differnece -> How do AI agent learn and update
  - Q-Learning Visualization

2. What is Reinforcement Learning?
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
