**How do we evaluate the performance of a foreground/background model design quantitatively?**

## Interrupt latency
Interrupt latency is the time between the interrupt event and the start of the activity related to servicing it (the context switch usually). This excludes the context switching time.

T_latency = max(T_disabled, T_instr)
T_disabled -> the longest period the interrupts are disabled for (i.e. critical section, other interrupts)
T_instr -> longest execution time for any instruction 
## Interrupt response
Interrupt response is the time between the interrupt event and the start of the code that responds to it (the ISR response). This includes the context switching time. Interrupt response is equivalent to the sum of the interrupt latency and the context switching time.

T_response = max(T_disabled, T_instr) + T_csw
T_csw = context switching time (part of it may be in the ISR prologue)
## Interrupt recovery
Interrupt recovery is the time for the microprocessor to return to the code that got interrupted at the end of the interrupt.

## Tail chaining
When chaining ISRs, the context of the foreground will not change, so it is inefficient 