# PayCrypto.Me SDK PHP

**A stable, convenient PHP integration surface for PayCrypto.Me payment capabilities.**

PayCrypto.Me SDK PHP gives PHP applications a clear way to use payment
capabilities without coupling their integration code to the internal machinery
that provides them.

It is designed as a practical integration layer and a deliberate architectural
boundary: something that can evolve with the capabilities behind it without
forcing every application to inherit those changes.

> **We own the integration boundary, not payment domain semantics.**

Rather than expose domain object graphs, payment orchestration, protocol
composition, cryptographic libraries, or implementation adapters, the SDK
keeps those concerns behind a PHP-facing surface.

---

## Why this project exists

Payment capabilities need an integration surface that remains useful while the
way they are provided evolves.

Applications can otherwise become coupled to internal domain models, low-level
protocol and cryptographic details, or a particular implementation strategy.
Each internal change then becomes an application integration change.

The SDK takes a different path:

```text
concrete integration need
        ↓
convenient PHP interaction
        ↓
Core's admitted public/application boundary
        ↓
contained implementation change
```

The goal is not to create another payment engine.

The goal is to make PayCrypto.Me payment capabilities **clear to integrate,
stable to depend on, and able to evolve without spreading implementation
concerns across every application**.

## What makes SDK different?

### Integration-first

The SDK grows from concrete integration requirements rather than from an
application's existing classes or an internal implementation's object graph.
Contract details remain open until the required integration is understood.

### Change containment

The SDK is a controlled integration boundary. A change in how a payment
capability is provided should be absorbed there instead of propagating through
every application that uses it.

This is why the SDK is more than a convenience wrapper.

### Semantic preservation

Core owns payment semantics. The SDK may offer convenient PHP representations
and translate interactions at its boundary, but it does not create a second
payment model for routes, instructions, allocation, reconciliation, or related
domain meaning.

### Implementation shielding

SDK users work with PHP-facing contracts. They should not need to know the
object graph, protocol machinery, cryptographic implementation, or adapter
behind a payment capability.

Low-level types and implementation details do not belong in the SDK surface.

### Transport-neutral

The presence of an SDK does not establish HTTP, RPC, a network service, a
remote or hosted runtime, or a serialization protocol. Those are independent
decisions that require their own evidence.

## Current architectural direction

PHP is the first justified materialization of the SDK boundary. It is an SDK
for PHP applications, not an adaptation of any particular application's
classes or lifecycle.

The architectural role does not establish a permanent single SDK or one SDK
per language. Future materializations are demand-driven.

The interface develops from evidence at that boundary. Current requirement
areas include payment creation and instructions, enabled routes,
payment-presentation data, status or evidence where Core exposes it, and the
configuration required to invoke Core. They do not yet freeze method names,
DTOs, or classes.

## PayCrypto.Me Public Architecture

Before reading or changing this repository's domain architecture, start with
[PayCrypto.Me Public Architecture](./docs/PUBLIC-ARCHITECTURE.md). It is the
shared entry point and authority map: it establishes the public architecture's
scope, the relationship between its domains, and the context in which the SDK
operates.

Then read the current [SDK canonical architecture](./docs/paycrypto-sdk-canonical-v0.1.md).
The public architecture document provides context and navigation; the SDK
canonical remains the authority for the SDK's internals and evolution.

For human and AI-agent work, the default context is:

```text
PUBLIC-ARCHITECTURE.md
        +
current SDK canonical
```

Load other canonicals and evidence only when the work crosses or may affect
their architectural boundaries.

## Architecture is part of the project

The code tells you what currently exists.

The canonical architecture explains **why the SDK exists, which decisions are
intentional, what remains open, what has been rejected, and how the project may
legitimately evolve**.

Before introducing a public interaction:

```text
What concrete integration need does it serve?
        ↓
Which Core-admitted capability does it invoke?
        ↓
Can the SDK represent it conveniently while preserving its meaning?
        ├── yes → define the interaction and mapping
        └── no  → resolve the boundary before creating SDK semantics
```

The canonical architecture is therefore a contribution contract, not background
reading.

## Project status

The SDK boundary is established in the pre-1.0 v0.1 canonical architecture.
Its internal composition and concrete contracts are intentionally being
developed from real requirements.

The public API and value model, mappings and result translation, and lifecycle,
configuration, versioning, compatibility, and package design remain open.

An unresolved internal decision is preferable to a prematurely frozen API or a
weakened boundary.

For the current source of truth, read the
[SDK canonical architecture](./docs/paycrypto-sdk-canonical-v0.1.md).

## Contributing

Contributions should preserve the integration-first model.

Before proposing a public interaction, identify:

1. the concrete PHP integration requirement;
2. the Core-admitted capability it invokes;
3. the PHP-facing representation or interaction required;
4. how the mapping preserves payment semantics;
5. which implementation details must remain shielded;
6. why an existing interaction cannot express the requirement, if proposing a
   new abstraction.

An existing application structure, library API, or assumed transport is not
architectural evidence by itself.

Architectural changes should update the canonical documentation rather than
allowing implementation drift to redefine the project silently.

## License

PayCrypto.Me SDK PHP is released under the [MIT License](./LICENSE).

## The guiding idea

> **The goal is to let applications use PayCrypto.Me payment capabilities
> without inheriting the changing internals that make those capabilities
> possible.**

PayCrypto.Me SDK PHP exists as a **stable, intentional integration boundary in
its own right**.
