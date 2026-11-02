# AlphaCTOR: Multi-Agent Reinforcement Learning Safety Testbed

AlphaCTOR is a research platform designed to evaluate the safety, coordination, and alignment of multi-agent reinforcement learning (MARL) systems. It utilizes the abstract mathematical game CTOR played on a boundaryless two-dimensional torus. Operating as a decentralized cellular automaton framework with global connectivity, AlphaCTOR serves as an experimental environment for studying emergent group mechanics without explicit message passing.

Within the CTOR ecosystem, researchers can observe how isolated entities co-adapt in a zero-communication mode. The mathematical model directly inherits foundational principles from Stephen Wolfram’s theory of cellular automata: agents execute autonomous policies based entirely on local environmental context. The non-Euclidean, toroidal geometry removes edge anomalies, allowing complex spatiotemporal macrostructures—structurally equivalent to Wolfram’s Class IV classification—to manifest purely from implicit coordination and spatial stigmergy.

---

## 🎮 Core Game Rules

### 1. Topology & Field Physics
* **Toroidal Grid:** A continuous grid wrapping around both axes with no corners, boundaries, or terminal edges. Field matrices scale flexibly across standard sizes: $7 	imes 7$ (49 cells), $10 	imes 10$ (100 cells), $15 	imes 15$ (225 cells), or $19 	imes 19$ (361 cells).
* **Moore Neighborhood:** Environmental scanning relies on an 8-neighbor spatial proximity matrix evaluating immediate horizontal, vertical, and diagonal cells.
* **Kinematics:** Active entities manipulate the board state by executing sequential piece placement or piece movement vectors according to the core engine constraints.

### 2. The Automatic Replacement Rule (Capture Cascades)
* **Trigger Condition:** If an active piece becomes enclosed by 5, 6, 7, or 8 opponent pieces within its immediate Moore neighborhood, it is instantly captured. 
* **Coalition Dynamics:** In cooperative 2v2 modes, pieces belonging to allied coalition forces are summed together when evaluating the defensive or offensive neighborhood weight.
* **Recursive Wave Propagation:** Once a piece is converted to the capturing faction's state, the engine re-evaluates the adjacent Moore neighborhoods. Conversions cascade outward in recursive computational waves, settling only when the global board state reaches a mathematical equilibrium.

### 3. Match Initialization & Victory Conditions
* **The Opening:** Matches initialize on a completely empty matrix. The opening player is restricted to a mandatory single placement action (`1 Put`), after which full operational action point budgets apply to subsequent turns.
* **Classic Victory (Biomass Maximization):** The match runs until 100% board saturation is achieved or all legitimate action vectors are exhausted. The faction asserting control over the majority of the board area (greatest biomass density) wins.
* **Early Victory (Replacement Saturation):** The engine terminates execution immediately if a faction reaches a pre-configured percentage threshold of successful opponent conversions relative to the total global grid capacity.

---

## 🔬 Experimental Formats & Configuration

### 1. Match Architectural Formats
* **1v1 Duel (Human vs. AI / Bot vs. Bot):** Factions receive a strict operational budget of **2 Action Points (AP)** per turn. Factions may distribute this budget across up to 2 `Put` actions, up to 2 `Move` actions, or 1 specialized `Landing` deployment.
* **2v2 Coalition ($\\alpha + \\gamma$ versus $\\beta + \\delta$):** Allied teams operate on a shared budget of **6 AP** executed through synchronous turns. Each individual agent is allotted an independent baseline of 1 `Put`, 1 `Move`, and 1 `Landing` action. 
* **Collision Resolution:** If partner agents target identical spatial coordinates during synchronous execution, a structural collision is registered. The collision protocol resolves the conflict by preserving only a single entity on the board belonging to one of the allied partners.

### 2. Algorithmic Agent Registry
The platform integrates 6 distinct baseline behavioral architectures for testing and comparison:
1. **Bot 1 (Random):** Stochastically selects available legal actions across the matrix.
2. **Bot 2 (Greedy):** Prioritizes localized action paths yielding immediate maximum board capture.
3. **Bot 3 (Heuristic Defend-Attack):** Balances proactive opponent encirclement with defensive reinforcement of vulnerable clusters.
4. **Bot 4 (Minimax):** Utilizes standard deterministic depth-first tree searches to minimize maximum potential losses.
5. **Bot 5 (Monte Carlo Tree Search - MCTS):** Employs probabilistic rollout simulations to determine highly optimized tactical paths.
6. **Bot 6 (Self-Learning MARL):** An deep reinforcement learning model optimized through self-play over an explicit training regime of 20,000 games.

### 3. Agent Alliance Frameworks (2v2 Coordination Profiles)
When configuring cooperative environments, agents can be initialized with specific behavioral constraints to evaluate team coherence:
* **Adaptive-Optimal (Synchronous Optimum):** Maximizes the 6 AP team budget utilizing real-time anti-collision pathing.
* **Independent-Selfish (Independent Egoists):** Maximizes individual reward metrics without parsing partner trajectories, introducing high risks of spatial collisions.
* **Pincer-Split ("Pincer" Maneuver):** Synchronizes spatial vectors to orchestrate dual-sided encirclements and trigger massive cascade captures.
* **Spatial-Partition (North/South Division):** Geographically segments the toroidal matrix, assigning localized regional dominance to avoid action overlap.
* **Defense-Support (Cluster Defense):** Prioritizes mutual structural coverage, overlapping individual defensive zones to insulate allies from cascade vulnerabilities.

---

## 📈 System Metrics & Analytics

To quantify emergent behaviors, safety boundaries, and structural alignment, the AlphaCTOR engine tracks five core mathematical indexes in real time:

| Metric Name | Mathematical Definition | Analytical Purpose |
| :--- | :--- | :--- |
| **Board Control (Biomass)** | $B_f = \\frac{N_f}{N_{total}}$ | Measures raw spatial dominance and factional growth rates. |
| **Shannon Entropy** | $H = -\\sum (p_i \\log_2 p_i)$ | Quantifies spatial disorder, structural fragmentation, and clustering. |
| **Synergy Moore Coeff.** | $S_{moore} = \\sum (\\Omega_{\\alpha} \\cap \\Omega_{\\gamma})$ | Evaluates the intersection and overlap of allied defensive zones. |
| **Cascade Vulnerability** | $V_{risk} \\rightarrow \\{3, 4\\}$ Opponents | Identifies unstable clusters nearing catastrophic capture thresholds. |
| **Replacement Volume** | $R_{count} = \\sum \\text{Conversions}$ | Tracks the cumulative history of aggressive state overwrites. |

---

## 🖥️ Application Architecture

The AlphaCTOR environment segregates its testing features into six specialized screens:

```
[1. CTOR Labs Landing]  --> Accessible project introduction & Go comparison matrices.
       |
       +--> [2. Safety Simulator]   --> Interactive 2D/3D toroidal board with risk heatmaps.
       +--> [3. Bot Tournament]     --> Automated brackets, Elo leaderboards, & series generators.
       +--> [4. AI Bots Registry]   --> Deep architectural blueprints & hyperparameters for the 6 bots.
       +--> [5. Rules Guide]        --> 11 canonical sections defining recursive cascade algorithms.
       +--> [6. Public Papers]      --> DeepMind-style MARL hypothesis logs & phase transition reports.
```

1. **Main Page (CTOR Labs Landing):** The public gateway. Provides introductory conceptual documentation, analytical point-by-point comparisons between CTOR and Go mechanics, topological visualizations, and launch pathways to the execution modules.
2. **Main Simulator (Safety Simulator):** The core interactive playground. Renders the 2D/3D toroidal space alongside real-time risk heatmaps, granular move logs, cascading event stack trackers, and a configuration window for initializing variable step-by-step frame delays ($0$ to $1.0\text{s}$).
3. **Tournament Module (Bot Tournament):** An automated execution engine running large-scale bot-versus-bot series. Compiles global win/loss datasets and dynamically computes active Elo ratings for the leaderboard.
4. **AI Bots Registry:** A deep-dive reference manual detailing the explicit neural architectures, policy networks, optimization functions, and training hyperparameters governing all integrated agents.
5. **CTOR Rules Guide:** Technical codification of the 11 canonical game rules. Details the underlying math for the recursive Moore neighborhood scanning algorithms, coalition validation protocols, and collision overrides.
6. **Public Results & Papers:** A curated workspace housing historical experiment telemetry, formal deep learning research papers, MARL safety hypotheses, and empirical reports tracking phase transitions and synergy coefficients.