Switch bouncing is where (due to human error) a pushed button flickers between high and low for a short time before settling high (on push down) or settling low (on release).

![](/images/Pasted%20image%2020240612093626.png)

This makes it hard to figure out how many times the button was actually pressed, and especially when using something like interrupts that trigger on a rising/falling edge.

**Debouncing** is the act of processing the switch signal so one press is not registered as multiple presses
# Hardware debouncing
Debouncing can be done in hardware. It reduced the software processing needed, but components are expensive (compared to a few lines of software).
## Double throw switches - SR flip-flop
It's likely that a switch will bounce on/off one contact multiple times, but bouncing between contacts is extremely unlikely. A **SR flip-flop** is effectively a pair of NAND gates feeding back into each other, meaning the switch will have to touch the opposite contact for the logical state to change, removing a lot of bouncing.
![](/images/Pasted%20image%2020240612095929.png)
## Single throw switches - RC circuit
### Schmitt trigger
A Schmitt trigger uses two thresholds to try and reduce uncertainty. It will output high if the inputted voltage is above its upper threshold (**H**), and continue to output high until it drops below its lower threshold (**L**) (and vice versa). If in middle zone, logical output is whatever threshold it crossed most recently. 
![](/images/Pasted%20image%2020240612100636.png)

A RC circuit-based approach to debouncing uses a resistor and capacitor with a Schmitt trigger to force the switch to be in a state for a set amount of time before registering HIGH.
When the switch is open, the capacitor will charge up. When the switch is closed, the capacitor will have to discharge to a certain level before the voltage level crosses the trigger's threshold.

![](/images/Pasted%20image%2020240612101655.png)

# Software debouncing
The TIVA boards we're using in ENCE361 don't have any hardware debouncing, so software debouncing is essential. The general idea is that the voltage settles on a value after the bouncing has finished, so keep polling until there are consecutive readings that are the same. This means that the value we've read is **reliable**.

We can't use pin-change interrupts as there would be too many voltage changes while it's bouncing, leading to too many interrupts being triggered and the MCU getting overloaded.
The alternative is polling using timers, which is still interrupt-based but leaves room for other tasks to execute in the gaps between polls.

```bash
# General idea of the algorithm; psuedocode
consecutive_count = 0;
while true:
	if (pin_state and current_state are different):
		consecutive_count++;
		if (consecutive_count is over needed count):
			break;
	else:
		consecutive_count = 0;
```

![](images/Pasted%20image%2020240612103711.png)

Best practice to make N1 small so user inputs seem rapid, and to make N2 large to avoid false detections. 

