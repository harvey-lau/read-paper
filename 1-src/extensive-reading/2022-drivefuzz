# The Extensive Reading of 2022-[*DriveFuzz: Discovering Autonomous Driving Bugs through Driving Quality-Guided Fuzzing*](https://dl.acm.org/doi/abs/10.1145/3548606.3560558)

- The **problem** is that while safety-critical bugs may exist in any layer and even across layers, relatively little attention has been given to testing the entire driving system across all the layers.
- The **solution** is DriveFuzz, which bases on the real-world traffic rules to detect safety-critical mis-behaviors and guides itself towards such mis-behaviors through driving quality metrics referring to the physical states of the vehicle.

As shown in Figure 1, the layers of autonomous driving system (ADS) consists of:

1. **Sensing**: LiDAR, camera, and GPS.
2. **Perception**: detection, prediction, and localization.
3. **Planning**: global planner and local planner.
4. **Actuation**: path follower.

The input and output of ADS are:

- **Input**: vehicle states, environment, map, and destination.
- **Output**: control commands.

As shown in Figure 2, the architecture and workflow of DriveFuzz includes:

A test case or a input scenario has 4 components:

- **Mission**, defined by the initial and goal positions.
- **Weather**, like sunny, rainy, and cloudy.
- **Actor**, like vehicles or pedestrians acting independently to the ego-vehicle.
- **Puddle** (invisible), affecting the frictional force of the road.

The mis-behavior detector check for the events that are closely related to human safety:

- **Collision**
- **Infraction**, including speeding, invading lanes, and running on red lights.
- **Immobility**

The driving quality metrics are:

- **Hard acceleration/braking**, the ratio of longitudinal acceleration of a vehicle $A_x$ to the gravitational constant $g$. $count(K_{ab} \ge 0.6)$ and $count(K_{ab} \le -0.6)$ are its quantitative indicators.
- **Hard turn**, depending on the lateral speed and steering wheel angle.
- **Over/under-steer**, depending on the steering wheel angle, longitudinal velocity, yaw rate, and lateral acceleration.
- **Minimum distance**, the minimum of distances from the ego-vehicle to all other actors (vehicles or pedestrians) per frame.

The driving quality score is given by their linear combination.

The videos of the bugs found by DriveFuzz are available at <https://www.youtube.com/channel/UCpCrUiGanDKX-qxj8jcUVGQ>.
