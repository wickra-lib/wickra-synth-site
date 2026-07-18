# Go

The Go binding links the C ABI via cgo. Construct a `Synth` from a JSON spec and
drive it with `Command(json) -> (json, error)`.

```bash
go get github.com/wickra-lib/wickra-synth-go
```

```go
package main

import (
	"fmt"

	wickra "github.com/wickra-lib/wickra-synth-go"
)

func main() {
	spec := `{"seed":42,"bars":20,"start_price":100.0,` +
		`"regimes":[{"kind":"trend","len":20,"drift":0.002,"vol":0.01}],` +
		`"microstructure":{"book_depth":5,"spread_bps":4.0,"trade_rate":8.0}}`

	synth, err := wickra.New(spec)
	if err != nil {
		panic(err)
	}
	defer synth.Close()

	out, err := synth.Command(`{"cmd":"generate"}`)
	if err != nil {
		panic(err)
	}
	fmt.Println(out)
}
```

## More

- [pkg.go.dev/github.com/wickra-lib/wickra-synth-go](https://pkg.go.dev/github.com/wickra-lib/wickra-synth-go)
- [Source & examples](https://github.com/wickra-lib/wickra-synth/tree/main/examples/go)
