---
layout: home
title: Wickra Synth — deterministic synthetic market microstructure
titleTemplate: false

hero:
  name: "Wickra Synth"
  text: "One seed. A whole market."
  tagline: "Deterministic synthetic market microstructure — OHLCV, order book, trades and funding from a single seed. A GenSpec is data, not code — byte-identical across ten languages."
  image:
    src: /wickra-mark.svg
    alt: Wickra Synth
  actions:
    - theme: brand
      text: View on GitHub
      link: https://github.com/wickra-lib/wickra-synth
    - theme: alt
      text: GenSpec & regimes
      link: https://github.com/wickra-lib/wickra-synth/blob/main/docs/SPEC.md
    - theme: alt
      text: API
      link: /api/rust

features:
  - icon: 🎲
    title: One seed, one market
    details: A fixed portable PRNG (SplitMix64 seeding xoshiro256++) lives only in the Rust core, so a given seed yields the byte-for-byte identical stream on every platform and through every language binding.
  - icon: 🧱
    title: The spec is JSON, not code
    details: A serde GenSpec describes a market regime — trend, drift, volatility and a microstructure block (book depth, spread, trade rate). Because it is data, the exact same generation crosses the C ABI and WASM unchanged.
  - icon: 📊
    title: Full microstructure
    details: "The core emits OHLCV candles plus order-book snapshots, trades and funding samples — realistic synthetic microstructure for tests, training and demos, not just a price line."
  - icon: 🌐
    title: Ten languages, one stream
    details: "The core is a JSON-over-C-ABI data API (Synth::command_json) in Rust, Python, Node.js, WASM, C, C++, C#, Go, Java and R. A developer in any language draws the same synthetic market."
  - icon: 🔌
    title: Drops into the ecosystem
    details: "Output mirrors the JSON shapes of the rest of Wickra, so a generated stream feeds any of the 514 indicators of the Wickra core, a backtest, a screen or an RL environment unchanged."
  - icon: 🧪
    title: Deterministic, proven
    details: The same seed replays the exact same stream, pinned by a golden corpus replayed through all ten bindings in CI. No wall-clock, no OS entropy — the RNG is portable and reproducible.
---

<script setup>
const installTabs = [
  { label: 'Python', lang: 'bash', code: 'pip install wickra-synth' },
  { label: 'Node',   lang: 'bash', code: 'npm install wickra-synth' },
  { label: 'Rust',   lang: 'bash', code: 'cargo add wickra-synth' },
  { label: 'WASM',   lang: 'bash', code: 'npm install wickra-synth-wasm' },
  { label: 'C',      lang: 'bash', code: '# prebuilt header + library from GitHub releases:\n# github.com/wickra-lib/wickra-synth/releases' },
  { label: 'C#',     lang: 'bash', code: 'dotnet add package Wickra.Synth' },
  { label: 'Go',     lang: 'bash', code: 'go get github.com/wickra-lib/wickra-synth-go' },
  { label: 'Java',   lang: 'xml',  code: '<!-- Maven Central -->\n<dependency>\n  <groupId>org.wickra</groupId>\n  <artifactId>wickra-synth</artifactId>\n  <version>0.1.0</version>\n</dependency>' },
  { label: 'R',      lang: 'r',    code: 'install.packages("wickrasynth", repos = "https://wickra-lib.r-universe.dev")' },
]

const pyCode = `import json
from wickra_synth import Synth

spec = json.dumps({
    "seed": 42,
    "bars": 20,
    "start_price": 100.0,
    "regimes": [{"kind": "trend", "len": 20, "drift": 0.002, "vol": 0.01}],
    "microstructure": {"book_depth": 5, "spread_bps": 4.0, "trade_rate": 8.0},
})

synth = Synth(spec)
out = json.loads(synth.command(json.dumps({"cmd": "generate"})))
print(len(out["candles"]), "candles from seed 42")`

const nodeCode = `import { Synth } from 'wickra-synth'

const spec = JSON.stringify({
  seed: 42,
  bars: 20,
  start_price: 100.0,
  regimes: [{ kind: 'trend', len: 20, drift: 0.002, vol: 0.01 }],
  microstructure: { book_depth: 5, spread_bps: 4.0, trade_rate: 8.0 },
})

const synth = new Synth(spec)
const out = JSON.parse(synth.command(JSON.stringify({ cmd: 'generate' })))
console.log(out.candles.length, 'candles from seed 42')`

const cliCode = `# Generate a synthetic market from a spec file, JSON to stdout:
wickra-synth --spec spec.json

# Same seed, same bytes — every time, on every machine:
wickra-synth --spec spec.json --format json > market.json`

const snippetTabs = [
  { label: 'Python', lang: 'python',     code: pyCode },
  { label: 'Node',   lang: 'javascript', code: nodeCode },
  { label: 'CLI',    lang: 'bash',       code: cliCode },
]
</script>

## The spec is JSON, not code

A generation is a `GenSpec`: a `seed`, a bar count, a `start_price`, a list of
`regimes` and a `microstructure` block. The regimes shape the price path; the
microstructure block shapes the book, trades and funding.

```json
{
  "seed": 42,
  "bars": 500,
  "start_price": 100.0,
  "regimes": [
    { "kind": "trend", "len": 300, "drift": 0.002, "vol": 0.01 },
    { "kind": "chop",  "len": 200, "drift": 0.0,   "vol": 0.02 }
  ],
  "microstructure": { "book_depth": 10, "spread_bps": 3.0, "trade_rate": 12.0 },
  "funding": { "interval": 480, "base_rate": 0.0001 }
}
```

## Install

The same synthetic market from every language — native Rust, Python, Node.js and
WASM, plus a C ABI for C, C++, C#, Go, Java and R.

<InstallTabs :tabs="installTabs" />

## Draw it from any language

Construct a `Synth` from the JSON spec, then drive it with
`command(json) -> json`. Every binding returns the same bytes for the same seed.

<InstallTabs :tabs="snippetTabs" />

## Built on the Wickra core

Wickra Synth is part of the [Wickra](https://wickra.org) ecosystem. Its output
mirrors the JSON shapes of [`wickra-core`](https://github.com/wickra-lib/wickra),
so a synthetic stream drops straight into a backtest, a feature build or a live
chart — the same numbers, from a reproducible seed.

> Wickra Synth is a software library, not a trading system, and comes with no
> warranty — use at your own risk.
