# Project Context: ROS 2 Localization Benchmark

Context for Claude. Read this before helping with anything in this project. (A copy of this file lives in the repo root as `CLAUDE.md`, so Claude Code reads it automatically.)

## Who I am

- **Olafur (Oli) Breki Gudnason.** M.S. in Autonomy (Embodied AI and Robotics Systems) at Purdue, Aug 2026 – May 2028.
- **Background:** B.Sc. in Electrical and Computer Engineering (University of Iceland), post-bacc in CS, and industry ML/automation work at ON Power.
- **Relevant experience I already have:**
  - Python and C
  - ML pipelines
  - Deploying a C inference service on a Raspberry Pi
  - Control theory
  - Sim-vs-real validation work (PowerFactory vs. real grid data at Landsnet)
- **Current coursework:** State Estimation, SLAM, Path Planning, Computer Vision, and the Autonomy Lab (Kalman/particle filtering, optimal control, MATLAB/Simulink). This project should reinforce that coursework, not duplicate homework.
- **Also going on this semester:**
  - Volunteer research in Prof. Upinder Kaur's ARIES Lab (VLA / robot learning, with PhD student Aathman Tharmasanthiran)
  - A course team project, likely bin-picking or smart-factory focused
  - Applying for Summer 2027 internships

## Where I'm starting from

- **New to ROS / ROS 2.** I have never built a ROS package.
- **Linux:** basic level and learning it on purpose through this project.
- **Dev machine:** Windows laptop, 32 GB RAM, integrated graphics only (no dedicated GPU), running Ubuntu 24.04 in WSL2. VS Code connects to WSL. Project files live in the Linux filesystem (`~/ros2_ws`).
- **C++:** I know C well. My modern C++ (templates, smart pointers, Eigen, CMake) is weaker and improving through this project.
- **Hardware on hand:** the laptop above, an old Surface (not used for this), and a Raspberry Pi. No robot yet.

## Why this project exists

1. **Close the ROS 2 gap on my resume.** Almost every robotics posting asks for it.
2. **Turn my estimation coursework into visible code with real numbers.** The EKF and particle filter should be my own implementations, not just configured packages.
3. **Continue my sim-vs-real theme**, ending with the same filters on real hardware.
4. **Stay distinct from the course project.** That one covers manipulation and factory systems; this one covers estimation and navigation.

## Fixed decisions (don't re-litigate unless something is broken)

| Area | Decision |
|---|---|
| Environment | Ubuntu 24.04 in WSL2 on Windows; integrated graphics only |
| ROS | ROS 2 Jazzy |
| Simulator | Gazebo Harmonic (not Gazebo Classic) |
| Robot | TurtleBot3 (Burger or Waffle) in sim |
| Language | C++ (rclcpp) with Eigen for the filters. Python is fine for plotting and evaluation scripts. |
| Architecture | Filter math lives in a plain C++ library with unit tests (no ROS dependency). The ROS 2 nodes are thin wrappers. |
| Ground truth | True pose from Gazebo, bridged into ROS 2 |
| Baselines | `robot_localization` (EKF) and Nav2 AMCL (particle filter) |
| Evaluation | Recorded rosbag2 runs replayed through each filter; trajectory error computed with `evo` |
| Build / packaging | colcon; Docker once v0.1 works |

## How I want Claude to help

- **Teach, don't just produce.** I need to explain every line of this in an interview. When you give me code, explain the key parts and why they're written that way. Point me to the relevant equations from my coursework where it helps.
- **Small steps.** Give me the next concrete step that runs and can be checked, not a 500-line dump. Tell me how to verify it worked (a command, an expected topic or output, a plot).
- **Let me try first when it's math.** For the filter implementations, outline the structure and equations, and let me attempt it before you write the full solution, unless I ask for it directly.
- **Debug systematically.** Ask for the exact error or output, suggest one likely cause at a time, and tell me what command confirms it.
- **Flag version issues.** ROS 2 tutorials online often target Humble or Gazebo Classic. Warn me when advice may not apply to Jazzy and Gazebo Harmonic.
- **WSL2 awareness.** Assume WSL2 with integrated graphics. For GUI or performance problems, consider WSL-specific causes first (graphics driver, D3D12 vs. llvmpipe, files under `/mnt/c`). Prefer headless Gazebo + RViz when the Gazebo GUI is slow.
- **I'm learning Linux.** Explain any shell command before suggesting or running it. During setup, tell me what to run and let me type it myself unless I say otherwise.
- **Division of work.** I write the filter math in `loc_core` myself. Claude Code can handle ROS plumbing (nodes, topics, TF, launch files), CMake/package.xml, Docker, and debugging.
- **Tools.** Claude Code runs as the CLI inside WSL, started from the repo root. The Claude chat project is for math, design, planning, and conceptual debugging. Claude Code is for work in the repo and build/runtime errors.
- **For Claude Code specifically:** I keep command approval on. Keep changes small, say which files you're changing and why, and don't touch the filter logic in `loc_core` unless I ask. If a problem looks conceptual rather than a bug, say so and suggest I work it through in the chat project.
- **Be honest about scope and time.** I'm part-time, with courses, research, and applications going on at once. If a step is a rabbit hole, say so.

## Resume and portfolio rules

- **Only claim what's actually built and working at the time.** No planned features in bullets.
- **Use present tense while in progress** ("Implementing..."), and past tense with real numbers once results exist.
- **Numbers must come from my own recorded runs.** Never estimate them or use placeholders.
- The project goes on my resume once **v0.1** works. See `project_outline.md`.
