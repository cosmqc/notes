#ENCE361 

Pulse width modulation (PWM) is carrying information via changing the pulse width of a periodic square wave. The square wave is generated with a programmable digital timer.
We don't use the voltage as the information carrier as it's too susceptible to noise.
![[Pasted image 20240227121010.png]]

i.e. encode steering wheel position
- Left turn: *reduced* pulse width
- Center: average pulse width (1/2 pulse period)
- Right turn: *increased* pulse width
![[Pasted image 20240227121032.png]]

### Motor control
Uses PIC16F690 - an MCU. H-bridge allows clockwise or anticlockwise rotation of the motor. Motor speed controlled by average voltage - dependant on duty cycle. 
If we don't switch them in pairs, the current will shoot down only one side of the H bridge, not through the motor, meaning there will be a massive current applied to the board :(
#### Clockwise
![[Pasted image 20240227122250.png]]

#### Anti-clockwise
![[Pasted image 20240227122359.png]]

### Generate PWM on TIVA
Tiva C-series Launchpad has 2 PWM modules, M0 and M1.
Each module consists of 4 PWM generators (0, 1, 2, 3) and a control block
- Each generator produces 2 PWM signals
- 8 PWM signals from a module are called PWM0 - PWM7
Control block determines:
- Mode of operation
- Which pins PWM signals are passed to
![[Pasted image 20240227122838.png]]

![[Pasted image 20240227122905.png]]

If we change the threshold on the comparator, we adjust the duty cycle.

Maximum period purely using the microprocessor clock is very small, ~2ms.
To increase this, we can either increase the number of bits of the clock (not ideal), or add a **prescaler**.

Each PWM generator only has 1 PWM clock. The clock is dervied from the microprocessor clock via a prescaler: `/2`, `/4`, `/8`, `/16`, `/32`, `/64`.

Produce 2 PWM signals with the same period
-  2 PWN signals can have different duty cycles
- 2 PWM signals can be complementary with dead-band delay inserted
	- Allows time for the switch to open/close before switching the other switch. Again, prevents short circuit
![[Pasted image 20240227123915.png]]




