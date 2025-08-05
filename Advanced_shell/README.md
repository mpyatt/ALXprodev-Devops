# Advanced Shell – Pokémon API Automations

A collection of small, self‑contained **Bash** utilities that showcase advanced shell scripting techniques—API calls, JSON parsing, text processing, retries, parallelism, and reporting—using only core Unix tools (`curl`, `jq`, `awk`, `sed`, `bash` built‑ins).

> **Directory:** `Advanced_shell/`
> **Repo:** [`ALXprodev‑Devops`](https://github.com/your‑org/ALXprodev‑Devops)

---

## Prerequisites

| Tool          | Purpose                            |
| ------------- | ---------------------------------- |
| **bash ≥ 4**  | Array support & process management |
| **curl**      | HTTP requests                      |
| **jq**        | JSON querying                      |
| **awk / sed** | Text transformation                |

Install via your package manager, e.g. `sudo apt install bash curl jq gawk sed`.

---

## Script Catalogue

| Task  | File (executable)                 | What it does                                                                                                     |
| ----- | --------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| **0** | `apiAutomation-0x00`              | Fetches **Pikachu** and saves to `data.json`; logs failures to `errors.txt`.                                     |
| **1** | `data_extraction_automation-0x01` | Reads `data.json`; prints > “*Pikachu is of type Electric, weighs 6 kg, and is 0.4 m tall.*”                     |
| **2** | `batchProcessing-0x02`            | Serially downloads 5 Pokémon (Bulbasaur ➜ Charmeleon) with retry & back‑off; outputs `pokemon_data/<name>.json`. |
| **3** | `summaryData-0x03`                | Scans `pokemon_data/*.json`, builds `pokemon_report.csv`, prints average height & weight.                        |
| **4** | `batchProcessing-0x04`            | Parallel version of Task 2—spawns background jobs, waits, logs failures.                                         |

---

## Quick‑start Workflow

```bash
# 1) Fetch Pikachu
./apiAutomation-0x00

# 2) Pretty summary sentence
./data_extraction_automation-0x01

# 3) Bulk fetch five Pokémon (serial with retry)
./batchProcessing-0x02

# 4) OR fetch them faster in parallel
./batchProcessing-0x04

# 5) Generate CSV & averages
./summaryData-0x03
```

### Example CSV (`pokemon_report.csv`)

```csv
Name,Height (m),Weight (kg)
Bulbasaur,0.7,6.9
Ivysaur,1.0,13.0
Venusaur,2.0,100.0
Charmander,0.6,8.5
Charmeleon,1.1,19.0
```

```md
Average Height: 1.08 m
Average Weight: 29.48 kg
```

---

## Error Handling

* **Status codes** – non‑`200` responses trigger retries (3×) then append a line to `errors.txt`.
* **Partial downloads** – corrupt JSON files are removed before retry/logging.
* **Rate limits** – default back‑off: `attempt × 1 s`. Increase `DELAY` in the scripts if you see HTTP 429.

---

## Customising

🎛️ **Change Pokémon list** – edit the `POKEMON_LIST` array in `batchProcessing‑0x02` or `‑0x04`.

🐢 **Throttle speed** – raise `DELAY` or decrease parallelism by splitting the list.

🗂️ **Data directory** – override `DATA_DIR` env variable when invoking:
`DATA_DIR=mydir ./batchProcessing-0x04`.
