# R

The R package links the C ABI. Build a synth from a JSON spec with `wksynth_new`,
then drive it with `wksynth_command`.

```r
install.packages("wickrasynth", repos = "https://wickra-lib.r-universe.dev")
```

```r
library(wickrasynth)

spec <- '{"seed":42,"bars":20,"start_price":100.0,
          "regimes":[{"kind":"trend","len":20,"drift":0.002,"vol":0.01}],
          "microstructure":{"book_depth":5,"spread_bps":4.0,"trade_rate":8.0}}'

synth <- wksynth_new(spec)
out <- wksynth_command(synth, '{"cmd":"generate"}')
cat(out)
```

## More

- [wickra-lib.r-universe.dev](https://wickra-lib.r-universe.dev)
- [Source & examples](https://github.com/wickra-lib/wickra-synth/tree/main/examples/r)
