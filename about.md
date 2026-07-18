# About Wickra Synth

Wickra Synth generates deterministic synthetic market microstructure — OHLCV
candles, order-book snapshots, trades and funding — from a single seed. A
generation is a JSON document — **data, not code** — so the exact same synthetic
market is drawn in every one of ten languages and is byte-for-byte identical for a
given seed.

## What makes it different

- **One seed, one market.** A fixed portable PRNG (SplitMix64 seeding
  xoshiro256++) lives only in the Rust core, so a given seed yields the identical
  stream on every platform and through every binding — no wall-clock, no OS entropy.
- **The spec is data.** A serde `GenSpec` — a `seed`, a bar count, a `start_price`,
  a list of `regimes` and a `microstructure` block. Because it is data, it crosses
  the C ABI and WASM unchanged.
- **Full microstructure.** Not just a price line: OHLCV candles plus order-book
  snapshots, trades and funding samples, mirroring the JSON shapes of the rest of
  the ecosystem.
- **Deterministic, proven.** The same seed replays the exact same stream, pinned by
  a golden corpus replayed through all ten bindings in CI.

## Why it exists

Realistic market data for tests, training and demos is hard to source and rarely
reproducible. Wickra Synth defines the generator **once**, in Rust, and exposes it
as a JSON-over-C-ABI data API to Rust, Python, Node.js, WASM and — over a C ABI —
C, C++, C#, Go, Java and R. The spec itself is portable JSON, so the same synthetic
market runs anywhere and feeds a backtest, a screen or an RL environment unchanged.

## Open source

Released under the **MIT OR Apache-2.0** license — permissive, OSI-approved, free
for any use including commercial. Source, issues and releases on
[GitHub](https://github.com/wickra-lib/wickra-synth).

## Disclaimer

Wickra Synth is a software library, **not** a trading system, and is provided
**as-is with no warranty**. It generates synthetic data; it does not give financial
advice and its output is not real market data. Use it at your own risk.
