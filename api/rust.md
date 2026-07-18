# Rust

The native crate. Generate a market from a `GenSpec` with `generate`, or drive a
`Synth` handle with the JSON command protocol every other binding uses.

```bash
cargo add wickra-synth
```

```rust
use synth_core::{generate, GenSpec};

let spec = GenSpec::from_json(SPEC).expect("valid spec");
let out = generate(&spec);

println!("{} candles from seed {}", out.candles.len(), spec.seed);
```

## More

- [crates.io/crates/wickra-synth](https://crates.io/crates/wickra-synth) - [docs.rs](https://docs.rs/wickra-synth)
- [Source & examples](https://github.com/wickra-lib/wickra-synth/tree/main/examples/rust)
- [GenSpec & regimes](https://github.com/wickra-lib/wickra-synth/blob/main/docs/SPEC.md)
