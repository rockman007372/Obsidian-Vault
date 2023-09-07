
### Overflow

Signed numbers are of fixed range, hence overflow can occur if result of addition/subtraction exceeds this range.

Oveflow can easily be detected when:
- positive + positive → negative
- negative + negative → positive

Example: 4-bit 2s-complement system
- Range: -8 to +7
- 5 + 6 = 0101 + 0110 = 1011 = -5?
- -7 + (-3) = 1001 + 1101 = 0110 = 6?

### 2s Complement on Addition and Subtraction

Addtion:
1. Perform binary addition
2. **Ignore the carry out of the MSB**
3. Check for overflow (look at sign / check carry in != carry out)

Subtraction: 
1. Take 2s-complement of B
2. Addition

### 1s Complement on Addition and Subtraction

Addtion:
1. Perform binary addition
2. **Add the carry out of the MSB** to result (add 1 to result)
3. Check for overflow (look at sign difference)

Subtraction: 
1. Take 1s-complement of B
2. Addition

![[Pasted image 20220826110507.png]]