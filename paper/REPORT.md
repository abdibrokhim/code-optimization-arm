# Report: Code optimization for STM-32 f103/STM-32 F407 Discovery Time and Memory

## Literature review

Performance-oriented Programming
Mobile embedded processors prioritize energy efficiency, requiring more effort for high-performance code than desktop/server processors.
Embedded processors typically lack these features:
Execute instructions in program order, limiting parallelism.
Have simpler caches with fewer hierarchy levels and lower bandwidth.

ARM Technology
ARM stands for Advanced RISC Machine, based on the RISC (Reduced Instruction Set Computer) philosophy.
Data must be explicitly loaded into registers before processing and stored back to memory after.
ARM processors can be programmed using various high-level languages, with C being the focus for performance optimization.
Note: The STM32F103 microcontroller is based on the ARM architecture.

ASCON
ASCON is a family of lightweight cryptographic primitives designed for the Internet of Things (IoT) and embedded systems.


### Research focus & goals

Research focus areas:
Code Optimization for STM32 Microcontrollers. Specifically reducing execution time and minimizing memory usage.
Goals:
Improve performance by achieving significant reductions in execution time and decrease memory consumption.
Evaluate the effectiveness of different optimization strategies.
Identify performance bottlenecks and their solutions.
Study different algorithms and their performance to the given task.


## Methods

### STM32F4 – Code Optimization

We know that `embedded systems` usually have *limited computing/memory resources*. But we can always use various optimizations to *reduce space size* or *improve computing performance*. Here are some of the most common optimization techniques:

#### Memory Footprint Optimization

Build without enabled optimization

![Build without enabled optimization](/stuff/build-without-opt.png)

Build with enabled optimization

![Build with enabled optimization](/stuff/build-with-opt.png)

From the images above, we can see that the code size has been reduced from `(141,320 B)` to `(3,920 B)`.

#### Isolated Optimization

Here, one (or more) optimizations can be selected.

![Isolated Optimization](/stuff/isolated-opt.png)

![Benchmark Singleopt](/stuff/benchmark-singleopt.png)

The experimental results show the following:

* Size optimized library newlib achieves the best result reducing from `(O2: 137,732 B)`, `(O1: 141,248 B)`, `(NA: 141,320 B)`, `(O5: 141,320 B)`, `(O7: 141,320 B)`, `(O6: 141,344 B)` to approx `(O8: 28,028 B)`.
* There are many unused sections in the original, which are removed by the second best optimization `(O4)`.
* The space optimizations `(O3)` performs similarly good.
* Some overhead can be reduced by disabling exceptions (O2). The optimization effect is diminished by the fact, exception handling is not removed from the (already compiled) libraries.
* Minimal advantage is obtained by replacing new and delete with malloc and free `(O1)`.
* Other optimization `(O5, O7)` are ineffective in our test case, and perform as no optimization is used `(NA)`. `(O6)` performs even worse than `(NA)`.

#### Optimization Combinations

Here, multiple optimizations can be selected.

![Optimization Combinations](stuff/optimization-combinations.png)

The experimental results show the following optimization combination are the most effective:

* *O1 (mem. allocation)*, *O2 (exception handling)*, *O3 (size optimization)* reduce the code size from `141,320 B` to `13,060 B`.
* *O8 (size optimized library)* with *(O1, O2, O3)* reduce the code size to `8,616 B`.
* *O4 (remove unused code)* with *(O1, O2, O3, O8)* reduce the code size to `4,012 B`.
* *(O1-O8)* reduce the code size to `4,012 B`.
* **C++** exception handling is space consuming. The best optimization without *O2* is `11,700 B` *(see O1 O3 O4 O8)*.
* **C++** memory management without exception handling is relatively cheap. `(O2 O3 O4 O8)` reduce the code size to `4248 B`.

#### Identify space-wasting code

![Identify space-wasting code](/stuff/space-wasting-code.png)

The memory management (see top 3: _mallor_r, __malloc_av_, _free_r) consumes a huge amount of space relative to other part of the code.

We can simply use `(08)` to mitigate this issue.

![Optimization space-wasting code](/stuff/space-wasting-code-opt.png)

### ASCON



## Results

## Discussion

## Conclusion

## References