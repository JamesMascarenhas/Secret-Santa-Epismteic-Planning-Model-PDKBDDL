# Secret Santa Epistemic Planning (PDKbDDL / RPMEP)

**Course:** CISC 813 – Automated Planning  
**Topic:** Multi-Agent Epistemic Planning (Week 10)  
**Planner Used:** RPMEP (via Planutils)

---

## Overview

This project models a multi-agent epistemic planning setting using a structured **Secret Santa** scenario.  
The focus is on how agents **gain**, **lose**, **reason about**, and **update** their knowledge and beliefs through actions, communication, and inference.

Across seven progressively more complex problems, the model demonstrates key concepts from the Week 10 lectures, including:

- Public announcements  
- Private announcements  
- Belief vs. knowledge  
- Modal possibility  
- Conflicting statements and uncertainty  
- Structural reasoning and deduction  
- Nested beliefs (depth 2)  
- KD45 doxastic logic  
- PDKB-based epistemic states  
- RPMEP-style planning with syntactic belief updates

---

# 1. Domain Summary

The Secret Santa domain contains three interacting layers:

## Physical World
Agents move among **main-room**, **bowl-room**, and **gifts-room**, where:
- movement is publicly observable
- gift selection is visible to colocated agents
- room connectivity is common knowledge

## Assignment Layer
- Each agent must draw one unique target.
- Gifts are associated with a specific intended recipient.
- The planner must coordinate drawing and gift-picking actions.

## Epistemic Layer
Agents have epistemic fluents using modal operators:

- `[a](φ)` — agent *a* knows φ  
- `<a>(φ)` — agent *a* considers φ possible  

These are updated by:
- private communication (whispers)  
- public communication (talk)  
- observation rules via derive-conditions  
- explicit inference actions  

Nested modalities such as `[a][c](φ)` appear in more advanced problems.

---

# 2. Actions and Epistemic Effects

### Movement
Publicly observed; forms the basis for visibility during communication and drawing.

### draw-name
If an agent draws in the bowl-room, anyone present updates knowledge of the assignment.

### pick-gift
Publicly reveals the drawer’s target because each gift uniquely encodes a recipient.

### whisper-assign
Private announcement:  
Only the receiving agent updates their belief.

### talk-assign
Public announcement:  
Any agent in the room updates their belief accordingly.

### confuse-assign
Injects uncertainty:  
The listener simultaneously considers φ and ¬φ possible.

### Inference actions (Problem 5)
Agents eliminate impossible candidates and eventually infer missing assignments using structural reasoning.

---

# 3. Problem Set Overview

## Problem 1 — Baseline (Depth 1)
**Concepts:**  
Publicly observable actions, KD45 belief updates, no communication, no nesting.

Agents draw names, pick gifts, and each learns only their own assignment.

---

## Problem 2 — Private Communication (Depth 1)
**Concepts:**  
Private announcements and asymmetric knowledge.

A whisper gives one agent privileged information unavailable to others.

---

## Problem 3 — Public Communication (Depth 2)
**Concepts:**  
Public announcements, group knowledge, nested beliefs.

Talk-actions propagate universally to colocated agents, enabling reasoning such as  
`[a][c](draws b c)`.

---

## Problem 4 — Conflicting Announcements (Depth 1)
**Concepts:**  
Suspicion and uncertainty, possibility modalities.

A confuse-assign action leads to `<c>(φ)` and `<c>(¬φ)` simultaneously.

---

## Problem 5 — Deductive Inference (Depth 1)
**Concepts:**  
Reasoning about structural constraints, candidate elimination, enforced inference.

Agent C deduces B’s assignment *without* being told, using:
- rule-out operators  
- remaining candidates  
- an explicit infer action

---

## Problem 6 — Mixed Communication & Nested Knowledge (Depth 2)
**Concepts:**  
Combination of whisper and talk, nested beliefs, perspective-taking.

Plan must include both:
- at least one whisper  
- at least one public announcement  

and produce nested knowledge.

---

## Problem 7 — Five-Agent Large-Scale Epistemic Reasoning (Depth 2)
**Concepts:**  
Scalability, multi-agent uncertainty, distributed communication, nested belief propagation.

One agent learns the entire 5-agent assignment cycle; another maintains uncertainty.

---

# 4. Relationship to Lecture Topics

This project directly implements key concepts from Week 10:

- KD45 axioms (consistency, introspection)  
- Public announcement logic  
- Private announcement logic  
- Dynamic epistemic effects via derive-conditions  
- Modal possibility `<a>(φ)`  
- Syntactic belief representation (RP-MEP style)  
- PDKB-based preprocessed knowledge states  
- Depth-bounded reasoning (1 vs. 2)  
- Conflicting information and uncertainty  
- Structural inference  

Each problem is crafted to showcase specific lecture concepts in increasing complexity.

---

# 5. Planner Notes

Executed with:

```
rpmep file.pdkbddl
```

Approximate depth levels:

- Depth 1: Problems 1, 2, 4, 5  
- Depth 2: Problems 3, 6, 7  

Problem 7 is the largest (5 agents, ~36 steps), demonstrating scalability.

---

# 6. Summary

This project presents a structured epistemic planning model covering:
- public and private communication  
- uncertainty and conflicting beliefs  
- deductive reasoning within the assignment structure  
- nested belief modeling  
- multi-agent coordination  
- RPMEP belief updates with PDKB preprocessing  
- increasing complexity across 7 problems  

The Secret Santa domain successfully illustrates the full set of epistemic planning concepts taught in CISC 813 Week 10.
