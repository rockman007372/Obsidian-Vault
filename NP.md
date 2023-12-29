
A problem is in NP if we can verify whether an input is the answer to the problem in polynomial time.

To prove if a problem is in NP:
1. Reduce it to a **decision problem**  
2. Define the following:
	- **Instance** of the problem (its inputs)
	- **Certificate:** a potential answer to the problem
	- **Certifier:** an algorithm to verify if the certificate gives the answer in polynomial time.

Example: Given an integer s, is s composite?
1. Decision problem: is there a t such that s % t == 0?
2. Define:
	1. **Instance**: s
	2. **Certificate**: t
	3. **Certifier**: whether t > 1 and t < s, and s % t == 0.