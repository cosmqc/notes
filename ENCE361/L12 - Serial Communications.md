Serial communications is the process of sending/receiving bits over a write one-at-a-time.
Tx buffer used by a transmitter, and a Rx buffer used by a receiver. If a device is both a transmitter and receiver, it has both buffers. Usually sent using packets.
### Simplex
- One way communication (unidirectional)
	- One device acts as transmitter, and the other as a receiver.

![](/images/Pasted%20image%2020240612112202.png)
### Full Duplex
- Two way communication (bidirectional)
	- Both devices act as transmitters and receivers
- Tx and Rx happening simultaneously

![](images/Pasted%20image%2020240612112502.png)

### Half Duplex
- Two way communication (bidirectional)
	- Both devices act as transmitters and receivers
- Either transmitting **or** receiving at one time
- Data rate is halved compared to full duplex
- Uses time-divison multiplexing to coordinate who is transmitting/receiving

![](images/Pasted%20image%2020240612112653.png)

## Packet structure
![](/images/Pasted%20image%2020240612113103.png)
- When no data is being sent, the line is idle at HIGH.
- Baud rate measured in bits per second
- Start bit (0)
- Data (LSB first usually, I2C uses MSB first)
- [[#Parity bit]]
- Stop bit (1)

### Parity bit
A parity bit is an extra bit added, usually immediately after the data section of the packet.
It's optional, but is a simple and relatively effective way of detecting errors in transmission.
There is even and odd parity. If you sum the data section and the parity bit, the resulting number should be even or odd (depending on the parity type, even parity -> even sum).
If the resulting number doesn't match the parity type, then at least one bit has been flipped.
A single parity bit can only detect one bit error, but doesn't know where it is.

