# CTOR Agent Specification

This document defines the required interface for all CTOR agents:

- Human agents (H-H)
- Heuristic AI agents (H-AI)
- Autonomous agents (AI-AI)
- Team-based agents (TEAM-TEAM)

All agents MUST conform to this specification.

---

## 1. Agent Responsibilities

An agent MUST:

1. Receive the current game state  
2. Produce a valid move  
3. Follow the agent interface contract  
4. Never modify the game state directly  
5. Support deterministic and non-deterministic modes  

---

## 2. Agent Interface

Every agent MUST implement:

```
Agent {
  id: string,
  version: string,
  getMove(GameState): Promise<Move>,
  configure(options): void,
  reset(): void
}
```

### Requirements:

- `id` MUST be unique  
- `getMove` MUST return a move in the required format  
- `getMove` MUST NOT mutate the input state  
- `configure` MAY accept branch-specific options  
- `reset` MUST clear internal memory  

---

## 3. Determinism

Agents MUST support:

- deterministic mode (seeded)  
- stochastic mode (randomized heuristics)  

---

## 4. Time Constraints

Agents MUST:

- respond within the allowed time budget  
- expose a timeout policy  

---

## 5. Evaluation Hooks

Agents MAY expose:

- `explainMove()`  
- `getHeuristicScore()`  
- `getSearchDepth()`  

These are optional but recommended for debugging and research.

---

## 6. Compatibility Requirements

Agents MUST be compatible with:

- Local Engine Runner  
- UI interaction layer  
- Simulation pipelines  

---

# End of Agent Specification
