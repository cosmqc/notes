#ENCE361 
## Schedulers
### Round-robin
Also called *free-running cyclic* or *polling* scheduling
Pros:
- Simple to implement
- Same worst-case response for every task
Cons:
- Same worst-case response for every task (no prioritization)
- Tasks cannot be very long (if no task splitting)

```c
void main (void) {
	while (1) {
		if ( * I/O device A needs service /)
			// Handle data to/from Device A
		if ( * I/O device B needs service /)
			// Handle data to/from Device B
		...
		if ( * I/O device Z needs service /)
			// Handle data to/from Device Z
	}
}
```

### Time-triggered
Also called *time-division multiplexing* of MCU
Pros:
- Tasks performed at controlled times
- Limited task prioritisation
Cons:
- Worst-case response time depends on the run time of previously scheduled tasks
- Tasks cannot be very long (without time slicing)

```c
void timerInterruptHandler (void) {
	for (uint8_t i = 0; i < N_TASKS; i +) {
		if (scheduled_task[i].delay = 0) {
			scheduled_task[i].ready = true;
			scheduled_task[i].delay = scheduled_task[i].period; // reset task
		} else {
			scheduled_task[i].delay--;
		} 
	}
} 

void main (void) {
	while (true) {
		for (uint8_t i = 0; i < N_TASKS; i +) {
			if (scheduled_task[i].ready) {
				// Call task handler
				scheduled_task[i].ready = false;
			}
		}
	}
}
```

### Interrupt-triggered
Using the foreground/background model, can use either of the other two but will have interrupt-triggered tasks if they have higher priority

![[Pasted image 20240502132211.png]]

Pros:
- Fast response to asynchronous events
- Interrupts are prioritised
- Background tasks can be long
Cons:
- Worst-case response time depends on interrupt arrival rates
- Foreground tasks cannot be very long
	- Premption possible to split interrupt tasks into smaller chunks (interrupting other interrupts)

```c
volatile boolean flagDeviceA = false;
⋮
volatile boolean flagDeviceZ = false;

void deviceAIntHandler (void) {
	// Handle device A I/O, set flag
}
⋮
void deviceZIntHandler (void) {
	// Handle device Z I/O, set flag
} 

void main (void) {
	while (true) {
		if (flagDeviceA) // Handle data to or from Device A and reset flag
		⋮ 
		if (flagDeviceZ) // Handle data to or from Device Z and reset flag
	}
}
```

