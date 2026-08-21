# Applied AI Systems & Product Delivery

Applied AI portfolio focused on product discovery, specification-driven and agent-assisted delivery, reproducible evaluation harnesses, and governed AI systems.

**Anton Trofimov**<br>
Product Owner / Delivery Lead (AI / GenAI)

## Development Approach

Projects are organized as controlled product-delivery systems.

### Delivery cycle

- Product problem and business context
- Discovery and bounded hypothesis
- Specifications and acceptance criteria
- Agent-assisted implementation
- Reproducible evaluation
- Review and error analysis
- Product or architecture decision

The objective is to make AI development traceable, measurable, reviewable, and controlled within defined system boundaries.

## 1. Projects

### 1.1. RAG Retrieval Trade-offs

**Status:** Published<br>
**Repository:** [rag-retrieval-tradeoffs](https://github.com/Anton-Trofimov/rag-retrieval-tradeoffs)<br>
**Results and decisions:** [RESULTS-AND-DECISIONS.md](https://github.com/Anton-Trofimov/rag-retrieval-tradeoffs/blob/main/RESULTS-AND-DECISIONS.md)<br>
**Related publication:** [Why RAG Is More Than “Adding Search”](https://habr.com/p/1040938/)

**Evaluation scope:** 4 hypotheses, 14 evaluation cases, 55 annotated facts, and 956 run records across the evaluation matrix: 728 generation records (182 warm-ups and 546 measured runs) and 228 retrieval records (57 warm-ups and 171 measured runs). These are run records, not 956 independent evaluation cases.<br>
**Reference stack:** Python 3.12, Ollama, Chroma, `qwen3-embedding:0.6b`, and `mistral:7b`.<br>
**Outcome:** local operating decisions on RAG use, `top_k`, chunk size, and retrieval unit for the evaluated corpus, context-admission policy, models, and reference environment.

#### Summary

A reproducible product and architecture evaluation examining how retrieval strategy affects evidence completeness, context size, citation behavior, input tokens, TTFT, E2E latency, and context-admission failure modes in a local RAG system.

The project uses a controlled reference setup to evaluate how retrieval, context-construction, and runtime variables interact and how to select a rational operating point for a defined product and operating context.

The objective is not to propose universal RAG settings, but to demonstrate a repeatable approach to architecture evaluation and evidence-based decision-making.

The evaluation system includes frozen inputs, structured records, schemas, validators, deterministic context assembly, integrity checks, retained raw results, and a recorded reference environment with pinned Python dependencies.

#### Key findings

The measured evaluation showed that RAG configuration should be assessed as a system of interacting variables rather than optimized through isolated parameters. Corpus structure, retrieval unit, chunking, `top_k`, context-admission policy, model behavior, latency, and product requirements must be evaluated together.

The project demonstrates a repeatable approach: define bounded hypotheses and evaluation cases, measure evidence and operating trade-offs, analyze failure modes, and make configuration-specific product and architecture decisions. Concrete results for the evaluated setup are documented in [Results and Decisions](https://github.com/Anton-Trofimov/rag-retrieval-tradeoffs/blob/main/RESULTS-AND-DECISIONS.md).

### 1.2. Governed Agent Runtime

**Status:** Public baseline published / ongoing validation<br>

**Repository:** [governed-agent-runtime](https://github.com/Anton-Trofimov/governed-agent-runtime)<br>

**Results and decisions:** [RESULTS-AND-DECISIONS.md](https://github.com/Anton-Trofimov/governed-agent-runtime/blob/main/RESULTS-AND-DECISIONS.md)<br>

#### Summary

A bounded agentic system for on-call incident-response scenarios in which the LLM interprets evidence and proposes the next step, while a deterministic runtime remains the operational control plane for policy, authorization, tools, confirmation, state transitions, and execution.

The project is developed through an SDD development harness that connects product hypotheses and human decisions to specifications, contracts, bounded AI-assisted implementation, tests, reproducible evaluation, published evidence, semantic review, and project-level decisions.

The project explores where bounded agent behavior provides useful autonomy compared with deterministic workflows while keeping operational authority, evaluation, and failure handling explicit.

The current public baseline includes a deterministic governed runtime path and Exp 18.1A: five single-step operational scenarios evaluated with Qwen `qwen3.8:27b` across 15 measured attempts.

- **Model quality:** `12 / 15 PASS`
- **Runtime control (containment):** `15 / 15 PASS`

The evaluation exposed an important boundary: schema-valid and runtime-contained model output can still contain unsupported semantic details. This led to separate evaluation of model quality and runtime containment rather than treating agent behavior as a single PASS / FAIL result.

The published repository already contains the measured baseline, source evidence, evaluation artifacts, and resulting project decisions. Subsequent stages extend the validation toward bounded multi-step behavior, controlled tool interaction, failure handling, latency and token economics, model comparison, and measurable user and business outcomes.

## 2. Publications

### 2.1. Why RAG Is More Than “Adding Search”

**Article:** [Why RAG Is More Than “Adding Search”](https://habr.com/p/1040938/)

#### Summary

An analysis of how retrieval strategy, evidence completeness, context budget, and latency affect practical RAG architecture decisions.

The article connects experimental results with product and architecture questions: when RAG is justified, why larger `top_k` is not automatically better, how chunking and retrieval units affect evidence, and why local findings should not be presented as universal settings.

### 2.2. Governed GenAI Pipeline

**Article:** [Governed GenAI Pipeline](https://habr.com/p/1050848/)

#### Summary

An architecture study of separating probabilistic model proposals from deterministic evidence checks, policy gates, answer-mode control, fallback, and runtime decisions.

The central conclusion is that the language model can operate inside a bounded proposal layer, while evidence sufficiency, policy enforcement, allowed outcomes, and fallback remain runtime responsibilities.

## 3. Links

**GitHub:** [Anton-Trofimov](https://github.com/Anton-Trofimov)<br>
**Habr:** [Anton Trofimov — articles](https://habr.com/ru/users/Anton_Trofimov/articles/)<br>
**LinkedIn:** [Anton Trofimov](https://www.linkedin.com/in/ai-trofimov)
