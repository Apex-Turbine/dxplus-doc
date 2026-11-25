# Headless Offline Query CLI (`DX+OfflineQueryCli`)

**`DX+OfflineQueryCli`** is a headless command-line execution and validation utility bundled with DX+ that loads offline design graphs (`.dpd` / `.json`), resolves multi-match database records and reference perturbations, simulates Viewer tree construction and plot queries, and prints diagnostics without launching a graphical window.

---

## Common Use Cases

- Automating batch validation of `.dpd` analysis templates across regression `.dxdb` databases.
- Inspecting multi-match source conflicts and processor reference perturbation keys (`Signal Math`, `FDFT` Trigger Reference, `Rev Resample`, `Relative Phase`) before GUI submission.
- Simulating plot slider playback loops (`strip`, `history`, `message`) to benchmark query throughput and verify zero Phoenix engine errors (`exit code 0`).
- Generating synthetic multi-source test fixtures (`RAW` + `Scaled`) with `--generate-fixture`.

---

## Command-Line Options Reference

| Long Flag | Short | Argument | Purpose | Requirement / Default |
| :--- | :--- | :--- | :--- | :--- |
| `--graph` | `-g` | `<path>` | Input offline graph file (`.dpd` or `.json`) | **Required** *(unless `-R` or `-G` is used)* |
| `--dxdb` | `-d` | `<path>` | Target SQLite `.dxdb` / `.dxdb.index` database | **Required** |
| `--record` | `-r` | `<id[,id...]>` | One or more 1-based record numbers (comma-separated or repeated) | **Required** *(default `1` with `-R`)* |
| `--stream` | `-s` | `<source:stream>` | Explicit query target formatted as `sourceName:streamName` | **Required** *(unless `-P` or `-R` is used)* |
| `--event` | `-e` | `<id[,id...]\|all>` | Target event ID(s) or `all` | Optional *(default `-1` / all)* |
| `--select-sources` | `-M` | `<name[,name...]\|rec=name,...>` | Select matching DB sources per record (e.g. `RAW,Scaled` or `1=RAW`) | Optional *(default: all)* |
| `--select-perturbations` | `-X` | `<all\|default\|key=opt1,opt2>` | Filter processor reference/math perturbations | Optional *(default: `all`)* |
| `--simulate-plots` | `-P` | — | Build the full DataViewer tree (`ApexDataTableItem` / `StreamDataItem`), print `plotSourceLabel()` groupings, and execute plot queries for every resolved stream | Optional flag |
| `--test-multi-match-refs` | `-R` | `<signal-math\|fft-trig\|rev-resample\|relative-phase\|all>` | Synthesize and execute end-to-end multi-match reference scenarios against `--dxdb` | Optional |
| `--generate-fixture` | `-G` | `<dir>` | Synthesize a multi-source `.dxdb` database and generic `StreamSelect` `.json` design into `<dir>` | Optional |
| `--plot-count` | `-p` | `<count>` | Simulated plot instances per stream | Default `1` |
| `--plot-type` | — | `<auto\|history\|strip\|message>` | Simulation mode (`strip` runs one query; `history`/`message` step through playback) | Default `auto` |
| `--steps` | `-c` | `<count>` | Playback slider steps per loop | Default `1` |
| `--slider-step` | `-T` | `<seconds>` | Time advance per simulated step | Default `1.0` |
| `--loops` | `-l` | `<count>` | Number of rewind/playback cycles | Default `1` |
| `--history-duration` | `-H` | `<seconds>` | Active history window duration | Default `0.0` |
| `--reader-type` | `-t` | `<uuid>` | Override database reader adapter UUID | Auto-resolved |
| `--single-step` | `-S` | — | Force bounded single-step query mode | Optional flag |
| `--verbose` | `-v` | — | Print detailed log output and sample payload values | Optional flag |

---

## Examples

### Simulate Full DataViewer Plot Tree & Queries for a Design

```powershell
DX+OfflineQueryCli.exe -g "C:\designs\turbine_analysis.dpd" -d "C:\data\run01.dxdb" -r 1 -P -v
```

### Query a Specific Stream with Filtered Sources & Event Window

```powershell
DX+OfflineQueryCli.exe -g "C:\designs\fft_order.dpd" -d "C:\data\run01.dxdb" -r 1 -e 2 `
  -s "FDFT:CH1" -M "1=RAW,Scaled" -T 0.5 -c 10
```

### Generate Multi-Source Fixture & Validate Reference Processors

```powershell
DX+OfflineQueryCli.exe -G "C:\temp\fixture_out" -d "C:\temp\fixture_out\multi.dxdb" -R all -v
```

---

## Exit Codes

| Code | Meaning | Resolution Hint |
| :--- | :--- | :--- |
| `0` | **Success** | All resolution, simulated plot trees, and queries completed with 0 Phoenix errors. |
| `1` | Command Syntax Error | Check CLI flag spelling and argument pairing. |
| `2` | Missing Required Arguments | Provide `--graph`, `--dxdb`, `--record`, and `--stream` (or `--simulate-plots`). |
| `3` | Graph File Unreadable | Verify file path and read permissions on `.dpd`/`.json`. |
| `4` | Graph JSON Parse Error | Validate JSON structure of the design file. |
| `5` | Interface Open Failure | Verify **ApexLM** license service connectivity (`dx+offlineanalysis` or dev build). |
| `6` | Reader Resolution Failure | Ensure database plugin libraries (`plugins/database`) are next to executable. |
| `7` | Graph Submit Failure | Inspect graph topology for disconnected or circular links. |
| `8` | Invalid Stream Format | Format `--stream` strictly as `sourceName:streamName`. |
| `9` | Source Not in Graph | Verify target component UUID or logical source name exists in the graph. |
| `10` | Stream Not in Source | Verify target stream name exists in the named source component. |
| `11` | Query Execution Error | One or more queries triggered a runtime Phoenix error; re-run with `-v`. |
| `12` | Fixture Writer Unavailable | Verify SQLite database writer plugin is installed for `--generate-fixture`. |
