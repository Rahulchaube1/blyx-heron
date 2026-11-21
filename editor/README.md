# Blyx Heron

Track one sensor feed’s accepted messages, duplicate sequence numbers, out-of-order arrivals and missed deadlines.

This extension includes the Blyx Heron 0.1.0 source, a runnable example and completions for its public functions. It uses the Blyx Language extension for syntax highlighting and execution.

## Run in the editor

1. Open an empty file named `heron-demo.blyx`.
2. Type `blyx-heron-demo` and select **Heron — runnable example**. You can also use **Snippets: Fill File with Snippet**.
3. Choose **Blyx: Run File** from the command palette. Change an argument near the end of `fn main()` to try another input.

Expected output

```text
2
1
late
```

## Use Heron in a project

Extract the starter into a new folder. It contains `main.blyx`, the licensed framework source in `vendor/heron`, and a VS Code task. With the Blyx 0.2.1 compiler and host toolchain installed, run `blyxc native-run main.blyx` from that folder. Type `blyx-heron-` in a Blyx file to see the framework completions. [Download the starter ZIP](https://github.com/Rahulchaube1/blyxxxx/releases/download/framework-editors-v0.1.0/blyx-heron-starter-0.1.0.zip)

[API and input requirements](https://www.blyx-lang.space/packages/heron) · [Framework source](https://github.com/Rahulchaube1/blyx-heron/tree/945ce68dbeb541d760351f359a71252694b2db06) · [Report an issue](https://github.com/Rahulchaube1/blyx-heron/issues)

[GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) · [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube)
