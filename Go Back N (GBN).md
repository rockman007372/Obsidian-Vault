## GBN 

![[Pasted image 20230302173720.png]]

Key features: 
- Client sends multiple packets within window size and wait.
- Once client receives an accumulative ACK, it increments the window accordingly and send the new unsent packets.
- If packet N is not received, server **discard** subsequent packets after N and **resend ACK N** after each received packet to signal N is not received. 
- Once there is timeout, client resends packet N and all the subsequent packets in the window.

**GBN Sender:**
- Have up to N unACKed packets in pipeline (N = window size)
- Insert **k-bits sequence number** in header where $k = lg(N)$
- Use **[[Sliding Window]]** to keep track of unACKed packets
- ! Keep a timer for the **oldest** unACKed packet
- `timeout(n)`: Retransmit packet n and all subsequent packets in the window 

**GBN Receiver:**
- Only ACK packets that arrive in order 
- Discard out of order packets and ACK the *last in-order* sequence number → *Cumulative ACK*: ACK m means all packets up to m are received

![[Pasted image 20220910225503.png]]

GBN can be time-wasting, if most the packets received are out of order and hence discarded:

![[Pasted image 20220910225405.png]]