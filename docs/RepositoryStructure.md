Overview  
The CTOR ecosystem consists of multiple specialized platforms that together support human gameplay, AI research, student competitions, team‑based strategy studies, and engine development.  
Each repository serves a distinct purpose but integrates with others through shared rules, APIs, and agent interfaces.

This structure ensures:

- clarity for contributors  
- modular development  
- clean separation of concerns  
- scalability for future research and competitions  

---

## Repository List

### 1. CTOR‑Labs  
**Type:** Meta‑repository  
**Purpose:**  
- Central documentation hub  
- Ecosystem architecture and design principles  
- Roadmaps, research directions, and publications  
- Links to all CTOR projects  
- Official identity and branding for CTOR‑Labs  

---

## Full CTOR Ecosystem Architecture

The CTOR ecosystem is organized into several coordinated repositories, each responsible for a specific domain.  
Together they form a modular, scalable, and interoperable architecture:

```
CTOR-Labs/
│
├── CTOR-Engine
│     Canonical CTOR game engine (rules, move validation, topology)
│
├── CTOR-UI
│     Official browser UI shared across all CTOR modes
│
├── CTOR-H-AI
│     Human‑vs‑AI platform (heuristics, minimax, MCTS, RL, adaptive difficulty)
│
├── CTOR-AI-AI
│     AI‑vs‑AI tournament platform (protocols, match runner, baselines, analytics)
│
├── CTOR-H-H
│     Human‑vs‑Human platform (competitive sessions, ratings, profiles)
│
├── CTOR-Team-Team
│     Reserved for future team‑based CTOR modes (architectural placeholder)
│
└── docs/
      Specifications, diagrams, research notes, and ecosystem documentation
```

Each repository is independent but interoperable through shared protocols and the canonical CTOR engine.
._
