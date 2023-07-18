---
title: "Diving deeper in basic Linux"
datePublished: Mon Jul 17 2023 05:18:16 GMT+0000 (Coordinated Universal Time)
cuid: clk7uggc6000h09le2kf581yw
slug: diving-deeper-in-basic-linux
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689657274211/47e1123e-9a95-40e6-9ebb-df784965dae7.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1689657487410/ba03ca15-4518-4044-aa85-af60ef6f603e.png
tags: linux, linux-basics, linux-commands, day3, trainwithshubham

---

Let's directly jump into the commands by doing some tasks that will cover some major Linux basic commands.

## 1️⃣Task 1

### To view what's written in a file🔎

Let's say I have a file called linux-basic.txt and in this text-based file there is some content written on it. And you want to see the contents.

Then there is a command for that called `cat`

**Cat** is used to concatenate and display files on the terminal.

* ***cat -n:*** This adds line numbers to all lines
    
* ***cat –E:*** This shows $ at the end of the line
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689624911604/f9d2ec74-31e3-42f1-bf94-1097d8c60a51.png align="center")

## 2️⃣Task 2

### To change the access permissions of files🔐

There will be a case where you don't want others to modify your file or vice-versa. To change the permissions of files, there is a command called `chmod`

```bash
chmod 755 linux-basic.txt
```

This sets the permissions of `linux-basic.txt` to read, write, and execute for the owner, and read and execute for the group and others.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689625431714/8028c4cc-335c-4c7a-a18d-e4fefc316d6c.png align="center")

* The next three characters, `rwx`, indicate the permissions for the file owner (`ubuntu` in this case). It means the owner has read (`r`), write (`w`), and execute (`x`) permissions.
    
* The following three characters, `r-x`, indicate the permissions for the group (`ubuntu` in this case). It means the group has `read` and `execute` permissions but does not have `write` permission.
    
* The last three characters, `r-x`, represent the permissions for others (users not in the owner or group). They have `read` and `execute` permissions but no `write` permission.
    

You can manage the accessibility according to you, like above.

## 3️⃣Task 3

### To check which commands you have run till now🗒️

To perform the above task, there is a command called `history`, where you can see all the commands you have used till now.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689625755112/64023fd9-8003-47ff-9c7f-9d9233f0db2a.png align="center")

## 4️⃣Task 4

### To remove a directory/ Folder📤

To remove a file, there is a command called `rm` ie **remove.** But we cannot remove a folder by running just rm cmd. There is another cmd to remove a folder that is called `rm -rf`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689627608151/92fc0913-aa81-4e66-9b90-e5c93d35cc79.png align="center")

The `rm -rf` command is a more powerful variation that forcefully removes files and directories recursively without prompting for confirmation.

* `-r` (or `--recursive`): This option enables the removal of directories and their contents recursively.
    
* `-f` (or `--force`): This option overrides any prompts or warnings and forcefully removes files and directories without asking for confirmation.
    

## 5️⃣Task 5

### To create a fruits.txt file and to view the content🧺

1. Create fruits.txt file - To perform this, there are two ways you can consider.
    
    * Run touch cmd, this will create a file with no content. Then run `vi/vim` cmd, this will open up a text editor where you can write whatever you want by changing its mode to insert(i) and then `esc` &gt; `:wq!` to **save** and **exit** from the editor.
        
    * Or you can run directly `vi/vim fruits.txt` cmd, this creates a file and open-up the editor directly.
        
        ```bash
        $vi fruits.txt
        
        This file is created to list my favourite fruit ie MANGO.
        --
        --
        :wq!
        ```
        
2. To view the content of the file - Run cat cmd as we have discussed earlier.
    
    ```bash
    $ cat fruits.txt
    This file is created to list my favourite fruit ie MANGO.
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689627595882/f51b84a1-800f-43d6-9091-1a45041dafeb.png align="center")

## 6️⃣Task 6

### Add content in devops.txt (One in each line) - Apple, Mango, Banana, Cherry, Kiwi, Orange, Guava🥗

To perform the above task, we have to create a file called devops.txt and then add on some given contents. Let's do that!

Again, there are two ways (some more ways, comments :)

Method 1: Using a text editor

1. Open the `devops.txt` file in a text editor (such as Nano or Vim).
    
2. Add the fruits manually, each on a new line.
    
3. Save the file and exit the text editor.
    

Methos 2: By using echo cmd

```bash
echo -e "Apple\nMango\nBanana\nCherry\nKiwi\nOrange\nGuava" >> devops.txt
```

This command appends the fruits to the file, with each fruit on a new line.

1. `echo`: The `echo` command is used to display text or values on the terminal.
    
2. `-e`: This option is specific to the `echo` command and enables the interpretation of backslash escapes. In this case, it allows the interpretation of `\n` as a newline character.
    
3. `"Apple\nMango\nBanana\nCherry\nKiwi\nOrange\nGuava"`: This is the string of text to be echoed. It consists of multiple fruits separated by newline characters (`\n`), ensuring each fruit is on a new line.
    
4. `>>`: The double greater-than symbol (`>>`) is a redirection operator in the shell. It appends the output of the command to the specified file instead of displaying it on the terminal.
    
5. `devops.txt`: This is the filename of the file where the output of the `echo` command will be appended. In this case, it is `devops.txt`.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689628130003/25a97089-2839-4945-ab89-02256c7a91f8.png align="center")

## 7️⃣Task 7

### Show only the top three fruits from the file🥭

To perform the above task we have,

```bash
head -n 3 devops.txt
```

This command displays the first three lines (fruits) from the file.

* `head`: The `head` command is used to display the first few lines of a file or input stream. By default, it displays the first 10 lines of a file.
    
* `-n`: The `-n` option is specific to the `head` command and is used to specify the number of lines to be displayed.
    
* `3`: In this case, `3` is the argument provided after the `-n` option. It specifies that we want to display the first three lines of the file.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689628345159/2ce2c999-ea64-42f6-8ebe-9007d48c8098.png align="center")

## 8️⃣Task 8

### Show only the bottom three fruits from the file🥝

This is similar to the above task-7. Predictable, right?

```bash
tail -n 3 devops.txt
```

This command displays the last three lines (fruits) from the file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689628490930/cf3adc56-c584-4324-9a06-83e49da1ba48.png align="center")

## 9️⃣Task 9

### To create another file Colors.txt and to view the content🧮

This is also what we have done above so I am not explaining this.

```bash
$vi Colors.txt

This file is created to list my fav colors ie Yellow & Blue.
--
--
:wq!
```

```bash
$ cat Colors.txt
This file is created to list my fav colors ie Yellow & Blue.
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689628678613/1ed7c962-1379-49a7-8d56-7da7e03468ad.png align="center")

## 1️⃣0️⃣Task 10

### Add content in Colors.txt (One in each line) - Red, Pink, White, Black, Blue, Orange, Purple, Grey🎨

Again, you know this.

```bash
echo -e "Red\nPink\nWhite\nBlack\nBlue\nOrange\nPurple\nGrey >> Colors.txt
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689629153431/36a0ef78-0b1e-471b-aaaf-c4873b88f37c.png align="center")

## 1️⃣1️⃣Task 11

### To find the difference between fruits.txt and Colors.txt files☯️

To perform the above task, there is a command called diff to see the difference between two files.

```bash
$diff fruits.txt Colors.txt
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689655213438/e1b0c5b9-91f5-4b2f-882e-d6aae891f700.png align="center")

1. To see a side-by-side comparison, use the `-y` option:
    
    ```bash
    $diff -y fruits.txt Colors.txt
    ```
    
2. To see a context-based comparison, you use the `-c` option:
    
    ```bash
    $diff -c fruits.txt Colors.txt
    ```
    
3. To generate a unified diff, you use the `-u` option:
    
    ```bash
    $diff -u fruits.txt Colors.txt
    ```
    

---

Thank you!🖤