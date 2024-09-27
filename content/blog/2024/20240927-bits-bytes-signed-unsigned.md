---
title: "Signed versus unsigned byte values"
date: 2024-04-25
tags: ["Signed", "Unsigned"]
---

2024-09-27, by Frank Delporte

When using bits and bytes to control electronic components, the conversion from a byte to, e.g., logging output can be a bit confusing as Java uses signed values. This means a byte value has a range of -128 till 127, while you would expect 0 (0x00) till 255 (0xFF).

For example, the hex value `0x8F` (`10001111`) is handled like this:

```java
var b = (byte) Integer.parseInt("10001111", 2);
System.out.println("Byte value 10001111: " + b);

// Output
Byte value 10001111: -113
```

You can use `Byte.toUnsignedInt(b)` to get the expected, unsigned value:

```java
var unsignedInt = Byte.toUnsignedInt(b);
System.out.println("Byte to unsigned integer: " + unsignedInt);

// Output
Byte to unsigned integer: 143
```

This gets explained more in detail [in this blog post](https://webtechie.be/post/2024-09-26-java-bits-bytes-short-int-long-signed-unsigned/) and this video:

{{< youtube PcKRJqo-c9Q >}}