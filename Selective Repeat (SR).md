## Selective Repeat

We will keep out-of-order packets in **buffer**, and will reorder it once all the in-order packets are received.

Sender maintains a **timer** for **each** unACKed packet → When timer expires, retransmit only the unACKed packet.

![[Pasted image 20220922173544.png]]

![[Transport Layer 2022-09-22 17.36.25.excalidraw||500]]

**Sender:**
- If there is an available sequence number in window, send packet! (Send until window is full)
- Keep a timer for each packet → Resend packet `n` if time runs out + reset timer
- Upon receiving `ACK(n)` in window `[sendbase, sendbase + N]`:
	- Mark pkt `n` as received
	- ! If `n` is the smallest unACKed pkt, advance **window base** to the **next unACKed sequence number**

**Receiver:**
- For `packet(n)` in `[rcvbase, rcvbase + N + 1]`:
	- Send `ACK(n)`
	- If packet is out-of-order: Buffer
	- If in-order: Deliver all the buffered packets in order, **advance window** to the **next not-yet-received packet**
- For packet `n` in `[rcvbase - N, rcvbase - 1]`:
	- `ACK(n)`  must have already been sent!
- Otherwise: Ignore, do not send any ACK