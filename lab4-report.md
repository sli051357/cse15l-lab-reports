# Lab Report 4

## Step 4

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/86a66e69-e791-4c43-8480-d5a6ea3cb406)

I used the command `ssh sal075@ieng6.ucsd.edu <enter>` to log in to my ieng6 account. The `ssh` command establishes a remote connection to a remote computer instead of my own, `sal075@ieng6.ucsd.edu` is the account name (or my email address), and the `<enter>` command runs the command.

## Step 5

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/bf1159e0-1668-4752-9223-0ca5f1e20c2d)

I used the command `git clone git@github.com:sli051357/cse15l-lab7.git <enter>` to clone the correct repository to my workspace. `git clone` copies the contents of the `cse15l-lab7` repository to the SSH workspace, while `git@github.com:sli051357/cse15l-lab7.git` is the `SSH` URL of the forked repository. The `<enter>` command then runs the command.

## Step 6

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/67d35094-2325-4d76-a581-2179333b39f7)

I first used the command `cd cse15l-lab7 <enter>` to enter the `cse15l-lab7` directory that I had just cloned. I then used the `ls <enter>` command to see what files were available in the directory, which included `test.sh`, or the bash script that I needed to run to run the tests. Then, I used `bash test.sh <enter>` to run the test itself, which gave me the output that told me there were errors.

## Step 7

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/4da41860-5234-4e76-b435-5c745758f4e4)

To open the test file, I entered the command `vim ListTestExamples.java <enter>`, which opened `ListExamples.java` in vim so I could edit it.

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/24ddbd63-b342-4a18-9b09-b7884e894e93)

First, I used `<:><4><2>` to jump to the beginning of line 42, which was where the line to be changed was. I then did `<l><l><l><l><l>` to move to the specific character `1` in `index1`. Then, I pressed `<x>` to delete the character, `<i>` to enter insert mode, `<2>` to insert the character `2` (in order to change the word from `index1` to `index2`, and then `esc` to exit insert mode and return to normal mode. I then entered `<:><w><q><enter>` to save and exit the file.

## Step 8

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/4ea8d583-1e5f-423a-a125-40123dbd06ff)

To run the tests again, I typed `<up><up><up><enter>` because in the history of commands, the `bash test.sh` command was three commands in the past. Once I reached the `bash test.sh` command, I pressed `<enter>` to run it again.

## Step 9
![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/d79a177f-785f-4833-bf0c-63d0b3987cb8)

First, I ran the command `git add ListExamples.java <enter>` which adds the file `ListExamples.java` to the list of files to be changed (or staging the changes). I then ran the command `git commit` to commit the changes to the repository, which opened up a file in vim that included a commit message.

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/07c50d7f-4072-471a-8635-dbf309ac3f90)

To edit this file, I pressed `<i>` to enter insert mode and edited `ListExamples.java` by inserting a commit message (specifically `changed ListExamples.java`). I then pressed `<esc>` to exit insert mode and return to normal mode, and then entered `<:><w><q><enter>` to save the file and exit. I then entered the command `git push <enter>` to push the changes to the repository, finishing the tasks.
