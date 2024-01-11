f# Lab Report 1

## cd command
**1) No Arguments**

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/2d3c6501-5fca-4a9d-af7f-ba1948f48747)

The working directory was the home directory and stayed the home directory.

There was no output because the ``cd`` command takes an argument to change the working directory to the given directory; since there was no argument, the working directory did not change.

The output is *not* an error.

**2) Directory Argument**

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/fd2ab1d2-8056-4c31-b79a-fc0d5ac5da4a)

The working directory was originally the home directory but then changed to be the lecture1 directory.

There was no output because the ``cd`` command successfully changed the working directory. However, at the beginning of the command (in the [user@sahara ~] area) you can see that the working directory has changed.

The output is *not* an error.

**3) File Argument**

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/029c6518-d226-4401-ac86-986cf103cecc)

The working directory was the lecture1 directory and stayed the lecture1 directory.

The output was an error message because we attempted to change directories to the README file, which then caused an error.

The output *is* an error because we attempted to change directories into a file, which is not possible because the README file is not a directory and you can't change directories to a file.
