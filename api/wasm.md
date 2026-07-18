# WASM

The WebAssembly build runs the same Rust core in the browser or any WASM runtime.
Construct a `Synth` from a JSON spec and drive it with `command(json) -> json`.

```bash
npm install wickra-synth-wasm
```

```javascript
import init, { Synth } from 'wickra-synth-wasm'

await init() // fetches and instantiates the .wasm module

const spec = JSON.stringify({
  seed: 42, bars: 20, start_price: 100.0,
  regimes: [{ kind: 'trend', len: 20, drift: 0.002, vol: 0.01 }],
  microstructure: { book_depth: 5, spread_bps: 4.0, trade_rate: 8.0 },
})

const synth = new Synth(spec)
const out = JSON.parse(synth.command(JSON.stringify({ cmd: 'generate' })))
console.log(out.candles.length, 'candles')
```

The same seed yields a stream byte-identical to the native build. See the
[live demo](/demo) for the Wickra core running in your browser.

## More

- [npmjs.com/package/wickra-synth-wasm](https://www.npmjs.com/package/wickra-synth-wasm)
- [Source & examples](https://github.com/wickra-lib/wickra-synth/tree/main/bindings/wasm)
