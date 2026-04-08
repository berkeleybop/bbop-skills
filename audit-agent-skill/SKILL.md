---
name: assess-local-agent
description: Audits Python-based local AI agent repositories against 2026 standards for provenance, reproducibility, and scientific capability. Evaluates logging, versioning, tool validation, error correction, and cleanup. Use when the user asks to "audit the repo," "check agent compliance," "assess provenance," or "verify best practices" for local-first dual-mode agent systems (especially computational biology workflows).
---

# Assessment Skill: Local-First Dual-Mode Agentic Systems

This skill guides you through assessing a local AI agent repository against the 2026 standards for provenance, reproducibility, scientific capability, and user safety.

## Overview

Use this skill to assess local AI agent repositories (primarily Python-based) against the 2026 standards for **Local-First Dual-Mode Agentic Systems**. This assessment framework focuses on:

- **Local-first**: Agents that run on user machines with local provenance logging (not cloud-only SaaS)
- **Dual-mode**: Systems that support both conversational interaction and code execution workflows
- **Scientific capability**: Particularly relevant for computational biology, systems biology, and scientific research workflows

This skill is designed for repositories that:
- Implement AI agents in Python
- Use tools like MCP servers, Docker, or scientific computation frameworks
- Need provenance tracking for reproducibility
- Handle scientific data or workflows

**When NOT to use this skill:**
- General web applications without agent capabilities
- Non-Python codebases (though principles may still apply)
- Cloud-only SaaS products without local execution
- Simple scripts or libraries that aren't agent systems

## Usage

Invoke this skill when the user asks to:
- "audit the repo" or "audit this agent"
- "check compliance" or "assess against standards"
- "verify best practices" for agent systems
- "evaluate provenance" or "check reproducibility"
- "assess the agent capabilities"

The skill will guide you through systematic evaluation of 9 criteria across provenance, scientific capability, and user safety.

## Assessment Checklist & Criteria

You must evaluate the codebase against the following 9 criteria. For each item, search the file system for evidence and assign a status: **PASS**, **FAIL**, or **PARTIAL**.

### II. Provenance & Reproducibility

1.  **P1 - Logging (Standard: PROV-AGENT)**
    *   *Question:* Does the system write a local, structured log of the session?
    *   *Search For:* SQLite connections (`.db`), JSON-LD writers, or structured logging libraries. Look for logic writing to a `./logs` directory.
    *   *Pass Criteria:* System generates a persistent structured log (JSON/SQLite) containing prompts, code execution, and outputs.

2.  **P2 - Versioning (Standard: Reproducibility)**
    *   *Question:* Is the user-provided LLM version recorded?
    *   *Search For:* Configuration parsing logic that captures `model_name` or `model_version`. Check if these fields are written to the provenance log.
    *   *Pass Criteria:* The specific model identifier (e.g., `claude-3-7-sonnet-20260219`) is captured in the session metadata.

3.  **P3 - Logic Trace (Standard: SGR)**
    *   *Question:* Are "Reasoning Steps" captured separately from "Code"?
    *   *Search For:* Structured output definitions (Pydantic/JSON schemas) that enforce separate fields for `reasoning`/`thought` and `code`/`action`.
    *   *Pass Criteria:* The log distinguishes the *intent* (reasoning trace) from the *execution* (script).

4.  **P4 - Data Snap (Standard: OpenLineage)**
    *   *Question:* Does the system record the hash of the input data?
    *   *Search For:* Hashing functions (e.g., `sha256`, `md5`) applied to input files (genome files, media lists) at the start of a workflow.
    *   *Pass Criteria:* SHA-256 (or equivalent) hashes of inputs are recorded in the run log.

### III. Scientific Capability (Dual-Mode)

5.  **D1 - Tooling (Standard: MCP)**
    *   *Question:* Are comp bio tools wrapped via standard interfaces?
    *   *Search For:* Model Context Protocol (MCP) server definitions, JSON schemas defining tool inputs, or strict type hints on tool functions.
    *   *Pass Criteria:* Bio-tools (FBA, Gap Finding) have explicit schemas; the Agent does not guess CLI arguments.

6.  **D2 - Validation (Standard: Grounding)**
    *   *Question:* Is there a "pre-flight" check for ingredients/genes?
    *   *Search For:* Validation functions checking against local databases (e.g., `valid_ingredients.csv`, `chebi.db`) before simulation functions are called.
    *   *Pass Criteria:* IDs are validated against a local ontology/DB before being passed to the simulation engine.

7.  **D3 - Discovery (Standard: Self-Correction)**
    *   *Question:* Does Mode 2 (Code) have error-correction loops?
    *   *Search For:* `try/except` blocks around code execution that capture `stderr` and feed it back to the LLM for re-generation. Look for "max_retries" logic.
    *   *Pass Criteria:* System attempts to fix broken Python scripts automatically (up to N retries) using error feedback.

8.  **D4 - Context (Standard: RAG/Context)**
    *   *Question:* Can the user easily inject local "Human Insight"?
    *   *Search For:* Logic that scans a specific folder (e.g., `./context`, `./docs`) and loads text/PDF files into the agent's context window.
    *   *Pass Criteria:* Users can drop files into a folder to have them indexed by the agent.

### IV. User Experience & Safety

9.  **U2 - Cleanup (Standard: Hygiene)**
    *   *Question:* Does the system clean up temporary scripts/containers?
    *   *Search For:* `atexit` handlers, `finally` blocks, or Docker run commands with the `--rm` flag.
    *   *Pass Criteria:* Temporary run artifacts (scripts, containers) are cleared on exit (unless debug mode is on).

## Instructions for Claude

1.  **Analyze**: Systematically scan the codebase for the features described above.
2.  **Evidence**: Quote the specific file and line number that proves the presence or absence of a feature.
3.  **Report**: Generate a Markdown table summarizing the assessment.
4.  **Recommendations**: For any item marked **FAIL** or **PARTIAL**, provide a specific, actionable recommendation to bring the system up to standard.

## Example Output Structure

# Local Agent Assessment Report

| ID | Status | Category | Evidence / Observation |
|:---|:-------|:---------|:-----------------------|
| P1 | PASS | Logging | Found `logger.py` which writes session data to `logs/session.db` using SQLite. |
| P2 | FAIL | Versioning | Model version is read from `.env` but not written to the run log. |
|...|... |... |... |

### Recommendations
*   **P2:** Update `logger.py` to include `os.getenv("LLM_MODEL")` in the session initialization record.

