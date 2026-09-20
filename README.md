# VitaBoy V1 Description (URDF & MJCF)

## Overview

This package includes a humanoid robot description (URDF & MJCF) for the **VitaBoy V1** robot — a 29-DoF full-size humanoid with a 6-DoF leg pair, a 3-DoF waist and a 7-DoF arm pair.

MJCF/URDF for the VitaBoy V1 robot:


| MJCF/URDF file name | dof#leg | dof#waist | dof#arm | dof#neck | dof total |
| ------------------- | :-----: | :-------: | :-----: | :------: | :-------: |
| `vita_boy_29dof_v1` |   6*2   |     3     |   7*2   |  fixed  |    29    |

The `neck_yaw_joint` and `neck_pitch_joint` exist in the model but are **fixed** (not actuated), as is `d335_joint` (the head camera mount). The head therefore contributes geometry and inertia only — it is not part of the 29 DoF.

## Directory structure

```
vita_boy/
├── urdf/
│   └── vita_boy_29dof_v1.urdf
├── xml/
│   └── vita_boy_29dof_v1.xml
└── meshes/
```

## Actuator / joint order

The 29 actuators are declared in this order. The index is the position in `ctrl`, `qpos[7:]`, `qvel[6:]` and in the sensor arrays.

#### Lower body — left leg


| # | Joint                    | Axis |
| :-: | ------------------------ | :--: |
| 0 | `left_hip_pitch_joint`   |  Y  |
| 1 | `left_hip_roll_joint`    |  X  |
| 2 | `left_hip_yaw_joint`     |  Z  |
| 3 | `left_knee_joint`        |  Y  |
| 4 | `left_ankle_pitch_joint` |  Y  |
| 5 | `left_ankle_roll_joint`  |  X  |

#### Lower body — right leg


| # | Joint                     | Axis |
| :-: | ------------------------- | :--: |
| 6 | `right_hip_pitch_joint`   |  Y  |
| 7 | `right_hip_roll_joint`    |  X  |
| 8 | `right_hip_yaw_joint`     |  Z  |
| 9 | `right_knee_joint`        |  Y  |
| 10 | `right_ankle_pitch_joint` |  Y  |
| 11 | `right_ankle_roll_joint`  |  X  |

#### Waist


| # | Joint               | Axis |
| :-: | ------------------- | :--: |
| 12 | `waist_yaw_joint`   |  Z  |
| 13 | `waist_roll_joint`  |  X  |
| 14 | `waist_pitch_joint` |  Y  |

#### Upper body — left arm


| # | Joint                       | Axis |
| :-: | --------------------------- | :--: |
| 15 | `left_shoulder_pitch_joint` |  Y  |
| 16 | `left_shoulder_roll_joint`  |  X  |
| 17 | `left_shoulder_yaw_joint`   |  Z  |
| 18 | `left_elbow_joint`          |  Y  |
| 19 | `left_wrist_roll_joint`     |  X  |
| 20 | `left_wrist_pitch_joint`    |  Y  |
| 21 | `left_wrist_yaw_joint`      |  Z  |

#### Upper body — right arm


| # | Joint                        | Axis |
| :-: | ---------------------------- | :--: |
| 22 | `right_shoulder_pitch_joint` |  Y  |
| 23 | `right_shoulder_roll_joint`  |  X  |
| 24 | `right_shoulder_yaw_joint`   |  Z  |
| 25 | `right_elbow_joint`          |  Y  |
| 26 | `right_wrist_roll_joint`     |  X  |
| 27 | `right_wrist_pitch_joint`    |  Y  |
| 28 | `right_wrist_yaw_joint`      |  Z  |

Index ranges by group: **0–11 lower body** (6 DoF per leg), **12–14 waist**, **15–28 upper body** (7 DoF per arm).

## Sensors (MJCF)


| Sensor             | Count | Note                                    |
| ------------------ | :---: | --------------------------------------- |
| `jointpos`         |  29  | one per actuated joint,`<joint>_pos`    |
| `jointvel`         |  29  | one per actuated joint,`<joint>_vel`    |
| `jointactuatorfrc` |  29  | one per actuated joint,`<joint>_torque` |
| `framequat`        |   1   | base orientation                        |
| `gyro`             |   1   | base angular velocity                   |
| `accelerometer`    |   1   | base linear acceleration                |

## Visualization with [MuJoCo](https://github.com/google-deepmind/mujoco)

1. Open the MuJoCo viewer:

   ```bash
   pip install mujoco
   python -m mujoco.viewer --mjcf=vita_boy/xml/vita_boy_29dof_v1.xml
   ```

## License

This project is licensed under the [Apache License 2.0](LICENSE).
