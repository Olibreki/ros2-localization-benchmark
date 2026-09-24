# Progress Log

## 2026-09-23/24 — Phase 0: environment, sim, and first Nav2+AMCL goal

**What worked:**
- Full stack installed: ROS 2 Jazzy, Gazebo Harmonic + ros_gz, Nav2, TurtleBot3 sim packages.
- Wrote a custom headless launch file (custom_launch/turtlebot3_world_headless.launch.py)
  after discovering the stock TurtleBot3 launch file unconditionally starts a GUI client
  with no disable flag.
- Built a map with slam_toolbox by driving the robot via teleop; saved to
  maps/turtlebot3_world_map.{pgm,yaml}.
- Bridged Gazebo ground truth pose into ROS 2 via ros_gz_bridge.
- Launched Nav2 + AMCL against the saved map, set an initial pose via RViz's
  "2D Pose Estimate," and successfully sent a goal via "2D Goal Pose." Nav2
  planned a path and the controller drove the robot to it.

**What broke, and the actual fixes:**
- WSL2 DNS failing on apt: Tailscale MagicDNS conflict, fixed with
  `tailscale set --accept-dns=false`.
- Nav2 crashing with fastcdr symbol error: base ROS 2 install was months
  out of date. Fixed with `sudo apt upgrade`.
- "Frame [map] does not exist": AMCL needs an initial pose estimate before
  it broadcasts map->odom. Root cause of most downstream TF/RViz issues.
- TurtleBot3 launch file always spawns a GUI client with no disable arg;
  wrote a custom launch file without it.

**Still open / next session:**
- GitHub repo created locally, not yet pushed.
- Camera/vision sensor fusion deliberately deferred (scope discipline).
- Next milestone: starting loc_core, the EKF implementation.
EOFcat > PROGRESS.md << 'EOF'
# Progress Log

## 2026-09-23/24 — Phase 0: environment, sim, and first Nav2+AMCL goal

**What worked:**
- Full stack installed: ROS 2 Jazzy, Gazebo Harmonic + ros_gz, Nav2, TurtleBot3 sim packages.
- Wrote a custom headless launch file (custom_launch/turtlebot3_world_headless.launch.py)
  after discovering the stock TurtleBot3 launch file unconditionally starts a GUI client
  with no disable flag.
- Built a map with slam_toolbox by driving the robot via teleop; saved to
  maps/turtlebot3_world_map.{pgm,yaml}.
- Bridged Gazebo ground truth pose into ROS 2 via ros_gz_bridge.
- Launched Nav2 + AMCL against the saved map, set an initial pose via RViz's
  "2D Pose Estimate," and successfully sent a goal via "2D Goal Pose." Nav2
  planned a path and the controller drove the robot to it.

**What broke, and the actual fixes:**
- WSL2 DNS failing on apt: Tailscale MagicDNS conflict, fixed with
  `tailscale set --accept-dns=false`.
- Nav2 crashing with fastcdr symbol error: base ROS 2 install was months
  out of date. Fixed with `sudo apt upgrade`.
- "Frame [map] does not exist": AMCL needs an initial pose estimate before
  it broadcasts map->odom. Root cause of most downstream TF/RViz issues.
- TurtleBot3 launch file always spawns a GUI client with no disable arg;
  wrote a custom launch file without it.

**Still open / next session:**
- GitHub repo created locally, not yet pushed.
- Camera/vision sensor fusion deliberately deferred (scope discipline).
- Next milestone: starting loc_core, the EKF implementation.
-Next milestone: starting loc_core, EKF
