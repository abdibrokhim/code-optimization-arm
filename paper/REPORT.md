[what should we do?]:
<info>
Let's do ASCON

This is quite new algorithm. It's already optimized for some systems, so, you can download good source code

Analyze it, with CubeMX you can upload the code to the device and measure memory consumption

I would like to have a More complicated system to implement. For example, reading sensors, reacting to them, sending encrypted data, receiving encrypted answer/request, decrypt it and execute the order

https://github.com/haskucy/ascon_implementation_C/blob/main/ascon.c 
( This code uses 64bit architecture. But STM32 is 32bit processor )

https://github.com/ascon/ascon-c/tree/f1601cb5ff52e65baa475fcc6959e7d6e0be8d77/src 
( Here you can find way more variety of implementations )
</info>


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
<about>
...
</about>


### Research focus & goals

Research focus areas:
Code Optimization for STM32 Microcontrollers. Specifically reducing execution time and minimizing memory usage.
Goals:
Improve performance by achieving significant reductions in execution time and decrease memory consumption.
Evaluate the effectiveness of different optimization strategies.
Identify performance bottlenecks and their solutions.
Study different algorithms and their performance to the given task.



## Methods

## Results

## Discussion

## Conclusion

## References