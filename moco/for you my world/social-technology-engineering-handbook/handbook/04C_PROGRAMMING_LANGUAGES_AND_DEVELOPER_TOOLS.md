# 04C — Programming Languages, Code Execution and Developer Tools

**Series:** Technology Foundations  
**Edition:** English 1.0  
**Purpose:** Understand why programming languages were created, how code reaches a computer for execution, how to compare language choices and what tools contribute to professional software development.

---

## 1. What is programming?

Programming is the process of designing, expressing, testing and maintaining precise instructions for a computer. Writing source code is only one part of the work. Software engineering also includes problem definition, data modelling, algorithms, architecture, testing, deployment, security and maintenance.

A program combines instructions, data, rules and an execution environment. Its output may be a user-facing screen, a file, a network response, a machine-control signal, a report, a financial transaction or an event consumed by another system.

## 2. Why were programming languages invented?

Early computers had to be controlled with machine-specific numeric instructions or low-level operation codes. This was powerful but difficult for people, error-prone and tied to particular hardware architectures.

Assembly language introduced mnemonic names for machine instructions. High-level languages made it possible to express algorithms in more readable notation while compilers and interpreters handled translation and execution.

Educational histories from Cornell and OpenStax explain the different goals of language families such as FORTRAN, COBOL, BASIC, C and Java. The important point is that languages were not created for a fashion contest. Scientific calculation, business data processing, systems programming, interactive computing, Web development, safety and developer productivity shaped their designs.

## 3. A short history: major language milestones

Dates may refer to a design, public release or first implementation. Exact chronologies vary by source and language. This is a high-level timeline, not an exhaustive list.

| Period | Language or idea | Why it mattered |
|---|---|---|
| 1840s concept | Ada Lovelace's published algorithm for Babbage's Analytical Engine | An important early example of algorithmic work for a programmable machine |
| 1950s | Assembly and early high-level languages; FORTRAN (commercial release in 1957) | Made scientific and numerical programming more practical |
| 1959 onward | COBOL | Business records and data processing |
| 1960s | LISP, ALGOL, BASIC and Pascal | Symbolic computation, language theory, teaching and structured programming |
| 1970s | C and Smalltalk | Portable systems programming; object-oriented ideas and interactive environments |
| 1980s | C++ and Perl | C-based abstraction/performance; text processing and scripting |
| 1991 | Python's public-release era | Readability, general-purpose scripting and a broad later ecosystem |
| 1995 | JavaScript, Java and PHP emerge publicly | Browser scripting, virtual-machine portability and dynamic Web applications |
| 2000s | C#, Go (2009), Scala and others | Managed runtimes, productivity and modern service/concurrency needs |
| 2010s | Rust, Kotlin, Swift and mature TypeScript adoption | Memory-safety focus, modern mobile development and typed JavaScript development |

Do not describe one person as the sole inventor of all programming. Languages evolve through teams, standards groups, implementations and communities. C is strongly associated with Dennis Ritchie at Bell Labs; Java with James Gosling and the Sun Microsystems team; JavaScript with Brendan Eich's work at Netscape; Python with Guido van Rossum and community evolution. Each history includes many contributors beyond the best-known name.

## 4. Machine code, assembly and high-level languages

### Machine code

Processor instructions are represented using binary encodings defined by the processor's ISA. The CPU directly executes the machine instructions it supports. Machine code is architecture-specific.

### Assembly

Assembly is a human-readable mnemonic notation for machine instructions. An assembler converts it into machine code or object code. Assembly is useful for low-level hardware control, boot code, reverse engineering, performance-critical routines and education. However, writing most of a modern application manually in assembly is generally unnecessary.

### High-level languages

High-level languages provide readable constructs such as variables, functions, loops, objects, types, modules and exceptions. Compilers and runtimes handle many low-level details.

**Trade-off:** Abstraction can improve productivity and portability, but may add runtime overhead, limit control or hide complexity. Low-level control can require more work and create additional safety risks.

## 5. Building blocks of programming languages

| Concept | Meaning | Simple example |
|---|---|---|
| Variable | Named value or reference | `age = 18` |
| Type | Category and rules for a value | number, string, boolean |
| Expression | Computes a value | `price * quantity` |
| Condition | Selects a decision branch | `if score >= 50` |
| Loop | Repeats work | `for item in items` |
| Function | Reusable operation | `calculate_total()` |
| Data structure | Organises values | array, map, tree |
| Module | Code-organisation boundary | `auth` module |
| Exception/error | Represents or handles failure | invalid input |
| Interface/type contract | Defines expected data or methods | `User` type |

### Example: a simple decision

```ts
function canAccessPrivatePost(isOwner: boolean, isApprovedFollower: boolean) {
  return isOwner || isApprovedFollower;
}
```

This is only a teaching example. Real authorisation may also need to check block state, post visibility, account status, moderation state, organisation roles and other rules. Security-sensitive authorisation must not trust client-supplied booleans; the server should make decisions using trusted session and database state.

## 6. Data types and type systems

- **Static typing:** Many type checks are performed at compile or build time.
- **Dynamic typing:** Types and operations are checked during execution.
- **Strong/weak typing:** These are informal terms; their precise meaning differs by language and community.
- **Type inference:** A compiler or tool can infer types from context.

Examples:

- TypeScript adds static type checking to the JavaScript ecosystem, but its types do not automatically validate data at runtime.
- Python uses dynamic typing; type hints support tooling and optional checking.
- Java is statically typed and uses a managed runtime.
- C and C++ offer low-level control; memory safety depends heavily on developer discipline and additional tools.

Input validation and type checking are not the same. JSON received from a browser does not become safe merely because the application declares a TypeScript interface. Runtime validation is still required.

## 7. Compiler, interpreter and runtime: how does code execute?

### Compiler

A compiler translates source code or another representation into a different representation—machine code, bytecode, intermediate representation or another language. Compilation may include parsing, semantic checks, optimisation and code generation. The exact pipeline depends on the tool.

### Interpreter

An interpreter reads or evaluates a program representation and executes its behaviour. Modern interpreters may use bytecode and just-in-time compilation, so the statement “interpreted means line-by-line and always slow” is misleading.

### Runtime

A runtime environment provides services needed for program execution, such as memory management, garbage collection, standard libraries, exception handling, integration with thread scheduling, JIT compilation or dynamic linking.

### JIT (Just-In-Time) compilation

A runtime may compile and optimise frequently executed code while the program is running. This introduces trade-offs involving startup time, memory use and performance.

### Bytecode and virtual machines

Some languages compile source into intermediate bytecode. A virtual machine may interpret that bytecode or compile it to machine code using JIT techniques. Java and the JVM are familiar examples. The .NET CLR and managed languages form another example family.

**Nuance:** C is often compiled into native object/executable code. The common CPython implementation compiles Python source to bytecode and runs it on a virtual machine. Java source is compiled to bytecode, and a JVM implementation may combine interpretation and JIT compilation. Keep the distinction between a language specification and one implementation clear.

## 8. Language choices: what is each language commonly used for?

| Language/technology | Common strengths and uses | Trade-offs or notes |
|---|---|---|
| JavaScript | Browser UI, Node.js backend and tooling | Dynamic runtime; dependency discipline is important |
| TypeScript | Larger JavaScript codebases with static checks | Does not automatically provide runtime validation or security |
| Python | Automation, scripting, data science, AI and backend | CPU-bound performance and packaging/runtime choices matter |
| Java | Enterprise services, JVM applications and parts of Android ecosystem | JVM operations and verbosity may be relevant trade-offs |
| C | Systems, embedded software and OS components | Manual memory handling and undefined-behaviour risks |
| C++ | Game engines, high-performance software and systems | Complex language and memory/concurrency risks |
| C# | .NET services, desktop applications and games with Unity | .NET ecosystem and versioning considerations |
| Go | Network services, command-line tools and infrastructure tooling | A simpler language design is not ideal for every domain |
| Rust | Systems software with a strong compile-time memory-safety model | Learning curve and domain fit matter |
| Kotlin | Android and JVM development | Platform and runtime knowledge are still required |
| Swift | Apple-platform development | Focused on the Apple ecosystem |
| SQL | Querying and manipulating relational data | Declarative language; database-specific extensions exist |
| Bash/PowerShell | Shell automation and operating-system tasks | Quoting, permissions and platform differences require care |
| HTML/CSS | Web-document structure and presentation | Essential Web technologies, but not general-purpose programming languages in the same sense |

Choose a language based on the problem, team, ecosystem, performance, safety, maintenance and deployment environment—not popularity alone.

## 9. Programming paradigms

- **Procedural:** Organises work as step-by-step procedures and functions.
- **Object-oriented:** Uses objects/classes, encapsulation and polymorphism. Language support and design quality vary.
- **Functional:** Emphasises functions, composition, immutability and higher-order operations.
- **Declarative:** Describes the desired result or state rather than every low-level step. SQL and some UI paradigms are examples.
- **Event-driven:** An event occurs and a handler executes; common in browser interfaces, servers and messaging systems.
- **Concurrent/parallel:** Coordinates multiple flows or executes work across multiple processing units.

Real applications often combine paradigms. “Object-oriented versus functional” should not become a religious debate. Use the approach that improves correctness and maintainability for the problem.

## 10. Data structures and algorithms: beyond syntax

Learning language syntax is not enough. Programs must organise, search, update and transform data.

Common data structures:

- Array/list: ordered items.
- Hash map/dictionary: key-value lookup.
- Set: unique elements.
- Stack: last-in, first-out.
- Queue: first-in, first-out.
- Linked list: node-based sequence.
- Tree: hierarchical structure.
- Graph: nodes and relationships.
- Heap/priority queue: repeated minimum/maximum selection.

Algorithms include searching, sorting, traversal, shortest paths, deduplication, scheduling, hashing and optimisation.

### Introduction to complexity

Big-O notation describes growth trends such as O(1), O(log n), O(n), O(n log n) and O(n²). It is not a precise stopwatch prediction. Constants, input distribution, memory locality and runtime overhead matter.

Example: searching a list for a username may require a linear scan, O(n). A properly indexed map or database lookup may be faster on average. Database indexes add storage and write overhead; they are not free speed.

## 11. Developer tools: parts of a professional workflow

| Tool/category | Why it is needed | Examples |
|---|---|---|
| Code editor | Write and edit source | VS Code, Vim, JetBrains editors |
| IDE | Integrated editing, navigation, debugging and build tools | IntelliJ IDEA, Visual Studio |
| Compiler/interpreter | Transform or run code | TypeScript compiler, Python, JDK |
| Package manager | Install and update dependencies | npm, pnpm, pip, Maven, Cargo |
| Build tool | Create repeatable builds/bundles | Vite, Gradle, Make |
| Linter | Static style and error checks | ESLint, Ruff |
| Formatter | Consistent formatting | Prettier, Black |
| Debugger | Inspect and step through execution | Browser debugger, GDB, IDE debugger |
| Test framework | Automate behaviour checks | Vitest, pytest, JUnit |
| Version control | Record changes and branch work | Git |
| Code hosting | Collaboration and review | GitHub, GitLab, Bitbucket |
| CI/CD | Automate build, test and deployment | GitHub Actions, GitLab CI |

Tools can be replaced. Fundamentals—source code, build, dependency, test, version and release—remain important.

## 12. Git: code history and collaboration

Git is a distributed version-control system. It records commits and supports branches, merges and collaboration. Linus Torvalds started the Git project in 2005 in the context of Linux kernel development, after the previous source-control arrangement became unsuitable.

A basic workflow:

```bash
git init
git status
git add .
git commit -m "Add initial feature"
git branch feature/profile
git switch feature/profile
```

A shared-repository example:

```bash
git remote add origin <repository-url>
git push -u origin main
```

Replace `<repository-url>` with your own repository URL. Never commit secrets or passwords to a code repository.

### Important Git concepts

- **Working tree:** Current local files.
- **Staging area/index:** Selected changes for the next commit.
- **Commit:** A snapshot in repository history, with metadata.
- **Branch:** A movable reference to commit history.
- **Merge:** Combines histories.
- **Rebase:** Replays commits onto a new base.
- **Remote:** A reference to another repository.
- **Tag:** A named marker, often used for a release version.

GitHub is not Git. Git is version-control software; GitHub is a hosted collaboration service. Other repository-hosting services exist.

## 13. Package managers and dependencies

Modern applications use external libraries. Package managers install packages and resolve dependency graphs.

Risks include:

- Malicious packages and typosquatting.
- Vulnerable or outdated dependencies.
- Abandoned projects.
- Licence incompatibility.
- Compromised maintainer accounts.
- Dependency-confusion attacks.

Good practices:

1. Verify package names and publishers.
2. Commit a lockfile.
3. Keep dependencies minimal.
4. Use vulnerability alerts and scanning.
5. Review updates and run tests.
6. Maintain a licence inventory for commercial products.
7. Never hardcode secrets in package configuration or source code.

## 14. Environments: development, test, staging and production

- **Development/local:** Work on an engineer's machine.
- **Test/CI:** Automated verification environment.
- **Staging:** Production-like environment for release checks.
- **Production:** The real service with real users and business data.

Keep credentials, databases, storage buckets and permissions separate across environments. Do not mix a local test database with production user data.

Environment variables can provide configuration values, but a `.env` file is not automatically a secure vault. Store production secrets in an appropriate secrets manager or platform secret store.

## 15. Code quality: readability is more valuable than cleverness

Maintainable code usually has:

- Clear names.
- Small, cohesive functions.
- Explicit input/output contracts.
- Limited duplication where an abstraction genuinely helps.
- Useful error handling.
- Tests for important behaviour.
- Comments that explain why, rather than repeat what the code says.
- Logs with useful context but without passwords, tokens, private messages or sensitive personal data.

Architecture should match project scale. One well-structured application may be simpler and safer than premature microservices.

## 16. Practical programming sequence

Recommended learning order:

1. Problem-solving and pseudocode.
2. Variables, types, conditions and loops.
3. Functions and modules.
4. Arrays, objects/maps and sets.
5. Error handling and debugging.
6. Files and HTTP/API basics.
7. Data structures and algorithms.
8. SQL and database fundamentals.
9. Tests and Git workflow.
10. Build and deploy one complete small project.

For Web product development, JavaScript followed by TypeScript is a practical path because browsers and server ecosystems use them. Python is also an excellent first language for automation and data work. Choose according to your goal, not social-media trends.

## 17. Safe first project: a command-line contact notebook

**Goal:** Create, list, search and remove contacts stored in a local JSON file.

Version 1 requirements:

- Add a name and contact note.
- Reject empty names.
- List contacts.
- Search without case sensitivity.
- Save data to a file.
- Handle missing or corrupt files gracefully.
- Add unit tests for validation and search.

Version 2:

- Add unique IDs.
- Update a contact.
- Export a backup.
- Add command-line arguments.

Version 3:

- Replace file persistence with SQLite or PostgreSQL.
- Add an API layer.
- Add a simple user interface.

This project teaches data modelling, validation, persistence, error handling and incremental design without premature cloud complexity.

## 18. Common mistakes and misconceptions

- Learning syntax only and ignoring problem-solving.
- Believing one language is best for every task.
- Assuming TypeScript types validate untrusted network JSON at runtime.
- Believing GitHub automatically protects secrets that have been committed.
- Installing packages without checking their names, maintenance or licence.
- Using `try/catch` to silently ignore every error.
- Putting all business logic inside UI components or controllers.
- Starting with microservices before a real need exists.
- Copying code without understanding its inputs, outputs and security boundary.

## 19. Glossary

- **Source code:** Human-authored program text.
- **Machine code:** Processor-executable instruction encoding.
- **Assembler:** Converts assembly into machine or object code.
- **Compiler:** Translates source or another representation into a different representation.
- **Interpreter:** Executes or evaluates a program representation.
- **Runtime:** Services and environment that support program execution.
- **Bytecode:** Intermediate instruction representation for a virtual machine/runtime.
- **JIT:** Compilation during execution.
- **Type system:** Rules about values and operations.
- **Dependency:** An external library or component on which a program relies.
- **Lockfile:** A snapshot of exact dependency resolution.
- **Linter:** A static analysis and style tool.
- **Debugger:** A tool for inspecting program execution.
- **CI/CD:** Continuous integration and continuous delivery/deployment practices.
- **Repository:** A version-controlled project and its history.

## 20. References and further study

1. [OpenStax — Programming Language Foundations](https://openstax.org/books/introduction-computer-science/pages/7-1-programming-language-foundations)
2. [Cornell — History of Languages (course material)](https://www.cs.cornell.edu/courses/cs5142/2013fa/2013-0828-intro.pdf)
3. [Computer History Museum — Timeline of Computer History](https://www.computerhistory.org/timeline/computers/)
4. [Git Documentation](https://git-scm.com/docs/git)
5. [Git User Manual](https://www.kernel.org/pub/software/scm/git/docs/user-manual.html)
6. [Python Documentation](https://docs.python.org/3/)
7. [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
8. [MDN JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
9. [The Rust Programming Language Book](https://doc.rust-lang.org/book/)

**Completion test:** You can explain why programming languages were needed, the differences between a compiler, interpreter and runtime, JavaScript versus TypeScript, language selection, dependencies, Git commits/branches and a repeatable local-to-production workflow.
