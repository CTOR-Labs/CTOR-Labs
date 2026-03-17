# CTOR-Labs Design Document v1.0

CTOR-Labs is a modular research platform for studying collective intelligence, hybrid cognition, and multi-agent behavior. The system is built around a clear separation between the user interface and the simulation engine, enabling deterministic experiments, AI agent development, and human interaction through a modern web interface.

---

Overview

CTOR-Labs provides a formal environment where agents, humans, and teams interact through a deterministic simulation. The platform supports visualization, experimentation, AI-vs-AI competitions, and human-in-the-loop exploration. The architecture is designed for long-term extensibility, reproducibility, and compatibility with AI research workflows.

---

Goals

Support deterministic simulation of the CTOR environment  
Provide a browser-based UI for human interaction  
Enable ML, rule-based, and LLM-based agents  
Ensure reproducibility across platforms  
Support Kaggle-compatible environments  
Enable team-based and multi-agent experiments  
Provide a modular and extensible architecture  

---

Non-Goals

The system does not aim to provide 3D graphics  
The system does not aim to be a real-time multiplayer game  
The system does not aim to support arbitrary physics engines  
The system does not aim to replace full-featured game engines  

---

System Architecture

The system is divided into independent layers:

UI Layer (JavaScript)  
Handles visualization, user input, animations, and browser interaction. Runs entirely in the client environment.

API Bridge  
Transfers state and actions between the UI and the simulation engine using JSON.

CORE Engine (Python)  
Implements the CTOR simulation including rules, state transitions, determinism, and agent API.

Agents Layer (Python)  
Implements rule-based, ML-based, and LLM-based agents. Compatible with Kaggle environments.

Simulation Loop  
Executes deterministic state updates using the BR LOOP model.

State Model  
Defines the canonical representation of the environment.

---

Rationale for Key Decisions

JavaScript for UI  
JavaScript is the native language of the browser. It provides fast rendering, reactive interfaces, and universal accessibility.

Python for CORE  
Python is the standard for AI research. It provides ML libraries, scientific tooling, and compatibility with Kaggle.

Separation of UI and Engine  
This ensures modularity, reproducibility, and independent evolution of both layers.

JSON as the communication protocol  
Simple, universal, language-agnostic, and easy to debug.

Deterministic simulation  
Required for scientific reproducibility, debugging, and AI competitions.

---

Interaction Modes

The platform supports four modes:

H-AI Human vs AI  
AI-AI AI vs AI  
T-T Team vs Team  
H-H Human vs Human

All modes use the same simulation engine and the same BR LOOP execution model.

---

Data Flow

1. UI sends user input or requests state updates  
2. API Bridge forwards requests to CORE  
3. CORE computes the next state  
4. CORE returns updated state to UI  
5. UI renders the new state  
6. Agents receive observations and produce actions  
7. The cycle repeats until termination  

---

State Model

The state includes:

Grid layout  
Agent positions  
Agent orientations  
Resource locations  
Scores  
Turn counters  
Termination flags  

The state is fully serializable and can be logged, hashed, or replayed.

---

BR LOOP (Behavior–Reaction Loop)

The BR LOOP is the fundamental execution cycle of the CTOR simulation engine. It defines how agents interact with the environment and how the environment processes their actions. The loop is deterministic, synchronous, and reproducible.

Purpose  
The BR LOOP separates agent decision-making from environment updates. Agents choose actions; the engine applies rules.

Structure  
Behavior Phase: agents receive observations and output actions  
Reaction Phase: the engine validates actions, resolves conflicts, updates the state, and computes scores  

Cycle  
1. Engine generates observations  
2. Agents compute actions  
3. Engine collects actions  
4. Engine applies rules  
5. Engine updates state  
6. Engine checks termination  
7. Loop repeats  

Benefits  
Modularity, reproducibility, fairness, compatibility with RL frameworks, and clarity of execution.

---

Simulation Loop

The simulation loop is built on top of the BR LOOP. It ensures:

Synchronous updates  
Deterministic transitions  
Consistent ordering of operations  
Clear separation between agent logic and environment logic  

---

Agent API

Agents implement a single method:

act(observation, info) → action

Inputs  
observation structured view of the environment  
info metadata such as turn number and scores  

Output  
action one of the allowed moves  

The API supports rule-based, ML-based, LLM-based, and evolutionary agents.

---

UI Architecture

The UI is responsible for:

Rendering the grid  
Displaying agent positions  
Animating state transitions  
Handling user input  
Communicating with CORE  

The UI does not contain game logic. All rules reside in CORE.

---

Security and Isolation

The engine is designed to run in sandboxed environments such as Kaggle. Agents cannot access external resources or modify the environment outside the allowed API.

---

Performance Considerations

The engine is optimized for:

Deterministic execution  
Batch simulation  
Low overhead per step  
Compatibility with vectorized extensions  

Future versions may include GPU acceleration and parallel simulation.

---

Future Extensions

Replay system  
Tournament manager  
Vectorized simulation  
Advanced observation masking  
Multi-agent curriculum learning  
Extended UI features  

---

Alternatives Considered

Single-language architecture  
Rejected due to lack of ML support in JS and lack of browser support in Python.

Using a game engine (Unity, Unreal)  
Rejected due to complexity, lack of determinism, and poor compatibility with Kaggle.

Using Rust or C++ for CORE  
Rejected due to slower iteration speed and weaker ML ecosystem.

---

Appendix

Glossary of terms  
Architecture diagrams (text format)  
References to related research platforms  

