# 12D — Generative AI, RAG, agents, evaluation and AI safety

## 1. What generative AI does

Generative AI models learn statistical structure from data and generate output conditioned on prompts or other inputs. Large language models commonly predict token sequences using transformer architectures. Image, audio and video models may use diffusion, autoregressive or other methods. A model can sound confident and still be wrong: fluency is not proof.

A model may be accessed through a hosted API, managed deployment or local/self-hosted inference. Each path changes cost, latency, privacy, reliability, model choice, operational burden and vendor exposure.

## 2. Model, application and system are different layers

- **Model:** Learned parameters and inference process.
- **Application:** Prompting, routing, business rules, UI, tools and data access.
- **System:** Model + application + retrieval + policy + monitoring + human workflow + vendors.

Provider safety controls do not secure your complete application. A RAG layer can leak documents, a tool can execute unauthorized actions, a log can retain secrets, or an agent can be manipulated by untrusted content.

## 3. Retrieval-augmented generation (RAG)

RAG retrieves relevant information from an approved collection and provides it to a model as context. It can improve grounding and access to current/private knowledge, but does not guarantee truth.

Typical flow: ingest approved documents → parse while preserving source and permissions → chunk with metadata → create embeddings or lexical index → store → receive query → apply authorization filters → retrieve/rerank → send bounded context → generate answer with source IDs → validate and evaluate.

**Critical:** Authorization must be applied before retrieval, not after generation. The model must never receive documents the user cannot access. Permission changes and deletion must propagate to indexes, caches and derived chunks. An embedding vector may still represent personal information if linkable to a person/document.

## 4. Prompt injection and untrusted content

Prompt injection occurs when instructions embedded in user content, retrieved documents, webpages or tool output attempt to change the system's intended behaviour. A prompt saying “ignore malicious instructions” is not a sufficient defence.

Treat external content as data, not authority. Separate policies from retrieved text; restrict tools; validate arguments in deterministic code; use allowlists; require confirmation for high-impact actions; keep secrets out of model context; enforce permissions outside the model; and test adversarial documents. A read-only research assistant should not receive email-send, payment, shell or production-admin capability without a compelling, separately authorized design.

## 5. Agents and tool use

An agent is an application pattern where a model selects tools or steps. The execution layer remains responsible for authentication, authorization, budgets, state and side effects.

Safe design: narrow schemas, server-side validation, trusted user identity attached by application code, separate read/write tools, confirmation for irreversible actions, timeouts, maximum steps, audit records with redaction, loop prevention, error handling and human escalation. Never execute arbitrary generated text as SQL, shell, URL or code against production.

## 6. Evaluation: test the complete system

Measure factual correctness against trusted references; relevance/completeness; citation precision; refusal behaviour; injection resistance; tool selection and arguments; cross-user privacy leakage; latency/cost; multilingual quality; malformed-file robustness; accessibility; and high-impact human review.

Use representative and adversarial test sets. Track regressions after model, prompt, retrieval, index and tool changes. LLM-as-judge is itself a fallible model; calibrate it against human-labelled cases.

## 7. Hallucinations and source discipline

Distinguish sourced facts, inference, uncertainty and missing evidence. Citations must point to retrieved sources that actually support the statement; do not allow the model to invent URLs. If evidence is insufficient, say so. Keep source version/snapshot metadata when auditability matters. Changing facts such as laws, prices and schedules need current authoritative retrieval, not only a stale vector index.

## 8. Privacy and model data

Decide whether prompts, uploads, outputs and telemetry are stored; who can access them; where they are processed; which vendors receive them; how long they persist; and whether they may be used for training. Minimize, redact, encrypt and control access. Local inference reduces some external processing but does not solve local logs, backups, device compromise or model licensing.

## 9. AI risk management

NIST AI RMF uses Govern, Map, Measure and Manage as voluntary functions. Its Generative AI Profile adds risk considerations for generative systems. Use them as structured guidance, not universal certification. Consider data provenance/copyright, bias, privacy leakage, prompt injection, harmful/deceptive output, automation bias, accessibility, energy/compute cost and vendor dependency.

## 10. Build versus buy

Compare deterministic rules/search, hosted APIs, open-weight model on managed hosting, self-hosting, fine-tuning and training from scratch. Training from scratch is usually the most expensive/data-intensive. Fine-tuning does not automatically make a model factual or current. RAG often suits changing reference material; deterministic policy code is better for permissions and exact constraints.

Estimate total cost: tokens/GPU hours, retrieval, storage, indexing, monitoring, engineering, vendor minimums, retries, data transfer, privacy review and support.

## 11. Exercise

Build local RAG over public documents. Preserve source IDs, use read-only tools, test a document containing hostile instructions and verify the agent cannot exceed its permissions. Delete a document and prove it disappears from retrieval and caches.

## Sources

- NIST AI RMF: https://www.nist.gov/itl/ai-risk-management-framework
- NIST Generative AI Profile (AI 600-1): https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence
- NIST AI RMF Playbook: https://www.nist.gov/itl/ai-risk-management-framework/nist-ai-rmf-playbook
- OWASP Top 10 for LLM Applications: https://genai.owasp.org/llm-top-10/
- Google Rules of ML: https://developers.google.com/machine-learning/guides/rules-of-ml
