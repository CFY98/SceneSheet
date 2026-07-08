# SceneSheet

A script-breakdown generator which parses screenplays in the .pdf, .fdx, and .fountain file formats and exports them as .pdf, .docx, .json, .xlsx. Developed for production and development purposes for Script Supervisors, Producers, Script Editors, etc.

---

## 💫 Features

- Works completely offline so data never leaves the user's machine.
- Supports .pdf, .fdx, and .fountain file formats.
- CLI support for running SceneSheet via terminal commands.
- NLP-based filtering via spaCy to reduce false-positives in character detection.
- Scene-by-scene breakdown with AI-generated summaries.
- Exportable as .pdf, .docx, .json, or .xlsx (work-in-progress).

---

## 🎬 Why This Exists

Script breakdowns are typically done manually or via tools tied to specific screenwriting or workspace software, which can require cloud uploads of unreleased scripts and account signup as part of a subscription model. SceneSheet was built to explore a local-first alternative. It parses industry-standard script formats directly and using an on-device LLM for scene summarisation so nothing leaves the machine. No accounts, no cloud inference, no script data exposure. The intention is a one-time-payment licensing model rather than a subscription. It's as much an exercise in offline NLP/LLM pipeline design as it is a production tool.

---

## 💡 Philosophy

1) AI is not used for creative or editorial judgement. The purpose of the app is to generate a summarisation for each scene in the script.
2) Since LLM inferrence is performed locally, the scripts never leave the user's machine and are not used to train AI models.
3) This tool is not affiliated with any production company, broadcaster, or screenplay software company.

---

## 🚧 Project Status
- [x] .fdx parsing (XML-based extraction)
- [x] .fountain parsing (markup-based extraction)
- [x] .pdf parsing (margin-based inference)
- [x] spaCy-based character detection filtering
- [x] Local LLM scene summarization (llama-cpp-python)
- [x] DOCX export
- [x] PDF export
- [x] JSON export
- [ ] XLSX export
- [ ] Tauri desktop packaging

---

## 📁 File Format Notes

### Input

Each parser extracts the same structured scene data but via different methods depending on the format:

- **.fdx** - Element types are explicitly tagged in the XML structure.
- **.pdf** - Element types are inferred from industry-standard margins.
- **.fountain** - Element types are inferred from the markup language syntax.

### Output

- **.pdf** - For consistency and universal compatibility.
- **.docx** - For flexible formatting and editing.
- **.json** - For interoperability with other tools (e.g. scheduling software, other production apps).
- **.xlsx** - For cross-referencing with existing production spreadsheets.

---

## ⚙️ Process

The following fields are extracted:

| Field | Source | Method |
|---|---|---|
| Script Title | First Page | Auto-extracted from filename |
| Scene Number | Slugline | Auto-extracted if present, otherwise assigned sequentially |
| Scene Heading | Slugline | Auto-extracted (full string) |
| Characters | Character Cues + Action Lines | Auto-extracted |
| Locations | Slugline | Auto-extracted |
| Wardrobe | Action Lines | Auto-extracted |
| Props | Action Lines | Auto-extracted |
| Scene Actions | Action Lines | Auto-extracted (full string) |
| Scene Summaries | AI generated | llama-cpp-python + llm |

The scene summary is generated locally using a quantised llm via llama-cpp-python so no data leaves the user's machine.

---

## 📐 Architecture

```
Input (.fdx / .pdf / .fountain)
        ↓
Backend Loop (extension validation + routing)
        ↓
Parser Logic (structured scene extraction with regex and spaCy)
        ↓
Llama API Call (local, via llama-cpp-python)
        ↓
Compile Output
        ↓
Output Generation
        ↓
Format? → DOCX (python-docx) / PDF (ReportLab) / JSON / XLSX (openpyxl) - work in progress
        ↓
Local file download

```
---

## 🛠️ Tech Stack

- **Python** - Core language
- **FastAPI** - API framework and file delivery
- **pdf_oxide** - .pdf parsing
- **xml.etree.ElementTree** - .fdx parsing (built-in)
- **re** - .fountain parsing and filter patterns (built-in)
- **spaCy** - NLP-based filtering of false positives in character detection
- **llama-cpp-python** - local LLM inference
- **python-docx** - .docx generation
- **ReportLab** - .pdf generation
- **json** - .json generation
- **openpyxl** - .xlsx generation
- **Tauri** - Desktop wrapper
- **SQLite** - Tracks job queue and processing status

---

## 🤖 Local AI model

Uses `llama-cpp-python` for on-device inference. No cloud API required.

**Current test model:** `Llama-3.2-3B-Instruct-Q5_K_M.gguf` (Bartowski)

Recommended models by RAM tier:

| RAM | Recommended Model | Size |
|---|---|---|
| 4GB | Qwen 2.5 0.5B Instruct Q5_K_M | ~400MB |
| 6GB | Gemma 2 2B It Q5_K_M | ~1.8GB |
| 8GB+ | Llama 3.2 3B Instruct Q5_K_M | ~2.2GB |

___

## 🖥️ GPU Acceleration

> **Note** GPU acceleration is supported. CPU inference works on any machine but speed will vary significantly based on hardware, particularly with the larger models.

---

## 🔭 Prospective Developments

- Ionic for Android
- Batch processing
- Persist parsed results to allow resumtion from point of failure

## ⚠️  Known Limitations

- Character detection prioritises speaking roles via character cue lines. Non-speaking characters introduced in action lines are detected where possible, but may not always be detected depending on formatting.

---

## 📃 Note

This repository contains documentation only. The SceneSheet codebase is maintained in a private repository.
