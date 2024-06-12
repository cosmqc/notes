Quadrature is a way of determining distance and direction of rotation using two sine waves that are out of phase of each other by 90 degrees and a slotted disc.

![](/images/Pasted%20image%2020240612130448.png)

Distance/speed can be measured by the frequency of the wave, and direction can be measured by seeing which wave is leading the other. 

![](images/Pasted%20image%2020240612130614.png)

The states of the quadrature can be modeled with a finite state machine.
In the below diagram, we cannot move to states on opposite sides of the diagram (in normal operation) because the signals are 90deg out of phase; both signals can't change at the same time. This assumes we are polling with high enough resolution that each state is captured.

![](images/Pasted%20image%2020240612131510.png)