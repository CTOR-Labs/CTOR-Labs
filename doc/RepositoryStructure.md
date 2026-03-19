# CTOR Ecosystem — Repository Structure

This document provides a complete overview of the CTOR ecosystem and explains the purpose, scope, and relationships between all repositories maintained under CTOR‑Labs.  
It is intended for contributors, researchers, students, and platform integrators who need a clear understanding of how the system is organized.

---

## Table of Contents
1. [Overview](#overview)  
2. [Repository List](#repository-list)  
   - [1. CTOR-Labs](#1-ctor-labs)  
   - [2. CTOR-H-AI](#2-ctor-h-ai)  
   - [3. CTOR-AI-AI](#3-ctor-ai-ai)  
   - [4. CTOR-H-H](#4-ctor-h-h)  
   - [5. CTOR-TEAM-TEAM](#5-ctor-team-team)  
   - [6. CTOR-Engine](#6-ctor-engine)  
3. [Inter‑Repository Relationships](#inter-repository-relationships)  
4. [Future Extensions](#future-extensions)

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

This repository acts as the entry point for anyone exploring the CTOR ecosystem.

---

### 2. CTOR-H-AI
**Type:** Human vs AI Platform  
**Purpose:**  
- Main environment where humans play against computer agents  
- Testing ground for engine algorithms and adaptive strategies  
- Human‑in‑the‑loop evaluation of AI behavior  
- Goal: develop the strongest CTOR engine for human play  

This platform is essential for iterative engine improvement and behavioral tuning.

---

### 3. CTOR-AI-AI
**Type:** AI vs AI Competition Platform  
**Purpose:**  
- Educational and research platform where students develop their own AI bots  
- Bots compete under standardized rules and protocols  
- Used for tournaments, benchmarking, and strategy comparison  

**Branches:**  
- **JS branch** — existing implementation  
- **Python branch** — new version enabling Python‑based agents  

This repository is the foundation for student competitions and academic courses.

---

### 4. CTOR-H-H
**Type:** Human vs Human Online Platform  
**Purpose:**  
- CTOR equivalent of chess.com  
- Real‑time online gameplay between human players  
- Rating system, matchmaking, and game history  
- Canonical ruleset and official move validator  

This is the official platform for human tournaments and community play.

---

### 5. CTOR-TEAM-TEAM
**Type:** Team vs Team Platform (Collective Intelligence)  
**Purpose:**  
- Supports three types of teams:  
  - **H** — human teams  
  - **AI** — teams of AI bots  
  - **H+AI** — mixed human‑AI teams  
- Accepts AI bots developed in other CTOR repositories  
- Research environment for collective intuition, coordination, and group strategy  
- Focus on communication models, role assignment, and team decision‑making  

This platform enables advanced studies in hybrid intelligence and group behavior.

---

### 6. CTOR-Engine  
*(formerly **CORE**, renamed)*  
**Type:** Python Engine  
**Purpose:**  
- Core CTOR engine implemented in Python  
- BR‑loop, world simulation, and rule enforcement  
- Baseline agents and reference implementations  
- API layer for integration with other CTOR platforms  
- Foundation for Kaggle Game Arena and all AI‑related development  

This is the central engine powering the entire CTOR ecosystem.

---

## Inter‑Repository Relationships

- **CTOR-Engine** is the core dependency for:  
  - CTOR-H-AI  
  - CTOR-AI-AI (Python branch)  
  - CTOR-TEAM-TEAM  
- **CTOR-H-H** uses the canonical ruleset, which is mirrored in CTOR-Engine.  
- **CTOR-AI-AI** provides a standardized environment for student agents that can later be used in team‑based platforms.  
- **CTOR-Labs** documents and coordinates the entire ecosystem.

---

## Future Extensions

Potential future repositories or modules may include:  
- **CTOR-Kaggle** — official Kaggle Game Arena integration  
- **CTOR-Docs** — unified documentation portal  
- **CTOR-Research** — academic experiments, datasets, and analysis tools  
- **CTOR-Visualizations** — advanced UI/UX components for all platforms  

The structure is designed to scale as CTOR grows into a global research and competition environment.

---

_End of document._

