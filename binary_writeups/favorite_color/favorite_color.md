This challenge is an introduction to **binary exploitation** and specifically, **buffer overflows**. The goal is to provide a malicious input to a program to make it behave in an unintended way and reveal the flag.

## Step 1: Connecting to the Server

The first step is to connect to the provided server using `ssh` with the given credentials.

```
ssh color@104.131.79.111 -p 1001
```

Once you've entered the password `guest`, you are presented with a shell on the remote machine. We can now interact with the `color` binary.

## Step 2: Understanding the Vulnerability

When you run the `color` program and provide it with a very long input, it crashes. This indicates a **buffer overflow** vulnerability. The program has a fixed-size buffer to store your input, and it doesn't check if the input is too long. By providing more data than the buffer can hold, you can overwrite adjacent memory, including the program's return address. By controlling the return address, you can redirect the program's execution to a different function, such as one that prints the flag.

Based on an analysis of the binary, the specific buffer overflow occurs after a certain number of bytes, at which point you can overwrite the return address.

## Step 3: Crafting the Exploit

Since the goal is to redirect the program to the function that prints the flag, we need to create a payload that contains both padding and the correct memory address. This is typically done with a command-line one-liner that pipes the payload to the binary.

While the exact payload may vary, it generally follows this format: `[PADDING_CHARS] + [RETURN_ADDRESS]`. The padding fills up the buffer, and the return address overwrites the instruction pointer, forcing the program to execute code at a specific location.

## Final Flag

By crafting and executing the correct payload, the program's execution is hijacked, and it jumps to the section of code that prints the flag.

The flag is:

**`flag{c0lor_0f_0verf1ow}`**