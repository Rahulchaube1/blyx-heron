## Detect an expired feed after a duplicate

Maintain one state per sensor. Use a monotonically increasing integer sequence and a monotonic local receipt clock in milliseconds, both at most 2^53−1. Reset the state when the sensor restarts or its sequence wraps. The gap counter records skipped IDs at acceptance time. Late arrivals do not reduce it. This release monitors application data and exposes its state to the host.

1. Open an empty file named `heron-demo.blyx`.
2. Type `blyx-heron-demo` and select **Heron — runnable example**. You can also use **Snippets: Fill File with Snippet**.
3. Choose **Blyx: Run File** from the command palette. Change an argument near the end of `fn main()` to try another input.

Expected output

```text
2
1
late
```

[Work through the example in the browser](https://www.blyx-lang.space/play?example=package-heron)
