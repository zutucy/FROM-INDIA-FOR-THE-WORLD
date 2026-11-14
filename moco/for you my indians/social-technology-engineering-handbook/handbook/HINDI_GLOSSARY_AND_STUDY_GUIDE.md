# Hinglish Glossary and Study Guide

This companion helps a learner who studies in Hinglish while keeping standard English technical terminology intact. Learn the English term because documentation, error messages and engineering teams use it widely; use the Hinglish explanation to understand the idea.

| Term | Simple Hinglish meaning |
|---|---|
| Hardware | Computer ke physical parts jinhe touch kar sakte ho |
| Software | Instructions/programs jo hardware par run hote hain |
| Operating system | Software layer jo apps, memory, files, devices aur processes manage karti hai |
| Process | Running program ka isolated execution context |
| Thread | Process ke andar execution ka path |
| Network | Connected devices jo data exchange kar sakte hain |
| Protocol | Communication ke agreed rules |
| IP address | Network par device/interface ko identify karne wala address |
| DNS | Domain name ko network address se resolve karne ka system |
| Server | Computer/program jo requests receive karke service deta hai |
| Client | App/browser/device jo service request karta hai |
| Frontend | User ke saath interaction karne wala app/UI layer |
| Backend | Server-side logic, permissions aur data operations |
| API | Software systems ke beech defined interface/contract |
| Database | Structured ya document-oriented system jahan records manage hote hain |
| Query | Database se data read/change karne ki request |
| Index | Data locate karne ko faster banane wali extra structure; write/storage cost bhi hoti hai |
| Cache | Frequently used data ki temporary/derived copy |
| Object storage | Files/blobs ko durable keys ke through store karna |
| CDN | Users ke paas edge locations se content deliver karne ka network |
| Queue | Work items ko order/availability ke hisaab se process karne ka mechanism |
| Worker | Background job execute karne wala process |
| Authentication | Verify karna ki user/service kaun hai |
| Authorization | Decide karna ki verified identity kya kar sakti hai |
| Encryption | Data ko key ke bina unreadable form mein transform karna |
| Hashing | One-way digest banana; passwords ke liye dedicated slow password-hashing functions chahiye |
| Vulnerability | System ki weakness jo misuse ho sakti hai |
| Threat model | Assets, attackers, entry points aur possible harms ka structured analysis |
| Latency | Request ka response milne mein lagne wala time |
| Throughput | Ek time period mein complete hone wala work/data |
| Availability | Service kitni baar usable/working rehti hai |
| Scalability | Load grow hone par system ko handle karne ki capacity |
| Reliability | System predictable tareeke se required service deliver kare |
| Observability | Logs, metrics aur traces se internal state samajhne ki ability |
| Deployment | Software ko target environment mein release karna |
| Migration | Existing system/data schema ko controlled tareeke se change karna |
| Replication | Data/service ki additional copies maintain karna |
| Backup | Recovery ke liye independently retained copy |
| Sharding | Data ko multiple partitions/nodes mein distribute karna |
| Eventual consistency | Updates kuch time baad replicas/derived systems mein converge karte hain |
| Machine learning | Data se patterns/models learn karne wale methods |
| Model evaluation | Check karna ki model real target tasks par kitna achha/unsafe perform karta hai |
| RAG | Relevant external documents/data retrieve karke model response ko ground karna |
| SLO | Internal reliability target |
| SLA | Customer-facing service commitment, often with contractual consequences |
| RPO | Recovery ke baad kitna recent data loss tolerate kar sakte hain |
| RTO | Service ko kitne time mein restore karna target hai |

## Study method

1. **First pass:** Chapter ko bina code ke read karo. Har new term ka simple meaning likho.
2. **Second pass:** Diagram ko khud paper par redraw karo. Arrow kis direction mein ja raha hai aur data kis component se guzar raha hai, explain karo.
3. **Third pass:** Small lab run karo. Sirf commands copy mat karo; output ka meaning likho.
4. **Fourth pass:** Failure case socho. Network band, database slow, invalid input, expired session ya compromised account ho toh kya hoga?
5. **Teach-back:** Topic ko apne words mein 3–5 minutes mein samjhao. Jahan atko, wahi knowledge gap hai.

## A chapter is understood when you can answer

- Ye technology kis problem ko solve karti hai?
- Isse pehle teams kaise kaam karti thi?
- Iska simple internal flow kya hai?
- Iske alternatives aur limitations kya hain?
- Isse kaunse security/privacy/cost risks aate hain?
- Isko locally safe tareeke se kaise test kar sakte hain?
- Production mein kaun owner hoga aur failure par kaun action lega?
