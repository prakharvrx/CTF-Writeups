
This challenge involves a common binary exploitation technique known as a **string overflow** or **buffer overflow**. The goal is to provide a malicious input to a program to make it behave in an unintended way and reveal the flag.

## Step 1: Connecting to the Server

The first step is to connect to the provided server using `ssh` with the given credentials.

```
ssh blackbox@104.131.79.111 -p 1001
```

Once connected, we are presented with a shell on the remote machine. We can now interact with the `blackbox` binary.

## Step 2: Fuzzing the Program

After running the `blackbox` program, it prompts for input. A common technique for finding vulnerabilities is **fuzzing**, where you give the program a wide range of unexpected inputs, such as very long strings.

By providing a very long string, we can see that the program crashes or behaves strangely. This indicates that it's likely vulnerable to a buffer overflow. We need to find the exact point where the input overwrites a critical part of the program's memory. In this case, it appears the overflow happens at the 81st character, allowing us to control the program's execution.

## Step 3: Crafting the Exploit

We can use a simple Python one-liner to create the exact payload needed to trigger the vulnerability. The payload consists of two parts:

1. **Padding:** A long string of characters to fill up the buffer. The vulnerability is triggered after 80 characters, so we'll use a string of 80 '1's.
2. **Overwrite:** The specific sequence of bytes that will overwrite the program's return address, directing it to the code that prints the flag. The value `\x02\x00\x00\x00` seems to be the correct address to jump to.


The one-liner pipes the payload directly to the `blackbox` program:

```
python -c "print '11111111111111111111111111111111111111111111111111111111111111111111111111111111\x02\x00\x00\x00'" | ./blackbox
```

## Step 4: Finding the Flag

When the command is executed, the program's flow is hijacked, and it jumps to the section of code that prints the flag.

```
What is 1 + 1 = CORRECT! You get flag: 
flag{0n3_4lus_1_1s_Tw0_dumm13!!}
```

This challenge is a great introduction to how a seemingly harmless input field can be exploited to gain control of a program.

## Final Flag

The flag is:

**`flag{0n3_4lus_1_1s_Tw0_dumm13!!}`**