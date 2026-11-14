# QUESTION.md — The Questions That Lead Through the Handbook

> **A challenge for the curious:** You open an app, tap “Post”, and a video appears on someone's phone thousands of kilometres away. What had to happen between those two taps? Who built the foundations that make this possible? What can fail, who protects the user, and how does a company keep the system working?
>
> This file is a question map, not a shortcut answer sheet. Pick a question, follow its chapter links, and build the answer yourself. By the end, the questions connect into one picture of modern technology.

**Project:** Social & Technology Engineering Handbook  
**Creator & curator:** Vedansh Mandloi  
**AI assistance:** ChatGPT (GPT-6)

---

## 1. Before the Internet: how did the world get here?

1. **Before websites existed, how did computers communicate over long distances?** — Start with [Internet and Web history](handbook/01_HISTORY_OF_INTERNET_AND_WEB.md) and [networking foundations](handbook/05A_NETWORKING_FOUNDATIONS_AND_HISTORY.md).
2. **Why was ARPANET built, and what problem did packet switching solve?** — [Internet history](handbook/01_HISTORY_OF_INTERNET_AND_WEB.md), [networking history](handbook/05A_NETWORKING_FOUNDATIONS_AND_HISTORY.md).
3. **Who created the Web, and why is the Web not the same thing as the Internet?** — [Internet and Web history](handbook/01_HISTORY_OF_INTERNET_AND_WEB.md).
4. **How did a handful of early online communities turn into global platforms?** — [History of social networks](handbook/02_HISTORY_OF_SOCIAL_NETWORKS_AND_PLATFORMS.md).
5. **Why did some platforms grow while others disappeared?** — [Social-platform history](handbook/02_HISTORY_OF_SOCIAL_NETWORKS_AND_PLATFORMS.md), [product discovery](handbook/14A_PRODUCT_DISCOVERY_MARKET_RESEARCH_AND_PRODUCT_REQUIREMENTS.md).

## 2. The machine: what is actually happening inside a computer?

6. **When I click a button, how does a computer turn that action into electrical work?** — [Computer hardware](handbook/04A_COMPUTER_HARDWARE.md), [software and operating systems](handbook/04B_SOFTWARE_AND_OPERATING_SYSTEMS.md).
7. **What do CPU, RAM, GPU, SSD and cache each do, and why can't one replace the others?** — [Computer hardware](handbook/04A_COMPUTER_HARDWARE.md).
8. **How does an operating system share the CPU between many running apps?** — [Software and operating systems](handbook/04B_SOFTWARE_AND_OPERATING_SYSTEMS.md).
9. **What happens between writing code and the CPU executing instructions?** — [Programming languages and tools](handbook/04C_PROGRAMMING_LANGUAGES_AND_DEVELOPER_TOOLS.md), [operating systems](handbook/04B_SOFTWARE_AND_OPERATING_SYSTEMS.md).
10. **Why are there so many programming languages, and how do I choose one?** — [Programming languages and developer tools](handbook/04C_PROGRAMMING_LANGUAGES_AND_DEVELOPER_TOOLS.md).

## 3. The journey across the Internet

11. **What exactly happens after I type a website address and press Enter?** — [IP, DNS and routing](handbook/05B_IP_ADDRESSING_DNS_ROUTING_AND_GLOBAL_INTERNET.md), [browser request lifecycle](handbook/06A_BROWSER_AND_WEB_REQUEST_LIFECYCLE.md).
12. **How does DNS find a server without me remembering its IP address?** — [IP, DNS and routing](handbook/05B_IP_ADDRESSING_DNS_ROUTING_AND_GLOBAL_INTERNET.md).
13. **How does data cross oceans, ISPs, routers and networks to reach another country?** — [Global Internet](handbook/05B_IP_ADDRESSING_DNS_ROUTING_AND_GLOBAL_INTERNET.md).
14. **Why do TCP, UDP and QUIC all exist? Which one should an app use?** — [Protocols](handbook/05C_TCP_UDP_QUIC_HTTP_TLS_AND_APPLICATION_PROTOCOLS.md).
15. **What does HTTPS protect, and what does it not protect?** — [Protocols and TLS](handbook/05C_TCP_UDP_QUIC_HTTP_TLS_AND_APPLICATION_PROTOCOLS.md), [security foundations](handbook/11A_SECURITY_FOUNDATIONS_THREAT_MODELLING_AND_RISK.md).

## 4. From a screen to a working application

16. **How does a browser turn HTML, CSS and JavaScript into a screen I can interact with?** — [Browser lifecycle](handbook/06A_BROWSER_AND_WEB_REQUEST_LIFECYCLE.md), [HTML/CSS](handbook/06B_HTML_CSS_ACCESSIBILITY_AND_RESPONSIVE_DESIGN.md), [JavaScript and React](handbook/06C_JAVASCRIPT_TYPESCRIPT_REACT_AND_FRONTEND_ARCHITECTURE.md).
17. **Why do websites use frameworks such as React and Next.js instead of writing every page from scratch?** — [Frontend architecture](handbook/06C_JAVASCRIPT_TYPESCRIPT_REACT_AND_FRONTEND_ARCHITECTURE.md).
18. **What is the difference between frontend, backend, server and API?** — [Backend foundations](handbook/07A_BACKEND_FUNDAMENTALS_SERVERS_AND_RUNTIME.md), [API design](handbook/07B_API_DESIGN_HTTP_CONTRACTS_AND_INTEGRATION.md).
19. **How does a login request prove who I am, and how does the server decide what I can do?** — [Identity and API security](handbook/11B_IDENTITY_AUTHORIZATION_SESSIONS_AND_WEB_API_SECURITY.md).
20. **How do teams organise code so dozens of developers can work without breaking one another's features?** — [Software architecture](handbook/07C_SOFTWARE_ARCHITECTURE_MODULARITY_EVENTS_AND_SERVICE_BOUNDARIES.md), [team practices](handbook/17C_TEAM_DESIGN_HIRING_VENDORS_GOVERNANCE_AND_WORKING_PRACTICES.md).

## 5. Data: how does software remember anything?

21. **When I create an account, where does that information actually live?** — [Data modelling](handbook/08A_DATA_MODELLING_SQL_RELATIONSHIPS_AND_TRANSACTIONS.md), [database engines](handbook/08B_DATABASE_ENGINES_NOSQL_CACHE_AND_REPLICATION.md).
22. **Why use PostgreSQL, MongoDB, Redis or a search engine—and why not put everything in one database?** — [Database engines and cache](handbook/08B_DATABASE_ENGINES_NOSQL_CACHE_AND_REPLICATION.md).
23. **What happens if two users update the same record at the same time?** — [SQL transactions](handbook/08A_DATA_MODELLING_SQL_RELATIONSHIPS_AND_TRANSACTIONS.md), [distributed consistency](handbook/13A_DISTRIBUTED_SYSTEMS_FOUNDATIONS_CONSISTENCY_AND_CAP.md).
24. **How can a company recover data after accidental deletion or a server failure?** — [Data lifecycle and backups](handbook/08C_DATA_LIFECYCLE_BACKUPS_PRIVACY_AND_ANALYTICS_FOUNDATIONS.md), [recovery runbooks](handbook/18D_TESTING_DEPLOYMENT_OPERATIONS_RUNBOOKS_AND_RECOVERY.md).
25. **Why is a database replica not the same thing as a backup?** — [Database replication](handbook/08B_DATABASE_ENGINES_NOSQL_CACHE_AND_REPLICATION.md), [quality audit](handbook/QUALITY_AUDIT_AND_CROSS_PART_GAP_REGISTER.md).

## 6. Files, video, messages and real-time experiences

26. **Why should large photos and videos usually live in object storage instead of a normal database row?** — [Object storage and uploads](handbook/09A_OBJECT_STORAGE_UPLOADS_MEDIA_PIPELINES_AND_FILE_SECURITY.md).
27. **How does one uploaded video become several qualities and stream smoothly on slow networks?** — [Video streaming and transcoding](handbook/09B_VIDEO_STREAMING_TRANSCODING_CDN_AND_GLOBAL_DELIVERY.md).
28. **What is a CDN, and how can it deliver the same file quickly in different countries?** — [CDN and global delivery](handbook/09B_VIDEO_STREAMING_TRANSCODING_CDN_AND_GLOBAL_DELIVERY.md).
29. **How do chat, typing indicators and live notifications work?** — [Search, messaging and real-time systems](handbook/09C_SEARCH_MESSAGING_NOTIFICATIONS_AND_REALTIME_SYSTEMS.md).
30. **What is the difference between a queue, a worker and a real-time connection?** — [Real-time systems](handbook/09C_SEARCH_MESSAGING_NOTIFICATIONS_AND_REALTIME_SYSTEMS.md), [event streams and asynchronous work](handbook/13C_QUEUES_EVENT_STREAMS_IDEMPOTENCY_AND_ASYNCHRONOUS_WORK.md).

## 7. How does an idea become a running service?

31. **Where do servers live, and what do cloud providers actually rent to a startup?** — [Cloud and infrastructure](handbook/10A_CLOUD_COMPUTING_HOSTING_NETWORKS_AND_INFRASTRUCTURE.md).
32. **What are Docker, CI/CD and deployment, and how can a code update reach users safely?** — [Deployment and CI/CD](handbook/10B_DOCKER_CI_CD_RELEASES_SECRETS_AND_DEPLOYMENT.md), [release runbooks](handbook/18D_TESTING_DEPLOYMENT_OPERATIONS_RUNBOOKS_AND_RECOVERY.md).
33. **How does a team know when a service is slow or broken?** — [Observability and reliability](handbook/10C_OBSERVABILITY_RELIABILITY_INCIDENTS_AND_INFRASTRUCTURE_COSTS.md).
34. **What happens when one server goes down but the product must keep running?** — [Resilience and global scale](handbook/13D_GLOBAL_SCALE_RESILIENCE_CAPACITY_AND_MULTIREGION_DESIGN.md).
35. **When should a growing application split into multiple services, and when is that a mistake?** — [Architecture boundaries](handbook/07C_SOFTWARE_ARCHITECTURE_MODULARITY_EVENTS_AND_SERVICE_BOUNDARIES.md), [distributed systems](handbook/13A_DISTRIBUTED_SYSTEMS_FOUNDATIONS_CONSISTENCY_AND_CAP.md).

## 8. Security: how do you protect real users?

36. **How do hackers find weaknesses in an application—and how do defenders reason about risk?** — [Threat modelling](handbook/11A_SECURITY_FOUNDATIONS_THREAT_MODELLING_AND_RISK.md), [ethical testing](handbook/11D_ETHICAL_HACKING_PEN_TESTING_INCIDENT_RESPONSE_AND_LABS.md).
37. **Why is hiding a private post in the frontend not enough to protect it?** — [Identity, authorization and API security](handbook/11B_IDENTITY_AUTHORIZATION_SESSIONS_AND_WEB_API_SECURITY.md).
38. **How do password hashing, MFA, sessions and access tokens fit together?** — [Identity and sessions](handbook/11B_IDENTITY_AUTHORIZATION_SESSIONS_AND_WEB_API_SECURITY.md).
39. **How can an attacker compromise a project through a dependency or leaked secret?** — [Secure software lifecycle and supply chain](handbook/11C_SECURE_SDLC_SUPPLY_CHAIN_CLOUD_AND_SECRETS.md).
40. **What should an engineering team do after discovering a breach?** — [Incident response](handbook/11D_ETHICAL_HACKING_PEN_TESTING_INCIDENT_RESPONSE_AND_LABS.md), [SRE and incident management](handbook/17B_SRE_ONCALL_INCIDENT_MANAGEMENT_CUSTOMER_SUPPORT_AND_RUNBOOKS.md).

## 9. Algorithms and AI: how do systems make decisions?

41. **How does an application turn clicks, views and searches into useful analytics?** — [Data engineering](handbook/12A_DATA_ENGINEERING_EVENTS_PIPELINES_WAREHOUSES_AND_GOVERNANCE.md).
42. **How does a recommendation system rank thousands of possible items?** — [Statistics and recommendation systems](handbook/12B_STATISTICS_ALGORITHMS_EXPERIMENTS_AND_RECOMMENDATION_SYSTEMS.md).
43. **What is the difference between a rule-based algorithm and a machine-learning model?** — [Machine learning lifecycle](handbook/12C_MACHINE_LEARNING_LIFECYCLE_MODELS_EVALUATION_AND_MLOPS.md).
44. **How do RAG, agents and generative AI systems retrieve information and use tools?** — [Generative AI and agent systems](handbook/12D_GENERATIVE_AI_RAG_AGENTS_EVALUATION_AND_AI_SAFETY.md).
45. **How can a team test whether an AI system is useful, safe and reliable rather than merely impressive?** — [ML evaluation](handbook/12C_MACHINE_LEARNING_LIFECYCLE_MODELS_EVALUATION_AND_MLOPS.md), [AI safety](handbook/12D_GENERATIVE_AI_RAG_AGENTS_EVALUATION_AND_AI_SAFETY.md).

## 10. Scale: what changes when millions of people arrive?

46. **Why can one database and one server stop being enough?** — [Distributed systems foundations](handbook/13A_DISTRIBUTED_SYSTEMS_FOUNDATIONS_CONSISTENCY_AND_CAP.md).
47. **How do replication, partitioning and consensus help multiple machines coordinate?** — [Distributed storage and consensus](handbook/13B_PARTITIONING_REPLICATION_CONSENSUS_AND_DISTRIBUTED_STORAGE.md).
48. **How can a job be retried without accidentally charging or notifying someone twice?** — [Idempotency and asynchronous work](handbook/13C_QUEUES_EVENT_STREAMS_IDEMPOTENCY_AND_ASYNCHRONOUS_WORK.md).
49. **How do you estimate capacity, latency, bandwidth and cost before launch?** — [Global scale](handbook/13D_GLOBAL_SCALE_RESILIENCE_CAPACITY_AND_MULTIREGION_DESIGN.md), [cost and capacity capstone](handbook/18E_GLOBAL_LAUNCH_CAPACITY_COST_AND_CONTINUOUS_IMPROVEMENT.md).
50. **Why do “one million registered users” and “one million people online at once” mean different things?** — [Capacity planning](handbook/13D_GLOBAL_SCALE_RESILIENCE_CAPACITY_AND_MULTIREGION_DESIGN.md), [reference architecture](handbook/18A_END_TO_END_REFERENCE_PRODUCT_AND_ARCHITECTURE.md).

## 11. Product, business and people

51. **How do you know whether a problem is worth building a product for?** — [Product discovery](handbook/14A_PRODUCT_DISCOVERY_MARKET_RESEARCH_AND_PRODUCT_REQUIREMENTS.md).
52. **How do wireframes, accessibility and usability testing shape a product before code exists?** — [UX and experimentation](handbook/14B_UX_DESIGN_ACCESSIBILITY_PROTOTYPES_AND_EXPERIMENTATION.md).
53. **How does a free app pay for storage, bandwidth, salaries and support?** — [Growth and monetization](handbook/14C_GROWTH_MARKETING_NETWORK_EFFECTS_PRICING_AND_MONETIZATION.md), [startup finance](handbook/17D_STARTUP_FINANCE_BUDGETING_UNIT_ECONOMICS_AND_GOVERNANCE.md).
54. **Which roles are needed to build, test, secure and operate a real product?** — [Team and roadmap](handbook/14D_TEAM_ORGANIZATION_ROADMAP_METRICS_AND_GO_TO_MARKET.md), [team design](handbook/17C_TEAM_DESIGN_HIRING_VENDORS_GOVERNANCE_AND_WORKING_PRACTICES.md).
55. **What should a founder measure after launch besides total sign-ups?** — [Product metrics](handbook/14D_TEAM_ORGANIZATION_ROADMAP_METRICS_AND_GO_TO_MARKET.md), [operations and finance](handbook/17D_STARTUP_FINANCE_BUDGETING_UNIT_ECONOMICS_AND_GOVERNANCE.md).

## 12. Global rules, safety and the final build

56. **Can one application operate the same way in every country?** — [Global privacy and jurisdictions](handbook/15A_GLOBAL_PRIVACY_JURISDICTION_DATA_MAPPING_AND_CROSS_BORDER_TRANSFERS.md), [regional platform rules](handbook/15B_EU_UK_AND_REGIONAL_PLATFORM_RULES_GDPR_DSA_AI_ACT.md), [country comparison](handbook/15C_INDIA_US_CHINA_BRAZIL_JAPAN_AND_OTHER_MARKETS.md).
57. **How do data residency, cross-border transfers and local privacy rules affect architecture?** — [Global privacy](handbook/15A_GLOBAL_PRIVACY_JURISDICTION_DATA_MAPPING_AND_CROSS_BORDER_TRANSFERS.md), [global compliance matrix](handbook/15D_GLOBAL_LAUNCH_COMPLIANCE_MATRIX_DATA_TRANSFERS_AND_CHANGE_MONITORING.md).
58. **Who decides whether a reported post stays online, is removed or can be appealed?** — [Trust and safety](handbook/16A_TRUST_SAFETY_POLICIES_RISK_AND_MODERATION_FOUNDATIONS.md), [moderation operations](handbook/16B_REPORTING_ENFORCEMENT_APPEALS_AND_MODERATION_OPERATIONS.md).
59. **What extra protections are needed for children and other vulnerable users?** — [Child safety](handbook/16C_CHILD_SAFETY_MINOR_PROTECTION_AND_HIGH_RISK_HARM.md).
60. **How should a platform handle copyright claims, manipulated media and misleading content?** — [Copyright and content integrity](handbook/16D_COPYRIGHT_CONTENT_INTEGRITY_AND_TRANSPARENCY.md).
61. **How do you prove that a feature works across browsers, devices and heavy traffic?** — [Testing strategy](handbook/17A_TEST_STRATEGY_QA_AUTOMATION_PERFORMANCE_AND_ACCESSIBILITY.md).
62. **How should on-call engineers, moderators and customer support work together during an incident?** — [SRE and incident management](handbook/17B_SRE_ONCALL_INCIDENT_MANAGEMENT_CUSTOMER_SUPPORT_AND_RUNBOOKS.md).
63. **What should be ready before a public launch—not just before the code is deployed?** — [Global launch capstone](handbook/18E_GLOBAL_LAUNCH_CAPACITY_COST_AND_CONTINUOUS_IMPROVEMENT.md), [launch and recovery runbooks](handbook/18D_TESTING_DEPLOYMENT_OPERATIONS_RUNBOOKS_AND_RECOVERY.md).
64. **How would you design the whole product from the repository layout to the APIs and database?** — [End-to-end architecture](handbook/18A_END_TO_END_REFERENCE_PRODUCT_AND_ARCHITECTURE.md), [repository, data model and APIs](handbook/18B_REPOSITORY_STRUCTURE_DATA_MODEL_AND_API_CONTRACTS.md).
65. **How do security, privacy, child safety and legal review become actual launch gates?** — [Security and compliance gates](handbook/18C_SECURITY_PRIVACY_TRUST_AND_GLOBAL_COMPLIANCE_GATES.md).
66. **How do you operate, recover and improve the product after launch?** — [Testing, deployment and recovery](handbook/18D_TESTING_DEPLOYMENT_OPERATIONS_RUNBOOKS_AND_RECOVERY.md), [continuous improvement](handbook/18E_GLOBAL_LAUNCH_CAPACITY_COST_AND_CONTINUOUS_IMPROVEMENT.md).

---

## Your personal challenge

Choose one question above and write a one-page explanation in your own words. Then:

- draw the system or process;
- identify the components and their responsibilities;
- explain one failure mode;
- explain one security or privacy risk;
- identify one alternative technology;
- build a small, safe demonstration;
- record how you tested it and what you learned.

**The goal is not to memorise 66 questions. The goal is to become capable of asking better questions, tracing a system end to end, and proving your understanding through practical work.**
