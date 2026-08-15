# PortalKernel Architectural Decisions

This document records important decisions, assumptions, and open questions. It is intentionally lightweight and will grow with the project.

## Decision record format

For significant decisions, record:

- Context — what problem are we solving?
- Decision — what are we choosing?
- Alternatives — what else was considered?
- Reasoning — why was the decision made?
- Status — proposed, accepted, superseded, or rejected.

---

## ADR-001 — Educational project with a framework-oriented design

**Status:** Accepted

**Context**

The primary goal is to learn kernel development while building a working system. The project should remain understandable and should allow experimentation with different subsystem implementations.

**Decision**

PortalKernel will use a modular, framework-oriented design where practical. Subsystems should communicate through clear interfaces, while unnecessary abstraction should be avoided.

**Reasoning**

This supports the project's long-term goal of extensibility without turning modularity into an end in itself.

---

## ADR-002 — Replaceable filesystem implementations are a design goal

**Status:** Accepted as a design goal; implementation pending

**Context**

Filesystem standards and implementations can change. Higher-level kernel code should not need to be rewritten merely because a different filesystem backend is introduced.

**Decision**

PortalKernel should investigate a VFS/filesystem interface that allows multiple filesystem implementations to coexist or be replaced.

**Reasoning**

A stable abstraction can isolate higher-level code from concrete filesystem details and make future experimentation easier.

**Caution**

The abstraction must remain justified by real use. The project should not create a large VFS framework before there is a concrete filesystem problem to solve.

---

## ADR-003 — Kernel architecture is not decided yet

**Status:** Open

**Context**

The project could follow a monolithic, microkernel, hybrid, or another architecture.

**Decision**

No final architecture will be selected before the relevant concepts and trade-offs are understood.

**Reasoning**

Choosing a kernel architecture prematurely would optimize the project around assumptions that have not yet been tested.

---

## ADR-004 — Learning is more important than implementation speed

**Status:** Accepted

**Context**

The project is intended to teach low-level systems concepts rather than simply produce a working kernel as quickly as possible.

**Decision**

The implementation should be approached incrementally. Explanations, experiments, and architectural reasoning are part of the project rather than overhead.

**Reasoning**

A working subsystem whose design and operation are not understood does not fulfill the primary educational purpose of PortalKernel.
