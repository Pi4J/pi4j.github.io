---
title: "x86 vs ARM vs RISC-V"
weight: 10
---

This is an overview of the different processor types used in computers, so also in Single Board Computers (SBCs).

## ARM: Efficient by Design

[Arm Holdings plc](https://en.wikipedia.org/wiki/Arm_Holdings) (originally "Acorn RISC Machine", later "Advanced RISC Machines") is a British semiconductor and software design company. There primary business is the design of central processing unit (CPU) cores that implement the ARM architecture family of instruction sets. They don't manufacture the chips, but design the architecture and license it to others. This means that an application written for a [Qualcomm Snapdragon](https://en.wikipedia.org/wiki/Qualcomm_Snapdragon) processor should also work on a [Samsung Exynos](https://en.wikipedia.org/wiki/Exynos) or [Apple's M-series](https://en.wikipedia.org/wiki/Apple_M1) chip because they speak the same "ARM language". 

The ARM-standardization has resulted in billions of ARM chips shipped every year, countless apps optimized for ARM, and a development community that spans the globe. The same efficiency principles that make ARM perfect for smartphones are exactly what make it ideal for single board computers like the Raspberry Pi. Both need to do a lot with limited power.

The [ARM architecture](https://en.wikipedia.org/wiki/ARM_architecture_family) uses a [RISC (Reduced Instruction Set Computer)](https://en.wikipedia.org/wiki/Reduced_instruction_set_computer) with a focus on power efficiency. The instruction set is relatively simple, with most instructions executing in a single clock cycle. ARM processors typically feature:

- **Power consumption**: 1-15W for typical SBC implementations
- **Instruction set**: 32-bit in ARMv1-ARMv7, mixed 32/64-bit in ARMv8, 64-bit in ARMv9
- **Licensing model**: Arm Holdings is the owner and it's primary business is selling licenses to manufacturers like Broadcom, Qualcomm, Apple,...

### ARM on Mobile Devices

If you're reading this on a smartphone, there's a 99% chance you're holding an ARM-powered device right now. ARM has achieved almost total dominance in the mobile market. Every major manufacturer uses ARM architecture for their mobile chips. 

The reason? Power efficiency! The RISC architecture in an ARM processor, allows smartphones to deliver impressive performance with low power consumption, making sure your battery lasts a day... 

### ARM on Raspberry Pi

The most popular SBC is the Raspberry Pi, and it uses an ARM processor, which is integrated in the System-On-Chip (SOC) combining CPU, GPU, memory controller, USB controller, etc. For instance:

* [Raspberry Pi 1](https://api.pi4j.com/board-information/MODEL_1_A): BCM2835 SOC with 1x ARM1176JZF-S @ 700Mhz ARMv6
* [Raspberry Pi Zero 2](https://api.pi4j.com/board-information/ZERO_V2): BCM2710A1 SOC with 4x Cortex-A53 @ 1000Mhz ARMv8
* [Raspberry Pi 4](https://api.pi4j.com/board-information/MODEL_4_B): BCM2711 SOC with 4x Cortex-A72 @ 1800Mhz ARMv8
* [Raspberry Pi 5](https://api.pi4j.com/board-information/MODEL_5_B): BCM2712 SOC with 4x Cortex-A76 @ 2400Mhz ARMv8

As you can see, throughout the history of Raspberry Pi boards, newer ARM versions have been introduced with more cores and higher speeds. With the change from ARMv6 to ARMv8, it also became possible to switch to a 64-bit operating system.

### ARM on Cloud Computing

ARM can also be found in the cloud! AWS uses it for their [Graviton Processors](https://aws.amazon.com/ec2/graviton/) that are ARM-based chips specifically designed for cloud workloads, and they're delivering impressive results:

* Up to 40% better price-performance compared to x86 instances.
* Using up to 60% less energy.

Many AWS customers use Graviton to run everything from application servers and microservices to databases and high-performance computing workloads.

### ARM in the Apple M-Series

Perhaps the most impressive proof that ARM can compete with x86 at the high-end came in 2020 when Apple announced its M1 chip. It's an ARM-based processor for Mac computers. At that time, it was a huge gamble, as they ditched Intel processors that had powered Macs for over 10 years in favor of their own ARM-based silicon. 

But the results were revolutionary! The M1 delivered performance that matched or exceeded Intel chips while using a fraction of the power. [An M1 Mac Mini draws just 39 watts at maximum load compared to 122 watts for the 2018 Intel-based Mac Mini with a 6-core Core i7](https://en.wikipedia.org/wiki/Apple_M1#Performance_and_efficiency). The secret is Apple's System-on-Chip design with Unified Memory Architecture, where the CPU, GPU, Neural Engine, and memory all share the same memory pool on a single chip. This tight integration, combined with ARM's efficient instruction set, allows the M-series to deliver desktop-class performance in fanless laptops. 

Each time I need to use a Windows laptop, I'm overwhelmed by the fan noise and the heat coming out of it. My M1 MacBook Air, in contrast, seems to have no fan at all and is completely silent, even when compiling code or running multiple Java applications. This isn't just about comfort but is proof of ARM's power efficiency. 

Apple's success with M-series chips has proven that ARM isn't just for mobile and embedded. It can go head-to-head with traditional desktop processors, and often wins on both performance and efficiency.

### Java on ARM

What I love about ARM for Java development is the mature ecosystem. The JVM has been heavily optimized for ARM, and the Pi4J library (designed for the Raspberry Pi) works seamlessly because the hardware support is rock-solid.

The entire Java ecosystem (OpenJDK, popular frameworks, and build tools) works seamlessly on ARM instances, including Apple's M-series and AWS Graviton. This means the same ARM-optimized Java code you're running on your Raspberry Pi could theoretically scale all the way up to massive cloud deployments on AWS Graviton. The architecture that powers your 20-euro Raspberry Pi Zero 2 is the same one handling enterprise-scale workloads in data centers. That's the beauty of ARM's versatility. It ranges from microcontrollers, to smart phones, to embedded systems, to cloud infrastructure, all with consistent tooling and development practices.

## x86: Running the Same Code Since 1985

The x86 architecture of [Intel](https://en.wikipedia.org/wiki/Intel) (x86-64/AMD64 for modern systems) takes a different approach. It's a [CISC (Complex Instruction Set Computer)](https://en.wikipedia.org/wiki/Complex_instruction_set_computer) architecture with a rich, complex instruction set that's evolved over decades.

Key characteristics:

- **Power consumption**: 10-65W for SBC-class processors (like the Atom or Celeron series)
- **Instruction set**: 32-bit and 64-bit
- **Compatibility**: Can run decades-old x86 software without modification

Intel-based SBCs like the LattePanda IOTA offer complete x86 compatibility. If you need to run legacy Windows applications or x86-specific software, Intel is your only choice. However, you pay for this with higher power consumption and heat generation.

For Java developers, Intel means maximum compatibility with desktop tooling and slightly better performance in some JVM workloads due to decades of JIT optimization for x86.

### Decades of Desktop, Laptop, and Server Dominance

For most computing history, Intel's x86 architecture has been synonymous with personal computers. From the 1990s through the 2010s, if you were using a desktop, laptop, or server, you were almost certainly running on Intel silicon. At its peak, Intel controlled over 99% of the server market and dominated desktop and laptop sales with an overwhelming market share. The x86 architecture became the standard not just because of Intel's engineering prowess, but because of decades of backward compatibility. Newer x86 processors could run programs written for processors from the 1980s. This created an enormous software ecosystem where every application, every operating system, every driver was optimized for x86. 

When [Apple switched from PowerPC to Intel in 2006](https://en.wikipedia.org/wiki/Mac_transition_to_Intel_processors), it was validation that x86 was the only serious choice for high-performance computing (at that time). Intel's dominance extended into data centers and cloud computing, where their Xeon processors powered the infrastructure behind almost every major web service. 

### AMD versus Intel: Two Implementations of x86

While Intel dominated x86 for decades, [Advanced Micro Devices, Inc. (AMD)](https://en.wikipedia.org/wiki/AMD) has been its primary competitor since the 1980s. The interesting story here is that both companies make x86 processors, but through different licensing arrangements. In the early 1980s, [IBM required Intel to license x86 to a second manufacturer (AMD) to avoid single-supplier risk](https://en.wikipedia.org/wiki/AMD#Intel_partnership). Since then, both companies have independently designed their own processor architectures that implement the x86 instruction set. This means a program compiled for x86 will run on both Intel and AMD processor, they speak the same language. 

However, the internal designs differ significantly. AMD innovated by creating the x86-64 (AMD64) instruction set in 2003, extending x86 to 64-bit computing while maintaining backward compatibility with 32-bit software. Intel's attempt at 64-bit ([Itanium/IA-64](https://en.wikipedia.org/wiki/Itanium)) failed in the market, so Intel ended up licensing AMD's 64-bit extensions, which means, today, both companies' processors use AMD's 64-bit architecture underneath! The competition between them has been hard... AMD's recent [Ryzen](https://en.wikipedia.org/wiki/Ryzen) processors have challenged Intel's market dominance, particularly in desktop and server markets where AMD has gained significant ground. For developers and users, the practical differences come down to performance per watt, core counts, cache sizes, and pricing rather than fundamental compatibility. Your Java code will run on either.

### Intel's Attempt at the Small Form Factor: NUC and x86 SBCs

Intel didn't ignore the small form factor market. With the [NUC (Next Unit of Computing)](https://en.wikipedia.org/wiki/Next_Unit_of_Computing) line launched in the early 2010s, Intel attempted to bring x86 architecture into the compact computing space. NUCs were 4x4 inch mini PCs powered by Intel processors, offering desktop-class performance in a palm-sized package. Intel also produced x86-based single board computers for industrial and embedded applications. However, these Intel-based SBCs faced fundamental challenges compared to ARM competitors like the Raspberry Pi, with power consumption being the critical issue. An Intel NUC typically draws 10-20 watts under load compared to just 2-4 watts for a Raspberry Pi 4. 

Intel boards require active cooling with fans, adding noise and complexity. Price was another barrier: NUCs started around $200-300 (often without RAM or storage), while a complete Raspberry Pi setup cost under $100. Most importantly, Intel's x86 SBCs lacked the GPIO pins and hardware interfacing capabilities that made ARM boards so popular for electronics projects and IoT applications. 

In 2023, Intel discontinued the NUC line entirely. But many other companies are still building x86 SBCs for small factor desktop systems, [Network-Attached Storage (NAS)](https://en.wikipedia.org/wiki/Network-attached_storage), and [Internet of Things (IoT)](https://en.wikipedia.org/wiki/Internet_of_things) devices. And some of these do provide GPIO's (like the [LattePanda IOTA](https://webtechie.be/post/2025-11-25-first-test-lattepanda-iota-with-ubuntu-and-java/)). 

## RISC-V: Open Source Goes Hardware

[RISC-V](https://en.wikipedia.org/wiki/RISC-V) (pronounced "risk five") is the new kid on the block, and it's shaking things up. Unlike ARM and Intel, RISC-V is an open standard, and anyone can implement it without licensing fees. Features of the ARM architecture:

- **Power consumption**: Varies wildly (1-20W depending on implementation).
- **Instruction set**: Modular base instruction set with optional extensions.
- **Licensing model**: Open standard, free to implement.

RISC-V boards like the [StarFive VisionFive 2](https://www.starfivetech.com/en/site/boards), [OrangePi RV2](http://www.orangepi.org/html/hardWare/computerAndMicrocontrollers/details/Orange-Pi-RV2.html), or [BeagleV](https://www.beagleboard.org/beaglev) are becoming more common, but the ecosystem is still maturing. 

The big advantage of RISC-V? Complete transparency and customization potential at lower cost.

### Java on RISC-V

As I mentioned at the start, one of my goals for 2025 is to dive deeper into Java on RISC-V. This is where things get really exciting, but also really experimental...

The good news is that Java officially supports RISC-V with the [OpenJDK RISC-V Port Project](https://wiki.openjdk.org/spaces/RISCVPort/overview) and the [sources on GitHub > openjdk > riscv-port](https://github.com/openjdk/riscv-port). Today, you can run Java on RISC-V hardware with:

- **Full JVM support**: The port includes the Interpreter, C1 (client compiler), and C2 (server compiler)
- **All garbage collectors**: Epsilon, Serial, Parallel, G1, ZGC, and Shenandoah all work
- **Complete tooling**: JVMTI, Java Flight Recorder, and other serviceability features
- **Desktop support**: Even AWT and Swing should work

The port targets the RV64G configuration (64-bit RISC-V with the standard general-purpose extensions), and there's experimental support for vector operations (RVV) and compressed instructions (RVC). Builds for Ubuntu of Java 17, 21, and 25 are available from [Adoptium](https://adoptium.net/supported-platforms).

I was not able to test this myself yet, but as you can see on the pictures at the beginning of this post, they are waiting right beside me to be powered on... :-)

### Performance and Ecosystem Maturity

But let's be honest, as far as I understand, RISC-V is not yet competitive with ARM in terms of performance. The current RISC-V boards like the StarFive VisionFive 2 are significantly slower than equivalent ARM boards. We're talking 2-3x slower than a Raspberry Pi 4 running at the same clock speed. 

As RISC-V is a community project, things evolve slower compared to Intel, AMD, ARM,...

**Hardware limitations**: Current RISC-V cores run at lower clock speeds. The hardware simply isn't as optimized yet.

**Software ecosystem**: While the JVM port is complete and functional, it lacks the years of optimization that the x86 and ARM port has received. There are fewer intrinsics (hand-optimized assembly routines) for common operations like cryptography, string manipulation, and mathematical functions. This means the JIT compiler can't take full advantage of RISC-V-specific instructions yet.

**Compiler maturity**: GCC and LLVM support for RISC-V is improving rapidly, but they don't generate code that's as optimized as what they produce for ARM or x86. This affects both native code and the performance of the JVM itself.

### Why Java and RISC-V Are a Perfect Match (In Theory)

Despite the current performance gap, there are reasons why Java and RISC-V make sense together:

**Both are open**: Java is open-source through OpenJDK, and RISC-V is an open [Instruction Set Architecture (ISA)](https://en.wikipedia.org/wiki/Instruction_set_architecture). No licensing fees, no vendor lock-in, complete transparency. For projects where you want full control over both hardware and software, this is incredibly powerful.

**Platform independence**: Java's "write once, run anywhere" philosophy aligns perfectly with RISC-V's goal of providing a standard, open instruction set. Your Java application doesn't care whether it's running on ARM, x86, or RISC-V.

**Embedded focus**: Both Java and RISC-V are targeting the embedded and IoT space. As RISC-V boards become more common in industrial applications, having mature Java support will be crucial.

**Community-driven**: Both ecosystems thrive on community contributions and collaboration. The work being done to optimize Java for RISC-V benefits everyone, and all improvements go upstream to OpenJDK.

## Java Development Considerations

As a Java developer working with embedded systems, here's what matters:

* ARM
  * Excellent JVM support (Many distributors, like [Azul](https://www.azul.com/downloads/?architecture=arm-64-bit&package=jdk#zulu), provide ARM builds)
  * Pi4J and native libraries are mature and well-tested
  * Best power consumption for long-running Java applications
  * GPIO and peripheral access is standardized (at least on Raspberry Pi)
* x86
  - Maximum JVM compatibility, every Java feature works
  - Better performance for computationally intensive tasks
  - Higher power consumption means active cooling often required
* RISC-V
  * OpenJDK support is improving but still experimental
  * Not sure yet if Pi4J works on RISC-V
  * Great for contributing to open-source JVM development
  * Exciting to experiment with new hardware platforms
