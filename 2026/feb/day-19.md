#  Bash Scripting Mastery -- Beginner to Strong Foundation

------------------------------------------------------------------------

#  1. What is Bash?

Bash (Bourne Again Shell) is a command-line interpreter used in Linux
and Unix systems.

It allows you to: - Run commands - Automate tasks - Write scripts -
Control system processes

A **Bash script** is simply a text file that contains multiple Linux
commands written in sequence.

------------------------------------------------------------------------

#  2. Shebang (#!) -- The Most Important First Line

##  What is Shebang?

The shebang is the very first line of a script:

``` bash
#!/bin/bash
```

It tells the operating system:

 "Use this interpreter to run this script."

------------------------------------------------------------------------

##  Why is it Necessary?

When you run:

``` bash
./script.sh
```

Linux: 1. Reads the first line 2. Sees `#!` 3. Uses the interpreter path
after it 4. Executes the script using that interpreter

Without shebang, the system does not know which program should execute
your script.

------------------------------------------------------------------------

##  Best Practice (Professional Way)

``` bash
#!/usr/bin/env bash
```

Why better?

-   It finds bash automatically in your system
-   Works across different Linux systems
-   More portable

 Always prefer this in professional scripts

------------------------------------------------------------------------

#  3. File Permissions -- Why Your Script Doesn't Run

Linux is permission-based.

When you create a script:

``` bash
touch script.sh
```

It cannot run immediately.

------------------------------------------------------------------------

##  Check Permissions

``` bash
ls -l script.sh
```

Example output:

    -rw-r--r-- 1 user user 0 script.sh

This means: - Owner can read & write - Group can read - Others can
read - Nobody can execute

------------------------------------------------------------------------

##  Add Execute Permission

``` bash
chmod +x script.sh
```

Now run:

``` bash
./script.sh
```

------------------------------------------------------------------------

##  Understanding Permission Numbers

  Permission    Value
  ------------- -------
  Read (r)      4
  Write (w)     2
  Execute (x)   1

Example:

``` bash
chmod 755 script.sh
```

755 means:

-   Owner → 7 (4+2+1 = rwx)
-   Group → 5 (4+1 = r-x)
-   Others → 5 (4+1 = r-x)

------------------------------------------------------------------------

#  4. Variables -- Storing Information

Variables store data.

##  Creating Variables

``` bash
name="Ashim"
age=21
```

 Important Rule: No spaces around `=`

Wrong:

``` bash
name = "Ashim"
```

------------------------------------------------------------------------

##  Using Variables

``` bash
echo $name
```

or

``` bash
echo ${name}
```

------------------------------------------------------------------------

##  Taking User Input

``` bash
read -p "Enter your name: " username
echo "Hello $username"
```

------------------------------------------------------------------------

##  Special Variables

  Variable   Meaning
  ---------- ---------------------
  \$0        Script name
  \$1        First argument
  \$#        Number of arguments
  \$@        All arguments
  \$\$       Process ID

Example:

``` bash
echo "Script name: $0"
echo "First argument: $1"
```

Run:

``` bash
./script.sh hello
```

------------------------------------------------------------------------

#  5. Operators -- Making Decisions & Calculations

##  Arithmetic Operators

Used like this:

``` bash
echo $((5 + 3))
```

  Operator   Meaning
  ---------- ----------
  \+         Add
  \-         Subtract
  \*         Multiply
  /          Divide
  \%         Modulus

------------------------------------------------------------------------

##  Numeric Comparison Operators

Used in conditions:

``` bash
if [ $a -gt $b ]; then
    echo "A is greater"
fi
```

  Operator   Meaning
  ---------- ------------------
  -eq        Equal
  -ne        Not equal
  -gt        Greater than
  -lt        Less than
  -ge        Greater or equal
  -le        Less or equal

------------------------------------------------------------------------

##  String Comparison

``` bash
if [ "$name" == "Ashim" ]; then
    echo "Correct"
fi
```

------------------------------------------------------------------------

##  Logical Operators

Used inside double brackets:

``` bash
if [[ $a -gt 5 && $b -lt 10 ]]; then
    echo "True"
fi
```

  Operator   Meaning
  ---------- ---------
  &&         AND
             
  !          NOT

------------------------------------------------------------------------

#  6. Loops -- Repeating Tasks Automatically

Loops help repeat commands.

------------------------------------------------------------------------

##  For Loop

``` bash
for i in {1..5}
do
    echo $i
done
```

This prints numbers 1 to 5.

------------------------------------------------------------------------

##  C-Style Loop

``` bash
for ((i=1; i<=5; i++))
do
    echo $i
done
```

------------------------------------------------------------------------

##  While Loop

``` bash
count=1

while [ $count -le 5 ]
do
    echo $count
    ((count++))
done
```

Runs while condition is true.

------------------------------------------------------------------------

##  Until Loop

``` bash
count=1

until [ $count -gt 5 ]
do
    echo $count
    ((count++))
done
```

Runs until condition becomes true.

------------------------------------------------------------------------

#  Final Professional Example

``` bash
#!/usr/bin/env bash

read -p "Enter first number: " num1
read -p "Enter second number: " num2

sum=$((num1 + num2))

if [[ $sum -gt 100 ]]; then
    echo "Large number: $sum"
else
    echo "Result: $sum"
fi

for i in {1..3}
do
    echo "Loop number $i"
done
```

------------------------------------------------------------------------

#  What You Have Mastered

✅ Shebang\
✅ File Permissions\
✅ Variables\
✅ Operators\
✅ Loops


