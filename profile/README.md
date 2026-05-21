<div align="center">
  <img src="https://raw.githubusercontent.com/TJLSmith0831/sirenspec/main/docs/logo/crest.svg" alt="SirenSpec" width="120"/>
  <h1>SirenSpec</h1>
  <p><strong>YAML-first agent orchestration for humans.</strong></p>
  <p>Define multi-agent workflows in plain YAML. Run them against any LLM backend.</p>

  [![CI](https://github.com/TJLSmith0831/sirenspec/actions/workflows/ci.yml/badge.svg)](https://github.com/TJLSmith0831/sirenspec/actions/workflows/ci.yml)
  [![PyPI](https://img.shields.io/pypi/v/sirenspec)](https://pypi.org/project/sirenspec)
  [![Python 3.13+](https://img.shields.io/badge/python-3.13+-blue.svg)](https://www.python.org/downloads/)
  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
</div>

---

## What is SirenSpec?

SirenSpec lets you describe multi-agent pipelines the same way you'd describe them to a colleague — in plain language, structured as YAML. No framework boilerplate, no hidden abstractions. Just agents, nodes, and edges.

```yaml
version: "0.1"

agents:
  analyst:
    model: "anthropic:claude-haiku-4-5-20251001"
    system: "You are a concise financial analyst."

nodes:
  summarize:
    agent: analyst
    writes: output.summary

input:
  message: "Summarize Q1 earnings for NVDA."
```

```bash
sirenspec run workflow.yaml
```

That's it. One file. One command. A complete agent run with a structured JSON trace.

---

## Ecosystem

| Repository | Description |
|-----------|-------------|
| [sirenspec](https://github.com/TJLSmith0831/sirenspec) | Core SDK — YAML parser, execution engine, CLI, guardrails |
| [sirenspec/docs/cookbook](https://github.com/TJLSmith0831/sirenspec/tree/main/docs/cookbook) | 12 runnable workflow examples |

---

## Key Capabilities

**Node types** — four primitives cover most patterns:
- **Agent** — single LLM call, writes to a context path
- **Swrm** — fan-out to `N` agents in parallel, optionally synthesise
- **Factory** — spawn one agent per item in a runtime list
- **Tool** — call an HTTP endpoint or Python callable, no LLM required

**Providers** — OpenAI, Anthropic, and Ollama out of the box, selected with a simple `provider:model` URI.

**Guardrails** — prompt-injection detection and output-length limits at the workflow or per-agent level.

**Retry & failure handling** — exponential backoff, fallback nodes, default outputs, and per-error-type retry rules.

**Template interpolation** — reference prior node outputs, environment variables, and runtime inputs directly in prompts with `{{ expr }}` syntax.

---

## Quickstart

```bash
pip install sirenspec

export OPENAI_API_KEY=sk-...
export ANTHROPIC_API_KEY=sk-ant-...

sirenspec run path/to/workflow.yaml
```

See the [full documentation](https://github.com/TJLSmith0831/sirenspec#readme) and [cookbook examples](https://github.com/TJLSmith0831/sirenspec/tree/main/docs/cookbook) to go further.

---

## Contributing

SirenSpec is open source and welcomes contributions. To get started:

```bash
git clone https://github.com/TJLSmith0831/sirenspec
cd sirenspec
uv sync --extra dev
source .venv/bin/activate
pytest
```

Please open an [issue](https://github.com/TJLSmith0831/sirenspec/issues) before submitting a large PR so we can align on direction.

---

<div align="center">
  <sub>Built with care. Designed for clarity.</sub>
</div>
