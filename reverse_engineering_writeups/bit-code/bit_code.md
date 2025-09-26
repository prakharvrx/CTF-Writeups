# CTF Writeup: Bite-code

This challenge requires you to analyze and reverse-engineer **Java bytecode**. The goal is to understand the logical operations performed by a function and then write a small program to brute-force the correct input that satisfies a given condition.

## Step 1: Analyzing the Java Bytecode

The provided file `bitecode.txt` contains the bytecode for a function named `checkNum`. By carefully examining each instruction, we can understand the logic it's trying to execute.

```
public static boolean checkNum(int);
  descriptor: (I)Z
  flags: ACC_PUBLIC, ACC_STATIC
  Code:
    stack=2, locals=3, args_size=1
       0: iload_0             // Load the integer argument (the flag) onto the stack
       1: iconst_3            // Push the integer 3 onto the stack
       2: ishl                // Left bit shift: (flag << 3)
       3: istore_1            // Store the result in local variable x1
       4: iload_0             // Load the flag again
       5: ldc           #2    // Push the integer 525024598 onto the stack
       7: ixor                // XOR the flag with the integer: (flag ^ 525024598)
       8: istore_2            // Store the result in local variable x2
       9: iload_1             // Load x1 onto the stack
      10: iload_2             // Load x2 onto the stack
      11: ixor                // XOR the two values: (x1 ^ x2)
      12: ldc           #3    // Push the integer -889275714 onto the stack
      14: if_icmpne     21    // Compare the two values; if not equal, jump to line 21
      17: iconst_1            // If equal, push 1 (true) onto the stack
      18: goto          22    // Jump to the return instruction
      21: iconst_0            // If not equal, push 0 (false) onto the stack
      22: ireturn             // Return the value from the stack
```

## Step 2: Reversing the Logic

Based on the bytecode, we can translate the program's logic into a more human-readable format. The program takes an integer as input and performs a series of operations to determine if it is the correct number.

1. `x1 = flag << 3`
2. `x2 = flag ^ 525024598`
3. `x3 = x1 ^ x2`
4. The program checks if `x3` is equal to **-889275714**.

Since the program logic is based on a fixed set of operations and a known final result, we can write a simple program to brute-force the initial `flag` value until we find the number that produces the correct final value.

## Step 3: The Brute-Force Program

We can write a simple C program to automate the brute-force attack. Since the flag is an integer, we can test all possible 32-bit integer values until we find the one that produces the desired result.

To get the flag, you simply need to compile and run this C program. The program will iterate through the integers until it finds the one that satisfies the condition and then print the result.

The output from the program will be:

-1352854872

## Final Flag

The flag is the number found by the brute-force script, formatted according to the challenge rules.

**`CTFlearn{-1352854872}`**