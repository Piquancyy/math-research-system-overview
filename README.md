# Mathematical Research System

一个面向长期数学研究的、以证据与审计为中心的工作流系统。

A research workflow system for long-running mathematical work, designed around explicit evidence, reviewable state, and clear boundaries between research process and mathematical proof.

## Purpose

Long mathematical projects can lose rigor when claims silently change, source scope drifts, local checks are described as global results, failed routes are forgotten, or task context is carried only in informal summaries.

This project organizes those risks into an explicit research workflow. It is designed to help maintain a reliable record of what is known, conditional, blocked, mechanically checked, or ready for further review.

## Core Workflow

- **Claim cards** record the exact statement, hypotheses, conclusion, constants, endpoints, source scope, and fragile proof steps.
- **Source-fidelity review** compares a local claim with its original source before the claim is reused or strengthened.
- **Proof gates** distinguish open questions, conditional conclusions, local certificates, source-faithful statements, mechanical checks, and public-claim-ready results.
- **Formula-first certificates** require explicit maps, estimates, constants, errors, and limiting steps at proof-critical transitions.
- **Adversarial review** searches for counterexamples, hidden assumptions, endpoint failures, and conclusions stronger than the available evidence.
- **Obstruction ledgers** preserve failed routes and reusable negative results.
- **Reproducible state records** support recovery across long research cycles.

## Evidence Boundary

This system manages research process and evidence. It is **not** an automated theorem prover.

A successful build, a passing automated check, a version-control record, a finite computation, or AI-generated analysis is useful engineering evidence, but none is mathematical proof authority by itself. Substantive claims require explicit certificates, source verification, and appropriate human review.

## Result Classification

Research outcomes are recorded with explicit status rather than a generic "proved" label:

| Status | Meaning |
| --- | --- |
| `open` | Essential obligations remain unresolved. |
| `conditional` | The conclusion relies on an unproved assumption or missing input. |
| `counterexample` | The current formulation is refuted or obstructed. |
| `proved-local` | A local certificate exists, while other review gates remain open. |
| `source-faithful` | The stated scope has been checked against the original source. |
| `mechanically-verified` | Deterministic mechanical checks have passed. |
| `public-claim-ready` | Required source, proof, review, and mechanical evidence has been aligned for the exact claim. |

## Availability

This public repository describes the research methodology and system design.

The implementation, active research materials, unpublished proofs, internal automation, and project-specific evidence remain under controlled access. They are not included here to protect intellectual property, active research integrity, and private project context.

## Scope

The system does not claim to solve a specific open problem. Its role is to provide disciplined infrastructure for mathematical research, where process consistency must never be confused with proof correctness.
