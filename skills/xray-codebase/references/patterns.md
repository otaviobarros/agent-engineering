# Pattern catalog

Proven structural patterns for the [X-ray](../SKILL.md). Each entry gives the
signs that call for it, the move, the payoff, the conditions that rule it out, and
the diagram that shows it. Cite the pattern's source on its candidate stop. A
pattern outside this catalog needs a named published source and the same fields.

## Explicit state machine

Source: Harel statecharts; the State pattern in *Design Patterns* (Gamma et al.).

- **Signs:** several booleans or status strings describe one lifecycle; guards
  such as `if paid and not cancelled and not shipped` repeat across files; fix
  commits add guards for flag combinations; data types allow states the business
  forbids.
- **Move:** one state field with an enumerated type, one transition table or
  function that owns every legal transition, and side effects attached to named
  transitions. Callers request a transition by event name.
- **Payoff:** illegal states become unrepresentable or rejected in one place; the
  diagram documents the lifecycle; tests enumerate transitions.
- **When not:** two or fewer states, or flags that vary independently.
- **Diagram:** before, a flowchart of the files that read and write each flag;
  after, a `stateDiagram-v2` with every state and labeled transition.

## Ports and adapters

Source: Cockburn, hexagonal architecture.

- **Signs:** domain rules call HTTP clients, databases, queues, the clock, or the
  file system directly; tests need network or heavy mocks; one vendor change
  touches domain files.
- **Move:** the domain defines a port (an interface in its own terms); an adapter
  implements it for each technology; wiring happens at the edge.
- **Payoff:** domain tests run in memory; vendors change in one adapter.
- **When not:** one thin integration with no domain logic around it, or a
  framework that already provides the seam.
- **Diagram:** before, domain nodes with edges straight to external systems;
  after, domain, port, and adapters, with external systems behind adapters only.

## Deep module

Source: Ousterhout, *A Philosophy of Software Design*.

- **Signs:** callers repeat setup or sequencing a module could own; pass-through
  functions; an interface as large as its implementation; the deletion test moves
  no complexity.
- **Move:** merge shallow pieces behind a smaller interface that hides the
  sequencing and defaults.
- **Payoff:** fewer concepts for callers; changes stay inside one module.
- **When not:** callers truly need the separate steps, or the pieces have
  different owners or release cycles.
- **Diagram:** before, callers with edges to many small modules; after, callers
  with one edge to the deep module.

## Functional core, imperative shell

Source: Bernhardt, "Boundaries".

- **Signs:** decision logic interleaved with I/O; the same rule hard to test
  without fixtures; time or randomness read deep inside rules.
- **Move:** pure functions compute decisions from plain values; a thin shell
  gathers inputs, calls the core, and performs effects.
- **Payoff:** fast, exhaustive tests for the core; effects in one visible place.
- **When not:** logic that is mostly I/O orchestration with few decisions.
- **Diagram:** a sequence diagram of shell, core, and effects, before and after.

## Command-query separation

Source: Meyer, *Object-Oriented Software Construction*.

- **Signs:** functions that both return data and change state; reads that
  trigger writes; callers unsure whether a call is safe to repeat.
- **Move:** split each such function into a query with no side effects and a
  command that returns nothing or only an identifier.
- **Payoff:** queries are safe to cache, retry, and call in any order.
- **When not:** atomic operations that must read and write together, such as
  compare-and-swap or queue pop.
- **Diagram:** before and after call graphs with read and write edges labeled.

## Parse at the boundary

Source: King, "Parse, don't validate"; value objects in Evans, *Domain-Driven Design*.

- **Signs:** raw strings or numbers for money, IDs, emails, or units; the same
  validation repeated in several places; bugs from mixed units.
- **Move:** parse input once at the boundary into a type that can only hold valid
  values; pass that type inward.
- **Payoff:** validation in one place; the type system rejects mixed units.
- **When not:** values that pass through without rules.
- **Diagram:** a flowchart from input through the parser to typed domain code.

## Strategy or table dispatch

Source: Strategy pattern in *Design Patterns*; Fowler, "Replace Conditional with
Polymorphism".

- **Signs:** the same `if` or `switch` on a type or kind in several places; each
  new kind edits many files.
- **Move:** one table or interface maps each kind to its behavior; a new kind adds
  one entry.
- **Payoff:** additions touch one place; missing behavior shows at registration.
- **When not:** one conditional site, or kinds that never grow.
- **Diagram:** before, call sites fanning out to branches; after, one dispatcher
  and one node per strategy.

## Anti-corruption layer

Source: Evans, *Domain-Driven Design*.

- **Signs:** an external API's names, formats, or status codes appear across
  domain code; an upstream change forces edits in many files.
- **Move:** one translation layer maps the external model to the domain model.
- **Payoff:** upstream changes stay in the layer; the domain keeps its language.
- **When not:** the external model already is the domain model, such as a thin
  admin tool over one API.
- **Diagram:** a flowchart with the external system, the layer, and the domain.

## Idempotent side effects

Source: idempotency keys in payment APIs; transactional outbox in Richardson,
*Microservices Patterns*.

- **Signs:** retries around calls that charge, send, or create; duplicate
  messages or records in incident fixes; database writes and messages sent
  without one transaction.
- **Move:** give each effect a stable idempotency key, or record the effect in an
  outbox inside the same transaction and deliver it separately.
- **Payoff:** retries become safe; crashes no longer lose or duplicate effects.
- **When not:** effects that are already idempotent by design, such as an
  upsert by natural key.
- **Diagram:** a sequence diagram of a retry before and after.

## Modular boundary

Source: Parnas, "On the Criteria To Be Used in Decomposing Systems into Modules".

- **Signs:** co-change across directories for one feature; circular imports;
  shared mutable state across modules; one change touching many layers.
- **Move:** regroup code so that each likely change stays inside one module, and
  expose a narrow interface between modules.
- **Payoff:** features change in one place; ownership and tests follow the module.
- **When not:** the co-change comes from a one-time migration, not a recurring
  change.
- **Diagram:** a before and after module map with co-change edges weighted.
