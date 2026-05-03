---
name: software-architecture
description: Apply Clean Architecture, SOLID principles, design patterns, and software architecture best practices when designing systems, reviewing code structure, planning a new project, or refactoring existing code. Use when the user asks about architecture decisions, how to structure a project, which design pattern to use, how to apply SOLID, or when reviewing code for architectural quality. Covers: Clean Architecture layers, SOLID, DDD, common patterns (Repository, Factory, Strategy, Observer, CQRS), and anti-patterns to avoid.
---

# Software Architecture

## Clean Architecture

### Layer Structure (outside → inside)
```
┌─────────────────────────────────────┐
│  Frameworks & Drivers               │  ← FastAPI, Express, React, DB drivers
│  (Infrastructure Layer)             │
├─────────────────────────────────────┤
│  Interface Adapters                 │  ← Controllers, Presenters, Gateways
│  (Adapter Layer)                    │
├─────────────────────────────────────┤
│  Application Business Rules         │  ← Use Cases, Application Services
│  (Use Case Layer)                   │
├─────────────────────────────────────┤
│  Enterprise Business Rules          │  ← Entities, Domain Models
│  (Domain Layer)                     │
└─────────────────────────────────────┘
```

**Dependency Rule:** Dependencies only point inward. The domain knows nothing about the database.

### Practical Application
- Domain entities have no framework imports
- Use cases define interfaces (ports); infrastructure implements them (adapters)
- Controllers are thin — they translate HTTP to use case calls, nothing more
- The database is a detail, not the architecture

---

## SOLID Principles

**S — Single Responsibility**
A class/module has one reason to change. If you need "and" to describe what it does, split it.

**O — Open/Closed**
Open for extension, closed for modification. Add behavior via new classes, not by modifying existing ones. Strategy pattern is the classic implementation.

**L — Liskov Substitution**
Subtypes must be substitutable for their base types without breaking the program. If you find yourself checking `isinstance()` in business logic, Liskov is violated.

**I — Interface Segregation**
Many specific interfaces > one general interface. Clients shouldn't depend on methods they don't use.

**D — Dependency Inversion**
High-level modules don't depend on low-level modules — both depend on abstractions. Inject dependencies; don't construct them inside classes.

---

## Essential Design Patterns

### Creational
**Factory Method** — when you need to create objects without specifying the exact class
**Builder** — when constructing complex objects step by step

### Structural
**Repository** — abstracts data access behind an interface; use case calls `user_repo.find_by_id()`, doesn't know if it's Postgres or Redis
**Adapter** — wraps incompatible interfaces; isolates third-party code

### Behavioral
**Strategy** — encapsulates interchangeable algorithms; inject the algorithm, don't hardcode it
**Observer/Event** — decouple producers from consumers; domain events are the DDD version
**Command** — encapsulate requests as objects; enables undo, queuing, logging

---

## Domain-Driven Design (Core Concepts)

**Entity** — has identity (ID), state can change, two entities with same ID are the same object
**Value Object** — no identity, defined by its attributes, immutable (Money, Address, Email)
**Aggregate** — cluster of entities/VOs with a root; transactions happen within one aggregate
**Domain Event** — something that happened in the domain that other parts care about
**Repository** — collection-like interface to access aggregates
**Service** — domain logic that doesn't fit in an entity

---

## Architecture Patterns

### CQRS (Command Query Responsibility Segregation)
Separate read models from write models. Commands change state; queries return data. Use when read and write load patterns differ significantly.

### Event Sourcing
Store events, not state. Current state = replaying all events. Use when audit trail, temporal queries, or undo are requirements. Warning: significant complexity cost.

### Hexagonal Architecture (Ports & Adapters)
Application core defines ports (interfaces); adapters implement them. Database, HTTP, and message queue are all adapters. Core is fully testable without infrastructure.

---

## Anti-Patterns to Avoid

**Big Ball of Mud** — no clear structure, everything depends on everything
**Anemic Domain Model** — entities are just data bags, all logic in services
**God Object** — one class knows too much and does too much
**Leaky Abstractions** — database details seeping into business logic
**Premature Optimization of Architecture** — adding CQRS/Event Sourcing before scale requires it

---

## Architecture Decision Template

When making an architecture decision, document:
```
Context: [What situation are we in?]
Decision: [What we chose]
Rationale: [Why — including rejected alternatives]
Consequences: [What becomes easier, what becomes harder]
```

---

## Quick Heuristics

- If a change requires modifying multiple unrelated files → coupling problem
- If testing requires running the full application → dependency inversion violated
- If the code can't be understood without knowing the framework → architecture leaked
- If you're not sure where new code goes → the layer structure isn't clear enough

Source: adapted from ComposioHQ/awesome-claude-skills/software-architecture + standard references
