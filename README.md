# Current CS2 Offsets

**Current CS2 Offsets** is a modern, reproducible CS2 offset collection project.
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
- **CI-ready**
  - GitHub Actions workflow for build/release packaging.

---

## Quick Start

### 1) Download or build locally
- Download a built binary from [GitHub Releases](https://github.com/YOUR_GITHUB_USERNAME/current-cs2-offsets/releases) (once published).
- Or build from source with Rust 1.74.0+.

### 2) Run
Run from the project root while CS2 is open (main menu is enough):

```bash
cargo run --release
```

Or run the compiled binary:

```bash
./target/release/cs2-dumper
```

### 3) Output
By default, all generated files are written to `./output`.

---

## Output Artifacts

The dumper writes multiple formats for different consumers:

- `json` — ready-to-consume runtime offset object
- `hpp` — C++ header
- `cs` — C# classes/consts
- `rs` — Rust const modules
- `zig` — Zig source

### Example structure (JSON)

```json
{
  "client.dll": {
    "dwCSGOInput": 33949395,
    "dwEntityList": 35322339,
    "dwGameEntitySystem": 35346515
  }
}
```

This is exactly the format you asked for: module names at top level and a `dw...` key/value map per module.

---

## CLI Overview

`cs2-dumper` supports:
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
