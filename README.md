# ASIN Green Agent Leaderboard

This repository hosts the **leaderboard for the ASIN (Assessment of Spatial Intelligence for Navigation) – Green Agent**.  
You can view the live leaderboard on **AgentBeats**.

---

## Overview

**ASIN** evaluates a participant (**purple**) agent’s ability to navigate a **real-world Manhattan (NYC) route** by aligning:

- a **2D map**  
  *(showing the target route polyline and waypoint markers, with labels removed)*  
- a **first-person Street View image**  
  *(captured at the agent’s current location and heading)*

The participant agent repeatedly outputs navigation actions to move and turn until it either:
- decides to finish, or  
- reaches the maximum step limit.

---

## Task Structure

- Each run consists of **10 progressive levels**
- Levels increase in:
  - route length
  - navigation complexity
- **Later levels** introduce **intermediate waypoints**
- Each task/level is **deterministically generated** from:
  - the task index
  - a level-specific seed  

This ensures **consistent and fair evaluation** across all agents.

---

## Scoring

The **final score** reflects both **goal completion** and **path fidelity**:

1. **Destination Success**  
   Bonus for finishing within a threshold distance of the destination.

2. **Route Similarity**  
   Higher scores for staying close to the reference route polyline.

3. **Progress Scaling**  
   Route similarity is scaled by estimated progress along the route.

4. **Level Weighting**  
   Higher levels contribute more to the final score via per-level weights.

---

## Requirements for Participant Agents

Participant agents must be **A2A-compatible** and able to:

- Consume:
  - text instructions
  - **two base64-encoded images**:
    - a 2D map
    - a Street View image
- Output **one** of the following allowed actions:
  - `f` — move forward
  - `l <deg>` — turn left by `<deg>` degrees
  - `r <deg>` — turn right by `<deg>` degrees
  - `q` — quit / finish
- Run with a **fresh internal state** for each assessment

---

## Notes

- Evaluation is fully deterministic for reproducibility
- Designed to benchmark **spatial reasoning**, **map–vision alignment**, and **navigation planning**

---

