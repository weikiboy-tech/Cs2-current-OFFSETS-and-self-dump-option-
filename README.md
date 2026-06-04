# CS2 Current OFFSETS and Self-Dump Option!

**CS2 Current OFFSETS and Self-Dump Option!** is a modern, reproducible CS2 offset collection project.
It provides a command-line dumper that reads live game memory through `memflow` and exports clean, parser-friendly
offset artifacts in one command.

Repository goal:
- keep offsets up to date as Valve updates CS2,
- keep output deterministic and automation-friendly,
- offer a GitHub-style workflow for regular updates.

---

## Key Features

- **Single workflow to get your own offsets**
  - run once locally, generate fresh offsets without waiting for third parties.
- **Cross-platform runtime**
  - Windows and Linux support via `memflow` connectors.
- **Structured output**
  - produces `json`, `hpp`, `cs`, `rs`, and `zig` artifacts by default.
- **Drop-in compatible offsets**
  - the generated JSON keys match common external consumer layouts and are ready for integration with popular CS2 DMA projects.
- **CI-ready**
  - GitHub Actions workflow for build/release packaging.

---

## Quick Start

### 1) How to Use the Offsets

**Option A: Copy Current Offsets**
- Check your cheat codebase to see which file formats you need (e.g., `json`, `hpp`, `cs`, etc.)
- Copy the corresponding files from the `output` directory of this project
- Integrate them directly into your cheat

**Option B: Dump Offsets Yourself**
- Want to generate the latest offsets on your own? No problem!
- Follow the instructions below and run the dumper yourself

---

## Output Artifacts

The dumper generates multiple formats for different use cases:

- `json` — runtime offset object (most commonly used)
- `hpp` — C++ header
- `cs` — C# classes/consts
- `rs` — Rust const modules
- `zig` — Zig source

The `json` files (`offsets.json`) are fully compatible with commonly used CS2 tools like:
- [`Enoouo/Pro-CS2_DMA`](https://github.com/Enoouo/Pro-CS2_DMA)
- [`KEV0143/Direct-memory-access-CS2-DMA`](https://github.com/KEV0143/Direct-memory-access-CS2-DMA)

Just copy the generated JSON offsets directly into your project's offset files!

### Example Structure (JSON)

```json
{
  "client.dll": {
    "dwCSGOInput": 33949395,
    "dwEntityList": 35322339,
    "dwGameEntitySystem": 35346515
  }
}
```

The modules and `dw...` keys follow the standard format expected by most tools.

---

## Dumping Offsets Yourself

### 1) Download or Build the Binary
- Download a pre-built binary from [GitHub Releases](https://github.com/weikiboy-tech/Cs2-current-OFFSETS-and-self-dump-option-/releases).
- Or build it yourself with Rust 1.74.0+.

### 2) Run
Start CS2 (main menu is enough) and run the dumper:

```bash
cargo run --release
```

Or use the compiled binary:

```bash
./target/release/cs2-dumper
```

### 3) Output
All generated files will be written to the `./output` directory.

---

## CLI Overview

`cs2-dumper` supports the following options:
- `-c, --connector <connector>` (optional): memflow connector name.
- `-a, --connector-args <connector-args>` (optional): connector arguments.
- `-f, --file-types <file-types>`: generated formats.
- `-i, --indent-size <indent-size>`: JSON indentation.
- `-o, --output <output>`: output directory (default `output`).
- `-p, --process-name <process-name>`: target process (default `cs2.exe`).
- `-v...`: increase verbosity.
- `-h, --help` and `-V, --version`.

---

## Contributing

- Keep commits focused and include output format impact in your commit message.
- Update signatures/output schema together so automation stays deterministic.
- Add tests for formatting and critical parser assumptions when changing core dump behavior.

## License

MIT License. See [LICENSE](./LICENSE).
