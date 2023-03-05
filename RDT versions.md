
Understanding Finite State Machine:

![[Pasted image 20220910220232.png]]

Overview of the rdt versions:

![[Pasted image 20220910220417.png]]

### RDT 1.0: Perfectly Reliable Channel

![[Pasted image 20220910220723.png]]

### RDT 2.0: Data Bit Error

Packages may have bit errors over unreliable network transfer → Use **checksum** and **ACK/NAK** 

It follows **Stop-and-wait** protocol: Sender sends one packet at at ime, then waits for receiver response

![[Pasted image 20220910221028.png||700]]

### RDT 2.1: ACK/NAK Bit Error

Fatal flaw of 2.0 is ACK and NAK can also have bit errors → Need to resend package, but do not know whether package is received or not → **Packet Sequence Number**

![[Pasted image 20220910221602.png||730]]

### RDT 2.2: NAK-Free

Instead of sending NAK, receiver sends ACK for the **last packet received OK** → Receiver must explicity include sequence # of the packet being ACKed

![[Pasted image 20220910222040.png]]

### RDT 3.0: Packet Loss

To handle packet loss, we can implement a **timeout** for sender:
- Sender waits an amount of time for ACK
- If ACK not received by timeout, resend the packet.

In RDT 3.0, the sender relies on **timeout** to resolve both packet loss and packet corruption! Hence sender and receiver do nothing and wait for timeout.

There are **3 scenarios** for packet loss:
1. Packet is **lost** or **corrupted** → receiver does nothing, sender waits for timeout and resend

 ![[Pasted image 20220910222316.png]]

2. ACK is **lost** or **corrupted** → Sender does nothing , also wait for timeout

![[Pasted image 20220910222349.png]]

3. ACK is **delayed**:

![[Pasted image 20220910222506.png]]

## Performance (Utilization)

To measure the performance or RTD, we use utilization.

The utilization of RDT refers to the percentage of time that the communication channel is being used to transmit data.

To measure the utilization of RDT, you can use the following formula:

Utilization = (Data transmitted / Total time) x 100%

where:

-   Data transmitted: the total amount of data transmitted over the communication channel during the measurement period.
-   Total time: the total amount of time that the communication channel was available during the measurement period.

RDT's performance is pretty ass, due to the **stop-and-wait operation**.

![[Transport Layer 2022-09-10 22.29.56.excalidraw||500]]

We can increase the utilization by using the pipelining technique!

![[Pasted image 20230302172606.png]]

With window size of 3, we can increase utilization by a factor of 3!

$$U_{sender} = \frac {3 * L / R}{(RTT + L/R)}$$
