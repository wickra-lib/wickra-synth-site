# Node.js

The Node package is a native napi addon over the Rust core. Construct a `Synth`
from a JSON spec and drive it with `command(json) -> json`.

```bash
npm install wickra-synth
```

```javascript
import { Synth } from 'wickra-synth'

const spec = JSON.stringify({
  seed: 42,
  bars: 20,
  start_price: 100.0,
  regimes: [{ kind: 'trend', len: 20, drift: 0.002, vol: 0.01 }],
  microstructure: { book_depth: 5, spread_bps: 4.0, trade_rate: 8.0 },
})

const synth = new Synth(spec)
const out = JSON.parse(synth.command(JSON.stringify({ cmd: 'generate' })))
console.log(out.candles.length, 'candles')
```

## More

- [npmjs.com/package/wickra-synth](https://www.npmjs.com/package/wickra-synth)
- [Source & examples](https://github.com/wickra-lib/wickra-synth/tree/main/examples/node)
