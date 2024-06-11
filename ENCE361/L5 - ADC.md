#ENCE361 
## Sampling
We are sampling the world via sight, sound etc. We can't always be sampling though due to limitations on our 'hardware' eg blinking, leading to a small amount of data being lost.
If we're sampling quickly enough though, the physical data doesn't have enough time to change so we can estimate what the values were when we were recovering. (i.e. blink is a very short amount of time, so unless something is happening extremely quickly we won't miss any data)
**Analogue** - 
**Digital** - 


Digital processing of analogue signals
- Analogue to digital converter (ADC)
- Digital signal processor (DSP)
- Digital to analogue converter (DAC)

low-frequency signal - signal is quite predictable, don't need to sample as much.
high-frequency signal - signal is erratic, need to sample more.
![[Pasted image 20240228121535.png]]

Continous signals - infinite
- continuous in time - can continue getting data via sampling
- continuous in amplitude - a problem, cannot get infinite amplitude with finite processor
- cannot be directly processed due to above reasons

sampling: time domain -> discrete time 
quantisation: amplitude -> table lookup

ADC takes an analogue domain and converts it to a digital domain via some conversion process.
![[Pasted image 20240228122425.png]]

Continuous -> anti-alias filter -> sampler with zero-order hold (ZOH) -> Quantiser -> Digital

Zero-order hold: Sets the signal at the last sample until another sample comes in.
First-order hold: waits until the next signal comes in, then generates a linear line between the two. More accurate but slight delay due to being one sample cycle behind. 
![[Pasted image 20240228123120.png]]
### Nyquist-Shannon Sampling Theorum
Continous to discrete time: uniform sampling
- How fast should we sample a continuous signal so it can be perfectly reconstructed from the discrete-time samples?
Modeling ideal sampling using a uniform unit impulse train.

![[Pasted image 20240228123903.png]]

![[Pasted image 20240228123917.png]]
![[Pasted image 20240228124138.png]]

Find `w` via oscilliscope fourier spectrum?
Anti-alias filter:
- keep all low frequency signals
- lower strength of mid frequency
- reject high frequency signals
Less high frequency signals -> more predictable, less aliasing
![[Pasted image 20240228124721.png]]

### Digital Signal Conditioning
Noise is everywhere; ie electronic/thermal noise within circuitry, nearby signals, sampling jitter. Need to condition the digital signal vi signal averaging.