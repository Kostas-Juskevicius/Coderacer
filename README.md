# CodeRacer

A “TypeRacer” + "LeetCode" hybrid - practice writing and solving coding problems as fast and as accurately as possible.

---

## Table of Contents

1. [Game Modes](#game-modes)  
2. [Tech Stack](#tech-stack)  
3. [Architecture Overview](#architecture-overview)  
4. [Data Models](#data-models)  
5. [API Endpoints](#api-endpoints)  

---

## Game Modes

Two distinct game modes for different skill development goals:

1) Track typing / coding speed, accuracy, and other performance metrics
- Post-game analysis for self-assessment and improvement  
- Difficulty tiers: *easy*, *medium*, *hard*  
- Per-tag level selection  
- Leaderboards to compete with other users

2) Solve LeetCode-like problems (currently only supported in Java)
- Get a problem, given input and expected output example
- Write a solution
- Execute it (directly in the browser) - get output of your compiled code
- Iterate on the solution until the problem is solved

## Tech Stack

- **Backend**: _Spring Boot (Java)_, _Maven_  
- **Frontend**: _React_  
- **Database**: _PostgreSQL (cloud-hosted)_  
- **Auth**: _JWT_  
- **Containerization & Security**: _Docker, Seccomp_  
- **Hosting/CI**: _Microsoft Azure, GitHub Actions_  

---

## Architecture Overview

[ Frontend ] ⇄ [ REST API ] ⇄ [ Backend Services ] ⇄ [ Database ]  
                         ⇵  
                 [ Code Execution Microservice ]  

---

- **Frontend**
  - Profile dashboard  
  - Leaderboards  
  - Code Typing & LeetCode-style gameplay interfaces  

- **Backend**
  - Controllers  
  - Services  
  - Repositories  
  - (Optional) Integration with a **code execution microservice** for LeetCode-like problem mode  
    - Securely executes Java code submissions  
    - Uses containerization, segmentation, and Seccomp for isolation  
    - Returns compilation and execution results  

- **Database**
  - Tables for accounts, levels, sessions, submissions  
  - Views for leaderboard entries and account metrics  
