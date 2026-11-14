# 04B — Software, Operating Systems and How a Computer Runs Programs

**Series:** Technology Foundations  
**Edition:** English 1.0  
**Purpose:** Understand how software runs on physical hardware, what an operating system does, how processes, memory and files are managed, and how desktop, mobile and server environments differ.

---

## 1. What is software?

Software is an organised collection of instructions, programs, data definitions and supporting files that allows a computer to perform tasks. Software is not a physical object, but it exists in encoded form in storage and memory and executes on hardware.

Common categories include:

1. **System software:** Operating systems, drivers, firmware utilities and core system services.
2. **Application software:** Browsers, office applications, editing tools, accounting software, games and communication applications.
3. **Development software:** Editors, compilers, debuggers, testing frameworks and build tools.
4. **Middleware/platform software:** Databases, message brokers, web servers, runtimes and API gateways.
5. **Embedded software:** Software in cars, routers, medical equipment, appliances and industrial controllers.
6. **Firmware:** Low-level software stored in device firmware memory, often used for boot and hardware-control tasks.

Categories can overlap. A database is application software from one user's perspective and infrastructure software inside a company.

## 2. Software history: why were operating systems needed?

Early computers had tightly coupled hardware and operator workflows. Programs could be loaded and run through manual setup. As computers became faster and more expensive, operators wanted less idle time, reliable job execution, shared resources and easier interaction.

### 2.1 Batch processing

Jobs were collected and executed in batches. This reduced repeated operator intervention, but users did not receive immediate interactive responses.

### 2.2 Multiprogramming and time-sharing

Multiple programs could be kept in memory. If one program had to wait—for example, for input/output—the operating system could schedule another ready program. Time-sharing developed interactive computing in which multiple users could access a computer through terminals.

### 2.3 The historical role of UNIX

Around 1969, Ken Thompson, Dennis Ritchie and colleagues at Bell Labs developed UNIX. Its design became important for portable, multi-user and multitasking computing. A major UNIX rewrite was carried out in C in 1973. Compared with machine-specific assembly, higher-level C code could be easier to port to another architecture, although hardware-specific code and compiler support were still required.

### 2.4 Personal computers and graphical interfaces

Microprocessors and lower hardware costs made personal computers practical. Alongside command-line interfaces, graphical user interfaces—with windows, icons, pointer devices and desktop applications—made computing accessible to a broader audience.

### 2.5 Linux and open collaboration

Linus Torvalds started the Linux kernel project in 1991. Linux is influenced by Unix-like design ideas, but it is not a direct derivative of the UNIX codebase. The Linux kernel project explains that Linux is one component of a usable distribution. A complete distribution combines the kernel with user-space tools, package management, libraries and other components.

**History lesson:** An operating system does more than hide hardware details. It manages resource sharing, isolation, permissions, filesystems, networking and reliability.

## 3. What does an operating system do?

An **Operating System (OS)** manages hardware resources and provides controlled services and interfaces to applications.

Core responsibilities include:

- Process and thread scheduling.
- Memory allocation and virtual memory.
- Filesystem and storage access.
- Device drivers and input/output.
- Network stack.
- User identity and permissions.
- Isolation and security boundaries.
- System services and user-interface support.

The OS protects application developers from having to manage every device register manually. Applications use operating-system APIs and system calls.

## 4. Kernel, user space and system calls

### 4.1 Kernel

The kernel is the privileged core of an operating system. Depending on the design, it manages CPU scheduling, memory, device access, filesystems and core networking functions.

### 4.2 User space

Ordinary applications and many system services run with restricted privileges. This can prevent one application's error or malicious behaviour from gaining complete control over the system, provided isolation is implemented correctly.

### 4.3 System call

When an application needs a protected OS operation—such as opening a file, creating a process, opening a network socket or mapping memory—it invokes an operating-system interface. A system call may involve a transition from user mode to kernel mode.

**Example:** A text editor opens `report.txt`. It calls an OS filesystem API. The OS checks permissions, locates filesystem metadata, asks the storage driver/device to read the required blocks and returns the bytes to the application.

## 5. The boot process: from the power button to the desktop

A simplified PC boot flow is:

1. The power supply provides stable power.
2. The CPU starts from its reset state.
3. Firmware (a BIOS/UEFI-class system) performs initial hardware setup and selects a boot target.
4. Firmware starts a bootloader or operating-system boot entry.
5. The bootloader loads and starts the kernel.
6. The kernel initialises memory, CPUs, drivers and core subsystems.
7. The initial user-space process or service manager starts.
8. A login manager or desktop/session becomes available to the user.

The exact sequence depends on hardware, firmware configuration, Secure Boot and the operating system. Phones, consoles and embedded devices may use different boot chains.

### Firmware versus operating system

Firmware is low-level software that configures or operates a device in its initial state. The OS then provides broader resource management and application support. Do not casually interrupt a firmware update; a failed update can make a device unbootable.

## 6. Processes, threads and scheduling

- **Program:** A stored set of instructions or files.
- **Process:** A running program with an execution environment, resources and state.
- **Thread:** An execution path inside a process. Threads commonly share the process address space and resources.
- **Scheduler:** Allocates CPU time to runnable processes or threads.

### Example: a browser

A browser may use multiple processes for the browser UI, tabs/renderers, extensions, GPU work and networking services. The exact architecture varies by browser, version and security model. A multi-process design can improve crash isolation, security sandboxing and responsiveness, but it also uses memory and requires coordination.

### Concurrency versus parallelism

- **Concurrency:** Multiple tasks make progress during an overlapping time period through coordination.
- **Parallelism:** Multiple tasks execute literally at the same time, commonly on multiple cores or processing units.

A single-core system can create the appearance of concurrent work through time-slicing. Parallel execution requires hardware capacity and software coordination.

## 7. Memory management and virtual memory

Applications use virtual address spaces. The OS and Memory Management Unit (MMU) map virtual addresses to physical memory pages.

Benefits include:

- Isolation between processes.
- A simpler address-space abstraction for each process.
- Page-based read, write and execute permissions.
- Paging strategies and controlled memory overcommit.
- Shared libraries and memory-mapped files.

### Stack and heap: an introductory view

- **Stack:** Often stores function-call state, local execution data and return addresses. Its lifetime is commonly tied to function scope.
- **Heap:** Stores dynamically allocated objects or data. Their lifetime may be managed explicitly by an allocator or automatically by a runtime/garbage collector.

The actual memory model depends on the language and runtime. The stack/heap explanation is a useful simplification, but not every language implementation behaves identically.

### Memory leak

A program allocates memory but fails to release it or stop retaining references when the data is no longer needed. A long-running process may continue to increase memory usage. Even in garbage-collected languages, retaining references can create logical memory leaks.

## 8. Filesystems and storage

A filesystem organises files and directories on a storage device.

Important concepts:

- **Path:** A file or directory location.
- **Metadata:** Size, timestamps, permissions, ownership and other attributes.
- **File descriptor/handle:** A process-level reference to an open file or resource.
- **Journal/log:** A technique used by some filesystems to improve crash recovery and consistency.
- **Mount:** Attaching a filesystem into a directory tree on Unix-like systems.
- **Permissions:** Rules that determine who can read, write or execute.

Windows commonly uses drive-letter paths, while Unix-like systems use a unified directory tree. Filesystem behaviour varies by platform. A hidden file is not automatically a secure or encrypted file.

### Delete versus secure erase

A normal delete operation often removes metadata or a reference; it does not guarantee that underlying storage blocks are immediately overwritten. SSD wear-leveling and TRIM behaviour make secure erasure more complex. For sensitive-data disposal, follow sanitisation guidance supported by the drive/device vendor and applicable standards.

## 9. Drivers and device input/output

A device driver is a software bridge between the operating system and hardware. Examples include GPU, printer, Wi-Fi and storage-controller drivers.

Bad or incompatible drivers can cause crashes, device failures, performance problems or security vulnerabilities. Install drivers through trusted vendors or operating-system update mechanisms. Random driver-download websites can be risky.

## 10. Services, daemons and background processes

Operating systems run many background services: network managers, update services, print spoolers, logging, time synchronisation, databases, web servers and others.

A service manager controls startup, stop/restart behaviour, dependencies and service configuration. Common examples include systemd on many Linux distributions, launchd on macOS and Service Control Manager on Windows. Not every Linux system uses systemd.

## 11. Operating-system families and their use cases

| OS family | Common use | Notes |
|---|---|---|
| Windows | PCs, offices, gaming and enterprise | Broad commercial software and hardware support |
| macOS | Apple desktops and laptops | Apple hardware integration and Unix-based foundations |
| Linux distributions | Servers, cloud, development, desktop and embedded systems | Many distributions; shared kernel, different user-space choices |
| Android | Phones, tablets, TVs and embedded systems | Linux kernel plus Android platform/framework and vendor components |
| iOS/iPadOS | Apple mobile devices and tablets | Apple-controlled platform and application-distribution model |
| Embedded RTOS | Devices needing predictable responses | Workload-specific timing and resource constraints |

No operating system is universally best. Hardware support, application ecosystem, administration, security model, cost, compliance and team expertise all matter.

## 12. Linux: kernel versus distribution

Linux is commonly called an operating system, but technically Linux is the kernel. Ubuntu, Debian, Fedora, Arch and other distributions combine the Linux kernel with user-space components, libraries, package management, tools and policies.

Why Linux is common on servers:

- Flexible deployment and automation.
- Strong networking and process tools.
- Large software ecosystem.
- Source availability and licensing flexibility, subject to licence obligations.
- Broad cloud and container support.

Limitations include the administration learning curve, distribution differences, hardware/application compatibility and ongoing security-maintenance responsibility.

## 13. Virtual machines versus containers

| Virtual machine | Container |
|---|---|
| Virtual hardware plus a guest OS | Isolated process environment that shares the host kernel |
| Usually has a heavier startup/resource footprint | Usually lighter to start and package |
| Can use different guest kernels when supported by the hypervisor | Requires compatibility with the host kernel family |
| Provides a strong virtual hardware abstraction | Isolation depends on kernel features and configuration |

Docker is one popular container tooling ecosystem. It is not the same as a virtual machine and is not the only way to run containers.

### Example

A developer's laptop may run Linux containers through a Linux VM on Windows or macOS. The container image contains the application and its dependencies; the VM supplies a Linux kernel environment. This helps explain why a container may behave differently between local development and production.

## 14. Application lifecycle: from click to execution

Imagine a user opens a photo editor:

1. The OS locates and loads the executable.
2. Dynamic libraries and runtime dependencies are loaded.
3. A process address space is created.
4. The main thread starts.
5. The application uses OS graphics, file and input APIs.
6. The user opens an image; filesystem reads and memory mapping may occur.
7. The CPU/GPU processes pixels.
8. The interface redraws.
9. When the user saves, the output file is written and flushed according to the application and OS behaviour.

An application hang may be caused by a CPU loop, lock contention, memory pressure, a blocked network call or a driver issue. Diagnosis uses logs, stack traces, performance profiles and system metrics.

## 15. Software updates and patch management

Update categories include:

- Security patches.
- Bug fixes.
- Feature releases.
- Driver and firmware updates.
- Dependency/library updates.
- Operating-system version upgrades.

A safer update workflow is:

1. Review release notes and known issues.
2. Ensure a backup or recovery option exists.
3. Test critical systems in staging or with a canary rollout.
4. Apply the update.
5. Verify health and compatibility.
6. Use the rollback or recovery plan if a problem appears.

Indefinitely delaying updates creates security risk; installing every update blindly can create availability risk. Use a risk-based patch policy.

## 16. Software-licensing basics

Software is distributed under different licences, including:

- Proprietary or commercial licences.
- Permissive open-source licences, such as MIT, BSD and Apache-2.0.
- Copyleft licences, including the GPL family.
- Freeware, shareware and other terms.

“Open source” does not mean “no rules”. Attribution, notices, source-distribution, patent and redistribution obligations depend on the licence. A company using dependencies should review licences and maintain an inventory.

## 17. Security principles

- **Least privilege:** Give a process or user only the permissions it needs.
- **Secure defaults:** Do not make open access the default.
- **Patch management:** Fix known vulnerabilities.
- **Process isolation:** Separate one faulty process from others.
- **Defence in depth:** Use multiple independent protection layers.
- **Auditability:** Record meaningful system events without logging secrets.
- **Recovery:** Test restore and rollback procedures.

Operating-system permissions do not replace application-level authorisation. A Web application must still authorise every protected request on its backend.

## 18. Practical labs

### Lab A — Inspect processes on Windows

```powershell
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10 ProcessName, Id, CPU
Get-Service | Where-Object {$_.Status -eq 'Running'} | Select-Object -First 20 Name, Status
```

### Lab B — Linux basics in a VM or safe test environment

```bash
uname -a
ps aux | head
free -h
df -h
ls -la
```

Use `sudo` only when you understand the command. Do not experiment on a production machine.

### Lab C — Process and memory experiment

1. Open a browser and inspect the process list.
2. Add several tabs and note changes in processes and memory.
3. Close the browser and observe whether its processes terminate.
4. Save and open a text file; inspect its path and permissions.

## 19. Questions to test understanding

1. What is the difference between a kernel and an operating-system distribution?
2. Why are a program and a process not the same thing?
3. Why can threads in the same process share memory?
4. What benefit does virtual memory provide?
5. How is a driver different from an application?
6. Why is a container not a full virtual machine?
7. Why should backups or staging checks precede important patches?
8. Why does open-source software not necessarily mean unrestricted use without obligations?

## 20. References

1. [Linux Kernel — About Linux](https://kernel.org/linux.html)
2. [The Linux Kernel Documentation](https://docs.kernel.org/)
3. [The Open Group — UNIX standards](https://www.opengroup.org/)
4. [Microsoft Learn — Windows documentation](https://learn.microsoft.com/windows/)
5. [Apple Platform Security](https://support.apple.com/guide/security/welcome/web)
6. [Docker Docs — What is a container?](https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-container/)
7. [NIST — Secure Software Development Framework](https://csrc.nist.gov/Projects/ssdf)

**Completion test:** You can explain the boot process, kernel and user space, process and thread, virtual memory, filesystem, driver, service, VM/container and OS update process in your own words.
