#ENCE361 

Control is the strategy we use to give the inputs to get the outputs we want.
![[Pasted image 20240430120944.png]]
^ Components of a control system

![[Pasted image 20240430120840.png]]
^ Helicopter example

### Open loop
- Uses a controller to directly control the process.
- Requires accurate knowledge of the plant
- Unreliable if the system experiences unexpected variations (i.e. noise)
- Shown in the images above, 
### Closed loop
Controller behaviour is adjusted based on input ("feedback") from a sensor, which monitors system output
![[Pasted image 20240430121112.png]]
e(t) = Error = desired response - system output

## Control Strategies
### Bang-bang control
control signal = c(t) = e(t) > 0 = error > 0 = is there error?

### Proportional control
c(t) = kp × e(t)
kp = proportional gain
Controller drives actuator in proportion to error signal.
![[Pasted image 20240430121631.png]]

![[Pasted image 20240430121810.png]]
As we increase kp, we get overshoot if the amplitude increases above its maximum value.
As we increase kp, we get ringing (purple and yellow), where there are local maxs and mins, but still settles on a final value
If too high, the ringing turns into oscillation where the function never settles on a final value.

Overshoot error is a percentage of the difference of the max value relative to the final value.
![[Pasted image 20240430122341.png]]

Steady-state error is where the final value never reaches the desired value (would require kp=infinity).
Steady state error = desired value - final value

![[Pasted image 20240430122701.png]]

### Integral Control
- Offset error is integrated so that c(t) increases to correct it
- Even if e(t) = 0, c(t) can still be non-zero!
- Integrating the error signal also reduces sensitivity to noise.
- The integral controller output, c(t) depends on the entire history of e(t).
- Still has overshoot and ringing

![[Pasted image 20240430122733.png]]
#### Issues
##### Output Saturation
- Control signal has no limit on its magnitude
- But actuator may not be able to 'follow' controller output, bc power or physical constraints
- So further demands from controller have no effect
- i.e. mobility scooter on motorway, no matter how fast you want it to go, not going 100k

##### Integral Windup
Can get very large if the system takes a while to react to inputs, leading to significant overshoot.
### Proportional-integral control
complete 
```c
// PI Code
const float Kp = …;
const float Ki = …;

float controller (float setpoint, float sensor_reading) {
	static float I = 0;
	float error = setpoint - sensor_reading; // Calculate error
	float P = Kp * error; // Proportional term
	float dI = Ki * error * delta_t;
	float control = P + I;
	
	// Check for saturation:
	if (control > OUTPUT_MAX)
		control = OUTPUT_MAX;
	else if (control < OUTPUT_MIN)
		control = OUTPUT_MIN;
	else
		I = (I + dI); // Only update if not saturated to prevent windup
	return control;
}

void main (void) {
	⋮ 
	mainDC = controller(alt_setpoint, alt_reading);
	setPWM(MAIN, mainDC);
}
```
### Proportional-integral-derivative control (PID ‼️‼️‼️‼️‼️‼️‼️)
complete
```c
const float Kp = …;
const float Ki = …;
const float Kd = …;

float controller (float setpoint, float sensor_reading) {
	static float I = 0;
	static float prev_error = 0;
	float error = setpoint - sensor_reading;
	float P = Kp * error; // Proportional term
	float dI = Ki * error * delta_t; // Integral term
	float D = Kd * (error - prev_error) / delta_t; // Derivative term
	float control = P + (I + dI) + D;
	// Check for saturation:
	if (control > OUTPUT_MAX)
		control = OUTPUT_MAX;
	else if (control < OUTPUT_MIN)
		control = OUTPUT_MIN;
	else
		I = (I + dI); // Only update if not saturated to prevent windup
	prev_error = error; // (for next time!)
	
	return control;
}
```


