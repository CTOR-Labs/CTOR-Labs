# CTOR-Labs Specifications (Specs)

This directory contains the formal technical specifications for the CTOR ecosystem.  
Specs define the required behavior, data formats, and interaction contracts for all modules across all branches (H-H, H-AI, AI-AI, TEAM-TEAM).

## Contents

### 1. Engine Specification  
Defines the canonical CTOR rules engine, state transitions, move validation, and serialization formats.  
→ See: `engine-spec.md`

### 2. Agent Specification  
Defines the required interfaces, inputs, outputs, and constraints for all AI and human-driven agents.  
→ See: `agent-spec.md`

### 3. UI Specification  
Defines the required UI components, board rendering rules, interaction flows, and visualization standards.  
→ See: `ui-spec.md`

---

## Purpose of Specs

Specs ensure:

- consistency across all CTOR branches  
- compatibility between UI, Engine, and Agents  
- reproducibility of simulations  
- correctness of rule enforcement  
- modularity and clean architecture  

Specs are **binding** for all CTOR repositories.
