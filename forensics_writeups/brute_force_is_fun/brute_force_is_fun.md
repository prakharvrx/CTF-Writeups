### Step 1: Finding the Hidden File

The first step was to examine the picture file, `legotroopers.jpg`. It seemed like a regular image, but many challenges like this hide information inside of files. Using a tool that looks for hidden files, it was clear that a `.zip` file was secretly tucked inside the picture.

![[legotroopers.png]]
### Step 2: Unpacking the Hidden Files

Next, I used a tool called `foremost` to pull out all the files hidden in the `.zip` file. This created a new directory called `output`, which contained a new set of folders and another `.zip` file.

### Step 3: Discovering the Password-Protected Zip

Inside the `output` folder, I found a very important file: `00000012.zip`. This file was protected with a password. The goal of the next steps was to find that password.

### Step 4: Finding the Password Hint

To find a clue about the password, I searched through all the folders with the command `grep -R flag`. This command looks for the word "flag" inside every file. The search revealed a hint in a text file:

```
folders/73/47/p:The password is: "ctflag*****" where * is a number.
folders/73/43/p:The password is: "ctflag*****" where * is a number.
```

This was a huge clue! It told me the password format: it starts with `ctflag` and ends with a five-digit number.

### Step 5: Brute-Forcing the Password

Now that I knew the password format, I could write a script to try every possible combination of five digits (from `00000` to `99999`) until it found the right one. This method is called **brute force**. I used a simple Python script to do this:

```
#!usr/bin/python3
from zipfile import ZipFile
from string import digits
import itertools

# Create every possible five-digit number
brute = itertools.product(digits, repeat=5)

# Try each password on the zip file
with ZipFile("00000012.zip") as zf:
    for i in brute:
        i = ''.join(i)
        password = "ctflag" + i
        try:
            zf.extractall(pwd=bytes(password, 'utf-8'))
            print("Flag: " + password)
        except:
            pass
```

The script successfully found the password: `ctflag48625`.

### Step 6: Getting the Final Zip File

With the correct password in hand, I unzipped `00000012.zip`. This action created a new file called `flag.zip`.

### Step 7: Decoding the Final Flag

After unzipping `flag.zip`, I found the final file, `flag.txt`. When I opened it, the text looked like this: `RkxBR3ttYXlfdGhlX2JydXRlX2ZvcmNlX2JlX3dpdGhfeW91fQ==`. This jumbled string of letters and numbers is a common form of text encoding called **Base64**.

To reveal the final message, I used a simple command to decode the text:

```
cat flag.txt | base64 -d
```

### Step 8: The Final Answer

Running the command decoded the text and revealed the final flag:

`FLAG{may_the_brute_force_be_with_you}`