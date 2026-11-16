# Applied AI Systems & Product Delivery

**Anton Trofimov** · Product Owner / Delivery Lead (AI / GenAI)

My background is in enterprise IT product and project delivery, including the development and evolution of enterprise platforms and services, master data solutions, complex integrations, and systems supporting production processes, operational accounting, and planning. I have managed projects with budgets up to RUB 240M and cross-functional teams of up to 30 people. My applied-AI work combines system design, implementation, quality evaluation, and architecture decisions.

This portfolio presents **implemented systems, measured results, and supporting evidence**. The AI work is independently developed and validated in bounded environments; it is **not a claim of commercial AI production deployments**.

## Selected work

### 1. Governed Agent Runtime — controlled agent execution

**Problem.** An LLM can suggest a useful action, but it must not grant itself permission to execute it.

**System design.** An agent interprets evidence and proposes a next step for a synthetic incident-response service. A **deterministic runtime** controls what can happen next:

- **Structured contracts and state machine:** typed proposals, tool contracts, explicit workflow states and allowed state transitions.
- **Execution governance:** controlled context, policy and authorization gates, action preconditions, human-in-the-loop (HITL) confirmation, and bounded tool calling.
- **Traceability and evals:** execution traces, audit lineage, reproducible evaluations, and separate checks for model decision quality, runtime containment, and the provenance of semantic evaluation criteria.

**Measured outcomes and boundaries**

- **Single-step baseline:** 5 scenarios, 15 measured attempts with Qwen `qwen3.8:27b`; **12/15 PASS** for model quality and **15/15 PASS** for runtime containment.
- **Bounded multi-step execution:** six completed synthetic recovery trajectories from two operator requests and three paired seeds, with individually confirmed state-changing actions and runtime-verified rollback.
- **Evaluation findings:** structurally valid, runtime-contained proposals can still contain unsupported reasoning. An explicit evaluation traceability gate separates source-backed criteria from unreviewed semantic assumptions.
- **Operator experience:** a local interactive UI covers confirmation, refusal, expiry, and initial dialogue; live Ollama inference was exercised locally. The public [interactive demo](https://антонтрофимов.рф/gov-agent/) uses recorded behavior, **not live model inference**.
- **Delivery approach:** specification-driven development (SDD), AI-assisted implementation, contracts, automated tests, CI, review, and retained decision/evidence records.

**Scope:** results are specific to the evaluated scenarios. Production readiness, general reliability, and business impact have not been established.

**Evidence:** [Repository](https://github.com/Anton-Trofimov/governed-agent-runtime) · [Results and decisions](https://github.com/Anton-Trofimov/governed-agent-runtime/blob/main/RESULTS-AND-DECISIONS.md) · [Multi-step measured review](https://github.com/Anton-Trofimov/governed-agent-runtime/blob/main/reports/reviews/bc-008-measured-review.md) · [Interactive demo](https://антонтрофимов.рф/gov-agent/)

### 2. RAG Retrieval Trade-offs — retrieval quality, latency & context

**Question.** How do retrieval and context-assembly choices affect evidence completeness, citations, response time, and context budget?

- **Evaluation:** 4 hypotheses, 14 evaluation cases, 55 annotated facts, and **956 run records** (including warm-ups); these are **not** 956 independent cases.
- **Measurements:** retrieval coverage, citation behavior, input tokens, time to first token (TTFT), end-to-end latency, and context-admission failures.
- **Decision:** retrieval unit, chunk size, `top_k`, and context-admission policy must be selected for the specific corpus, model, and product requirements rather than treated as universal defaults.
- **Reference stack:** Python 3.12, Ollama, Chroma, `qwen3-embedding:0.6b`, and `mistral:7b`.

**Evidence:** [Repository](https://github.com/Anton-Trofimov/rag-retrieval-tradeoffs) · [Results and decisions](https://github.com/Anton-Trofimov/rag-retrieval-tradeoffs/blob/main/RESULTS-AND-DECISIONS.md)

### 3. AI Systems Integration — Document Workflows & Agent Tooling

Assessment of open-source components and their **enterprise adoption requirements**: integration, data lifecycle, access boundaries, resource needs, and operational controls.

- **Document workflows — Open WebUI + Ollama:** deployed a containerized service with persistent storage and a backup procedure; verified document ingestion, indexing, retrieval with source references, and a one-time document sync through `oikb`. Investigated a case where answer correctness concealed a Top-5 retrieval coverage gap. Distinguished source-of-truth documents from indexed and generated copies.
- **Agent platforms — OpenClaw + GigaAgent:** configured persistent context, memory conventions, subagent delegation, and a user channel; exercised local model inference, HITL, bounded Docker execution, and agent continuation. Reviewed permission and trust boundaries.
- **Tooling and memory — MCP + Mem0 + Qdrant:** validated a custom MCP server's tool discovery and result flow and cross-chat retrieval of persistent memory. Examined integration and resource constraints.
- **Next assessment criteria:** concurrent workloads, latency and capacity under load, CPU/GPU memory budgets, update/delete propagation, document-level access enforcement, multi-user isolation, restore, and scaling architecture. **Load testing, enterprise ACL enforcement, and scale-out are not yet validated.**

## Publications

1. [**От предложений LLM к управляемому исполнению: опыт разработки AI-агента**](https://habr.com/p/1105178/) — agent execution boundaries, multi-step control, evaluation findings, and SDD.
2. [**Зачем GenAI-ассистенту platform logic: как управлять источниками, evidence и ответами**](https://habr.com/p/1050848/) — evidence sufficiency, policy gates, answer control, and fallback outside the model.
3. [**Почему RAG — это не просто «добавить поиск»: latency, качество и выбор стратегии retrieval**](https://habr.com/p/1040938/) — retrieval trade-offs, evaluation, and product-level configuration decisions.

## Links

[Personal site](https://антонтрофимов.рф/) · [GitHub](https://github.com/Anton-Trofimov) · [Habr](https://habr.com/ru/users/Anton_Trofimov/articles/) · [LinkedIn](https://www.linkedin.com/in/ai-trofimov)
