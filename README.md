CrewRoute OS (v4.0) 🌿
Autonomous Multi-Agent Logistics Consensus & Dispatching Engine
verify
Production Deploy
Engine License
CrewRoute OS is a production-grade, containerized operational engine designed to solve high-density logistics routing through a highly resilient, multi-agent consensus architecture.
Rather than relying on single-model completions or basic API wrappers, this system orchestrates concurrent model evaluations, tracks exact dollar-cost telemetry back to PostgreSQL, and executes self-healing error pathways (Dead Letter Queues) to optimize dispatching.
⚙️ The System Architecture
🚀 Key Engineering Moats
1. Parallel Multi-Model Consensus (Debate Track)
To bypass single-model bias and hallucinations when scheduling high-stakes operational routes, the system calculates an Urgency Ratio at ingestion:
If this ratio is ￼, the engine intercepts the execution path and spins up a concurrent debate:
1 Round 1: Queries ⁠Claude-3-5-Sonnet⁠, ⁠Grok-2⁠, and ⁠Gemini-1-5-Pro⁠ in parallel to generate independent routing models.
2 Round 2 (Peer Review): Cross-pollinates the models. Each agent evaluates its peers' models based on travel times and priority density, adjusting its own output.
3 Synthesis: ⁠Claude-3-Opus⁠ ingests the final peer transcripts to compile a mathematically optimized, structured JSON routing map.
2. Zero-Dependency Alert Client (⁠alerts.py⁠)
To prevent container startup lag and dependency collision vulnerabilities during cloud deployments, the notification client uses zero external libraries (built entirely using Python's native ⁠urllib⁠ standard library).
￼ It contains an Adaptive Parsing Layer that converts raw HTML layouts (for Telegram) into clean, high-priority Markdown structures (for Discord) on the fly.
￼ Operates inside an isolated thread with a strict 10-second socket timeout to prevent slow network APIs from hanging the main database transactional thread.
3. Absolute Schema Guardrails
To prevent silent data corruption or database drift during automated deployments, schema management is decoupled:
￼ The system dynamically parses and executes version-controlled ⁠schema/sqlite_schema.sql⁠ files at initialization.
￼ If directories are isolated, it instantly falls back to clean, structurally identical inline definitions to guarantee a successful boot.
4. Downstream Payload Gate (⁠_shape_for_make⁠)
To protect database schemas and keep downstream automation triggers like Make.com or Zapier lightweight, the engine intercepts raw JSON output and filters keys against a strict, predefined payload structure:
📊 Performance & Telemetry
Every model execution logs live metrics directly to a PostgreSQL analytics dashboard:
￼ Token Distribution: Compiles precise prompt vs. completion ratios.
￼ Cost Tracking: Estimates micro-cent USD spend per run to track computational ROI.
￼ Latency Profiles: Tracks engine processing speed in milliseconds to evaluate API degraded-state conditions.
This repository represents a sanitized public demonstration of the proprietary architecture powering CJS operations.