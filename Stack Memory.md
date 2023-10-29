![[Pasted image 20230903172507.png]]

- Stack memory region stores information for function invocation.
- Stack frame: Information of a function invocation
- ! Stack Pointer: (**always**) points to the top of the stack
- Stack memory grows upward dynamically in the "free memory".

## What is in a stack frame?

Example C program:

```C
function f(a, b) { // caller
	int sum = g(a, b);
	...
}

functtion g(x, y) { // callee
	int local;
	local = x + y;
	return local;
}
```

>[!remember]
> Stack frame consists of:
> - Return address of the caller function (Return PC)
> - Previous Stack Pointer  of caller (Saved SP)
> - Previous Frame Pointer of caller (Saved FP)
> - Arguments of the callee function (Parameters)
> - Local Variables in callee
> - Saved Registers: Previous values in the registers 

![[Pasted image 20230903173232.png]]

- Other info in stack frame:
	- Frame Pointer: facilitate access of stack frame items through **displacement of a fixed frame pointer**. Optional, only for ease of access.
	- Saved Register: save data in memory temporarily when registers run out (aka **register spilling**)

>[!summary]
> Stack frame contains 2 type of info:
> - Caller's info: Saved PC, Saved SP, Saved FP, Saved Registers
> - Callee's info: Local Variables, Parameters

## Stack Frame Setup / Teardown

On executing function calls:
- Caller: 
	- Pass arguments using stacks/registers.
	- Save Returned PC on stack.
- Transfer control from Caller to Callee using new PC
- Callee: 
	- Save previous content of registers it intends to use.
	- Save old FP, SP.
	- Allocate space for local variables of callee on stack.
	- Adjust SP to point to new stack top. Adjust FP accordingly.

On returning from function call:
- Callee: Place return result in register + Restore saved registers, FP, SP
- Transfer control from callee to caller using saved PC
- Caller: continue execution of program.