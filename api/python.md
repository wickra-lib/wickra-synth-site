# Python

The Python package wraps the Rust core over the C ABI. Construct a `Synth` from a
JSON spec and drive it with `command(json) -> json`.

```bash
pip install wickra-synth
```

```python
import json
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
print(len(out["candles"]), "candles")
```

## More

- [pypi.org/project/wickra-synth](https://pypi.org/project/wickra-synth/)
- [Source & examples](https://github.com/wickra-lib/wickra-synth/tree/main/examples/python)
