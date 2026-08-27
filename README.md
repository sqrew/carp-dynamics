# carp-dynamics

A high-performance Newtonian dynamics and integration library for the [Carp](https://github.com/carp-lang/Carp) programming language.

This library provides the "nouns of motion"—managing forces, velocity, and integration logic. It acts as the bridge between static transforms and a fully simulated physical world.

## Features
- **Physically Consistent Damping**: Uses a time-step safe exponential decay model ($v = v \cdot damping^{dt}$) to prevent numerical energy growth.
- **Semi-Implicit Euler**: Uses the standard game industry integration order (Update Velocity $\to$ Update Position) for maximum stability.
- **Simulation Guardrails**: Built-in Delta-Time clamping to prevent simulation "explosions" during frame spikes or window dragging.
- **Static Body Support**: First-class support for immovable objects with enforced invariants (infinite mass, zero inverse-mass).
- **Lightweight**: Zero external dependencies beyond the standard library and `carp-transform`.

## Installation
```clojure
(load "https://github.com/sqrew/carp-dynamics@master")
```


## Examples

See [examples.md](examples.md) for usage examples.
## Design Philosophy
`carp-dynamics` follows the **Separation of Mechanisms** principle. It handles *how* objects move through space based on forces, but it does not have opinions about *why* they collide. This makes it perfectly suitable for both traditional rigid-body physics and custom SDF-based resolution systems.

## License
MIT
