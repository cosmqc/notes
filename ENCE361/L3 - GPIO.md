#ENCE361 

# GPIO
GPIO is a signal pin on a circuit / circuit board. It provides an I/O interface for the [MCU]().
It's able to be programmed for input or output, digital or analogue, serial comms etc.

[TIVA board]() provides up to 43 GPIO pins, the one we'll be using will have 40 pins.
- 4 in-line headers (J1 - J4), each having 10 pins
- Accessible via 7 ports (PA - PG)
	- ie 'PA1' -> PIN1 on PORTA
	- PORTE only has (PE0-PE5), PORTF only has (PF0-PE4)

![[images/Pasted image 20240222130714.png]]
![[images/Pasted image 20240222131124.png]]

## Initialization
GPIO ports, as system peripherals, need to be enabled before use to avoid crashing.
```c
GPIOPORTF->CFR = 0x02
# or the TIVA method
SysCtlPeripheralEnable(SYSCTL_PERIPH_GPIOF);
```
Some special pins have to be unlocked prior to being used.
![[images/Pasted image 20240222132845.png]]
```c
# Set GPIO pin as WPU or WPD
void GPIOPadConfigSet (ui32Port, ui8Pins, ui32Strength, ui32PinType);
# Set GPIO pin as input or output
void GPIODirModeSet (ui32Port, ui8Pins, ui32PinIO);
void GPIOPinTypeGPIOInput (ui32Port, ui8Pins);
void GPIOPinTypeGPIOOutput (ui32Port, ui8Pins)
```
## Access
```c
# GPIO Read and Write
int32_t GPIOPinRead (ui32Port, ui8Pins)
void GPIOPinWrite (ui32Port, ui8Pins, ui8Val)
```

Example access:
```c
# Enable the associated ports
SysCtlPeripheralEnable(SYSCTL_PERIPH_GPIOF)

# Configure the GPIO ports
GPIOPadConfigSet (ui32Port, ui8Pins, ui32Strength, ui32PinType) // WPU/WPD eg
GPIOPinTypeGPIOInput (ui32Port, ui8Pins) // Input eg
GPIOPinTypeGPIOOutput (ui32Port, ui8Pins) // Output eg

# Data access
GPIOPinRead (ui32Port, ui8Pins) // Input eg
GPIOPinWrite (ui32Port, ui8Pins, ui8Val) // Output eg
```

# Output LEDs and Input Switches
[TIVA board]() has 3 LEDs (red, green, blue), and 2 buttons (SW1, SW2).
All of these are on PORT F.
![[images/Pasted image 20240222131509.png]]

## LEDs
All active HIGH. Transistors are used as switches, so voltage to the base must be above 0.7V to allow current flow.
![[images/Pasted image 20240222131912.png]]

## Switches
On their own, they don't have debouncing circuitry.

> **Debouncing**
> Due to human error, slight variations in pressure when you push the button can result in multiple pushes. 'Debouncing' is the process of remove those extra unwanted pushes.

# Programmable Control
- Weak pull-up (WPU) for reading button push
- Weak pull-down (WPD) for driving LEDs


# Example Program
```c
#define RED_LED GPIO_PIN_1
#define BLUE_LED GPIO_PIN_2
#define GREEN_LED GPIO_PIN_3
int main(void) { 
	uint32_t clock_rate;
	// Set up the system clock rate to 20 MHz
	SysCtlClockSet(
		SYSCTL_USE_PLL | 
		SYSCTL_OSC_MAIN | 
		SYSCTL_XTAL_16MHZ | 
		SYSCTL_SYSDIV_10
	);
	// Allow oscillator to settle down
	SysCtlDelay(100); 
	// Clock rate in pulses/s
	clock_rate = SysCtlClockGet();
	SysCtlPeripheralEnable(SYSCTL_PERIPH_GPIOF); // Enable Port F
	GPIOPadConfigSet(GPIO_PORTF_BASE, GREEN_LED, GPIO_STRENGTH_4MA, GPIO_PIN_TYPE_STD_WPD); // Configure PF3, 4mA, WPD
	
	GPIODirModeSet(GPIO_PORTF_BASE, GREEN_LED, GPIO_DIR_MODE_OUT); // Set PF3 as output
	
	// Write a zero to the output pin 3 on port F
	GPIOPinWrite(GPIO_PORTF_BASE, GREEN_LED, 0x00); // Turn off Green LED
	// Enter a gadfly loop (kernel) to make the LED blink
	while (1)
	{ 
	// Delay (passing the argument value clock_rate /3 gives a delay of 1 sec)
		SysCtlDelay(clock_rate /12); // Turn on the LED
		GPIOPinWrite(GPIO_PORTF_BASE, GREEN_LED, GREEN_LED); // Delay
		SysCtlDelay(clock_rate /12); // Turn off the LED
		GPIOPinWrite(GPIO_PORTF_BASE, GREEN_LED, 0x00); 
	} 
}

```

Period is the sum of the two delays.
Duty cycle is the ratio of the two delays