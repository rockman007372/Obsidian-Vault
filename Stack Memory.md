![[Pasted image 20230903172507.png]]

- Stack memory region stores information for function invocation.
- Stack frame: Information of a function invocation
- ! Stack Pointer: (**always**) points to the top of the stack
- Stack memory grows upward dynamically in the "free memory".

>[!remember]
> Stack frame consists of:
> - Return address of the caller function (Return PC)
> - Previous stack frame's pointer (Saved SP)
> - Arguments (parameters) of the function
> - Local variables in callee
> - Frame Pointer
> - Saved Registers

- Other info in stack frame:
	- Frame Pointer: facilitate access of stack frame items through **displacement of a fixed frame pointer**. Optioanl, only for ease of access.
	- Saved Register: save data in memory temporarily when registers run out (aka **register spilling**)

![[Pasted image 20230903173232.png]]

## Stack Frame Setup / Teardown (role)

On executing function calls:
- Caller: 
	- Pass arguments with stacks/registers.
	- Save Returned PC on stack.
- Callee: 
	- Save registers used by calles.
	- Save old FP, SP.
	- Allocate space for local variables of callee on stack.
	- Adjust SP to point to new stack top. Adjust FP.

On returning from function call:
- Callee: Restore saved registers, FP, SP
- Transfer control from callee to caller using saved PC
- Caller: continue execution of program.