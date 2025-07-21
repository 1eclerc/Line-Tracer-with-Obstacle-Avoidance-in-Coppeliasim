# 🧭 Line Tracer with Obstacle Avoidance in CoppeliaSim

This project simulates a mobile robot in CoppeliaSim (formerly V-REP) that follows a line and dynamically avoids obstacles using sensor feedback and a PD controller. The simulation is controlled via the ZeroMQ Remote API in Python.

## 🚀 Features

- **Line Following**: Uses 3 vision sensors (left, middle, right) to follow a black line on a surface.
- **Obstacle Avoidance**: Detects obstacles using a proximity sensor and performs a right turn maneuver to avoid them.
- **Search & Realignment**: After avoiding an obstacle, the robot searches for the line and aligns itself to continue following.
- **Live Visualization**:
  - Robot path plotted in real-time.
  - Left and right motor speeds plotted live.
- **Non-blocking Execution**: Uses simulation polling rather than delays for smoother transitions.

## 🛠 Requirements

- Python 3.x
- [CoppeliaSim](https://www.coppeliarobotics.com/)
- Required Python packages:
  ```bash
  pip install numpy opencv-python matplotlib
  ```
- `coppeliasim_zmqremoteapi_client` Python module (provided in CoppeliaSim installation)

## 📁 File Structure

- `06_05_line_tracer_obstacle_nodelay.py`: Main Python script that controls the simulation.
- Sensors and motors expected:
  - `/LeftSensor`, `/MiddleSensor`, `/RightSensor`
  - `/Proximity_sensor`
  - `/Vision_sensor`
  - `/DynamicLeftJoint`, `/DynamicRightJoint`
  - `/LineTracer` (robot base)

## ▶️ How to Run

1. Launch **CoppeliaSim** and load a scene that includes:
   - A line on the floor.
   - The robot with correctly named sensors and motors.
2. Start CoppeliaSim in **remote API server mode**.
3. Run the script:
   ```bash
   python 06_05_line_tracer_obstacle_nodelay.py
   ```

The robot should start moving autonomously, following the line and avoiding obstacles while plotting its movement.

## 🧠 Control Logic Summary

- **Line Following**:
  - Uses a simple PD control logic based on sensor error from the center.
- **Obstacle Detection**:
  - Triggers avoidance if obstacle distance < 0.30m.
- **Avoidance Maneuver**:
  - Right turn → forward → search pattern until the line is found again.
- **Realignment**:
  - Adjusts heading to re-enter FOLLOWING state.

## 📊 Visual Output

- Real-time plot of robot position (X, Y).
- Real-time motor speed graphs (Left & Right).
- Optional live camera feed from `Vision_sensor`.

## 📸 Simulation Snapshots

<img width="561" height="302" alt="image" src="https://github.com/user-attachments/assets/e840355c-7655-4ad7-b8b1-28ea5781deb0" />

<img width="562" height="301" alt="image" src="https://github.com/user-attachments/assets/89cdc009-6150-4af2-b59b-fd58c7625451" />

## 🧩 Notes

- Ensure the object names in the scene match the ones in the script.
- The robot assumes a black line on a white surface.
- ESC key can be used to close the camera feed window.

## 📄 License

This project is provided for educational and research purposes.

## 👥 Contributors

- @1eclerc | [GitHub](https://github.com/1eclerc)
- @ishowkenobi | [GitHub](https://github.com/ishowkenobi)
