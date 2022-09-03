---
layout: default
title: PicoCTF notes, part 1 - General Skills
excerpt_separator: <!--more-->
---

These are notes from the PicoCTF General Skills challenges I've done. Spoilers abound, though no flags.

I'm working through these in an Ubuntu WSL2 instance, and using a Python 3.9.6 virtualenv where needed. Usually I'd use Poetry for dependency management, but for playing around like this, that seems like overkill - so pyenv and pyenv-virtualenv are all I need here.

On to the challenges!
<!--more-->

### Obedient Cat (5 points)

There's a file you can download, and it's easy to look in for the answer.

### Python Wrangling (10 points)

The test Python file does require a third-party library, so I figured it was best to make a virtualenv to try this out.

Other than that, it was pretty simple.

### Wave a flag (10 points)

The downloadable file is a Linux executable, and the hints and program responses tell you what to do. `strings` would also solve this for you.

### Nice netcat... (15 points)

When you run the command it suggests, the response is a list of numbers. Looks like they're Unicode code points. (Well, also ASCII; they're low enough that the two are the same.)

### Static ain't always noise (20 points)

I ignored the bash script entirely and had a look at the binary (first with `less`, because I am sometimes foolish, and then with `strings`).

That was enough!

That said, the bash script also points out `objdump`, which will be useful soon, I think.

### Tab, Tab, Attack (20 points)

Once you've unzipped the downloaded file, this is an exercise in using tab complete to not knacker your hands. The final file you get to is another binary, and `strings` gets you the flag.

### Magikarp Ground Mission (30 points)

This is a reminder of how to navigate Unix directory structures. The flag is in three parts, each found in different places.

This is the first of the general skill challenges that spawns an instance for us to play around with. And as a neat touch, when you enter the flag, it ends the instance and logs you out.

### Lets Warm Up (50 points)

This is a very easy one if you check the hint, which points out that it should be submitted in flag format (so something like `picoCTF{hello}`).

Honestly, I think this is too easy for 50 points - much like the next one - but it's nice to blaze through things sometimes.

### Warmed Up (50 points)

Like the previous one, this is very easy if you have something that converts hex to decimal. I have a Python REPL open for this.

### 2Warm (50 points)

This one needs decimal to binary.

### what's a net cat? (100 points)

Useful note - the syntax for netcat is `nc <hostname> <port>`. You don't need a `-p` before the port number.

### strings it (100 points)

`strings` is useful here again! This time, piping it through `less` so that you can search for the flag prefix is also needed.

### Bases (100 points)

The string we get is quite short, so my first guess was that it was base64 - and it was! It wasn't the whole flag, but we know how to deal with flags without the prefix already.

### First Grep (100 points)

grep may be good to find things, but I used `less` and then `/pico` to search for the flag prefix.

If you wanted to do this in grep, I think ` grep "picoCTF" file` would be a good approach.

### Codebook (100 points)

You don't need to do anything much for this, just follow the instructions in the challenge.

### convertme.py (100 points)

You could do this with a reference tool, but I got lucky with the number it gave me and I converted to binary in my head.

### fixme1.py (100 points)

The Python error message for this is pretty helpful (and if you've spent some time with Python the error is obvious from the source).

### fixme2.py (100 points)

As the flag itself points out, Python doesn't let you assign to things in comparisons, but that's pretty easy to solve.

### Glitch Cat (100 points)

The glitch isn't too bad - a few moments in a Python REPL will sort it out.

### HashingJobApp (100 points)

To do this I learned that you can have multiple WSL terminals open at the same time, which is neat.

In order to hash a string in the terminal, you can use `echo -n "pancakes" | md5sum`. The `-n` flag is important - without it, `echo` adds a newline at the end of the string you asked it to hash, and that'll change the hash.

### PW Crack 1 (100 points)

Ooh, this one reminds me of an early level in Microcorruption! (Which I will write up some time later.)

The password you need is readable and easy to find.

### PW Crack 2 (100 points)

The password takes a bit of computing, but it's still easy to find.

### PW Crack 3 (100 points)

It's very kind to give us some potential passwords!

I guess we could try them all, but instead I decided to figure out which was right.

We can hash those like we did for HashingJobApp earlier, and then read the hash file in as bytes and use the `.hex()` method on it to get the hex MD5 sum. Then we see which one matches that.

### PW Crack 4 (100 points)

This is like the previous challenge, but it's tedious to do them all by hand. We can import the password list (and also the hashing function) from the Python file, and then compare the hash of each of them against the hash from the file. (We don't need the `.hex()` method for that.)

### PW Crack 5 (100 points)

Like the previous one, but instead of importing the password list from a Python file, we read it in from the dictionary file.

This is basically teaching you about dictionary attacks on passwords.

### runme.py (100 points)

Okay, this one is super easy again. You can either run the script or read the code to get it.

### Serpentine (100 points)

Some editing is required for this.

### First Find (100 points)

The title and flag make a point - you can do this with `find` if you want - but I keep forgetting the syntax so I just looked at what files the `unzip` command listed, and navigated there.

### Big Zip (100 points)

Unzipping this takes quite a while - "big zip" is accurate! Though it's a little frustrating that `unzip` doesn't give some sort of progress meter by default.

Once it's all unzipped, ` grep "picoCTF" <the unzip location>/big-zip-files/ -r` is enough to find you the flag in among all the other things.

### Based (200 points)

This one accidentally prints the first answer before it gives you the binary. I don't think that's intended!

Anyway, you have three sets of numbers to convert. First is binary (pretty obvious), next is octal (I didn't realise this until a little way in), and last is hex.

### plumbing (200 points)

Everyone loves pipes! `nc <hostname> <port> | your_filename.txt` will send the output of netcat to a local file.

### mus1c (300 points)

This one is pretty fun! The lyrics are obviously programmatic, and reminded me a bit of [Chef](https://esolangs.org/wiki/Chef), so I went to check if there was an esolang for song lyrics.

And there is! It's called [Rockstar](https://esolangs.org/wiki/Rockstar), and a look at the sample code indicates that that's the language we're looking for.

The main website for it has an online interpreter, and putting the code in there gives us a list of numbers we can turn into a string, which we then put into the flag format.

### flag_shop (300 points)

The C source code is quite simple, so where's the potential exploit?

Well, it is a bit weird that both `account_balance` and `total_cost` are defined as `int`, which by default is signed - that is, it can go negative.

So, as it turns out, you can spend enough on buying terrible knock-off flags that `total_cost` overflows to be negative, and thus your account balance goes up rather than down. That means you have enough to buy the real flag.

### 1_wanna_b3_a_r0ck5tar (350 points)

This is more Rockstar code. I needed to tweak the line "Rock is electric heaven", as the online interpreter wanted to understand "Rock" not as a variable but as a queue operation (see [rockstar docs](https://codewithrockstar.com/docs)), so I turned it to "Rocking" instead.

The way that variables are set in Rockstar is also pretty cool! However, it's hard to follow, so I also used [yyyyyyyan/rockstar-py: Python transpiler for the esoteric language Rockstar](https://github.com/yyyyyyyan/rockstar-py)  to get a first pass of what it would look like in Python. (This doesn't cope with end-of-line exclamation marks, or with `They are dazzled audiences`, so it doesn't produce Python that runs - but it's enough to help.)

With the transpiled code, I could see two requests for input, and an idea of what input it was expecting. And so, putting those in in separate lines in the online interpreter, it gives us some numbers, which can be converted to characters in the flag!

---

That's all of the General Skills challenges! I liked the esoteric language ones, even though the votes on them indicate they're a lot less popular than the others. I think it's a neat touch to use something like that.
