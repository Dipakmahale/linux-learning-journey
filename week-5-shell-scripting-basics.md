
# 🐧 Week 5: Shell Scripting Basics  

Welcome to **Week 5** of my Linux learning journey!  
This week, I stepped into one of the most powerful areas of Linux — **Shell Scripting** — where automation, logic, and control come together.  

---

## ⚙️ What is Shell Scripting?  

A **shell script** is a file that contains a series of Linux commands that the shell executes sequentially.  
Shell scripting helps in automating repetitive tasks such as file backups, user management, service restarts, and more.  

---

## 🧾 Basic Shell Commands  

```bash
echo $0         # shows current shell (e.g., bash)
echo $SHELL     # shows default shell (e.g., /bin/bash)
echo $PATH      # shows directories searched for executable files


✍️ Creating Your First Shell Script
vim a.sh

#!/bin/bash
echo "date"            # prints the word 'date'
echo "$(date)"         # executes and prints the actual date
touch a
useradd -s /sbin/nologin sarah

chmod +x a.sh          # make it executable
./a.sh                 # execute it


🌍 Variables in Shell Scripting

🟡 Local Variables
Local variables are defined by users and exist only within the shell session.

var1=25
name="Savita"
echo "My age is $var1"
echo "My name is $name"

🟢 Environmental Variables
Predefined by the system to store environment-related information.

echo "Current user: $USER"
echo "Home directory: $HOME"


💡 Environment variables are declared in /etc/bashrc.
To make a variable permanent, add it to .bashrc and use:

export var1=25

🧮 Arithmetic Operations

expr 10 + 3      # 13
expr 10 \* 3     # 30 (escape * with backslash)
expr 10 / 3      # 3
⚠️ Always put spaces between operands and operators in expr.

🔀 Conditional Statements (if–else)
Conditionals add logic and decision-making to your script.

vim inter.sh

#!/bin/bash
echo "Hello! Kindly mention your name:"
read p

if grep -w "$p" /etc/passwd &> /dev/null
then
    echo "Hi $p, welcome to system $(hostname)"
else
    echo "Hi $p, you are not our user"
fi


chmod +x inter.sh
./inter.sh

🔁 Loops in Shell Scripting

1️⃣ Simple For Loop
#!/bin/bash
for n in a b c
do
   echo $n
done

2️⃣ Range-Based For Loop
#!/bin/bash
for n in {1..5}
do
   echo $n
done

3️⃣ Array-Based For Loop
#!/bin/bash
s=("football" "cricket" "hockey")
for n in ${s[@]}
do
   echo $n
done

4️⃣ C-Style For Loop
#!/bin/bash
n=7
for (( i=1; i<=$n; i++ ))
do
   echo $i
done

5️⃣ Infinite For Loop (with break)
#!/bin/bash
n=4
for (( ; ; ))
do
   if [ $n -eq 9 ]; then
       break
   fi
   echo $n
   ((n=n+1))
done

🔄 While Loop
#!/bin/bash
x=1
while [ $x -le 5 ]
do
   echo "Welcome $x times"
   x=$((x + 1))
done


⚙️ Challenges I Faced
Remembering syntax for arithmetic and escaping special characters
Understanding difference between local and environment variables
Debugging missing spaces in if–else blocks
Practicing different loop structures efficiently

