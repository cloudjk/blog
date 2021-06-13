---
title: Shell Scripting Basic
sidebar: mydoc_sidebar
permalink: linux_shell_scripting_basic.html
folder: linux
---
## Check shell type operating system supports.

```bash
  cat /etc/shells
```

## Where bash is located

```bash
  which bash
```

## How to make a bash file

```bash
#! /bin/bash
echo "Hello World"  
```

## How to run a bash file
 ```bash
 ./hellow.sh
 ```

## How to write a comment
```bash
#! /bin/bash
# This is a comment
echo 'Hello World' # This is a comment
```

## How to use environment variables and user variables
```bash

# This is environment variables
echo $BASH
echo $PWD

# This is user variables
name=Mark
echo The name is $name
val=10
echo The value is $val
```
## Read user input
```bash
# one user input
echo "Enter name : "
read name
echo "Name : $name"

# multiple user input
echo "Enter names : "
read name1 name2 name3
echo "Names : $name1, $name2, $name3"

# display user input in the same line
read -p 'username: ' user_Var   # -p : allow user to enter input in the same line
read -sp 'password : ' pass_var   # -s : silent flag : do not show password info
echo    # This prevents from showing input user name in the same line with password
echo "username: $user_var"
echo "password: $pass_var"

# array user input
echo "Enter names : "
read -a names
echo "Names : ${names[0]}, ${names[1]}"  # user curly braces when the type is array !!!

# user input without read variable
echo "Enter name: "
read
echo "Name : $REPLY"
```

## Passing arguments to a Bash Script
```bash
# when arguments are not array, then $0 shows the shell you are running.
echo $0 $1 $2 $3

# when arguments are array, index 0 shows first argument not shell
args=("$@")
echo ${args[0]} ${args[1]} ${args[2]} ${args[3]}

# how to pass arguments
./a.sh a b c

# displays all arguments
echo $@ 

# display the number of arguments
echo $#
```

## If statement
```bash
# if format
if [ condition ]
then
  statement
fi

# Integer comparision

-eq - is equal to - if [ "$a" -eq "$b" ]
-ne - is not equal to - if [ "$a" -ne "$b" ]
-gt - is greater than - if [ "$a" -gt "$b" ]
-ge - is greater than or equal to - if [ "$a" -ge "$b" ]
-lt - is less than - if [ "$a" -lt "$b" ]
-le - is less than or equal to - if [ "$a" -le "$b" ]
< - is less than - (("$a" < "$b"))
<= - is less than or equal to - (("$a" <= "$b"))
> - is greater than - (("$a" > "$b"))
>= - is greater than or equal to - (("$a" >= "$b"))

# String comparision

= - is equal to - if [ "$a" = "$b" ]
== - is equal to - if [ "$a" == "$b" ]
!= - is not equal to - if [ "$a" != "$b" ]
< - is less than, in ASCII alphabetical order - if [[ "$a" < "$b" ]]
> - is greater than, in ASCII alphabetical order - if [[ "$a" > "$b" ]]
-z - string is null, that is, has zero length

word=a

if [[ $word == "b"]]
then
  echo "condition b is true"
elif [[ $word == "a"]]
then
  echo "condition a is true"
else
  echo "condition is false"
fi

```
## File Test Operators
```bash
# -e : enable the interpreation of backslash and put the cursor in the same line.
echo -e "Enter the name of the file : \c"    
read file_name

# -e : check whether file exists
# -f : check whether file is regular file [regular file : text or binary data in contast to directrories, symbolic link and sockets ]
# -d : check whether directory exists
# -b : check wheter binary file exists
# -c : check wheter text file exits
# -s : check wheter file is empty
# -r : check whter file has read permission
# -w : check wheter file has write permission
# -x : check whter file has execute permission

if [ -e $file_name ]
then
  echo "$file_name found"
else
  echo "$file_name not found"
fi

```

## How to append output to the end of text file
```bash
#! /bin/bash

echo -e "Enter the name of the file : \c"
read file_name

if [ -f $file_name ]
then
  if [ -w $file_name ]
  then
    echo "Type some text data. To quit press ctrl + c."
    cat >> $file_name
  else
    echo "The file does not have a write permission"
  fi
else
  echo "$file_name not exists"
fi
```

## Logical 'And' Operator
```bash
#! /bin/bash

# if [ condition A ] && [ condition B ]
# if [ condition A -a condition B ]
# if [[ condition A && condition B ]]

age=50
if [ "$age" -gt 18 ] && [ "$age" -lt 30 ]
if [ "$age" -gt 18 - a "$age" -lt 30 ]
if [[ "$age" -gt 18 && "$age" -lt 30 ]]
then
  echo "Valid age"
else
  echo "Invalid age"

```

## Logical 'Or' Operator
```bash
#! /bin/bash

# if [ condition A ] || [ condition B ]
# if [ condition A -o condition B ]
# if [[ condition A || condition B ]]

age=50
if [ "$age" -gt 18 ] || [ "$age" -lt 30 ]
if [ "$age" -gt 18 - o "$age" -lt 30 ]
if [[ "$age" -gt 18 || "$age" -lt 30 ]]
then
  echo "Valid age"
else
  echo "Invalid age"

```

## Arithmetic Operator
```bash
#! /binm/bash

num1=20
num2=5

# First way
echo $(( num1 + num2 )))
echo $(( num1 - num2 )))
echo $(( num1 * num2 )))
echo $(( num1 / num2 )))
echo $(( num1 % num2 )))

# Second way
echo $( expr $num1 + $num2 )
echo $( expr $num1 - $num2 )
echo $( expr $num1 \* $num2 )
echo $( expr $num1 / $num2 )
echo $( expr $num1 % $num2 )
```


## Floating Math operaions
```bash
#! /bin/bash

User bc (basic calculator library - type man bc to check whether the library is installed)

num1=20.5
num2=5

echo "$num1+$num2" | bc
echo "$num1-$num2" | bc
echo "$num1*$num2" | bc
echo "$num1/$num2" | bc <= wrong
echo "$num1%$num2" | bc

# By using scale, we can expect exact outcome from division and it also restrict floating number.
echo "scale=2;$num1/$num2"

# To use math library like sqrt, pow.. use "| bc -l" and -l stands for library

echo "scale=2;sqrt($num1)" | bc -l
echo "scale=2;3^3" | bc -l

```

## Case statement
```bash
#! /bin/bash

case expression in
  pattern1 )
    statements ;;
  pattern2 )
    statements ;;
  ...
esac

# Real example
vehicle=$1
case $vehicle in
  "car" )
    echo "Rented $vehicle is 500" ;;
  "truck" )
    echo "Rented $vehicle is 400" ;;
  "convertible" )
    echo "Rented $vehicle is 2000" ;;
  * )
    echo "Unkonwn Vehicle" ;;
esac
```

## Case statement with pattern
```bash

echo -e "Enter some character : \c"
read value

case $value in
  [a-z] )
    echo "User entered $value a to z" ;;
  [A-Z] )
    echo "User entered $value A to Z" ;;
  [0-9] )
    echo "User entered $value 0 to 9" ;;
  ? )
    echo "User entered $value special character" ;;
  * )
    echo "Unkown input" ;;
esac

# If A-Z is not implemented as it is expected then run LANG=C in command
# LANG environment variable indicates that the language/locale and encoding, where "C" is the language setting.
```

## Array variables
```bash
#! /bin/bash

# Declare array
os=('ubuntu' 'window' 'mac')

# Add, Update, Delete
os[3]='android'
os[0]='linux'
unset os[2]

# get array value(s), indices, length
echo "${os[@]}"
echo "${os[0]}"
echo "${!os[@]}"
echo "${#os[@]}"

# get value which is not array using array
string=asklfjdkdlsjf
echo "${string[@]}" : return asklfjdkdlsjf
echo "${string[0]}" : return asklfjdkdlsjf
echo "${string[1]}" " return blank line

# Array variables ignore position so if we add variable in 100 index it will be printed just next to the last index saved before 100.
# Some memebers of array can be uninitialized and gaps in array are okay.
```

## While loops
```bash
#! /bin/bash

n=1

while [ $n -le 10 ]
do
    echo "$n"
    n=$(( n+1 ))
done

while (( $n <= 10 ))
do
  echo "$n"
  (( n++ ))
  sleep 1
done

# sleep 1 : sleep for 1 second 
```

## Read a file content
```bash
#! /bin/bash

while read p
do
  echo $p
done < readFile.sh

cat readFile.sh | while read p
do
  echo $p
done

while IFS= read -r line  #Internal File seperator. -r option is for escaping backslash interpretion
do
  echo $line
done < readFile.sh
```

## Until loop
```bash
#!/bin/bash
n=1

until [ $n -ge 10 ]
do
  echo $n
  n=$(( n+1 ))
done

n=1

until (( $n > 10 ))
do
  echo $n
  (( n++ ))
done
```

## For loop
```bash
#!/bin/bash

echo ${BASH_VERSION}
for i in {0..10}  # above bash version 3.0, {START..END..INCREMENT} # above 4.0
do
  echo $i
done

for (( i=0;i<10;i++ ))
do
  echo $i
done
```

## For loop to execute commands
```bash
#!/bin/bash

for command in ls pwd date
do
  echo "----------------$command----------------"
  echo $command
done

for item in *
do
  if [ -d $item ]
  then
    echo $item
  elif
  then
    echo $item
  fi
done

```

## Select loop
This is used to show menu and select one of the options.
```bash
#!/bin/bash

select name in john ben mark tom
do
  echo "$name selected"
done

select name in john ben mark tom
do
  case $name in
  john)
    echo "john selected"
    ;;
  ben)
    echo "ben selected"
    ;;
  mark)
    echo "mark selected"
    ;;
  tom)
    echo "tom selected"
    ;;
  *)
    echo "Error please provied the no between 1..4"
  esac
done

```

## Break and Continue
```bash
#!/bin/bash

for (( i=0; i<10; i++ ))
do
  if [[ $i > 5 ]]
  then
    break
  fi
  echo "$i"
done

for (( i=0; i<10; i++))
do
  if [[ $i == 3 || $i == 6 ]]
  then
    continue;
  fi
  echo $i
done
```

## Functions
```bash
#!/bin/bash

function print(){ # function can be omitted
  echo $1 $2 $3
}

quit() {
  exit
}

print Hellow World Again
quit
```
```bash
#!/bin/bash

usage() {
  echo "You need to provide an argument : "
  echo "usage : $0 file_name"
}

is_file_exist() {
  local file="$1"
  [ -f "$file" ] && return 0 || return 1
}

[ $# == 0 ] && usage  # $# : number of arguments

if ( is_file_exist "$1" ) {
  then
    echo "File found"
  else
    echo "File not found"
fi
}
```

## Local variables
```bash

function print() {
  local name=$1
  echo "the name is $name"
}

name="Tom"

echo "The name is $name : Before"

print Max

echo "The name is $name : After"
```

## Readonly
```bash
#!/bin/bash
var=31

readonly var

var=50 # provoke an error
```
```bash
#!/bin/bash
hello() {
  echo "Hello World"
}

readonly -f hello

hello() {
  echo "Hello World Again" # raise an error
}

readonly # show readonly variables
readonly -p # same result with readonly

# show readonly functions
readonly -f

```

## Signals and Traps
Most used **SIGNALS** : SIGINIT(Ctrl + C), SIGKILL(KILL -9 Pid), SIGTSTP(Ctrl + Z)  
**TRAP** Command provides the script to capture and interrupt and then clean it up within the script. (can use either value or command)
```bash
man signal

#!/bin/bash
echo pid is "$$"  // "$$" show running process id
while (( COUNT < 10 ))
do
  sleep 10
  (( COUNT++ ))
  echo $COUNT
done
exit 0  # success signal
```
```bash
#!/bin/bash
trap "echo Exit command is detected" 0  # whenever we receive signal 0, execute command in ""

echo "Hello World" 

exit 0
```
```bash
#!/bin/bash 
trap "echo Exit signal is detected" SIGINT # TRAP is unable to cache SIGKILL AND SIGSTOP signals

echo "pid is $$"
while (( COUNT < 10 ))
do
  sleep 10
  (( COUNT++ ))
  echo $COUNT
done
exit 0
```
You can do some cleanup after task is finished or interrupted using **Trap**
```bash
#!/bin/bash
file=/Users/jinyong/www/ryan/bash-shell/hello.sh
trap "rm -f $file && echo file deleted;exit 0" 0 2 15

echo "pid is $$"
while (( COUNT < 10 ))
do
  sleep 10
  (( COUNT++ ))
  echo $COUNT
done
exit 0
```
```bash
trap # list all traps
trap - 0 2 15 # remove traps
```

## debug
There are 3 ways to debug bash
```bash

# first way to debug bash by running a command
bash -x ./hello.sh 

# second way by using -x option
#!/bin/bash -x
file=/Users/jinyong/www/ryan/bash-shell/hello.sh
trap "rm -f $file && echo file deleted;exit 0" 0 2 15

echo "pid is $$"
while (( COUNT < 10 ))
do
  sleep 10
  (( COUNT++ ))
  echo $COUNT
done
exit 0

# third way by using set option
#!/bin/bash
set -x  # activate debugging
file=/Users/jinyong/www/ryan/bash-shell/hello.sh

set +x # deactivate debugging
trap "rm -f $file && echo file deleted;exit 0" 0 2 15

echo "pid is $$"
while (( COUNT < 10 ))
do
  sleep 10
  (( COUNT++ ))
  echo $COUNT
done
exit 0
```