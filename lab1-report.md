# Lab Report 1

## `cd` command
**1) No Arguments**

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/2e132d6a-ab3b-4b9d-b1bb-0fba36446ea4)

The working directory was the `messages` directory and turned into the `home` directory.

There was no output because the ``cd`` command takes an argument to change the working directory to the given directory; since there was no argument, the working directory changed to the outermost directory, or the `home` directory.

The output is *not* an error.

**2) Directory Argument**

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/fd2ab1d2-8056-4c31-b79a-fc0d5ac5da4a)

The working directory was originally the `home` directory but then changed to be the `lecture1` directory.

There was no output because the ``cd`` command successfully changed the working directory. However, at the beginning of the command (in the `[user@sahara ~]` area) you can see that the working directory has changed.

The output is *not* an error.

**3) File Argument**

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/029c6518-d226-4401-ac86-986cf103cecc)

The working directory was the `lecture1` directory and stayed the `lecture1` directory.

The output was an error message because we attempted to change directories to the `README` file, which then caused an error.

The output *is* an error because we attempted to change directories into a file, which is not possible because the `README` file is not a directory and you can't change directories to a file.

---

## `ls` command
**1) No Arguments**

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/9d8a5943-b505-4cef-b6f4-7fcab5cab0b8)

The working directory was the `lecture1` directory. 

The output was a list of all the files in the `lecture1` directory, including directories.

The output is *not* an error.

**2) Directory Argument**

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/94954b63-29b6-4c77-98ef-5e8d41f7f643)

The working directory was the `lecture1` directory.

The output was a list of all the files inside the `messages` directory, since we passed that directory as an argument to the command.

The output is *not* an error.

**3) File Argument**

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/88d8a0c1-70b3-4b59-9e8a-826e33acae53)

The working directory was the `lecture1` directory.

The output was just the `README` file (but just the name) because it was a list of the `README` file (since the output could be considered a list of a singular file).

The output is *not* an error.

---

## `cat` command
**1) No Argument**

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/c09c7075-4e6c-4fab-b218-a5a76a0e4bc4)

The working directory was the `lecture1` directory.

There was no output because passing no arguments into the `cat` command means that it would just repeat anything that is entered into the terminal and unless the command is exited out of it, this will continue indefinitely.

The output is *not* an error (even though you can't do anything else until you exit the command).

**2) Directory Argument**

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/8aba7e2b-1f23-49cf-99eb-b92d69e8e35f)

The working directory was the `lecture1` directory.

The output was an error message that specified that the `messages` directory was not a file.

The output *is* an error because the `cat` command expected a file argument but received a directory instead, which caused an error because you can't print out the specific data inside the directory.

**3) File Argument**

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/5030bb3d-73c0-496c-ba2a-160f089e53d9)

The working directory was the `lecture1` directory.

The output was the contents of the `README` file; if you opened up the `README` file and looked inside, the contents would be the same as the output.

The output is *not* an error.
