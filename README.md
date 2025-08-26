# Code-for-Evaluating-Reinforcement-Learning-Algorithms-for-Navigation-in-Simulated-Robotic-Quadrupeds
This research/code explores the effectiveness of three different types of reinforcement learning  algorithms in training a simulated quadruped robot for autonomous navigation and obstacle avoidance.
Welcome to the simulation project for training a robotic guide dog using reinforcement learning algorithms (PPO, DQN, and Q-learning) in Webots.

This README provides setup and usage instructions for running the robot in different environments, including static and dynamic obstacle settings.

---

# Project Structure

Ensure you unzip the project archive and maintain the original folder structure. This is essential for Webots to correctly reference controller paths and resources.

Code-for-Evaluating-Reinforcement-Learning-Algorithms-for-Navigation-in-Simulated-Robotic-Quadrupeds/

├── simple_environment/

│   ├── PPO/  (same internal layout as below)

│   ├── DQN/

│   └── Q/

└── dynamic_environment/

    ├── PPO/
    
    │   ├── controllers/
    
    │   │   ├── run_ppo/               # robot controller + PPO training/eval code
    
    │   │   ├── run_pedestrian/        # (dynamic env) moving obstacle controller
    
    │   │   └── supervisor_controller/ # episode reset, metrics, IPC
    
    │   └── worlds/
    
    │       ├── bioloid_dog.wbt
    
    │       └── bioloid_dog_complex.wbt
    
    ├── DQN/
    
    │   ├── controllers/
    
    │   │   ├── run_dqn/               # robot controller + DQN (replay, target net)
    
    │   │   ├── run_pedestrian/
    
    │   │   └── supervisor_controller/
    
    │   └── worlds/
    
    │       ├── bioloid_dog.wbt
    
    │       └── bioloid_dog_complex.wbt
    
    └── Q/
    
        ├── controllers/
        
        │   ├── run_q/                 # robot controller + tabular Q-learning
        
        │   ├── run_pedestrian/
        
        │   └── supervisor_controller/
        
        └── worlds/
        
            ├── bioloid_dog.wbt
            
            └── bioloid_dog_complex.wbt



---

# Setup Instructions

1. **Open Webots**  
   Launch the Webots simulator (ensure it's installed – tested with Webots R2025a (I think you can have other versions but this one is the latest version and the same one I used.)).

2. **Load a World File**  
   Open a world file from the `/worlds/` directory:
   - `simple_environment.wbt` – Static map
   - `dynamic_environment.wbt` – Moving obstacles, includes dynamic pedestrian robot

3. **Assign the Correct Controller(s)**  
   - In the **Scene Tree**, click on the **Bioloid robot** node.
   - Under the `controller` field, select the appropriate controller:
     - `run_ppo` (for PPO-based control)
     - `run_dqn` (for Deep Q-Network control)
     - `run_qlearning` (for table-based Q-learning)
   - **Important:** The name of the controller must match the folder name inside `/controllers/`.

   If using `dynamic_environment.wbt`:
   - Also assign a controller to the **Pedestrian** robot (e.g. `run_pedestrian` if required).

4. **Run the Simulation**
   - Click the **Play** button in Webots to start.
   - The agent will begin navigating using the selected algorithm.

---

## Notes

- Controller names **must match** the controller folder names exactly for Webots to load them properly.
- If the robot doesn't move:
  - Make sure you've selected the correct controller.
  - Check terminal output for warnings/errors (e.g., `generic` controller, invalid state etc).
- Training was ran on a capped 20,000 episodes (which isn't nearly enough for PPO and DQN to truly benefit on the dynamic maps.) PPO and DQN use neural networks, so learning takes time. I have deleted all pre-trained models as there were thousands for each algorithm in each environment (as expected approx 20,000) which was taking up space, and ran at a cap. So please allow training from scratch.
- Simulation speed may vary based on your computer's processing power – complex environments can take longer to run, expect issues with the amount of computational power required. Also running over GPU will cause less strain than CPU.

---

## Algorithms

| Controller | Description |
|------------|-------------|
| `ppo`      | Actor-Critic based PPO algorithm (on-policy, continuous or discrete) |
| `dqn`      | Deep Q-Network using experience replay (off-policy) continuous or discrete|
| `q_learning` | Classic Q-learning with discrete state/action mapping discrete only|

---

Made with love (and a lot of tears) the University of Hertfordshire MSc AI & Robotics programme.

### For citation please note:

preferred-citation:
  - type: article
  - title: Evaluating Reinforcement Learning Algorithms for Navigation in Simulated Robotic Quadrupeds
  - authors:
    - family names: Harrison
    - first names: Emma
  - license: Apache-2.0
  - journal: arXiv
  - year: 2025
  - url: (http://arxiv.org/abs/2507.13277)
