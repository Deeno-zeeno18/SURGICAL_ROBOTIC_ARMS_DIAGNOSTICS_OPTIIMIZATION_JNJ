# Robotic Arm Control System Diagnostics

Virtual Work Experience task at Johnson $ Johson MedTech.
Robotics and Contorl Engineer Intern and Job simulation (Forage)


This notebook was initially a starter from Forage.
## The  Problem
A customer ticket reported delayed responses in a surgical robotic arm,
with rotate_joint flagged as the problem command.

## What I did
- Measured response times for move_arm, rotate_joint and adjust_grip
- Compared them to expected values and documented the discrepancies
- Applied a simulated 20% improvement factor and noted its limits

## Findings
- rotate_joint was the slowest command (0.15 s)
- move_arm and adjust_grip were within expected values
- The optimization was arithmetic only, so a real code change
  and re-measurement is the next step

## Files
- Control_System_Diagnostics_Notebook.ipynb:one of my completed notebooks

## Skills practiced
Python, performance diagnosis, technical reporting
