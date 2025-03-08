# Self-Learning Robot Maze Navigator

![Robot Maze Navigation](https://via.placeholder.com/800x400?text=Robot+Maze+Navigation+Simulation)

## Overview

The Self-Learning Robot Maze Navigator is an interactive simulation that demonstrates how a robot can learn to navigate through complex environments using reinforcement learning and few-shot learning techniques. This simulator serves as both an educational tool and a practical platform for developing navigation algorithms that can be transferred to physical robots.

## Features

- **Self-Learning Robot**: The robot autonomously learns to navigate through randomly generated mazes
- **Reinforcement Learning**: Utilizes Q-learning with adaptive parameters for efficient learning
- **Few-Shot Learning**: Remembers successful navigation paths to improve future attempts
- **Sensor Simulation**: Realistic lidar and depth camera sensor simulation
- **3D Visualization**: Toggle between 2D and 3D point cloud visualization of sensor data
- **Data Export/Import**: Save and load learned knowledge for transfer to physical robots
- **Dynamic Maze Generation**: Create random maze configurations for varied learning scenarios

## How It Works

### Learning Process

The robot uses a combination of reinforcement learning and few-shot learning:

1. **Exploration**: Initially, the robot explores the environment randomly
2. **Learning**: It builds a Q-table to associate state-action pairs with expected rewards
3. **Exploitation**: As learning progresses, the robot relies more on its learned knowledge
4. **Memory**: Successful trajectories are stored and reused when encountering similar situations

![Learning Process](https://via.placeholder.com/700x300?text=Learning+Process+Diagram)

### Sensor System

The robot uses two main sensor systems to perceive its environment:

- **Lidar Sensor**: Provides distance measurements in multiple directions around the robot
- **Depth Camera**: Simulates a forward-facing depth sensor similar to Intel RealSense

You can switch between traditional 2D visualization and 3D point cloud visualization to better understand what the robot "sees."

![Sensor Visualization](https://via.placeholder.com/700x300?text=Sensor+Visualization+Comparison)

### State Representation

The robot's perception of the world is encoded as a discrete state:

- Discretized lidar readings
- Relative angle to goal
- Distance to goal

This state representation allows the robot to generalize its learning across similar situations.

### Reward System

The robot learns through a carefully designed reward structure:

- **Positive Rewards**:
  - +15 for reaching the goal
  - Small rewards for moving closer to the goal
  
- **Negative Rewards**:
  - -2.0 for colliding with walls or obstacles
  - -0.05 per step (time penalty)

### Advanced Learning Features

- **Adaptive Learning Rate**: Learning rate decreases over time for better convergence
- **Eligibility Traces**: Rewards propagate to previous actions that led to success
- **Exploration-Exploitation Balance**: Gradually shifts from exploration to exploitation

## Getting Started

### Running the Simulation

1. Open the HTML file in a modern web browser
2. Click the "Start" button to begin the learning process
3. Watch as the robot learns to navigate the maze
4. Use the controls to modify the simulation:
   - "Pause Training" to temporarily halt learning
   - "New Maze" to generate a different maze configuration
   - "Reset Learning" to start learning from scratch

![Simulation Controls](https://via.placeholder.com/700x200?text=Simulation+Controls)

### Monitoring Progress

The simulation provides real-time statistics:

- **Episodes**: Total number of navigation attempts
- **Success Rate**: Percentage of episodes that successfully reached the goal
- **Avg Steps**: Average number of steps taken per episode
- **Learning Mode**: Current learning approach (Few-shot learning)

A log of episode outcomes is displayed at the bottom of the screen.

## Transferring to Physical Robots

One of the key features of this simulation is the ability to transfer learned knowledge to physical robots:

### Exporting Learned Data

1. Train the robot in the simulation until it performs well
2. Click "Export Data" to access the learning data
3. Copy the data to clipboard or download as a JSON file

![Export Data](https://via.placeholder.com/600x300?text=Export+Data+Interface)

### Importing to a Physical Robot

To implement the learned model on a physical robot:

1. Configure the physical robot's sensors to match the simulation parameters:
   - Similar lidar ray configuration
   - Comparable depth camera setup
2. Implement the same state representation system
3. Load the exported JSON data containing the Q-table and successful trajectories
4. Use the same action selection logic, with a lower exploration rate for deployment

## Technical Details

### Learning Algorithm

The simulation uses Q-learning with the following parameters:

```
Learning Rate (α): 0.15 (adaptive)
Discount Factor (γ): 0.9
Initial Exploration Rate: 1.0
Minimum Exploration Rate: 0.1
Exploration Decay: 0.99
```

The Q-update formula:

Q(s,a) ← Q(s,a) + α[r + γ·max Q(s',a') - Q(s,a)]

Where:
- s is the current state
- a is the action taken
- r is the reward received
- s' is the next state
- max Q(s',a') is the maximum expected future reward

### State Space

The state space is constructed from:

- 8 discretized lidar readings (4 discrete values each)
- Discretized angle to goal (4 discrete values)
- Discretized distance to goal (4 discrete values)

This creates a manageable state space that balances specificity with generalization.

### Action Space

The robot can perform three actions:
- Move forward
- Turn left
- Turn right

### Data Format

The exported data includes:

```json
{
  "version": "1.0",
  "timestamp": "2025-03-08T12:00:00.000Z",
  "stats": {
    "episodes": 150,
    "successfulEpisodes": 87,
    "successRate": 0.58,
    "totalSteps": 52684,
    "avgSteps": 351.23
  },
  "learning": {
    "qTable": { /* Q-table data */ },
    "successfulTrajectories": [ /* Trajectory data */ ]
  },
  "config": {
    "lidarRays": 8,
    "depthWidth": 40,
    "stateResolution": 4
  }
}
```

## Version 1.0 Improvements

Version 1.0 introduces several enhancements over the original implementation:

- **Improved Learning**: Added distance-based rewards to guide the robot toward the goal
- **Enhanced State Representation**: Increased precision of lidar data and added distance-to-goal feature
- **Faster Training**: Increased robot speed and reduced episode length for quicker learning
- **Adaptive Learning Rate**: Learning rate decreases over time for better convergence
- **Memory of Previous Success**: Basic eligibility traces to help propagate rewards to previous actions
- **Stronger Incentives**: Increased penalties for collisions and rewards for goal achievement
- **3D Point Cloud Visualization**: Added option to view lidar data as a 3D point cloud

## Future Development Directions

Potential areas for future enhancement:

1. **Dynamic Obstacles**: Adding moving obstacles for more challenging navigation
2. **Multi-Goal Training**: Training with varying goal positions for more generalized navigation
3. **Curriculum Learning**: Progressively increasing difficulty as the robot improves
4. **ROS Integration**: Adding Robot Operating System support for hardware deployment
5. **Sensor Fusion**: Combining lidar and depth data for more robust perception
6. **Deep Reinforcement Learning**: Implementing neural networks for handling more complex environments

## Technical Requirements

The simulation runs in any modern web browser with JavaScript enabled. No additional installations are required.

## License

This project is available under the MIT License.

## Acknowledgments

This simulation was developed to demonstrate reinforcement learning concepts for autonomous robot navigation. It draws inspiration from various research in the fields of robotics, reinforcement learning, and few-shot learning.
