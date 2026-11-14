# Technical Glossary and Study Guide

This companion explains common engineering terms in clear, accessible English. Keep the standard technical term in mind because documentation, error messages, code reviews and engineering teams use these terms widely. The definitions are intentionally concise; the linked chapters provide deeper explanations and examples.

| Term | Plain-English meaning |
|---|---|
| Hardware | The physical parts of a computer that can be seen, touched or measured. |
| Software | Instructions and programs that run on hardware. |
| Operating system | Software that manages applications, memory, files, devices, processes and other system resources. |
| Process | A running program with its own execution state and resources. |
| Thread | A path of execution inside a process. |
| Network | Connected devices and systems that exchange data. |
| Protocol | Agreed rules that systems follow when communicating. |
| IP address | A network-layer address used to identify an interface or destination for routing. |
| DNS | A distributed system that resolves domain names and service records. |
| Server | A computer or program that receives requests and provides a service. |
| Client | An application, browser or device that requests a service. |
| Frontend | The application layer through which users interact with a product. |
| Backend | Server-side logic, permissions and data operations. |
| API | A defined interface and contract through which software systems communicate. |
| Database | A system that stores and manages structured or document-oriented records. |
| Query | A request to read, create, update or delete data, depending on the system. |
| Index | An additional data structure that can make data easier to locate, at a storage and write-performance cost. |
| Cache | A temporary or derived copy of frequently used data. |
| Object storage | A storage service/model for durable files or blobs addressed by keys. |
| CDN | A distributed network that delivers content from edge locations closer to users. |
| Queue | A mechanism that holds work items until workers can process them. |
| Worker | A background process that executes queued or scheduled tasks. |
| Authentication | The process of verifying who a user or service is. |
| Authorisation | The process of deciding what an authenticated identity is allowed to do. |
| Encryption | Transforming data so that it cannot be read without the appropriate key. |
| Hashing | Producing a one-way digest. Passwords require dedicated, deliberately slow password-hashing functions. |
| Vulnerability | A weakness in a system that may be misused. |
| Threat model | A structured analysis of assets, attackers, entry points, threats and possible harms. |
| Latency | The delay before a request or operation receives a response. |
| Throughput | The amount of work or data completed in a period of time. |
| Availability | The degree to which a service is usable or reachable. |
| Scalability | The ability of a system to handle increasing load. |
| Reliability | The ability of a system to deliver its required service predictably. |
| Observability | The ability to understand internal system behaviour through logs, metrics and traces. |
| Deployment | Releasing software into a target environment. |
| Migration | A controlled change to an existing system or data schema. |
| Replication | Maintaining additional copies of data or a service. |
| Backup | An independently retained copy used for recovery. |
| Sharding | Distributing data across multiple partitions or nodes. |
| Eventual consistency | A model in which replicas or derived systems may converge after some delay. |
| Machine learning | Methods that learn patterns or models from data. |
| Model evaluation | Testing how well and how safely a model performs on target tasks. |
| RAG | Retrieval-Augmented Generation: retrieving relevant external documents/data to ground a model response. |
| SLO | Service Level Objective: an internal, measurable reliability target. |
| SLA | Service Level Agreement: a customer-facing service commitment, often with contractual consequences. |
| RPO | Recovery Point Objective: the amount of recent data loss an organisation is prepared to tolerate. |
| RTO | Recovery Time Objective: the target time to restore a service after an interruption. |

## Study method

1. **First pass — understand the problem:** Read the chapter without running code. Write a one-sentence explanation of each new term.
2. **Second pass — redraw the system:** Recreate each important diagram on paper. Explain the direction of every arrow and which component handles the data.
3. **Third pass — practise:** Run a small lab in an environment you own or are authorised to use. Do not just copy commands; explain what the output means.
4. **Fourth pass — consider failure:** Ask what happens when the network is unavailable, a database is slow, input is invalid, a session expires or an account is compromised.
5. **Teach-back:** Explain the topic in your own words for three to five minutes. The points where you struggle reveal knowledge gaps.
6. **Connect chapters:** Identify which earlier concepts a new chapter depends on. For example, media upload depends on HTTP, authorisation, object storage, queues and monitoring.
7. **Keep an engineering notebook:** Record assumptions, commands, observations, mistakes, sources and design decisions.

## You understand a chapter when you can answer

- Which problem does this technology solve?
- How did people or teams solve the problem before it existed?
- What is its basic internal workflow?
- Why do teams use it, and what alternatives are available?
- What are its limitations and common failure modes?
- What security, privacy, accessibility and cost risks does it introduce?
- How can it be tested safely on a local or authorised system?
- Who owns it in production, and who responds when it fails?

## A practical rule for learning technology

Do not memorise tool names as if the names themselves were expertise. Learn the problem, the contract, the data flow, the failure modes and the operating responsibilities. A tool may be replaced; the underlying engineering reasoning remains useful.
