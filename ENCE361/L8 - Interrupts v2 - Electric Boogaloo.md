#ENCE361 

An **interrupt** is a (mostly peripheral) events requiring attention of the MCU
- Microcontroller stops to run interrupt service routine (ISR) / interrupt handler
- Microcontroller returns to next code prior to interrupt
- More efficient tham polling for handling async events 


![[Pasted image 20240306120836.png]]
Main program has lowest priority, ISR_C has higher priority than ISR_A. A stops execution of main program to execute as it has higher priority, C stops execution of A as it has higher priority. If an interrupt happens **with the same priority** as the currently running one, it is just queued to run after the current one.


### ISR coding basics

#### ISR as a Function
At interrupt, microcontroller stops to run ISR from a new address
- Similar to a 'normal' function call in C program in terms of branching
- We should code ISR as a C function

'Normal' function vs ISR
- Normal function call is user planned (programmed)
- Interrupt (peripheral event) is async
	- Occurence time is **unpredictable**

```c
void ISR_name(void) {
	// Body of the ISR
}

unit32_t main(void) {
	uint32_t x, y, result;
	// Run while waiting for interrupt
	while (1)
	{
	}
}
```

ISR guidelines:
- ISR should not be called explicitly anywhere
- Should only do what is needed at the time of event
- Avoid delay loops
- Avoid floating point operations (requires massive amount more computation)
- Avoid operations that may halt or hang the system

### Inter-thread Communication
Through global memory
- Global variables are defined outside of all functions
	- Data
```c
int32_t chocolateCnt = 20;

void ChocolateIntHandler(void)
{
	chocolateCnt--;
}

uint32_t main(void)
{
	while (1)
	{
		if (chocolateCnt == 0)
		{
			// Display sold out info
		}
	}
}
```

-  ​Binary flag
```c
uint16_t flag = 0;

void ISR_name(void)
{
	flag = 1; // Set the flag
}

uint32_t main(void)
{
	while (1)
	{
		if (flag == 1)
		{
			flag = 0; // Clear the flag
			// Perform operations
		}
	}
}
```
- Mailbox (binary flag + data)
```c
uint32_t flag = 0, data;

void ISR_name(void)
{
	flag = 1; // Set the flag
	data = GetData(); // Read data
}

uint32_t main(void)
{
	while (1)
	{
		if (flag == 1)
		{
			flag = 0; // Clear the flag
			ProcessData(data);
		}
	}
}
```
- Circular buffer

#### Shared data-based communication
Problem of race conditions - Main thread is accessing global variables, ISR stops background and changes background variables. **Inconsistency may occur**
```c
uint32_t main(void)
{
	while(1)
	{
		line 1;
		line 2; // ISR could happen between line 2/3
		line 3;
		line 4;
		line 5; // ISR could happen between line 5/6
		line 6;
	}
}
```
If line / set of lines need to be undisturbed while executing, diable interupt before and reenable after.