# CTOR Ecosystem — Repository Structure

This document provides a complete overview of the CTOR ecosystem and explains the purpose, scope, and relationships between all repositories maintained under CTOR‑Labs.  
It is intended for contributors, researchers, students, and platform integrators who need a clear understanding of how the system is organized.

---

## Table of Contents
1. Overview  
2. Repository List  
   - 1. CTOR-Labs  
   - 2. CTOR-H-AI  
   - 3. CTOR-AI-AI  
   - 4. CTOR-H-H  
   - 5. CTOR-TEAM-TEAM  
   - 6. CTOR-Engine  
3. Inter‑Repository Relationships  
4. Future Extensions

---

## Overview

The CTOR ecosystem consists of multiple specialized platforms that together support human gameplay, AI research, student competitions, team‑based strategy studies, and engine development.  
Each repository serves a distinct purpose but integrates with others through shared rules, APIs, and agent interfaces.

This structure ensures:
- clarity for contributors  
- modular development  
- clean separation of concerns  
- scalability for future research and competitions  

---

## Repository List

### 1. CTOR-Labs
**Type:** Meta‑repository  
**Purpose:**  
- Central documentation hub  
- Ecosystem architecture and design principles  
- Roadmaps, research directions, and publications  
- Links to all CTOR projects  
- Official identity and branding for CTOR‑Labs  

---

### 2. CTOR-H-AI
**Type:** Human vs AI Platform  
**Purpose:**  
- Main environment where humans play against computer agents  
- Testing ground for engine algorithms and adaptive strategies  
- Human‑in‑the‑loop evaluation of AI behavior  
- Goal: develop the strongest CTOR engine for human play  

---

### 3. CTOR-AI-AI
**Type:** AI vs AI Competition Platform  
**Purpose:**  
- Educational and research platform where students develop their own AI bots  
- Bots compete under standardized rules and protocols  
- Used for tournaments, benchmarking, and strategy comparison  

**Branches:**  
- JS branch — existing implementation  
- Python branch — new version enabling Python‑based agents  

---

### 4. CTOR-H-H
**Type:** Human vs Human Online Platform  
**Purpose:**  
- CTOR equivalent of chess.com  
- Real‑time online gameplay between human players  
- Rating system, matchmaking, and game history  
- Canonical ruleset and official move validator  

---

### 5. CTOR-TEAM-TEAM
**Type:** Team vs Team Platform (Collective Intelligence)  
**Purpose:**  
- Supports three types of teams:  
  - H — human teams  
  - AI — teams of AI bots  
  - H+AI — mixed human‑AI teams  
- Accepts AI bots developed in other CTOR repositories  
- Research environment for collective intuition, coordination, and group strategy  
- Focus on communication models, role assignment, and team decision‑making  

---

### 6. CTOR-Engine  
*(formerly CORE)*  
**Type:** Python Engine  
**Purpose:**  
- Core CTOR engine implemented in Python  
- BR‑loop, world simulation, and rule enforcement  
- Baseline agents and reference implementations  
- API layer for integration with other CTOR platforms  
- Foundation for Kaggle Game Arena and all AI‑related development  

---
### 7. CTOR-UI
**Type:** Web UI (HTML/JS)  
**Purpose:**  
- Unified frontend for all CTOR platforms  
- Visualizes games, matches, teams, and ratings  
- Connects to CTOR-Engine and platform backends via APIs  
- Enables human interaction with CTOR in the browser  

## Inter‑Repository Relationships

- CTOR-Engine is the core dependency for:  
  - CTOR-H-AI  
  - CTOR-AI-AI (Python branch)  
  - CTOR-TEAM-TEAM  
- CTOR-H-H uses the canonical ruleset, which is mirrored in CTOR-Engine.  
- CTOR-AI-AI provides a standardized environment for student agents that can later be used in team‑based platforms.  
- CTOR-Labs documents and coordinates the entire ecosystem.

---

## Future Extensions

Potential future repositories or modules may include:  
- CTOR-Kaggle — official Kaggle Game Arena integration  
- CTOR-Docs — unified documentation portal  
- CTOR-Research — academic experiments, datasets, and analysis tools  
- CTOR-Visualizations — advanced UI/UX components for all platforms  

The structure is designed to scale as CTOR grows into a global research and competition environment.

---

_End of document._
