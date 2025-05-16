# 🧠 Obsidian-PKM-toolkit — Personal Knowledge Automation CLI
A Python-based CLI tool for managing, enhancing, and automating Obsidian-based knowledge workflows. Includes intelligent metadata enrichment, daily note generation, and LLM integrations for content creation and summarization.

## ✨ Features

### ✅ Metadata Enhancer
- Scans `.md` files in your Obsidian vault
- Adds or updates YAML frontmatter with:
  - `title`, `description`, `tags`
  - `type`, `created`, `modified`, `embedding_id`
- Optionally generates intelligent `description` fields via LLMs (OpenAI, Claude, Ollama)

### 📤 JSON Metadata Export
- Outputs a structured `obsidian_metadata_index.json` file
- Includes all note metadata + optional embedding IDs
- Ideal for indexing into RAG/vector DBs (Qdrant, Chroma)

### 📅 Daily Note Generator
- Creates a new daily note (YYYY-MM-DD format)
- Optional LLM-assisted prompting to help summarize the day or plan it
- Can pull from calendar sources or user prompts (future)

### 🎧 Media Summary Integration
- Accepts YouTube/podcast URLs or transcripts
- Uses a summarization engine (LLM or custom) to:
  - Extract highlights
  - Format into a new Obsidian note with title, source, and summary

## 🏗️ Planned Structure
```
obsidian-pkm-toolkit/
├── cli.py                 # Main CLI entry point (argparse or typer)
├── config.py              # Config file loading (vault path, API keys, etc.)
├── enhancer/
│   ├── metadata.py        # YAML enrichment functions
│   └── llm.py             # LLM description generation
├── generator/
│   ├── daily_note.py      # Create daily note w/ or w/o LLM
│   └── media_summary.py   # Summarize media input and write note
├── utils/
│   ├── file_utils.py      # Walk vault, read/write helpers
│   └── hashing.py         # Embedding ID / UUID generation
├── examples/              # Sample config, sample outputs
└── README.md
```

## ⚙️ Configuration (e.g., `config.yaml`)
```yaml
vault_path: /Users/{name}/ObsidianVault
output_json: true
use_llm: true
llm_provider: openai  # or "ollama", "anthropic"
openai_api_key: sk-...
ollama_model: llama3
description_max_tokens: 100
daily_template: "_templates/daily.md"
```

## 🚀 Example CLI Commands
```bash
# Enhance all notes with metadata and export index
python cli.py enhance --vault /path/to/vault --use-llm

# Create today's daily note (asks you questions via LLM)
python cli.py daily --interactive

# Summarize a YouTube video and add it as a note
python cli.py media-summary --url "https://youtu.be/xyz" --title "AI podcast episode 48"
```

## 🔌 Extensibility Roadmap
- [ ] Embedding chunking + Qdrant upload
- [ ] Calendar integration (Google/Outlook API)
- [ ] Tags & backlink analysis
- [ ] Git-based versioning of vault
- [ ] UI preview of note summaries
- [ ] GPT-powered search over metadata/index

## 📦 Requirements
- Python 3.9+
- `pyyaml`, `typer`, `openai`, `uuid`, `tqdm`, `requests`, etc.
- Optional: `llama-cpp-python`, `anthropic`, `google-api-python-client`
