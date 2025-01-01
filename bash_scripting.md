## Shell Scripting

Scripts end in the `.sh` filename. You can create a basic script using:

```bash
nano script_name.sh
```

All scripts should start from `shebang`, which means including the following at the top of your script:

```bash
#!/bin/bash
```

### Variables

```bash
echo "Whats your name"
read name
echo "Welcome, $name"
```

To give a script execution permissions, we can type:

```bash
chmod +x script_name.sh

./script_name.sh            // execute script
```

### Loops

```bash
#!/bin/bash
for i in {1..10}
do
echo $i
done
```

### Conditional Statements

```bash
#!/bin/bash
echo "Please enter your name first:"
read name
if [ "$name" = "Stewart" ]; then
        echo "Welcome Stewart! Here is the secret: THM_Script"
else
        echo "Sorry! You are not authorized to access the secret."
fi
```

### Comments

```bash
# this is a comment
```

### Authentication Example

```bash
#!/bin/bash

# Defining the variables
username=""
companyname=""
pin=""

# Defining the loop
for i in {1..3}; do
# Defining the conditional statements
        if [ "$i" -eq 1 ]; then
                echo "Enter your Username:"
                read username
        elif [ "$i" -eq 2 ]; then
                echo "Enter your Company name:"
                read companyname
        else
                echo "Enter your PIN:"
                read pin
        fi
done

# Checking if the user entered the correct details
if [ "$username" = "John" ] && [ "$companyname" = "Tryhackme" ] && [ "$pin" = "7385" ]; then
        echo "Authentication Successful. You can now access your locker, John."
else
        echo "Authentication Denied!!"
fi
```
