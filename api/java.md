# Java

The Java binding links the C ABI via a small JNI shim. Construct a `Synth` from a
JSON spec and drive it with `command(json) -> json`.

```xml
<!-- Maven Central -->
<dependency>
  <groupId>org.wickra</groupId>
  <artifactId>wickra-synth</artifactId>
  <version>0.1.0</version>
</dependency>
```

```java
import org.wickra.synth.Synth;

String spec =
    "{\"seed\":42,\"bars\":20,\"start_price\":100.0,"
  + "\"regimes\":[{\"kind\":\"trend\",\"len\":20,\"drift\":0.002,\"vol\":0.01}],"
  + "\"microstructure\":{\"book_depth\":5,\"spread_bps\":4.0,\"trade_rate\":8.0}}";

try (Synth synth = new Synth(spec)) {
    String out = synth.command("{\"cmd\":\"generate\"}");
    System.out.println(out);
}
```

## More

- [central.sonatype.com/artifact/org.wickra/wickra-synth](https://central.sonatype.com/artifact/org.wickra/wickra-synth)
- [Source & examples](https://github.com/wickra-lib/wickra-synth/tree/main/examples/java)
