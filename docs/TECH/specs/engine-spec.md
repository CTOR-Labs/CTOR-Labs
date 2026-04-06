# CTOR Engine Specification

This document defines the canonical CTOR rules engine.  
All branches (H-H, H-AI, AI-AI, TEAM-TEAM) must use an engine implementation that fully conforms to this specification.

---

## 1. Engine Responsibilities

The engine MUST:

1. Maintain the full game state  
2. Validate all moves  
3. Apply moves deterministically  
4. Detect win/draw/illegal states  
5. Provide a serializable representation of the game  
6. Support batch simulation mode (AI-AI)  
7. Guarantee rule consistency across all branches  

---

## 2. Game State Format

The engine MUST expose the game state as a structured object:

```
GameState {
  board: [...],
  activePlayer: "A" | "B",
  turn: number,
  history: Move[],
  metadata: {...}
}
```

Requirements:

- `board` MUST represent the full CTOR field  
- `activePlayer` MUST alternate strictly  
- `history` MUST contain all moves in order  
- `metadata` MAY contain additional fields (branch-specific)

---

## 3. Move Format

A move MUST follow this structure:

```
Move {
  from: Cell | null,
  to: Cell,
  type: "place" | "move" | "capture" | "special",
  timestamp: number
}
```

Rules:

- `from = null` for placement moves  
- `type` MUST be validated against CTOR rules  
- `timestamp` MUST be monotonic  

---

## 4. Move Validation

The engine MUST validate:

- legality of the move  
- cell occupancy  
- adjacency rules  
- color/shape constraints  
- special CTOR mechanics (defined in RULES)  

If invalid, the engine MUST return:

```
{ valid: false, reason: string }
```

---

## 5. State Transition

For every valid move, the engine MUST:

1. Update the board  
2. Update activePlayer  
3. Append to history  
4. Recalculate win/draw conditions  

---

## 6. Win/Draw Detection

The engine MUST implement:

- CTOR line completion rules  
- CTOR field constraints  
- stalemate detection  
- illegal repetition detection  

---

## 7. Serialization

The engine MUST support:

- `toJSON()`  
- `fromJSON()`  

Serialization MUST be deterministic.

---

## 8. Batch Simulation Mode (AI-AI)

The engine MUST support:

- running N simulations  
- returning aggregated results  
- deterministic seeding  

---

## 9. Error Handling

The engine MUST:

- never throw uncaught exceptions  
- return structured error objects  
- guarantee deterministic behavior  

---

# End of Engine Specification
