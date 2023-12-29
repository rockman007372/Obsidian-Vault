![[Pasted image 20231029125841.png]]

Basic idea:
- Memory holes are blocks of power of 2.
- A process is allocated the best-fit hole (smallest block larger than the process' size)
- Allows easy merging of buddy blocks.

Fragmentations:
- Internal: a process just slightly bigger than $2^k$ will be allocated a $2^{k+1}$ block.
- External: 2 non-buddy blocks cannot be merged.