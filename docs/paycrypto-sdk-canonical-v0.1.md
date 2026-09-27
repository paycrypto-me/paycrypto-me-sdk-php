# PayCrypto.Me SDK --- Canonical Architecture Reference

## Pre-1.0 Baseline v0.1

> **Role:** canonical pre-1.0 handoff for SDK inside PayCrypto.Me Public
> Architecture.\
> **Status:** incomplete internals; reason for existence and boundary
> are established.

# 0. Status rule

`v0.x` means incomplete, not optional. Labels: **FROZEN**, **ACCEPTED**,
**CANDIDATE**, **OPEN**, **REJECTED**.

# 1. Reason for existence

**FROZEN:**

``` text
Consumer -> SDK -> Core
```

Consumer does not directly depend on Core.

SDK is not merely convenience:

> Consumers depend on SDK rather than directly on Core so changes in how
> Core capabilities are provided can be absorbed at a controlled
> integration boundary instead of propagating across every Consumer.

SDK is therefore a **change-containment boundary**.

# 2. Boundary

**ACCEPTED:** SDK provides a stable/convenient Consumer-facing surface
while shielding Consumers from Core internals, Primitives,
crypto/protocol composition, external crypto libraries, and
implementation adapters.

SDK may translate between Consumer-facing interaction and Core's
admitted public/application boundary. Exact translation is OPEN.

SDK must not become a bypass around Core to reach Primitives.

# 3. What change containment does not imply

The SDK rationale does **not** establish:

``` text
HTTP
RPC
remote Core
hosted Core
network service
specific serialization protocol
```

Those require independent evidence.

# 4. Materialization/cardinality

**ACCEPTED:** a PHP SDK is currently justified by the real
PHP/WooCommerce Customer.

**OPEN:** neither "exactly one SDK forever" nor "one SDK per language"
is frozen. Future materialization is demand-driven. The architectural
role remains stable even if physical implementations evolve.

# 5. Consumer relationship

**FROZEN:** Consumer enters through SDK.

Consumers should not need Core object-graph internals,
allocation/reconciliation internals, Primitives, BIP32/ECC/encoding, or
implementation-library types.

SDK is not a WooCommerce-specific SDK; WooCommerce is one Customer.

# 6. Core relationship

**FROZEN:** Core owns domain semantics. SDK must not silently
duplicate/redefine them.

PaymentRoute, PaymentInstruction, allocation, reconciliation, and
related domain meaning remain Core-owned. SDK may expose convenient
representations but must preserve Core semantics.

# 7. Primitives relationship

**FROZEN:** SDK does not use Primitives as a supported bypass and must
not expose low-level primitive implementation details upward.

# 8. Evidence

WooCommerce grounds real SDK demand. Existing plugin code may reveal
integration needs but does not define SDK API.

Known requirement areas include payment creation/instruction, enabled
routes, payment presentation data, status/evidence where Core exposes
it, and configuration necessary to invoke Core. These are not frozen
method names or DTOs.

# 9. Rejected

``` text
Consumer -> Core as normal integration
Consumer -> Primitives
SDK exposing crypto-library objects
SDK independently owning payment semantics
SDK designed from WooCommerce classes
SDK dismissed as meaningless because initial deployment is local
future remote/hosted transport inferred without evidence
one SDK per language mandated speculatively
```

# 10. Open specialist agenda

-   public SDK API;
-   command/query/use-case surface;
-   Consumer-facing DTO/value model;
-   Core mappings;
-   error/result translation;
-   sync/async semantics;
-   lifecycle/resource management;
-   configuration;
-   versioning/compatibility;
-   PHP package design;
-   Core contract testing;
-   language conventions;
-   future multi-language criteria;
-   transport adaptation only if concrete architecture later requires
    it.

# 11. Handoff

The SDK specialist starts here rather than from zero. A change to
dependency direction or SDK's change-containment role requires explicit
reconciliation with the Public Architecture Canonical.
