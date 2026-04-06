# CTOR UI Specification

This document defines the required UI components, rendering rules, and interaction flows for all CTOR user interfaces.

---

## 1. UI Responsibilities

The UI MUST:

1. Render the CTOR board correctly  
2. Display legal moves  
3. Highlight active player  
4. Show move history  
5. Provide interaction controls  
6. Never implement game logic internally  
7. Use the Engine as the single source of truth  

---

## 2. Board Rendering Rules

The UI MUST:

- render the CTOR field with correct geometry  
- display shapes/colors according to RULES  
- support zoom/pan  
- support mobile and desktop layouts  

---

## 3. Move Interaction

The UI MUST:

- allow selecting a piece  
- allow selecting a target cell  
- validate moves via Engine  
- show errors returned by Engine  

---

## 4. State Synchronization

The UI MUST:

- subscribe to engine state updates  
- re-render on every state change  
- never mutate the state directly  

---

## 5. Visualization Standards

The UI MUST:

- use consistent color palette  
- use consistent shape rendering  
- follow CTOR branding guidelines  
- support dark/light modes (optional)  

---

## 6. Replay & History

The UI MUST support:

- step-by-step replay  
- jump to move N  
- export/import game history  

---

## 7. API Integration

The UI MUST:

- communicate with AI agents via API  
- send only serialized GameState  
- receive only Move objects  

---

# End of UI Specification
