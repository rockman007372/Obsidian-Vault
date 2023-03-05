
Instead of sending 1 packet and wait, we can send multiple yet-to-be-acked packets. This neccessitates more resources in exchange for greater transmission speed:
- Range of sequence numbers must be increased
- Buffereing at sender/receiver to order packets

There are 2 generic forms:
- [[Go Back N (GBN)]]
- [[Selective Repeat (SR)]]

