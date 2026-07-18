# C\#

The .NET binding wraps the C ABI. Construct a `Synth` from a JSON spec and drive
it with `Command(json) -> json`.

```bash
dotnet add package Wickra.Synth
```

```csharp
using Wickra.Synth;

const string spec =
    "{\"seed\":42,\"bars\":20,\"start_price\":100.0," +
    "\"regimes\":[{\"kind\":\"trend\",\"len\":20,\"drift\":0.002,\"vol\":0.01}]," +
    "\"microstructure\":{\"book_depth\":5,\"spread_bps\":4.0,\"trade_rate\":8.0}}";

using var synth = new Synth(spec);
var output = synth.Command("{\"cmd\":\"generate\"}");
Console.WriteLine(output);
```

## More

- [nuget.org/packages/Wickra.Synth](https://www.nuget.org/packages/Wickra.Synth)
- [Source & examples](https://github.com/wickra-lib/wickra-synth/tree/main/examples/csharp)
