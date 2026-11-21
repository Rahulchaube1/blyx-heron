<img src="assets/logo.png" width="112" height="112" alt="Heron bird logo">

# Blyx Heron

Track one sensor feed’s accepted messages, duplicate sequence numbers, out-of-order arrivals and missed deadlines.

A replayed packet can make an idle sensor appear healthy if every arrival resets its last-seen timer. ROS 2 distinguishes delivery and deadline policies. Heron lets an application choose a freshness deadline and updates that timer only when it accepts a new sample. [ROS 2, Quality of service settings](https://docs.ros.org/en/jazzy/Concepts/Intermediate/About-Quality-of-Service-Settings.html)

## Install and run

Install the Blyx 0.2.1 compiler and a Rust toolchain with a host linker. Clone the versioned release, then run its small example and regression suite.

```sh
cargo install --locked --version 0.2.1 blyxc
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-heron.git
cd blyx-heron
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

Expected output from the small example

```text
2
1
late
```

## Audit a sensor heartbeat trace

Replay sequence and local receipt-time pairs. The bundled trace contains a duplicate, a two-ID gap and one out-of-order delivery. You can feed your own two-column headerless trace into the same program.

```sh
blyxc native-run project.blyx
```

Try your own trace with `blyxc native-run project.blyx -- readings.csv`. Use one sequence number and receipt time per line, without a header.

Project output

```text
accepted=3
duplicates=1
out_of_order=1
skipped_ids=2
```

[Run the portable example in the browser](https://www.blyx-lang.space/play?example=package-heron) · [Follow the handbook exercise](https://doc.blyx-lang.space/guide/heron) · [Download the release](https://github.com/Rahulchaube1/blyx-heron/releases/tag/v0.1.0)

## Use the framework in your own project

From the folder containing your entry file, clone the release into `vendor/heron`.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-heron.git vendor/heron
```

```blyx
use vendor::heron::heron;

fn main() {
    let first = he_observe(he_start(), 10.0, 100.0);
    let next = he_observe(first, 13.0, 120.0);
    let repeated = he_observe(next, 13.0, 145.0);
    println!(at(repeated, 5));
    println!(at(repeated, 3));
    println!(he_status(repeated, 151.0, 30.0));
}
```

Run `blyxc native-run main.blyx`.

Maintain one state per sensor. Use a monotonically increasing integer sequence and a monotonic local receipt clock in milliseconds, both at most 2^53−1. Reset the state when the sensor restarts or its sequence wraps. The gap counter records skipped IDs at acceptance time. Late arrivals do not reduce it. This release monitors application data and exposes its state to the host.

| API | Behavior |
| --- | --- |
| `he_start(), he_observe(state, sequence, receipt_ms)` | Initialize or update [last sequence, last receipt, accepted, duplicates, out of order, skipped IDs]. |
| `he_age(state, now)` | Return milliseconds since the latest accepted observation, or −1 when unavailable. |
| `he_status(state, now, deadline)` | Return unseen, current, late or invalid. A reading remains current exactly at its deadline. |

## Contribute

When opening an issue, include the smallest reproducing Blyx input, the compiler version and the output you expected. [Source and issues](https://github.com/Rahulchaube1/blyx-heron/issues) · [Blyx community](https://www.blyx-lang.space/community)

Dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE).

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
