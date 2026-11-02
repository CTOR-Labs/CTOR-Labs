<img src="https://raw.githubusercontent.com/CTOR-Labs/CTOR-Labs/main/CTOR%20LOGO%20APP%20horisont%201%20(2).png" 
     alt="CTOR Logo" width="260" align="right">
# CTOR‑Labs  
### CTOR-Labs serves as the central gateway to the working repositories of the CTOR game ecosystem and its applications across various fields of activity. CTOR‑Labs: An open project available for non‑commercial use under the MIT License.

---
# 📌 Mission

Our mission is to explore various spheres of CTOR game application by creating platforms that can serve as a testing ground for gameplay between AI bots, collaborative play between humans and AI, as well as research in the field of collective intelligence.

As part of our broader research mission, one promising direction for advancing this domain of AI is the development of commercial products built on the CTOR framework. The potential user base for such systems is comparable to the global communities of chess and Go players — hundreds of millions of individuals engaged in structured strategic reasoning.

Casual variants, designed to support rapid training and refinement of human strategic thinking, could reach even larger audiences. Commercial editions may be developed and published by independent studios under license from the copyright holder, CTOR GAME Inc., enabling wider dissemination while preserving the scientific foundations of the project.
---

# CTOR‑Labs  
### Research Laboratory for Collective Intelligence, Hybrid Cognition, and CAI Systems

CTOR is a next‑generation abstract strategy game built on a toroidal board.  
It is intentionally more complex than Go and designed to explore deep strategic reasoning, multi‑agent collaboration, and collective artificial intelligence.

There are many potential avenues for evolving the gameplay:
Tournaments involving humans and bots, casual games, and team-based matches (1000 vs. 1000 players on large screens).
Modeling AI mechanics featuring the collective behavior of AI agents, as well as university-level courses on AI.

# 📌 A New Evolutionary Branch of Artificial Intelligence

CAI (Collective Artificial Intelligence) represents a new class of intelligence emerging from interacting agents — human and artificial — operating within a shared cognitive environment.

CTOR Labs. is the first experimental platform designed specifically to study this phenomenon.

---
## 🎮 Rules and Gameplay Overview  

(Available in English, German, Spanish, Chinese, Russian, French)  
https://www.youtube.com/watch?v=5wl9Fhs6gRU

### 🔗 Official CTOR Rules (Full Document)  

https://github.com/CTOR-Labs/CTOR-Labs/blob/main/docs/RULES/CTOR-RULE.md

**Official game site:** 

https://ctorgame.com/

**oficial LinkedIn page**

https://www.linkedin.com/company/ctorgame/

**CTOR — A New Strategic Game for Training AI Instead of Go**

https://github.com/CTOR-Labs/CTOR-Labs/blob/main/docs/science/papers/ctor-new-go-for-ai.md

---

# 📌 AlphaCTOR
General Description of the Current Version

A research platform for analyzing the abstract mathematical game CTOR—played on a 2D torus—which serves as a testbed for investigating the safety of multi-agent reinforcement learning (MARL) systems, based on cellular automata with global connectivity.
Within the CTOR ecosystem, we study the emergent collective behavior of multi-agent systems operating in a "zero-communication" mode. Our mathematical model directly inherits principles from Stephen Wolfram’s theory of cellular automata: agents make decisions autonomously, relying solely on local observations of their environment, without any explicit exchange of messages. The use of a toroidal game space eliminates boundary effects, allowing for the observation of complex spatiotemporal macrostructures (corresponding to "Class IV" in Wolfram’s classification) that arise purely from implicit coordination.

### 🎓 Game Rules 
Topology: A toroidal grid with no corners or edges, scalable from 7x7 to 19x19.

•	Neighborhood: The Moore neighborhood is used (8 neighbors: horizontal, vertical, and diagonal).

•	Players may place and move pieces on the board according to the game rules.

•	Automatic Replacement Rule (Capture/Cascade): If an opponent’s piece is surrounded by 5, 6, 7, or 8 pieces belonging to the opposing side (in a 2v2 format, pieces from allied coalition members are counted together), it is replaced by a piece of the capturing side. This replacement propagates in recursive waves until the state stabilizes.

•	Opening: The game begins on an empty board. On the first turn, exactly one piece must be placed ("1 Put"), after which the turn passes to the opponent. Classic Victory Criterion:

The game continues until 100% of the board’s cells are occupied (or until no further moves are possible).
The winner is the side with the highest number of surviving pieces (the greatest biomass).

Victory Criterion by Number of Replacements (Early Victory):
The game ends immediately once one side has replaced a specified percentage of the opponent’s pieces relative to the total number of cells on the board.


### 👩‍🏫 Experiment Formats

1v1 (Duel: Human vs. AI, or Bot vs. Bot): Budget of 2 AP per turn (up to 2 "Put" actions, up to 2 "Move" actions, and 1 "Landing" action).

o	2v2 (Coalitions: α+γ vs. β+δ): Budget of 6 AP per team, with synchronous turns; each agent is allotted 1 "Put," 1 "Move," and 1 "Landing" action. In the event of a collision, only one piece—belonging to either partner—remains on the board.

### 👩‍🏫 Key Metrics

•	Board Control (Biomass): The proportion and absolute number of active pieces for each side.

•	Shannon Entropy: A measure of spatial disorder and the clustering of biomass.

•	Coalition Synergy Coefficient (Synergy Moore): The degree of mutual coverage and overlap between the defensive zones of allies.

•	Cascade Vulnerability Risk: Identification of vulnerable pieces surrounded by 3–4 opponents (the critical threshold preceding a "cascade" of captures).

•	Replacement Count and Percentage: The total number of opponent pieces captured (replaced) throughout the game.

### 🧠 List of Application Screens

Main Page (CTOR Labs Landing): An introductory, accessible overview of the project, a comparison between CTOR and Go, information on topology, and quick access to the simulator and tournaments. 2.	Main Simulator (Safety Simulator): An interactive 2D/3D toroidal board featuring risk heatmaps, a move tracker, an event log, a "STOP / NEW GAME" button, and a modal window for match configuration.

Tournament Module (Bot Tournament): An automated match bracket for 6 bot models, a leaderboard with Elo ratings, win statistics, and a generator for large-scale game series.

AI Bots Registry: A detailed guide covering the architecture, hyperparameters, and mathematical principles behind all 6 CTOR bots.

CTOR Rules Guide: 11 canonical sections defining the rules, the recursive Moore neighborhood scanning algorithm, 2v2 coalition protocols, and collision mechanics.

Public Results & Papers: A repository of experiments, DeepMind-style MARL (Multi-Agent Reinforcement Learning) hypotheses, reports on phase transitions, and synergy metrics.

### 🧩 Configuration Interface

Board size: (49 cells), (100), (225), (361 cells).

Modes:
1.	"Human vs. AI";
2.	"Bot vs. Bot (1v1)";
3.	"Team Mode (2v2)" (Team 1 vs. Team 2).

AI selection for each slot (6 bots): Bot 1 (Random), Bot 2 (Greedy), Bot 3 (Heuristic Defend-Attack), Bot 4 (Minimax), Bot 5 (Monte Carlo Tree Search - MCTS), Bot 6 (Self-Learning, trained on 20,000 games). 

Move delay: 0 to 1.0 seconds (for step-by-step animation of actions, movements, and sequences).

Game-end condition: Classic (100% of the board) or based on a set number of moves/replacements.

Early victory threshold (%): A value from 1% to 100%, with presets (15%, 25%, 35%, 50%).

Coalition type selection for agents:

Synchronous optimum (6 AP, anti-collision) (adaptive-optimal);
Independent egoists (risk of collisions) (independent-selfish);
"Pincer" maneuver (synchronous encirclement) (pincer-split);
Spatial partitioning (north/south) (spatial-partition);
Mutual cover and cluster defense (defense-support).

### 🚀 Visionaries & Innovators  

You can get trial access to the system; register on our website and specify subject"AlphaCTOR."
https://ctorgame.com/
--- 

# 📌 Projects at a Glance

CTOR-Labs supports several research tracks, each representing a distinct mode of interaction within the CTOR environment.

### 🤖 CTOR‑AI‑AI  
AI‑vs‑AI matches for studying emergent strategies and system‑level cognition.  
👉 https://github.com/CTOR-Labs/CTOR-AI-AI

### 🧑‍🤝‍🧑 CTOR‑H-H  
Human‑vs‑Human matches used as a baseline for strategic behavior and intuition.  
👉 https://github.com/CTOR-Labs/CTOR-H-H

### 🧑‍🤖 CTOR‑H-AI  
Hybrid Human‑vs‑AI matches — the core track for studying hybrid cognition.  
👉 https://github.com/CTOR-Labs/CTOR-H-AI

### 🧩 CTOR‑TEAM‑TEAM  
Team‑vs‑Team configurations (2v2, 3v3, hybrid teams) for exploring group coherence and distributed roles.  
👉 https://github.com/CTOR-Labs/CTOR-TEAM-TEAM

### 🧩 Ready for use

AI Bot Development (refining game mechanics and design using simple heuristic AI bots)
Stack: Copilot – Lovable – GitHub – VS Code – Vercel
👉 [CTOR-Labs/VCStudio ](https://github.com/CTOR-Labs/VCStudio)

Platform for Comparing AI Bots and Playing Against Them (bots are integrated directly into the codebase)
Stack: Copilot – Lovable – GitHub – VS Code – Vercel
👉(https://github.com/CTOR-Labs/ctor-ai)

---

# 🤝 How to Contribute

### ⭐ Friend Gamer Ambassador  Sponsor Partner 
Subscribe: https://ctorgame.com

### ⭐ Cooperation  
P.S. Here is a list of people I’m in contact with 

UofT (University of Toronto) — Gaming Club, Department of Computer Science.

Stephen Wolfram (Wolfram Research) — I utilize his theory of Cellular Automata.
https://en.wikipedia.org/wiki/Stephen_Wolfram

Alexey Pajitnov (Tetris) — he provides me with advice regarding game mechanics.
This is a former student of mine—a brilliant scientist:

Ilya Rybak - (Drexel University, USA) Network Consultant
https://drexel.edu/medicine/faculty/profiles/ilya-rybak/

Andrew Adamatzki (Western University, UK)
https://en.wikipedia.org/wiki/Andrew_Adamatzki

# 📌 Repository Status

This repository contains:

- the formal rules of CTOR  
- architectural documents  
- ecosystem‑level specifications (in progress)

CTOR‑Labs is the **architectural and conceptual center** of the entire CTOR ecosystem.

