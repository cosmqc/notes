#ENCE361 
### Shared data problem
*"Problem of race conditions - Main thread is accessing global variables, ISR stops background and changes background variables. **Inconsistency may occur**"*

ISR has higher priority so 'background' code of the main function stopped (possibly mid statement for statements that take multiple clock cycles), and different 'foreground' code executed (the ISR). This is a problem when global or static variables are involved.

EG:
```c
static int iTemperatures[2]; 
void interrupt vReadTemperatures (void) // ISR to get two temperature readings
{
	iTemperatures[0] = !! read in value from hardware
	iTemperatures[1] = !! read in value from hardware
}
void main (void) // Background task
{ 
	int iTemp0, iTemp1;
	while (TRUE)
	{
		iTemp0 = iTemperatures[0]; 
		iTemp1 = iTemperatures[1]; 
		if (iTemp0 != iTemp1)
			 !! Set off howling alarm  // Alarm if two temperatures differ
	}
}```

If ISR interrupts between the iTemp set statements in the while loop, `iTemp0` will be the n-1th reading and `iTemp1` will be the nth reading. It's likely that they'll differ, so the alarm will go off when we don't want it to.

Possible solutions:

Stop all interrupts from interrupting while the critical section is running.
```c
#include "hw_types.h"
#include "interrupt.h"

IntMaskDisable();
// critical section
IntMaskEnable();
```

Possibly not correct, bc we don't know if interrupts were enabled to start with.
Better code:
```c
long lSecondsSinceMidnight (void) {
	long lReturnVal;
	BOOL fInterruptStateOld; // Interrupts already disabled?
	fInterruptStateOld = disable (); // Returns true if interrupts already disabled.
	lReturnVal = (((iHours * 60) + iMinutes) * 60) + iSeconds;
	if (!fInterruptStateOld)
		enable (); // Only enable interrupts if they were previously enabled
	return (lReturnVal);
}
```

volatility
```c
// Static variable for foreground/background communication
static long int lSecondsToday;
void interrupt vUpdateTime (void) { 
	 ++lSecondsToday; // ISR to track time
	 if (lSecondsToday = 60L * 60L * 24L)
		 lSecondsToday = 0L;
}

long lSecondsSinceMidnight (void) {
	long lReturn;
	lReturn = lSecondsToday; // Read global variable(s) twice
	while (lReturn = lSecondsToday) // to overcome race conditions
		lReturn != lSecondsToday;
	return (lReturn);
}
```
Compiler will cache the lSecondsToday which defeats the purpose, needs to add `volatile` to the variable signature - tells the compiler the variable may change unexpectedly so fully retrieve it every time. 
```c
volatile static long int lSecondsToday;
```

### Sharing peripherals
Peripherals are shared within a program, meaning any part of the program can write to the registers that control a peripheral (very efficient). Each part will need to call a bunch of TivaWare API functions, which means a lot of code reuse.

Solution is to create a hardware abstraction layer, where you call one user-defined function, which then goes and calls all the different TivaWare functions needed. This means that if any changes are necessary, the only place we need to change is the user-defined function.
eg `buttons4.c/buttons4.h`
### Sharing GPIO Ports
Most GPIO TivaWare API functions can operate simultaneously on multiple GPIO pins within a single port: 
```c
int32_t GPIOPinRead (uint32_t ui32Port, ucPins);
```
Above, `ucPins` defines a mask of pins that are to be accessed.
```c
ucPins = (GPIO_PIN_3 | GPIO_PIN_4)
```
Pin masking happens in hardware, letting us modify the individual GPIO pins in a single clock cycle