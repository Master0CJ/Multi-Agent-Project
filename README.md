# Multi-Agent-Project

# Advanced Agent — Developer Tools Research

Lightweight research agents that use Firecrawl and OpenAI to find, scrape, and analyze developer tools and companies.

## Projects in this repo
- advanced-agent — a research workflow that searches, scrapes, and produces structured company analyses and recommendations. See [advanced-agent/main.py](advanced-agent/main.py).  
  Key components:
  - [`src.workflow.Workflow`](advanced-agent/src/workflow.py) — main workflow orchestration and step implementations.  
    File: [advanced-agent/src/workflow.py](advanced-agent/src/workflow.py)
  - [`src.firecrawl.FirecrawlService`](advanced-agent/src/firecrawl.py) — wrappers over Firecrawl search/scrape.  
    File: [advanced-agent/src/firecrawl.py](advanced-agent/src/firecrawl.py)
  - [`src.prompts.DeveloperToolsPrompts`](advanced-agent/src/prompts.py) — prompt templates for the LLM.  
    File: [advanced-agent/src/prompts.py](advanced-agent/src/prompts.py)
  - [`src.models.CompanyAnalysis`, `src.models.CompanyInfo`, `src.models.ResearchState`](advanced-agent/src/models.py) — pydantic models used across the workflow.  
    File: [advanced-agent/src/models.py](advanced-agent/src/models.py)

- simple-agent — a minimal example using an MCP (tooling) client + an LLM to interactively use Firecrawl tools. See [simple-agent/main.py](simple-agent/main.py).

## Prerequisites
- Python >= 3.11 (see [simple-agent/.python-version](simple-agent/.python-version))
- Install project dependencies (each subproject has its own pyproject):
  - advanced-agent: [advanced-agent/pyproject.toml](advanced-agent/pyproject.toml)
  - simple-agent: [simple-agent/pyproject.toml](simple-agent/pyproject.toml)

## Environment variables
Both agents rely on:
- FIRECRAWL_API_KEY — Firecrawl API key  
  - advanced-agent: [advanced-agent/.env](advanced-agent/.env)  
  - simple-agent: [simple-agent/.env](simple-agent/.env)
- OPENAI_API_KEY — OpenAI API key

Store keys in the `.env` files (already present in each folder) or export them in your shell.

## Install & Run (example)
1. Create and activate a virtual environment:
```sh
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
```

2. From the repository root install dependencies for the project you want to run:
```sh
# Advanced agent
pip install -e advanced-agent/.[default]  # or pip install -r advanced-agent/requirements.txt if you create one

# Simple agent
pip install -e simple-agent/.[default]
```

3. Run:
```sh
# Advanced agent (interactive CLI)
python advanced-agent/main.py

# Simple agent (interactive CLI)
python simple-agent/main.py
```

## Usage overview
- advanced-agent: Enter a developer-focused query (e.g., "database hosting for startups"). The workflow (`[`src.workflow.Workflow`](advanced-agent/src/workflow.py)`) will:
  1. Search for relevant articles (using [`src.firecrawl.FirecrawlService`](advanced-agent/src/firecrawl.py)).
  2. Extract tool names using prompts (`[`src.prompts.DeveloperToolsPrompts`](advanced-agent/src/prompts.py)`).
  3. Scrape each tool/company site and produce structured analysis (`[`src.models.CompanyAnalysis`](advanced-agent/src/models.py)`).
  4. Emit concise recommendations.

- simple-agent: Interactive LLM agent that loads MCP tools and calls Firecrawl via a child process. See [simple-agent/main.py](simple-agent/main.py).

## Notable files
- [advanced-agent/main.py](advanced-agent/main.py) — CLI entrypoint for advanced research agent
- [advanced-agent/src/workflow.py](advanced-agent/src/workflow.py) — core workflow
- [advanced-agent/src/firecrawl.py](advanced-agent/src/firecrawl.py) — Firecrawl wrapper
- [advanced-agent/src/prompts.py](advanced-agent/src/prompts.py) — prompts used by the LLM
- [advanced-agent/src/models.py](advanced-agent/src/models.py) — pydantic models
- [simple-agent/main.py](simple-agent/main.py) — example interactive agent using MCP
- [simple-agent/pyproject.toml](simple-agent/pyproject.toml) — simple-agent dependencies
- [advanced-agent/pyproject.toml](advanced-agent/pyproject.toml) — advanced-agent dependencies

## Notes & tips
- The advanced workflow uses structured LLM outputs (pydantic) to populate `CompanyInfo` results. If you need to extend the schema, edit [`advanced-agent/src/models.py`](advanced-agent/src/models.py).
- If Firecrawl scraping fails, the agents fall back to available search metadata — see error handling in [`advanced-agent/src/workflow.py`](advanced-agent/src/workflow.py).
- Tune the LLM via `ChatOpenAI` parameters in [`advanced-agent/src/workflow.py`](advanced-agent/src/workflow.py).

## Contributing
- Add new prompt variations in [`advanced-agent/src/prompts.py`](advanced-agent/src/prompts.py).
- Add new fields to the structured output in [`advanced-agent/src/models.py`](advanced-agent/src/models.py) and update the analysis step in [`advanced-agent/src/workflow.py`](advanced-agent/src/workflow.py).

## License
Add your preferred license file at the repo root (e.g., LICENSE).

...existing code...
```// filepath: d:\AI-Agent\advanced-agent\README.md
...existing code...
# Advanced Agent — Developer Tools Research

Lightweight research agents that use Firecrawl and OpenAI to find, scrape, and analyze developer tools and companies.

## Projects in this repo
- advanced-agent — a research workflow that searches, scrapes, and produces structured company analyses and recommendations. See [advanced-agent/main.py](advanced-agent/main.py).  
  Key components:
  - [`src.workflow.Workflow`](advanced-agent/src/workflow.py) — main workflow orchestration and step implementations.  
    File: [advanced-agent/src/workflow.py](advanced-agent/src/workflow.py)
  - [`src.firecrawl.FirecrawlService`](advanced-agent/src/firecrawl.py) — wrappers over Firecrawl search/scrape.  
    File: [advanced-agent/src/firecrawl.py](advanced-agent/src/firecrawl.py)
  - [`src.prompts.DeveloperToolsPrompts`](advanced-agent/src/prompts.py) — prompt templates for the LLM.  
    File: [advanced-agent/src/prompts.py](advanced-agent/src/prompts.py)
  - [`src.models.CompanyAnalysis`, `src.models.CompanyInfo`, `src.models.ResearchState`](advanced-agent/src/models.py) — pydantic models used across the workflow.  
    File: [advanced-agent/src/models.py](advanced-agent/src/models.py)

- simple-agent — a minimal example using an MCP (tooling) client + an LLM to interactively use Firecrawl tools. See [simple-agent/main.py](simple-agent/main.py).

## Prerequisites
- Python >= 3.11 (see [simple-agent/.python-version](simple-agent/.python-version))
- Install project dependencies (each subproject has its own pyproject):
  - advanced-agent: [advanced-agent/pyproject.toml](advanced-agent/pyproject.toml)
  - simple-agent: [simple-agent/pyproject.toml](simple-agent/pyproject.toml)

## Environment variables
Both agents rely on:
- FIRECRAWL_API_KEY — Firecrawl API key  
  - advanced-agent: [advanced-agent/.env](advanced-agent/.env)  
  - simple-agent: [simple-agent/.env](simple-agent/.env)
- OPENAI_API_KEY — OpenAI API key

Store keys in the `.env` files (already present in each folder) or export them in your shell.

## Install & Run (example)
1. Create and activate a virtual environment:
```sh
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
```

2. From the repository root install dependencies for the project you want to run:
```sh
# Advanced agent
pip install -e advanced-agent/.[default]  # or pip install -r advanced-agent/requirements.txt if you create one

# Simple agent
pip install -e simple-agent/.[default]
```

3. Run:
```sh
# Advanced agent (interactive CLI)
python advanced-agent/main.py

# Simple agent (interactive CLI)
python simple-agent/main.py
```

##
