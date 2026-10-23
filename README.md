# SYP Labs — Agentic CI/CD Failure Analyzer

**SYP Labs** (`syplabs.site`) is an autonomous developer workflow agent that hooks into GitHub Actions and GitLab CI pipelines. When a build or test suite fails, the agent ingests raw execution logs, maps stack traces to repository AST nodes, and utilizes Anthropic's Claude API to generate validated pull-request fixes.

## Core Architecture
- **Log Ingestion & Filtering:** Strips ANSI noise and isolates failure windows from multi-megabyte CI logs.
- **AST Context Resolver:** Extracts relevant function definitions, imports, and recent git diffs surrounding the stack trace.
- **Claude Reasoning Engine:** Uses Claude Sonnet with prompt caching to diagnose root causes and synthesize minimal git unified diffs.

## Quickstart (Local CLI)
```bash
git clone [https://github.com/syp-labs/syplabs-agent.git](https://github.com/syp-labs/syplabs-agent.git)
cd syplabs-agent
pip install anthropic pydantic
export ANTHROPIC_API_KEY="sk-ant-..."
python agent.py --log ./sample_build.log
