
## E1 - README

- From  `index.php`, I understand that the content of `flag.txt` is read using `file_get_contents($url)` where `$url` is the raw unprocessed url parameter passed by user.
	- The `file_get_contents` function can read the contents of a file or resource into a string.
- This allows me to pass in the `php://filter/` stream wrapper to apply filters to data streams on server-side. 
	- A [stream wrapper](https://www.php.net/manual/en/class.streamwrapper.php) intercepts PHP's file-handling operations (like reading or writing) and maps them to underlying resource-handling logic.
- The full URL I used was http://cs2107-challs.nusgreyhats.org:5051/?url=php://filter/convert.base64-encode/resource=/flag.txt
	- `php://filter`: This specifies that the stream wrapper is being used to apply filters to the data.
	- `convert.base64-encode`: This is the filter being applied. It takes the input data and encodes it in Base64 format.
	- `resource=/flag.txt`: This specifies the target resource to which the filter should be applied. In this case, the resource is the file `/flag.txt`.
- On server side, the data in `flag.txt` will be encoded by the filter stream wrapper, before it is read into string. This prevents the `strpos()` function from detecting the string `CS2107`, allowing the encoded flag to be sent to client and decoded there.

![[Pasted image 20241117134212.png]]
## E2 - Minesweeper

- This is a buffer overflow challenge.
- First, I compiled `minesweeper.c` using `gcc -g -fno-stack-protector -o minesweeper-redacted minesweeper.c`
	- `-g` to allow debugging
	- `-fno-stack-protector` to allow buffer overflow attack on stack
- Then, I run the debugger `dbg` and identify the addresses of the local variables in `vuln` function stack frame

```c
(gdb) p &secret
$1 = (char (*)[16]) 0x7fffffffd6f0
(gdb) p &mine1
$2 = (char (*)[16]) 0x7fffffffd6e0
(gdb) p &mine2
$3 = (char (*)[16]) 0x7fffffffd6d0
(gdb) p &mine3
$4 = (char (*)[16]) 0x7fffffffd6c0
(gdb) p &buf
$5 = (char (*)[32]) 0x7fffffffd6a0
```

- This gives me information on how to visualize the stack frame:
	- Stack grows downward (from higher to lower memory addresses)
	- Array grows upwards (the first element in the array is at the lowest memory address)
- From the source code, I know that to obtain the flag, I have to overwrite from the buffer array such that:
	- the content of mine1, mine2 and mine3 arrays are not changed
	- the first 0x10 bytes of buffer and secret must be the same
- This gives me the overflow input: `"A" * 32 + "i165DnHauCmLqRHN" + "cZiwk5rfGFgPZYP4" + "O6FtZhpU6C6BXx16" + "A" * 16`
	- The first 32 bytes of A is to fill the `buf` array
	- `"i165DnHauCmLqRHN"`, `"cZiwk5rfGFgPZYP4"`, `"O6FtZhpU6C6BXx16"` are the content of mine3, mine2 and mine1 in that order. We must write from mine3 to mine1 to adhere to their order in the memory stack.
	- Finally, write the last 16 bytes of A into the `secret` array.
	- Hence, the content of mine1, mine2 and mine3 arrays are unchanged, and the first 16 bytes of both `buf` and `secret` are all As.

![[Pasted image 20241117134046.png]]

## E3 - Look Deeper

- This is a reverse engineer challenge. I have to decompile the binary to view the human-readable source code.
- I used [Binary Ninja](https://binary.ninja/) decompiler to decompile LookDeeper binary and obtained the following `main` function

```C
int64_t main() {
    setbuf(stdin, 0);
    setbuf(stdout, 0);

    int64_t var_38;
    __builtin_strncpy(&var_38, "ce`ubOcusbudO`qccg\x7fbt", 0x18);

    int64_t var_58;
    __builtin_strncpy(&var_58, "SC\"! 'kB#fOyCOVe^~1m", 0x18);

    void var_78;
    std::string::string(&var_78);

    std::operator<<<std::char_traits<char>>(&std::cout, "Enter the password: ");
    std::operator>><char>(&std::cin, &var_78);

    decode(&var_38, 0x10);

    if (std::operator==<char>(&var_78, &var_38) == 0)
        std::ostream::operator<<(std::operator<<<std::char_traits<char>>(&std::cout, "Wrong password!"), std::endl<char>);
    else {
        decode(&var_58, 0x10);
        std::ostream::operator<<(std::operator<<<std::char_traits<char>>(std::operator<<<std::char_traits<char>>(&std::cout, "Correct! The flag is "), &var_58), std::endl<char>);
    }

    std::string::~string(&var_78);

    return 0;
}
```

- From the source code, I obtained the encoded flag `SC\"! \'kB#fOyCOVe^~1m`
- From the `decode` function, I understand the decoding process involves xor-ing each byte of the encoded string with the key `0x10`. I wrote a Python decoding script to do just that to obtain the flag

![[Pasted image 20241117140519.png]]
## M1 - Blind Ping Pong

- Reading the server source code reveals that the `ping` endpoint is vulnerable to command injection
	- `response = os.system('ping -c 1 ' + url)` allows the client to concatenate commands in the url to be run by the server's system.
- The goal is to extract the contents of  `flag.txt` on the server, one character at a time, based on the exit status code of the command injected into the url parameter.
- The script builds the flag incrementally by guessing one character at a time and checking if the current guess matches the file's content up to that length.
	- This is done by the command `[ "$(head -c {len} flag.txt)" = "{flag}" ] && exit 0 || exit 1'`
	- It compares the first `len` characters in the flag.txt with the current guess and returns 0 if they match, otherwise 1.
- Using the exit code, we can perform a brute force check for each character in the flag. If the error code returned is 0, we have found the current character and can move onto the next.

![[Pasted image 20241114230654.png]]

## M3 - zzz 

- From the code, I understand that the flag, when transformed into an array of ascii number, have to follow a groups of constraints.
- Using the z3 package, given the constraints, we can solve for an array of ascii numbers that satisfy all these constraints.
- From the solution, I simply convert each ascii number back to its char representation to obtain the flag.

![[Pasted image 20241114233333.png]]

## H2

- There are 2 parts to the solution.
- In the first part, I obtained the actual address of the `main` function. 
	- From the code, I understand that I must modify `user` string from `"customer"` to `"rootuser"` in the stack frame of function `catalogue` so that this function would return the address of the `main` function.
	- This can be done using buffer overflow: After writing the first 0x40 bytes into the `input` buffer, I can continue writing `b'rootuser'` into the `user` array, since `user` is directly adjacent to `input` in memory.
	- ![[Pasted image 20241116175749.png]]

- In the second part, I replace the return address of the stack frame of function `cake` with the address of function `win()` so that `win()` is executed after function `cake` returned.
	- I first calculate the offset between the actual address of the `main` function and the address of the `main` function in the ELF symbol table.
		- `elf.address = address - elf.sym['main']`
	- Using this offset, I can calculate the actual address of function `win`  in memory.
		- `elf.sym[win]`
	- Since function `cake` writes to the `input` buffer an unspecified number of bytes, I can overflow the `input` buffer to modify the return address of function `cake`.
		- This is due to the use of function call `gets(input)`
	- However, I need to know the offset between the `input` buffer and the memory location of the return address of function `cake`.
	- Hence, I used gdb to identify the addresses inside function `cake` stack frame:
		- ![[Pasted image 20241116174807.png]]
	- From the gdb:
		- Address of input buffer: `0x7fffffffd6d0`
		- Address of saved rip (where return address is stored): `0x7fffffffd6f8`
		- This means the offset between the input buffer and the function return address is `0x28` bytes (40 bytes).
	- Hence, the payload to write to `input`  buffer is `b'A' * 40 + p64(elf.sym['win'])`. This allow me to obtain the flag:
		- ![[Pasted image 20241116181827.png]]