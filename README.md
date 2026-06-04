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
  - the generated JSON keys match common external consumer layouts and are ready for integration with projects like [`Enoouo/Pro-CS2_DMA`](https://github.com/Enoouo/Pro-CS2_DMA).
- **CI-ready**
  - GitHub Actions workflow for build/release packaging.

---

## Quick Start

### 1) Wie du die Offsets nutzt

**Option A: Aktuelle Offsets kopieren**
- Schau in deinem Cheat nach, welche Dateiformate du brauchst (z.B. `json`, `hpp`, `cs`, etc.)
- Kopiere die entsprechenden Dateien aus dem `output`-Verzeichnis dieses Projekts
- Integriere sie direkt in deinen Cheat

**Option B: Offsets selbst dumpen**
- Du möchtest die neuesten Offsets selbst generieren? Kein Problem!
- Folge den Anweisungen unten und führe den Dumper selbst aus

---

## Output Artifacts

Der Dumper generiert mehrere Formate für verschiedene Anwendungen:

- `json` — runtime offset object (am häufigsten verwendet)
- `hpp` — C++ header
- `cs` — C# classes/consts
- `rs` — Rust const modules
- `zig` — Zig source

Die `json`-Dateien (`offsets.json`) sind vollständig kompatibel mit häufig verwendeten CS2-Tools wie [`Enoouo/Pro-CS2_DMA`](https://github.com/Enoouo/Pro-CS2_DMA).

### Beispiel-Struktur (JSON)

```json
{
  "client.dll": {
    "dwCSGOInput": 33949395,
    "dwEntityList": 35322339,
    "dwGameEntitySystem": 35346515
  }
}
```

Die Module und `dw...` keys entsprechen dem Standard-Format, das die meisten Tools erwarten.

---

## Offsets selbst dumpen

### 1) Binary herunterladen oder bauen
- Lade ein fertiges Binary aus den [GitHub Releases](https://github.com/weikiboy-tech/Cs2-current-OFFSETS-and-self-dump-option-/releases) herunter.
- Oder baue es selbst mit Rust 1.74.0+.

### 2) Ausführen
Starte CS2 (Hauptmenü reicht aus) und führe den Dumper aus:

```bash
cargo run --release
```

Oder nutze das kompilierte Binary:

```bash
./target/release/cs2-dumper
```

### 3) Output
Alle generierten Dateien landen im `./output`-Verzeichnis.

---

## CLI Übersicht

`cs2-dumper` unterstützt folgende Optionen:
- `-c, --connector <connector>` (optional): memflow connector name.
- `-a, --connector-args <connector-args>` (optional): connector arguments.
- `-f, --file-types <file-types>`: generierte Formate.
- `-i, --indent-size <indent-size>`: JSON Einrückung.
- `-o, --output <output>`: output directory (default `output`).
- `-p, --process-name <process-name>`: target process (default `cs2.exe`).
- `-v...`: erhöhe die Verbosität.
- `-h, --help` und `-V, --version`.

---

## Contributing

- Keep commits focused and include output format impact in your commit message.
- Update signatures/output schema together so automation stays deterministic.
- Add tests for formatting and critical parser assumptions when changing core dump behavior.

## License

MIT License. See [LICENSE](./LICENSE).
