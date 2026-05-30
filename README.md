# Modular Multi-State AI Teaching Protocol (MMA-TP)

A conceptual guide to **MMA-TP**, a published AI tutoring protocol for structuring multi-turn LLM tutoring interactions with engineered prompts, JSON specifications, states, gates, and response constraints.

**Paper:** [Modular Multi-State AI Teaching Protocol (MMA-TP)](https://doi.org/10.54254/2755-2721/2026.CH32181)  
**Authors:** Ian Gorrell and Ethan Jordan

![MMA-TP overview diagram](images/mma-tp-overview.png)

*Figure: the same structured JSON specification can produce different tutoring behavior when paired with learner-specific engineered prompts.*

## What problem does MMA-TP address?

Large language models can be useful educational assistants, but ordinary chat-based tutoring can be inconsistent across longer interactions. Common issues include:

- drifting away from the intended lesson structure;
- giving full solutions too early;
- changing pacing, tone, or sequence across sessions;
- producing long explanations when a small next step would be more useful;
- generating unsupported or incorrect information with confidence.

MMA-TP addresses these problems at the **interaction level**. Instead of changing how the model is trained or modifying the model architecture, it changes how the tutoring session is structured and guided.

## What is MMA-TP?

MMA-TP pairs two components:

1. **Engineered prompt** — language-based instructions that define how the tutor should behave.
2. **Structured JSON specification** — a machine-readable rulebook that represents lesson states, transitions, gates, checkpoints, and response restrictions.

The prompt acts as the interpretive layer: it defines the tutor's role, tone, and response discipline. The JSON specification acts as the structured lesson logic: it defines what phase the tutor is in, what responses are allowed, and what must happen before the tutor can advance.

Together, these components bias the model toward protocol-consistent tutoring behavior while preserving the flexibility of natural-language interaction.

## Why is this not just a long prompt?

Prompt-only steering usually relies on one large block of plain-English instruction. This can work well early in a conversation, but as the chat grows, later messages may exert more influence and the original instruction can become less dominant.

MMA-TP adds explicit structure:

- states;
- gates;
- transitions;
- response constraints;
- phase-specific response rules;
- redirect behavior when a gate has not been cleared.

For example, a protocol can require a student to make an attempt before receiving a full answer. If the student tries to skip ahead, the tutor redirects without advancing. If the student satisfies the gate, the tutor can move to the next state.

The important idea is that protocol-consistent tutor behavior becomes part of the future context. Repeated patterns such as “try first,” “explain why,” “gate cleared,” or “we are staying in this step” help preserve the tutoring structure across later turns.

MMA-TP does not make the model deterministic. It still works through probabilistic generation. The protocol changes the structure of the interaction so that protocol-consistent behavior becomes more likely and easier to preserve.

## Basic interaction flow

A simplified MMA-TP interaction follows this pattern:

1. The student sends a message or request.
2. The tutor responds according to the current protocol state.
3. The current state applies phase-specific constraints.
4. A gate determines whether the student has satisfied the requirement for advancement.
5. If the gate is not satisfied, the tutor redirects while staying in the same state.
6. If the gate is satisfied, the tutor transitions to the next allowed state.
7. The tutor's own protocol-consistent responses re-enter the context as behavioral anchors.

## Evaluation summary

In the published evaluation, MMA-TP was compared with prompt-only tutoring baselines across 50 total sessions: 25 MMA-TP sessions and 25 prompt-only baseline sessions.

The evaluation covered multiple instructional tasks, including Python for-loops, Java if/else conditionals, web application fundamentals, C++ functions, and operating systems review.

Reported results included:

- **0 premature solution disclosures** across 25 MMA-TP sessions;
- **19 premature solution disclosures** across 25 prompt-only baseline sessions;
- declared phase order and guardrail behavior preserved in **23 of 25** MMA-TP sessions;
- **no full structural collapse** in MMA-TP sessions.

These results should be interpreted as behavioral evidence, not a formal guarantee. MMA-TP improves interaction structure, but it does not prove perfect or deterministic control over LLM behavior.

## Limitations

MMA-TP has important limitations:

- It does not modify model weights, training procedures, decoding strategies, or model architecture.
- It depends on the capabilities and behavior of the underlying model.
- Platform-level memory or hidden system context can interfere with local protocol behavior.
- The evaluation focused on behavioral stability, not measured student learning outcomes.
- It should not be described as a guarantee of perfect LLM behavior.

## Repository scope

This repository is an explanatory companion for the MMA-TP protocol. It focuses on the concept, mechanism, evaluation summary, and limitations.

It is not intended to be a complete lesson-plan library. Separate repositories may contain example tutor specifications, reusable lesson plans, or applied classroom materials.

## My contributions

I co-authored the published MMA-TP paper with Ian Gorrell. My contributions included editing, literature review support, tutor-session testing and evaluation, explanatory diagrams/graphs, and oral presentation materials. I also co-presented MMA-TP with Ian Gorrell at North Central College's Rall Symposium.

## Citation

Gorrell, I., & Jordan, E. (2026). *Modular Multi-State AI Teaching Protocol (MMA-TP).* Proceedings of CONF-SPML 2026 Symposium: The Artificial Intelligence Tools & Applications. https://doi.org/10.54254/2755-2721/2026.CH32181
