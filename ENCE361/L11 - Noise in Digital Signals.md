#ENCE361 

Noise is any signal we don't want in our digital signal.
Classified into two categories:
#### Random noise
- Stochastic
- i.e. Quantization error, sampling jitter, thermal noise in electronics, external interference
#### Systematic error
- Deterministic
- **Can be calibrated** (generally)
- i.e. Measurement offset, non-linear response

### Quantization error
Generated from quantization - converting infinite analogue possibilities to a deterministic digital signal.

### Sampling jitter
Sampling jitter makes sampling interval no longer uniform, resulting in sampling amplitude uncertainty.

maximum error magnitude = `2(pi)fA(dt)`

### Johnson noise
Due to random thermal motion of charge particles (usually electrons)
A resistor of resistance R generates thermal noise with a RMS voltage
`v_n = sqrt(4kTBR)`
k = Boltzmann's constant = `1.38 x 10^-23 J / degK`

### Interference
3 sources of interference that can be present simultaneously
- Conductive coupling
	- Noise current caused by a changing voltage in a nearby circuit
	- Cross-talk between closely space circuits
- Inductive coupling
	- Noise voltage caused by a changing current in a nearby circuit
- Resistive coupling
	- Occures when high-level signals share a wire with low level signals
	- Used when driving the motors, microcontroller on 3.3V, motors on ~12V

### Signal-to-noise ratio (SNR)
- Expressed in decibel (dB)
- `Blog(1 + SNR)`
- i.e. at very loud party, talking to friend has a low signal to noise ratio, so sometimes will have to repeat what you've said due to noise.
- Definition1: SNR = 10log(avg_signal_power / avg_noise_power)
- Definition2: SNR = 10log((signal_rms_voltage)^2 / (noise_rms_voltage)^2) 
				= 20log(signal_rms_voltage / noise_rms_voltage)
![[Pasted image 20240320123711.png]]

### How to choose sample buffer size (M)?


### Periodic Noise
Be careful when picking buffer size 