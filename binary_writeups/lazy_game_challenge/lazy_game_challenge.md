This challenge is a great example of a simple **logic flaw** in a program. The goal is to break the game's intended flow by providing an unexpected input, leading to an unfair advantage and, ultimately, the flag.

## Step 1: Connecting to the Game

The first step is to connect to the game server using `netcat` (`nc`) on the specified host and port.

```
nc thekidofarcrania.com 10001
```

Once connected, we are presented with a betting game. The initial attempts to play normally, by betting a positive amount and guessing a number, all result in losses. It seems impossible to win by playing fair.

## Step 2: The Logic Flaw

The core idea of the challenge is to **think differently** from the program's intended behavior. While attempting to bet a very large number like 1,000,000 fails, the true vulnerability lies in using a **negative number**.

By betting a negative amount (e.g., −100,000), the program's logic breaks. Instead of deducting a negative value from your balance, it adds it, as the subtraction of a negative number becomes addition. This causes an **integer underflow** or a simple logic error, skyrocketing your balance to a massive number.

## Step 3: Claiming the Flag

With a virtually infinite balance, the final step is to make a large bet and guess the number correctly.

After making the bet with a negative number, the game allows you to continue. The program's logic is now compromised. It now becomes a matter of giving the correct guess to get the flag. Since the numbers are low, it's easy to try each one until you find the right one.

## Final Flag

The flag is:

**`CTFlearn{d9029a08c55b936cbc9a30_i_wish_real_betting_games_were_like_this!}`**