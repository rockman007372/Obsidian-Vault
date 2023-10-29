### **Strong consistency**

Any reads immediately after an update must give the same result on all observers. => requires Blocking on Read.

![[Pasted image 20230923204827.png]]

### **Eventual consistency**

If the system is functioning and we wait long enough, **eventually** all reads will return the last written value. => there is possibility that reading Node C will give obsolete data.

![[Pasted image 20230923204900.png]]

NoSQL follows the BASE property:
- Basically Available: can read/write anytime
- Soft state: without guarantees, can have some probability of knowing a state
- Eventual consistency.

This is contrast to the ACID propery of RDBMS:
- Atomicity: either all effects of transaction T are reflected in db or none
- Consistency: T always yield the correct state
- Isolation: T is isolated from the effect of concurrent transactions
- Durability: after a commit of T, its effects are permanent

Implications:
- NoSQL suitable for applications that favor speed and availability over consistency (tweets, social network feeds,...)
- SQL suitable for application that prioritize consistency (financial transactions...)