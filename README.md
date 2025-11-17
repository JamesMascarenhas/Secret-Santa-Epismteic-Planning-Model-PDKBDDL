Secret Santa Epistemic Planning (PDKbDDl / RPMEP)

Course: CISC 813 – Automated Planning
Topic: Multi-Agent Epistemic Planning (Week 10)
Planner Used: RPMEP (via Planutils)

Overview

This project models a multi-agent epistemic planning setting using a playful but expressive domain: a structured Secret Santa game.
The focus is not on logistics, but on knowledge, uncertainty, and nested reasoning among agents.

Across seven progressively more sophisticated problems, the domain showcases:

Multi-agent knowledge and belief tracking using RPMEP modalities

Private and public communication actions

Epistemic preconditions driven by observations

Knowledge-producing, belief-altering, and uncertainty-introducing actions

Structured reasoning and elimination using domain-level inference operators

Nested beliefs up to depth 2

Multi-agent (3 → 5 agent) scaling to demonstrate generality

The project is designed to map directly onto topics taught in Week 10 lectures on Epistemic Planning, including:

Public announcements

Private announcements

Knowledge vs. belief

Possibility modalities

Conflicting information

Suspicion and uncertainty

Structural inference

Nested epistemic reasoning

KD45 doxastic logic

RPMEP syntax and PDKB semantics

Each problem demonstrates one or more of these concepts in a controlled environment.

1. Domain Summary

The Secret Santa domain models three core layers:

1. Physical World Layer

Agents move between three rooms arranged in a triangle
main-room, bowl-room, gifts-room

Gifts exist at fixed locations

Agents physically pick up their assigned gifts

Movement and object manipulation are publicly observable.

2. Assignment Layer

Each agent draws exactly one name (with no self-draws)

Each gift is uniquely mapped to its intended recipient

Actions create world-facts such as “A draws B” and “A has-gift g_ab”

3. Epistemic Layer

The domain is designed for epistemic effects using RPMEP:

Modal operators like a
 (agent a knows φ)

Possibility operators like <a>(φ)

Observability controlled by derive-condition

Private announcements

Public announcements

Inference steps

Nested beliefs (depth 2)

Different problems selectively activate different portions of this layer.

2. Core Actions and Their Epistemic Effects
Movement

Every agent always knows everyone’s location.
This provides the basic observability structure.

Draw-name

If an agent draws in the bowl-room, anyone present observes the result.
This encodes derive-condition–based epistemic visibility.

Pick-gift

Picking up gifts is also publicly visible, meaning agents may deduce the target based on gift identity.

Whisper (Private Announcement)

Only the receiver gets the epistemic update

Demonstrates private announcements, asymmetric belief updates, and the contrast with public communication

Talk (Public Announcement)

Anyone in the same room receives the epistemic update

Demonstrates public announcements, common knowledge formation, and perspective-sensitive updates

Confuse-assign (Uncertainty Action)

Introduces contradictory possibilities

Used to demonstrate suspicion, possibility modalities, and incomplete or ambiguous information

Inference Actions (Problem 5 only)

Agents eliminate candidate possibilities

Demonstrate structured reasoning, syntactic inference, and doxastic closure

Enforce that solutions must contain actual reasoning rather than communication shortcuts

3. Problem Set Overview

Each problem introduces new epistemic mechanisms and ties directly to specific lecture concepts.

Problem 1 — Baseline Draws (Depth 1)

Concepts Demonstrated:

Public observability

Basic knowledge without communication

KD45 belief update at depth 1

Simple doxastic closure

No nested reasoning

Summary:
Agents draw names and collect corresponding gifts.
Each agent ends knowing only their own assignment.

Problem 2 — Private Communication via Whisper (Depth 1)

Concepts Demonstrated:

Private announcements

Asymmetric information

Non-common knowledge

Perspective-dependent belief states

KD45 belief consistency

Summary:
One agent whispers their assignment to another, giving the receiver privileged knowledge that others do not have.

Problem 3 — Public Announcement via Talk (Depth 2)

Concepts Demonstrated:

Public announcements

Multi-agent knowledge alignment

Nested beliefs (e.g., A knows that C knows…)

derive-condition modelling visibility

Depth-2 KD45 introspection

Summary:
An agent publicly announces information in the presence of multiple agents.
Public observability requires nested epistemic modelling.

Problem 4 — Suspicion and Conflicting Announcements (Depth 1)

Concepts Demonstrated:

Possible-belief modality <a>(φ)

Conflicting information

Maintaining multiple possible worlds

Epistemic uncertainty without disjunctions

Non-deterministic belief states

Summary:
An ambiguous announcement creates a belief state where an agent must maintain uncertainty (both φ and ¬φ are possible).

Problem 5 — Structural Deduction and Reasoning Actions (Depth 1)

Concepts Demonstrated:

Elimination-based inference

Syntactic reasoning steps

Domain-level inference operators

Deduction without communication

Ensuring inference is required (via enforced fluents)

KD45 reasoning about eliminated possibilities

Summary:
Agent C deduces B’s assignment strictly from world structure and observations:

C eliminates impossible targets for B

When only one possibility remains, C infers B’s assignment

The planner must use inference actions, not communication

This mirrors lecture content on inference from constraints rather than announcements.

Problem 6 — Mixed Communication and Nested Beliefs (Depth 2)

Concepts Demonstrated:

Combination of public and private announcements

Depth-2 nested knowledge

Perspective-aligned belief updates

Mixed observability

Joint reasoning across communication types

Summary:
Agents use both whisper and talk actions.
Because both private and public communication occur, nested knowledge is required.

The plan must include:

At least one whisper

At least one public talk

Nested belief reasoning such as A knowing that C knows…

Problem 7 — Five-Agent Epistemic Reasoning (Depth 2)

Concepts Demonstrated:

Scaling epistemic planning to larger agent sets

Multi-agent nested beliefs

Persistence of uncertainty in larger domains

Distributed knowledge acquisition

Use of both communication modes

Complex multi-agent inference and observability constraints

Summary:
This is the capstone problem.
Involves:

Five agents

A full 5-cycle assignment

Mixed communication

Nested beliefs

One agent eventually learns the entire assignment

Another agent retains uncertainty

Mandatory use of whisper and talk

Demonstrates the full expressive power of the domain at scale.

4. Relationship to Lecture Topics

This project directly implements concepts from Week 10:

KD45 Epistemic Logic

All belief modalities satisfy:

Seriality (consistency)

Euclidian property (positive introspection)

Transitivity (negative introspection)

Public Announcements

Modeled by derive-conditions that propagate effects to all observers.

Private Announcements

Whispers modify only the receiver’s epistemic state.

Nested Beliefs

Problems 3, 6, 7 require depth-2 reasoning such as:

A knows that C knows φ

D knows that C knows ¬φ

Uncertainty & Possibility

Problem 4 uses:

<a>(φ)

<a>(¬φ)

Conflicting Information

Problem 4 uses explicit ambiguous communication to create contradictory possibilities.

Inference and Deduction

Problem 5 demonstrates:

Structural reasoning

Eliminating possibilities

Achieving knowledge through constraints alone

Explicit inference actions required in the plan

Observability Modelling

derive-condition clauses precisely match lecture descriptions:

At $agent$ l → agent sees event only if colocated

5. Planner Notes

The problems were validated using RPMEP via Planutils.
Plans range from simple (length 10–20) to large (length 36 for 5-agent case).
Depth settings:

Problems 1, 2, 4, 5 → depth 1

Problems 3, 6, 7 → depth 2

All problem files solve efficiently under RPMEP.

6. Summary

This project provides a complete, lecture-aligned demonstration of epistemic planning using RPMEP and PDKB:

Public vs. private communication

Suspicion and uncertainty

Multi-agent nested knowledge

Deductive inference without announcements

Perspective-based visibility modelling

Multi-agent coordination and belief alignment

Controlled scaling from 3 to 5 agents

Across seven problems, complexity increases in a way that mirrors the pedagogical progression of the course.

The result is a cohesive, expressive, and fully functional epistemic planning suite suitable both for academic evaluation and for future extension into more complex multi-agent epistemic scenarios.
