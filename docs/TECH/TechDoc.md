# CTOR-Labs TechDoc

## 1. Purpose

This document defines the shared technical architecture, tools, and development standards for all CTOR-Labs branches (H-H, H-AI, AI-AI, TEAM-TEAM).  
It serves as the central technical reference for the entire CTOR ecosystem, ensuring consistency, modularity, and scalability across all repositories.

---

## 2. CTOR Ecosystem Overview

(Will be completed later — describes the four-branch architecture, modular engine, UI layers, and multi-agent ecosystem.)

---

## 3. Shared Tools and Platforms

The CTOR‑Labs ecosystem relies on a unified set of core tools used across all four development branches (H‑H, H‑AI, AI‑AI, TEAM‑TEAM).  
These tools form the foundation of the multi‑agent, multi‑platform architecture and ensure consistency, portability, and rapid iteration throughout the entire project.

---

### 3.1 Claude — AI Logic, Algorithms, and Strategic Reasoning

Claude serves as the primary intelligence and analysis engine across all CTOR branches.  
It is used for:

- heuristic logic design  
- AI agent behavior modeling  
- algorithm development and refinement  
- strategic evaluation of game states  
- debugging and explaining agent decisions  
- generating test scenarios and simulations  
- validating rule interpretations  

Claude is not tied to any specific branch — it is a universal cognitive tool used for both development and analysis.

---

### 3.2 Replit — Code Sandbox, Engine Testing, and API Prototyping

Replit provides a fast, isolated environment for:

- engine module development  
- rapid JavaScript/Python experimentation  
- testing rule implementations  
- validating API endpoints  
- running micro‑simulations  
- prototyping utilities and helper modules  

Replit is used in all branches as a lightweight execution layer for testing logic before integrating it into the main codebase.

---

### 3.3 Local Engine Runner — Core Rule Execution and Simulation

The Local Engine Runner is the canonical implementation of CTOR rules.  
It is responsible for:

- applying moves  
- validating legality  
- updating game state  
- detecting win/draw conditions  
- running simulations  
- supporting batch testing for AI agents  

This module is the **single source of truth** for game mechanics across all branches.  
Every UI, AI, or team‑based system relies on the same engine to ensure consistency.

---

### 3.4 LLM‑Based Evaluators — Strategic Analysis and Meta‑Reasoning

LLM evaluators are analytical tools used to:

- assess board positions  
- compare move options  
- explain strategies  
- detect mistakes in human or AI play  
- analyze large batches of AI‑AI simulations  
- generate heuristics and evaluation functions  

They are not agents themselves — they are **meta‑tools** that help improve agents, rules, and strategies.

---

### 3.5 Lovable — UI Prototyping and Interaction Design

Lovable is used across branches for:

- rapid UI prototyping  
- layout and component exploration  
- interaction flow design  
- visual experimentation  
- early‑stage interface testing  

It allows fast iteration without requiring full implementation, making it ideal for early UX exploration.

---

### 3.6 GitHub — Version Control, Collaboration, and Modular Architecture

GitHub is the backbone of CTOR‑Labs:

- repository structure  
- modular code organization  
- versioning  
- documentation  
- issue tracking  
- branch‑specific development  

Each CTOR branch has its own repository, but all follow the shared architectural standards defined in CTOR‑Labs.

---

### 3.7 Netlify / Vercel — Deployment and Public Prototyping

These platforms provide:

- stable deployment of UI prototypes  
- public demos for testing  
- external access for evaluators and collaborators  
- fast CI/CD for front‑end builds  

They ensure that prototypes remain accessible outside the development environment.

---

### 3.8 Summary

These shared tools form the unified foundation of the CTOR‑Labs ecosystem.  
Each branch (H‑H, H‑AI, AI‑AI, TEAM‑TEAM) uses them differently, but all rely on the same core capabilities:

- **Claude** → intelligence, reasoning, algorithms  
- **Replit** → code sandbox, engine tests, API prototyping  
- **Local Engine Runner** → rules, state updates, simulations  
- **LLM Evaluators** → strategic analysis and meta‑reasoning  
- **Lovable** → UI prototyping  
- **GitHub** → architecture and collaboration  
- **Netlify/Vercel** → deployment and demos  

This shared foundation ensures consistency, modularity, and scalability across the entire CTOR ecosystem.

---

## 4. Technology Stack by Branch

Below are the branch‑specific applications of the shared toolset.

---

### 4.1 H-H — Human vs Human

(To be completed later — focuses on UI, rule validation, and game session management.)

---

### 4.2 H-AI — Heuristic AI Agents

The H-AI branch focuses on developing heuristic AI agents that play CTOR against human opponents.  
It builds on the shared CTOR-Labs toolset and applies it in the following way:

#### Role of Shared Tools in H-AI

- **Claude** → used for heuristic logic design, AI agent behavior modeling, and evaluation function refinement.  
- **Replit** → used for engine integration tests, algorithm prototyping, and API-driven experiments.  
- **Local Engine Runner** → used as the canonical rules engine for validating AI moves and running simulations.  
- **LLM-based evaluators** → used to analyze AI games, compare strategies, and debug decision-making.  
- **Lovable** → used to prototype human-vs-AI interaction flows and UI layouts.  
- **Netlify/Vercel** → used to deploy playable H-AI prototypes for external testing.

#### H-AI Architecture Focus

- Separation of UI, AI, and Engine  
- Heuristic decision-making instead of full search  
- API-driven integration between UI and AI modules  
- Support for human-vs-AI play and analysis
