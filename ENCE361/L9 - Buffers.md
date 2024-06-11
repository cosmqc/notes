#ENCE361 

Buffers is a region of physical memory (with continous addresses) for storing data temporarily. 
We need buffers:
- When data consumption is not in sync with data generation.
	- Temperature monitoring - regular readings buffered before transmission/processing
	- Online video playback - buffered for small amount so playback is continous
- Processing data in batches (batch-based/sliding-window processing)
	- Signal averaging buffers the most recent M samples, so does finite inpulse response (FIR) filtering.
	- Performing N-point discrete fourier transform (DFT) needs to buffer N samples

#### Sliding window processing
Processing batches in a continous fashion. i.e. samples coming in continously. Instead of waiting for each n inputs to come in before processing, it waits only once for n samples (samples \[0, n], then processes those. After the next input comes in, it processes samples \[1, n+1]. Then next input comes in, processes samples \[2, n+2].
This means we're processing a new batch on each new value's arrival, but our batch size is still n.

#### Shift register
Uses sliding window principle (FIFO). Shifts the first n-1 elements towards the end of the buffer and write the new sample to the beginning of the buffer. This works, but is very inefficient ( O(n) ) as you have to shift almost the entire buffer over. 
#### Circular buffer
Uses sliding window principle (FIFO) combined with a pointer pointing to the oldest sample. This means that we don't need to actually move all the data over in the buffer, we just overwrite the oldest value with the new datapoint, move the write index to the right, and wrap around when reading the buffer. This means we maintain the correct temporal order of all the samplings **without shifting them**.
![[Pasted image 20240307133428.png]]

**Data overrun** - When the write pointer managed to lap the read pointer, so data getting overwritten before ever being read.
### Key design considerations of buffers
- Data type
- Buffer size
- Write a data sample / a few data samples to buffer
- Read a data sample / a few data samples from buffer
- Memory allocation
	- Dynamic allocation vs static allocation - dynamic risky due to chance that we may overflow the heap, but more memory efficient  
	- On-chip memory vs external memory - external has v fast read speed but slow write speed.

```c
typedef struct { 
	uint32_t size; // Number of entries in buffer
	uint32_t *data; // Pointer to the starting address of the buffer
	uint32_t windex; // Index for writing (0 - size-1)
	uint32_t rindex; // Index for reading (0 - size-1)
} circBuf_t;

void writeCircBuf(circBuf_t *buffer, uint32_t entry)
{
	buffer->data[buffer->windex] = entry;
	buffer->windex++;
	if (buffer->windex >= buffer->size)
	{
		buffer->windex = 0;	
	}
}
```

#### Double Buffer
Provide protection to buffered contents under race conditions
Casecase two buffers with same size to form a large circular buffer

#### Calculate sampling frequency
sampling freqency should be >= 2 \* `w` \* `M`
`w` = maximum frequency of the input signal 
`M` = size of the sample buffer
`f_s >= 2w`
`f_s >= 2 * M * w`

Taking the mean over a larger buffer means the input signal is getting distorted.
This can be offset if the samples don't change very much between each of them, so sampling quicker decreases the level of distortion.