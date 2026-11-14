# 04A — Computer Hardware: From Electricity to Modern Servers

**Series:** Technology Foundations  
**Edition:** English 1.0  
**Purpose:** Understand the physical parts of computers, what they do, how they evolved, their trade-offs and where they are used.  
**Scope:** This chapter applies to laptops, phones, servers, gaming PCs, cloud data centres, scientific computers, embedded devices and almost every software system.

---

## 1. What is hardware?

Hardware means the physical parts of a computer or digital device—the components that can be seen, touched or measured. Examples include the processor, RAM, SSD, motherboard, display, keyboard, network card, battery, camera, cooling fan and power supply.

Software provides instructions and data. Hardware provides the physical mechanisms that execute, store and transfer those instructions and data. A practical computing experience depends on both.

**Analogy:** Restaurant equipment is similar to hardware; recipes and order procedures are similar to software. A recipe alone cannot prepare food, and equipment without instructions may not produce the intended result. The analogy is imperfect, but it provides a useful starting point.

## 2. Computer history: why did hardware evolve?

### 2.1 From manual calculation to programmable machines

People have used counting tools for centuries. The abacus, mechanical calculators, punched-card machinery and later electronic computers addressed different problems: repetitive calculation, census and data processing, navigation, science, cryptography, business accounting and military computation.

Charles Babbage's Analytical Engine concept presented an important design vision for a programmable general-purpose machine. Ada Lovelace wrote algorithmic instructions for the proposed machine and considered the possibility of non-numeric applications. However, the complete machine was not built as an operational system during that period because of manufacturing constraints.

Early twentieth-century electronic computers used relays, vacuum tubes and, later, transistors. Vacuum tubes could switch or amplify electrical signals, but they were bulky, hot, power-hungry and prone to failure. Smaller, cooler and more reliable switching devices were needed.

### 2.2 The transistor revolution

In December 1947, Bell Labs researchers John Bardeen and Walter Brattain demonstrated point-contact transistor action. William Shockley played an important role in transistor theory and later junction-transistor development. Compared with vacuum tubes, transistors offered a path to smaller size, lower power consumption and better reliability.

The Computer History Museum's semiconductor timeline documents milestones including the 1947 transistor demonstration, Jack Kilby's 1958 microcircuit and Robert Noyce's 1959 practical monolithic integrated-circuit concept. Integrated circuits made it possible to place multiple electronic components on one semiconductor chip.

### 2.3 Microprocessors and personal computing

In 1971, Intel announced the 4004 microprocessor. According to the Computer History Museum, the design was developed for Japanese calculator maker Busicom. Federico Faggin led important design work, while Ted Hoff was central to the architecture. The milestone opened a commercial path for integrating CPU functionality on a single chip.

Microprocessors later became cheaper and more capable. Memory density, storage, displays, networking and software also improved. Personal computers, laptops, smartphones, embedded controllers and cloud servers are outcomes of this long chain.

**History lesson:** One invention rarely creates a revolution by itself. Transistors, integrated circuits, manufacturing processes, memory, software, networks and mass production combined to create modern computing.

## 3. Digital data: bits and binary

Computers encode information through physical states. Digital systems commonly use binary representation:

- **Bit:** A binary digit, either 0 or 1.
- **Byte:** Commonly eight bits.
- **Kilobyte (KB), megabyte (MB), gigabyte (GB) and terabyte (TB):** Data-size units. Both decimal (base 1000) and binary (base 1024) conventions are used, so storage labels and operating-system displays may show slightly different values.

Binary does not mean that tiny printed zeroes and ones move inside a computer. Circuits distinguish voltage or current ranges, charge states or magnetic/flash states. The logical abstraction treats those states as 0 and 1.

### Example: how is text stored?

Text characters are mapped to numbers through character encoding. Unicode and UTF-8 are common in modern Web and software environments. An emoji is not necessarily a one-byte symbol; a UTF-8 character may use multiple bytes.

**Important distinction:** Bits represent data. The application, file format, encoding, protocol and context define what that data means.

## 4. Transistors, logic gates and chips

A transistor is a semiconductor device used to control or switch an electrical signal. Modern digital chips contain very large numbers of carefully arranged transistors.

Logic gates (AND, OR, NOT, XOR and others) produce outputs according to logical rules applied to binary inputs. These gates can be combined into adders, registers, control circuits, memory cells and larger processor structures.

- **AND:** Output is 1 only when both inputs are 1.
- **OR:** Output is 1 when at least one input is 1.
- **NOT:** Inverts the input.
- **XOR:** Output is 1 when the inputs differ.

Arithmetic and decision logic can be built from these components. Real chips also require engineering work on timing, power, heat, signal integrity, manufacturing defects and verification.

## 5. CPU — Central Processing Unit

The CPU is the central processor for general-purpose instruction execution. In a simplified model, it fetches instructions, decodes them, executes them and updates results or register state. Modern CPUs include pipelines, branch prediction, out-of-order execution, caches, multiple cores and many other optimisations. Actual processor design is considerably more complex.

### 5.1 Common internal concepts

| Component | Basic role |
|---|---|
| Control logic | Coordinates instruction execution |
| ALU | Performs integer arithmetic and logical operations |
| FPU | Performs floating-point calculations |
| Registers | Very small, very fast storage inside the CPU |
| Cache | Keeps frequently needed instructions and data close to the CPU |
| Clock | Provides a timing reference for coordinating cycles |
| MMU | Supports virtual-memory address translation and protection |

### 5.2 What does clock speed mean?

Clock frequency is expressed in hertz, commonly gigahertz (GHz). A 3 GHz clock represents roughly three billion clock cycles per second—not three billion completed application-level instructions. One instruction may require multiple cycles, and a processor may retire multiple operations in one cycle. Clock speed alone therefore cannot determine CPU performance.

Performance also depends on architecture, core count, cache, memory latency, instruction mix, power limits, thermal limits, compiler, software and workload.

### 5.3 Cores and threads

- **Core:** An execution engine or resource group within a processor.
- **Hardware thread/logical processor:** A capability that lets a core manage multiple execution contexts. The exact mechanism depends on the architecture.
- **Software thread:** An execution path managed by an operating system or runtime. It is not the same concept as a hardware thread.

An eight-core CPU does not make every application eight times faster. Software must be divided into parallel work, shared data must be coordinated and bottlenecks must be managed.

### 5.4 ISA: x86, Arm and RISC-V

An **Instruction Set Architecture (ISA)** defines the software-visible contract: supported instructions, registers, memory behaviour and execution conventions.

- **x86-64:** An ISA family widely used in desktop and server computing, including Intel and AMD ecosystems.
- **Arm:** An architecture family used in mobile devices, embedded systems and increasingly in servers and laptops.
- **RISC-V:** An open-standard instruction-set architecture with an extensible ecosystem.

An ISA and a microarchitecture are different. Two processors supporting the same ISA may have very different internal designs. Software portability also depends on the operating system, ABI, libraries and runtime.

## 6. Memory hierarchy: where is data stored, and how quickly can it be accessed?

Computer memory is not one single container. It is a hierarchy with trade-offs in speed, capacity, cost and persistence.

| Layer | Typical property | What happens when power is removed? |
|---|---|---|
| CPU registers | Extremely fast, very small | Contents are lost |
| L1/L2/L3 cache | Fast and small | Contents are lost |
| RAM | Working memory, larger capacity | Contents are normally lost |
| SSD/HDD | Persistent storage | Data is retained |
| Backup/object storage | Long-term or redundant storage | Designed for persistence |

### 6.1 RAM

RAM (Random Access Memory) holds active code and data for running programs. A CPU does not normally fetch every instruction directly from a storage drive. The operating system loads files into memory, memory management provides virtual address spaces, and CPU caches keep frequently used data closer to the processor.

When RAM is insufficient, the operating system may move pages to swap space or a page file. Because storage is much slower than RAM, heavy swapping can make a system noticeably slower.

### 6.2 Cache

CPU caches attempt to keep frequently accessed instructions and data close to the processor. L1 is generally the smallest and fastest, L2 is usually larger, and L3 is often larger and may be shared. Exact cache structures differ by processor design.

Cache performance depends on locality:

- **Temporal locality:** recently used data may be used again soon.
- **Spatial locality:** data near a recently used address may be needed soon.

A cache miss forces the system to fetch data from a lower level in the hierarchy, increasing latency.

### 6.3 HDD versus SSD

| HDD | SSD |
|---|---|
| Stores data magnetically on rotating platters | Uses flash memory and no moving storage parts |
| Mechanical seek and rotational delay | Much lower access latency for many workloads |
| Often lower cost per capacity | Often higher cost per capacity, depending on market and type |
| Mechanical movement can create noise and shock sensitivity | Generally quieter and more shock-resistant |
| Useful for some high-capacity storage workloads | Common for operating systems, applications and fast storage |

SSD types include SATA and NVMe drives. NVMe commonly uses PCIe and can support much higher parallel I/O than older SATA interfaces. Performance still depends on controller, flash type, thermal behaviour and workload.

## 7. GPU, NPU and other accelerators

A **GPU (Graphics Processing Unit)** is designed for high-throughput parallel processing. Graphics rendering is a major use, but GPUs also support AI training and inference, simulation, image processing and scientific computing.

An **NPU (Neural Processing Unit)** is an accelerator category designed to execute neural-network or AI-related operations efficiently. NPUs are not all equivalent: supported operations, memory bandwidth, software stack and performance differ.

Other accelerators include video encode/decode blocks, cryptographic accelerators, digital signal processors (DSPs), FPGAs and custom ASICs.

### CPU versus GPU: a simple comparison

| CPU | GPU |
|---|---|
| General-purpose control and mixed workloads | High-parallelism and high-throughput workloads |
| Often fewer, powerful cores | Often many execution lanes or cores; architecture-dependent |
| Operating systems, application logic and branching | Graphics, matrix and data-parallel work |
| Often effective for latency-sensitive tasks | Often effective for large parallel workloads |

A GPU is not automatically faster for every job. Data transfer, workload shape, memory bandwidth, available libraries and kernel-launch overhead all matter.

## 8. Motherboard, buses, power and cooling

- **Motherboard:** The main circuit board connecting components. It may include a CPU socket, RAM slots, storage connectors, expansion slots, firmware and power-delivery circuits.
- **Bus/interconnect:** Data and control communication paths between components. Modern systems often use complex point-to-point links and fabrics rather than one simple shared bus.
- **Power Supply Unit (PSU):** Converts wall power into regulated DC outputs. Quality, capacity, efficiency and protection matter.
- **Battery:** Stores energy in portable devices; charging and battery-management circuits control it.
- **Cooling:** Heat sinks, fans, liquid loops or passive thermal designs remove heat. When temperature or power limits are reached, a processor may use thermal throttling.

### Thermal-throttling example

A laptop runs a demanding video export. The CPU or GPU reaches a temperature or power limit. The system may reduce frequency or voltage. The export becomes slower even though the processor specification looks powerful. Cleaning blocked vents, maintaining appropriate cooling and tuning the workload may help. Unsafe overclocking is not a reliable fix.

## 9. Networking hardware

- **NIC (Network Interface Controller):** Provides a wired or wireless network interface.
- **Ethernet adapter:** Provides a wired network connection.
- **Wi-Fi radio:** Communicates over a wireless local-area network.
- **Router:** Forwards packets between networks. Home routers often combine routing, firewall, Wi-Fi access-point and switching functions.
- **Switch:** Forwards frames between devices on a local network.
- **Modem/ONT:** Connects a home or office network to the provider access network, depending on the ISP technology.

Networking protocols are covered in detail in Part 05.

## 10. Client-device hardware versus server hardware

Laptops and phones are optimised for user interaction: battery life, display, camera, keyboard or touch input, compact size and thermal limits.

Server hardware may prioritise:

- High memory capacity and, where needed, ECC memory.
- Multiple CPU sockets or high-core-count CPUs, depending on the workload.
- High-speed networking, such as 10/25/100+ GbE in suitable environments.
- Redundant power supplies and fans.
- Remote-management interfaces.
- RAID/HBA/storage controllers where appropriate.
- Rack density, cooling, serviceability and uptime.

Not every server is a huge machine. Small workloads may run on ordinary virtual machines or modest physical servers. Cloud users often do not need to choose the physical server; the provider offers a compute abstraction.

## 11. Virtualisation: multiple isolated environments on one physical machine

Virtualisation uses a hypervisor to run multiple virtual machines on one physical host. Each VM sees virtual CPUs, memory, disks and an operating-system environment.

- **Type 1 hypervisor:** Runs directly on or very close to the hardware.
- **Type 2 hypervisor:** Runs as an application-like layer on top of a host operating system.
- **Virtual machine:** A virtualised computer with a guest operating system.
- **Container:** Shares the host kernel while providing process, filesystem and network isolation. It does not normally include a fully separate guest kernel.

VMs and containers are covered further in Part 04B and the deployment chapters.

## 12. Hardware-security basics

Hardware features can support security layers:

- **Secure Boot:** Verifies a chain of trusted boot components.
- **TPM/secure element:** Provides a protected hardware context for storing or operating on cryptographic keys and measurements.
- **Hardware-backed key storage:** Can reduce key-extraction risk, but does not make a system immune to compromise.
- **IOMMU:** Helps constrain device DMA access to memory.
- **ECC RAM:** Helps detect or correct certain memory-bit errors; support and use cases vary.

Hardware security works together with software, configuration, threat modelling and operational controls.

## 13. Real-world examples across industries

| System | Possible hardware bottlenecks |
|---|---|
| E-commerce | Database RAM, network throughput and storage IOPS |
| Video streaming | CPU/GPU encoding, storage and CDN egress/network capacity |
| AI model training | GPU memory, GPU interconnect, power and cooling |
| Banking | Reliable storage, network security, redundancy and hardware security modules |
| Gaming | GPU, CPU, memory bandwidth, storage and latency |
| Industrial IoT | Low-power processors, sensors, connectivity and ruggedisation |
| Scientific computing | CPU/GPU throughput, high-speed interconnect and storage |

Hardware decisions should be driven by workloads. Buying a GPU or server because it is fashionable is not engineering.

## 14. Beginner troubleshooting checklist

1. **Power:** Verify the charger, cable, outlet and battery state.
2. **Temperature:** Are vents blocked? How does the fan behave? Does performance drop suddenly?
3. **Memory:** Check RAM pressure in Task Manager or System Monitor.
4. **Storage:** Check free space, drive-health indicators and disk usage.
5. **CPU/GPU:** Which process is creating the load?
6. **Network:** Separate Wi-Fi signal, packet loss, router and ISP issues.
7. **Logs:** Review relevant operating-system event or system logs.
8. **Recent changes:** Was there a driver, update, hardware or software change?

Opening unknown hardware, repairing a power supply or handling a punctured or swollen battery can be dangerous. Use a suitably trained technician.

## 15. Practical labs

### Lab A — Inventory your computer hardware

On Windows PowerShell:

```powershell
Get-CimInstance Win32_Processor | Select-Object Name, NumberOfCores, NumberOfLogicalProcessors
Get-CimInstance Win32_PhysicalMemory | Select-Object Manufacturer, Capacity, Speed
Get-CimInstance Win32_OperatingSystem | Select-Object Caption, Version, OSArchitecture
Get-PhysicalDisk | Select-Object FriendlyName, MediaType, Size, HealthStatus
```

These are read-only inventory queries. Output depends on the device. `Get-PhysicalDisk` availability may vary by Windows version and storage driver.

### Lab B — Observe a bottleneck

1. Open a browser with several tabs.
2. Observe CPU, RAM, disk and network activity in Task Manager or System Monitor.
3. Copy a local file and compare disk activity.
4. Play a video and observe GPU or decoder activity.
5. Close a demanding application and note the CPU/RAM difference.

### Lab C — Draw an architecture diagram

Draw a phone/laptop -> router -> ISP -> Internet -> cloud server -> database/object storage path. Under each box, write its hardware role and the impact of a failure.

## 16. Common misconceptions

- More GHz always means a faster CPU — false.
- More cores make every application faster — false.
- RAM is permanent storage — false for ordinary systems.
- An SSD and RAM are the same thing — false.
- A GPU is only for gaming — false.
- Cloud means there is no hardware — false; the provider manages the hardware.
- More expensive hardware is always best — false; workload and total cost matter.
- Hardware security alone makes a system secure — false.

## 17. Glossary

- **Semiconductor:** A material whose electrical conductivity can be controlled.
- **Transistor:** A semiconductor switching or amplification device.
- **Integrated circuit:** Multiple electronic components integrated on a chip.
- **Microprocessor:** Processor functionality integrated into a chip.
- **ISA:** The CPU instruction-set architecture contract.
- **Microarchitecture:** The internal implementation of a processor design.
- **Latency:** The time required for an operation or response.
- **Throughput:** Amount of work or data processed per unit of time.
- **Bandwidth:** Maximum or available data-transfer capacity in a defined context.
- **Volatile memory:** Memory that loses stored contents when power is removed.
- **Persistent storage:** Storage that retains data without continuous power.
- **Thermal throttling:** Reducing performance to control temperature or power.
- **Virtualisation:** Abstracting physical computing resources into virtual environments.

## 18. References and further study

1. [Computer History Museum — Timeline of Computer History](https://www.computerhistory.org/timeline/computers/)
2. [Computer History Museum — The Silicon Engine: Semiconductor Timeline](https://www.computerhistory.org/siliconengine/timeline/)
3. [Computer History Museum — Semiconductor Resources](https://www.computerhistory.org/siliconengine/resources/)
4. [Harvard CS50 — How Computers Work (PDF)](https://cs50.harvard.edu/ap/2025/curriculum/technology/references/how_computers_work.pdf)
5. [CBSE Academic — Computer System Fundamentals (PDF)](https://cbseacademic.nic.in/web_material/Curriculum23/publication/847_Electronics_Hardware_XI.pdf)

**Study rule:** Consider this chapter understood when you can explain the difference between a CPU, RAM, storage, GPU, network card, server, VM and container in your own words—and collect a hardware inventory from your computer.
