# Heron starter

Track one sensor feed’s accepted messages, duplicate sequence numbers, out-of-order arrivals and missed deadlines.

Open the extracted folder in VS Code. With Blyx 0.2.1 and its host toolchain installed, choose **Terminal → Run Task → Run Heron** or run the following command in this directory.

```sh
blyxc native-run main.blyx
```

Expected output

```text
2
1
late
```

The vendor directory contains the framework source for 0.1.0 and its license texts. [Read the API guide](https://www.blyx-lang.space/packages/heron) · [View the release](https://github.com/Rahulchaube1/blyx-heron/releases/tag/v0.1.0)
