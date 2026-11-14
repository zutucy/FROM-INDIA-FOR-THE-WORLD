# 04B — Software, Operating Systems and How a Computer Runs Programs

**Series:** Technology Foundations  
**Language:** Hinglish  
**Purpose:** Samajhna ki physical hardware par software kaise run hota hai, OS ka role kya hai, process/memory/files kaise manage hote hain aur modern desktop, mobile aur server environments kaise differ karte hain.

---

## 1. Software kya hota hai?

Software instructions, programs, data definitions aur supporting files ka organized set hai jo computer ko tasks perform karne deta hai. Software physical object nahi hota, lekin storage/memory mein encoded form mein exist karta hai aur hardware par execute hota hai.

Common categories:

1. **System software:** OS, drivers, firmware utilities and core system services.
2. **Application software:** browser, office app, editing tool, accounting software, games, communication apps.
3. **Development software:** editor, compiler, debugger, testing framework, build tools.
4. **Middleware/platform software:** databases, message brokers, web servers, runtimes and API gateways.
5. **Embedded software:** cars, routers, medical equipment, appliances, industrial controllers.
6. **Firmware:** low-level software stored in device firmware memory; boot and hardware control tasks.

Categories sometimes overlap. A database can be application software from user perspective and infrastructure software inside a company.

## 2. Software history: OS ki need kyun hui?

Early computers often had tightly coupled hardware and operator workflows. Programs could be loaded and run with manual setup. As computers became faster and more expensive, operators wanted less idle time, reliable job execution, shared resources and easier interaction.

### 2.1 Batch processing

Jobs ko batches mein collect karke run kiya jata. Isse operator intervention reduce hota, lekin user ko interactive response immediately nahi milta.

### 2.2 Multiprogramming and time-sharing

Multiple programs memory mein rakhe ja sakte the. CPU ek program wait kare (for example, input/output), toh OS another ready program ko schedule kar sakta tha. Time-sharing ne multiple users ko terminals ke through interactive computing dene ki direction di.

### 2.3 UNIX ka historical role

Bell Labs mein 1969 ke aas-paas Ken Thompson, Dennis Ritchie aur colleagues ne UNIX develop kiya. UNIX design portable multi-user, multitasking environment ke direction mein important bana. 1973 mein UNIX ka major rewrite C language mein hua—ye portability ke liye important tha: machine-specific assembly ke relative, higher-level C code ko new architecture par port karna easier ho sakta tha (although hardware-specific code and compiler support still needed).

### 2.4 Personal computers and graphical interfaces

Microprocessors aur lower hardware costs ne personal computers ko practical banaya. Command-line interfaces ke saath graphical user interfaces, windows, icons, pointer devices and desktop applications mainstream computing ko broader users ke liye accessible banane lage.

### 2.5 Linux and open collaboration

1991 mein Linus Torvalds ne Linux kernel project start kiya. Linux kernel Unix-like design ideas se influenced hai; Linux itself UNIX codebase ka direct derivative nahi. Kernel.org explains that Linux is one component; a complete usable Linux distribution kernel ke saath user-space tools, package management, libraries and other components combine karta hai.

**History lesson:** OS ka role hardware ko hide karna bhar nahi. OS resource sharing, isolation, permissions, file systems, networking and reliability provide karta hai.

## 3. Operating System (OS) kya karta hai?

Operating System hardware resources ko manage karta hai aur applications ko controlled services/interfaces deta hai.

Core responsibilities:

- Process and thread scheduling.
- Memory allocation and virtual memory.
- Filesystem and storage access.
- Device drivers and I/O.
- Network stack.
- User identity and permissions.
- Isolation and security boundaries.
- System services and user interface support.

OS application developer ko har device ke registers manually manage karne se bachata hai. Application OS APIs/system calls use karti hai.

## 4. Kernel, user space aur system calls

### 4.1 Kernel

Kernel OS ka privileged core hota hai. Ye CPU scheduling, memory management, device access, filesystems and core networking functions manage karta hai, design ke hisaab se.

### 4.2 User space

Normal applications and many system services restricted privileges ke saath run karte hain. Isse ek app ki error ya malicious behavior ko poore system par control milne se roka ja sakta hai—provided isolation correctly implemented hai.

### 4.3 System call

Application jab protected OS operation chahati hai—file open, process create, network socket, memory mapping—woh OS-provided interface invoke karti hai. System call boundary user mode se kernel mode transition involve kar sakti hai.

**Example:** Text editor `report.txt` open karta hai. Editor OS filesystem API call karta hai; OS permissions check karta hai, filesystem metadata locate karta hai, storage driver/device se blocks read karwata hai, aur bytes application ko return karta hai.

## 5. Boot process: power button se desktop tak

Simplified PC boot flow:

1. Power supply stable power provide karti hai.
2. CPU reset state se start karta hai.
3. Firmware (BIOS/UEFI class) initial hardware setup and boot selection perform karta hai.
4. Firmware bootloader/OS boot entry ko start karta hai.
5. Bootloader kernel load/start karta hai.
6. Kernel memory, CPU, drivers and core subsystems initialize karta hai.
7. Initial user-space process/service manager start hota hai.
8. Login manager or desktop/session user ke liye available hota hai.

Exact sequence hardware, firmware configuration, secure boot and OS ke according differ karta hai. Phones/consoles/embedded devices ka boot chain bhi alag ho sakta hai.

### Firmware vs operating system

Firmware device ko initial state mein configure/operate karne wala low-level software hai. OS uske baad broad resource management and applications provide karta hai. Firmware update ko casually interrupt nahi karna chahiye—failed update device ko unbootable bana sakta hai.

## 6. Process, thread and scheduling

- **Program:** stored instructions/file set.
- **Process:** running program ka isolated execution environment, resources and state.
- **Thread:** process ke andar execution path; threads commonly same process address space/resources share karte hain.
- **Scheduler:** runnable threads/processes ko CPU time allocate karta hai.

### Example: Browser

Browser ke multiple processes ho sakte hain—browser UI, tabs/renderers, extensions, GPU process, network service etc. Exact architecture browser/version/security model ke hisaab se change hota hai. Multiple-process design crash isolation, security sandboxing and responsiveness improve karne mein help kar sakta hai, at memory and coordination cost.

### Concurrency vs parallelism

- **Concurrency:** multiple tasks ka progress overlapping time window mein coordinate hota hai.
- **Parallelism:** multiple tasks literally simultaneously execute hote hain, typically multiple cores/processing units par.

Single-core system bhi time-slicing ke through concurrent tasks appear kara sakta hai. Parallel execution ke liye hardware capacity and software coordination chahiye.

## 7. Memory management and virtual memory

Applications virtual address spaces use karti hain. OS/hardware Memory Management Unit (MMU) virtual addresses ko physical memory pages se map karte hain.

Benefits:

- Processes ke beech isolation.
- Each process ko simpler address-space abstraction.
- Page-based permissions (read/write/execute).
- Memory overcommit and paging strategies.
- Shared libraries and memory-mapped files.

### Stack and heap (introductory view)

- **Stack:** function calls, local execution state, return addresses; lifetime often scope-based.
- **Heap:** dynamically allocated objects/data; lifetime explicit allocator or runtime/garbage collector manage kar sakta hai.

Actual memory model language/runtime dependent hai. Stack/heap simplification useful hai but every language implementation same nahi.

### Memory leak

Program memory allocate karta hai, lekin unneeded objects/resources release/reference-drop nahi karta. Long-running process ka memory usage grow ho sakta hai. Garbage-collected languages mein bhi references held rehne par logical memory leaks ho sakti hain.

## 8. Filesystem and storage

Filesystem storage device par files/directories ko organize karta hai.

Concepts:

- Path: file/folder location.
- Metadata: size, timestamps, permissions, ownership, etc.
- File descriptor/handle: open file/resource ka process-level reference.
- Journal/log: crash recovery consistency improve karne ke techniques (filesystem dependent).
- Mount: filesystem ko directory tree mein attach karna (Unix-like systems).
- Permissions: who can read/write/execute.

Windows commonly drive-letter paths use karta hai; Unix-like systems unified directory tree use karte hain. Filesystem behavior platform dependent hai. Hidden file ka matlab secure/encrypted file nahi hota.

### Delete vs secure erase

Normal delete often metadata/reference remove karta hai; underlying blocks immediately overwrite hona guaranteed nahi. SSD wear leveling and TRIM behavior secure erasure ko more complex banata hai. Sensitive data disposal ke liye drive/device/vendor-supported sanitization guidance follow karni chahiye.

## 9. Drivers and device I/O

Device driver OS aur hardware ke beech communication bridge hota hai. GPU driver, printer driver, Wi-Fi driver and storage controller driver examples hain.

Bad/incompatible drivers crash, device malfunction, performance problem or security vulnerabilities cause kar sakte hain. Drivers trusted vendors/OS update mechanisms se install karne chahiye; random driver download websites risky ho sakti hain.

## 10. Services, daemons and background processes

Many OS tasks background services run karte hain: network manager, update service, print spooler, logging, time synchronization, database service, web server etc.

Service manager start/stop/restart, dependencies and startup configuration manage karta hai. Linux distributions mein systemd common hai, but all Linux systems systemd use nahi karte. macOS mein launchd, Windows mein Service Control Manager use hota hai.

## 11. OS families and where they are used

| OS family | Common use | Notes |
|---|---|---|
| Windows | PCs, offices, gaming, enterprise | Broad commercial software/hardware support |
| macOS | Apple desktops/laptops | Apple hardware integration and Unix-based foundations |
| Linux distributions | Servers, cloud, development, desktop, embedded | Many distributions; kernel shared, userland differs |
| Android | Phones, tablets, TV, embedded | Linux kernel plus Android platform/framework and vendor components |
| iOS/iPadOS | Apple mobile devices/tablets | Apple-controlled platform and app distribution model |
| Embedded RTOS | Devices needing predictable responses | Workload-specific timing and resource constraints |

No OS is universally best. Hardware support, app ecosystem, administration, security model, cost, compliance and team expertise matter.

## 12. Linux: kernel vs distribution

Linux ko commonly OS bola jata hai, but technically Linux kernel hai. Ubuntu, Debian, Fedora, Arch and others are distributions combining the Linux kernel with user-space components, libraries, package management, tools and policies.

Why Linux is common on servers:

- Flexible deployment and automation.
- Strong networking and process tools.
- Large ecosystem.
- Source availability and licensing flexibility (license obligations still matter).
- Broad cloud/container support.

Limitations: admin learning curve, distribution differences, hardware/application compatibility and security maintenance responsibility.

## 13. Virtual machines vs containers

| VM | Container |
|---|---|
| Virtual hardware + guest OS | Isolated process environment sharing host kernel |
| Heavier startup/resource footprint (typical) | Usually lighter startup and packaging |
| Different guest kernels possible (hypervisor support dependent) | Same kernel family/compatibility requirement as host |
| Strong abstraction boundary | Isolation depends on kernel features and configuration |

Docker is one popular container tooling ecosystem, not the same thing as a virtual machine and not the only way to run containers.

### Example

A developer laptop may run Linux containers through a Linux VM on Windows/macOS. The container image contains application and dependencies; the VM supplies a Linux kernel environment. This detail helps explain why a container might behave differently between local and production.

## 14. Application lifecycle: click se run tak

Maan lo user photo editor open karta hai:

1. OS executable locate/load karta hai.
2. Dynamic libraries/runtime dependencies load hoti hain.
3. Process address space create hota hai.
4. Main thread start hota hai.
5. App OS graphics, file and input APIs use karti hai.
6. User image open karta hai; filesystem read and memory mapping occur.
7. CPU/GPU pixels process karte hain.
8. UI redraw hota hai.
9. Save par output file write/flush hoti hai.

App hang hone par CPU loop, lock contention, memory pressure, blocked network call or driver issue cause ho sakta hai. Diagnosis logs, stack traces, performance profiles and system metrics se hota hai.

## 15. Software updates and patch management

Updates categories:

- Security patches.
- Bug fixes.
- Feature releases.
- Driver/firmware updates.
- Dependency/library updates.
- OS version upgrades.

Safe update workflow:

1. Release notes and known issues check.
2. Backup or recovery option ensure.
3. Critical systems par staging/canary test.
4. Update apply.
5. Health checks and compatibility verify.
6. Problem par rollback/recovery plan use.

Updates ko indefinitely delay karna security risk hai; blindly install karna availability risk. Risk-based patch policy chahiye.

## 16. Software licensing basics

Software legally different licenses ke under distribute hota hai:

- Proprietary/commercial license.
- Open-source permissive licenses (MIT, BSD, Apache-2.0 examples).
- Copyleft licenses (GPL family examples).
- Freeware/shareware and other terms.

"Open source" ka matlab no rules nahi. Attribution, notice, source-distribution, patent and redistribution obligations license-specific hoti hain. Company codebase mein dependency use karne se pehle license review and inventory maintain karna useful hai.

## 17. Security principles

- Principle of least privilege: process/user ko minimum permissions.
- Secure defaults: open access ko default na banao.
- Patch management: known vulnerabilities fix karo.
- Process isolation: one faulty process ko others se separate rakho.
- Defense in depth: multiple independent protection layers.
- Auditability: meaningful system events record karo without logging secrets.
- Recovery: restore and rollback test karo.

OS-level permissions app-level authorization ka substitute nahi. Web app ko apne backend par har request authorize karni hoti hai.

## 18. Practical labs

### Lab A — Processes inspect karo (Windows)

```powershell
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10 ProcessName, Id, CPU
Get-Service | Where-Object {$_.Status -eq 'Running'} | Select-Object -First 20 Name, Status
```

### Lab B — Linux basics (VM or safe test environment)

```bash
uname -a
ps aux | head
free -h
df -h
ls -la
```

`sudo` commands tabhi run karo jab command samajh ho. Production machine par experimental commands mat chalao.

### Lab C — Process and memory experiment

1. Browser open karo; process list check karo.
2. Multiple tabs add karo; process and memory change note karo.
3. Browser close karo; processes terminate hue ya nahi observe karo.
4. Ek text file save/open karo; filesystem path and permissions inspect karo.

## 19. Questions to test understanding

1. Kernel aur operating system distribution mein kya difference hai?
2. Program aur process same kyu nahi?
3. Thread same process mein memory share kyu kar sakta hai?
4. Virtual memory ka benefit kya hai?
5. Driver aur application mein difference?
6. Container full VM kyu nahi?
7. Patch apply karne se pehle backup/staging kyun?
8. Open-source software free-to-use without obligations kyu necessarily nahi?

## 20. References

1. [Linux Kernel — About Linux](https://kernel.org/linux.html)
2. [The Linux Kernel Documentation](https://docs.kernel.org/)
3. [The Open Group — UNIX standards](https://www.opengroup.org/)
4. [Microsoft Learn — Windows architecture and development docs](https://learn.microsoft.com/windows/)
5. [Apple Platform Security](https://support.apple.com/guide/security/welcome/web)
6. [Docker Docs — What is a container?](https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-container/)
7. [NIST — Secure Software Development Framework (SSDF)](https://csrc.nist.gov/Projects/ssdf)

**Completion test:** Tum boot process, kernel/user-space, process/thread, virtual memory, filesystem, driver, service, VM/container aur OS updates apne words mein explain kar sako.
