CTOR‑Labs
Research Laboratory for Collective Intelligence, Hybrid Cognition, and CAI Systems
CTOR‑Labs is a research laboratory dedicated to studying system‑level intelligence emerging in hybrid environments where humans and AI agents interact.

We develop a new paradigm — CAI Systems (Collective Artificial Intelligence Systems) — and build experimental tools to validate it.

Our primary experimental platform is CTOR, a deep abstract strategy game invented in 1986 — one of the most complex games of the Go family.
https://ctorgame.com/

📌 Mission
Our mission is to investigate and formalize new forms of intelligence that arise:

not in individual models,

not in individual humans,

but in systems where many agents interact within a shared environment.

We study:

emergent cognitive regimes

collective intuition

hybrid forms of reasoning

system‑level cognitive identity

CTOR serves as a controlled environment for observing these phenomena.

📌 Who Is CTOR For?
🎓 Students of AI & Machine Learning
A hands‑on environment for studying multi‑agent systems, emergent behavior, and hybrid cognition.

👩‍🏫 Educators & Professors
A ready‑to‑use platform for teaching:

collective intelligence

agent‑based modeling

human–AI collaboration

system‑level cognition

🧠 AI Researchers
A controlled testbed for hypotheses about:

emergent strategies

distributed attention

collective intuition

hybrid cognitive regimes

🧩 Developers & Engineers
A modular system for building:

AI agents

analytics pipelines

multi‑agent architectures

experimental cognitive systems

🚀 Visionaries & Innovators
A glimpse into the next evolutionary step of intelligence —
not artificial, not biological, but collective.

📌 CAI Systems: A New Evolutionary Branch of Intelligence
CAI Systems represent a new class of intelligence emerging from interacting agents — human and artificial — operating within a shared cognitive environment.

CTOR is the first experimental platform designed specifically to study this phenomenon.

📁 Repository Structure
The full structure of the CTOR ecosystem is documented here:
docs/RepositoryStructure.md

📌 Projects at a Glance
CTOR‑Labs maintains several structured research branches, each representing a distinct interaction regime inside the CTOR environment.

🤖 CTOR‑AI‑AI
AI‑vs‑AI matches for studying emergent strategies and system‑level cognition.
👉 https://github.com/CTOR-Labs/CTOR-AI-AI

🧑‍🤝‍🧑 CTOR‑H-H
Human‑vs‑Human matches used as a baseline for strategic behavior and intuition.
👉 https://github.com/CTOR-Labs/CTOR-H-H

🧑‍🤖 CTOR‑H-AI
Hybrid Human‑vs‑AI matches — the core track for studying hybrid cognition.
👉 https://github.com/CTOR-Labs/CTOR-H-AI

🧩 CTOR‑TEAM‑TEAM
Team‑vs‑Team configurations (2v2, 3v3, hybrid teams) for exploring group coherence and distributed roles.
👉 https://github.com/CTOR-Labs/CTOR-TEAM-TEAM

📐 Updated CTOR Development Architecture
CTOR has transitioned to a modular architecture, where API, UI, and Engine evolve as independent but coordinated components.

New standards and documents define how these modules interact.

🔗 API Documentation
All API versions are located in:

Code
docs/API/
Each version is a standalone contract:

API-CONTRACT-v0.1.md — basic GameState/Move structures

API-CONTRACT-v0.2.md — timing, errors

API-CONTRACT-v0.3.md — network protocol (HTTP/WebSocket)

API-CONTRACT-v0.4.md — authorization, roles, tokens

API-CONTRACT-v0.5.md — matchmaking, rooms, lobbies

API index:
docs/API/README.md

📄 Architectural Documents
Additional documents describing system structure:

docs/RepositoryStructure.md — CTOR‑Labs repository structure

docs/design-doc-v1.md — CTOR architecture design (v1.0)

These documents define modularity, API standards, and component interaction.

🖥️ CTOR‑UI and API
The CTOR‑UI repository now uses API contracts as the single source of truth:

UI does not define its own GameState/Move structures

all data flows through API v0.x

networking follows API v0.3

authorization follows API v0.4

lobbies follow API v0.5

UI architecture follows design‑doc‑v1.md

This ensures compatibility across UI, Engine, AI bots, and server components.

🧭 Next Phase: UI Development
After completing API and repository structure, the next phase is CTOR‑UI implementation.

UI will use:

API v0.3 — WebSocket/HTTP

API v0.4 — authorization

API v0.5 — matchmaking

UI architecture will be documented in:

Code
docs/ui-design-v1.md
(to be created during development)

🌐 Project Website
https://www.ctorgame.com

🤝 How to Contribute
⭐ Ambassador
Share CTOR, invite others, spread the mission.

⭐ Team Member
Join development as CTO, CMO, or domain lead.

⭐ Sponsor
Support CTOR‑Labs development:
👉 https://paypal.me/CTORLabs
