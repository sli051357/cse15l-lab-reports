# Lab Report 3

## Part 1
I chose to work on the bug in the `ArrayTests` file, specifically for the one in the `reversed` method.

This is a failure-inducing input for the buggy program:
```java
@Test 
  public void testReversed2() {
    int[] input1 = new int[]{1, 2, 3};
    assertArrayEquals(new int[]{3, 2, 1}, ArrayExamples.reversed(input1));
  }
```

This is an input that does not induce a failure:
```java
@Test 
  public void testReversed3() {
    int[] input1 = new int[]{0, 0, 0};
    assertArrayEquals(new int[]{0, 0, 0}, ArrayExamples.reversed(input1));
  }
```

This is the symptom (or output of running the tests):
![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/94eecf1b-1f3f-48a3-8970-fa754ea1f498)
Note: I put the commands to compile and run the test file in a bash script, which is the first command I put into the terminal (`bash test.sh`)

This is the original code of the `reversed` method:
```java
static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```

This is the fixed code:
```java
static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }
```
The specific change that was made was that instead of assigning elements in `arr` to elements in `newArray` (which could have been 0), the code was fixed to assign elements in `newArray` to those of `arr`, since that would copy over the existing elements in the correct order to the new array. Then, instead of returning the old `arr` array, we returned `newArray` because it would have the correctly updated elements.

## Part 2 - The `grep` command

All commands and options were taken from the following site: https://www.geeksforgeeks.org/grep-command-in-unixlinux/

**`-c` option**

The `-c` option prints a count of the lines that match a given pattern.

Example 1:
```bash
sarah@LAPTOP-QRLQI3VA MINGW64 ~/College/CSE 15L/Lab 4/docsearch (main)
$ grep -c "base pair" technical/plos/journal.pbio.0020190.txt
2
```
This command is used to find the number of times that the string `"base pair"` is used in the file `technical/plos/journal.pbio.0020190.txt` (we know this file has the given string because that was one of the tasks from this lab). The command returns `2`, or the number of times `"base pair"` appears, but it does not tell us where in the file the string is. This is useful because if a file mentions a certain string many times, we could look at it and see its contents, since they would probably be more helpful than a text file that barely mentions the string.

Example 2:
```bash
sarah@LAPTOP-QRLQI3VA MINGW64 ~/College/CSE 15L/Lab 4/docsearch (main)
$ grep -r -c "base pair" technical/plos
technical/plos/journal.pbio.0020001.txt:0
technical/plos/journal.pbio.0020010.txt:0
technical/plos/journal.pbio.0020012.txt:0
technical/plos/journal.pbio.0020013.txt:0
technical/plos/journal.pbio.0020019.txt:0
technical/plos/journal.pbio.0020028.txt:0
technical/plos/journal.pbio.0020035.txt:0
technical/plos/journal.pbio.0020040.txt:0
technical/plos/journal.pbio.0020042.txt:0
technical/plos/journal.pbio.0020043.txt:0
technical/plos/journal.pbio.0020046.txt:0
...
technical/plos/pmed.0020249.txt:0
technical/plos/pmed.0020257.txt:0
technical/plos/pmed.0020258.txt:0
technical/plos/pmed.0020268.txt:0
technical/plos/pmed.0020272.txt:0
technical/plos/pmed.0020273.txt:0
technical/plos/pmed.0020274.txt:0
technical/plos/pmed.0020275.txt:0
technical/plos/pmed.0020278.txt:0
technical/plos/pmed.0020281.txt:0
```
This command recursively goes through every file in the `technical/plos` directory (thanks to the `-r` option) and checks if they have any lines with the string `"base pair"`. It then returns how many lines in the file have `"base pair"` (in this case, most of them have none). This command also prints out every single file in `technical/plos`, but I shortened it so that this lab writeup wouldn't take up 10 pages just on a singular output. This is useful because it lets you see which files have the specified term and which ones don't without needing to print out the contents of the files.

**`-h` option**

The `-h` option lists out the lines containing a certain string without specifying which file it is from.

Example 1:
```bash
sarah@LAPTOP-QRLQI3VA MINGW64 ~/College/CSE 15L/Lab 4/docsearch (main)
$ grep -r -h "base pairs" technical/plos
        sequence, which is a specific series of eight base pairs in the DNA of the bacterial
        chromosomes, on the order of one or two thousand base pairs of DNA (or less—their length is
```
This command recursively goes through every file in the `technical/plos` directory and checks if there are any lines with the string `"base pair"`. If there are, it prints those lines, but does not specify where the line is from. This can be useful if you know the words you want to search for in a file and want a little bit of context to how it is used, instead of needing to print out the entire file.

Example 2:
```bash
sarah@LAPTOP-QRLQI3VA MINGW64 ~/College/CSE 15L/Lab 4/docsearch (main)
$ grep -h "weight" technical/biomed/1468-6708-3-1.txt
        Older adults are frequently counseled to lose weight,
        even though there is little evidence that overweight is
        Many healthy older adults report gradual weight gain
        gradual weight gain is normative and associated with the
        weight standards be adjusted upwards for age [ 8 ] . Such
        ...
        'overweight' by the NHLBI guidelines. This suggests using
        obese or underweight older adults, and discouraging trials
        that address older adults who are merely overweight.
```
This command goes through the `technical/biomed/1468-6708-3-1.txt` file and searches up every instance of `"weight"`, before printing each line that contains it in the terminal (once again, I shortened the output so it wouldn't eat up half of my lab writeup). What is interesting about this is that words that contain the term `"weight"`, such as `"overweight"` and `"underweight"`, are also printed and included in the output, which explains that `grep` only looks for any instance of the string and not necessarily the string as a singular word.

**`-o` option**

The `-o` option prints out the matching part of each line that contains a specified string.

Example 1:
```bash
sarah@LAPTOP-QRLQI3VA MINGW64 ~/College/CSE 15L/Lab 4/docsearch (main)
$ grep -o "base pair" technical/plos/journal.pbio.0020190.txt
base pair
base pair
```
This command goes through the `technical/plos/journal.pbio.0020190.txt` file and prints out the exact times it finds the string `"base pair"`. Since both occurrences of `"base pair"` are specifically used in the word `"base pair"` there isn't much this command does except give us visual evidence that `"base pair"` is found twice within this file.

Example 2:
```bash
sarah@LAPTOP-QRLQI3VA MINGW64 ~/College/CSE 15L/Lab 4/docsearch (main)
$ grep -o "weight" technical/biomed/1468-6708-3-1.txt
weight
weight
weight
...
weight
weight
weight
```
Similar to the previous command, this command goes through the `technical/biomed/1468-6708-3-1.txt` file and prints out every occurrence of the string `"weight"`. What's interesting is that from using `grep -h`, we know that the string `"weight"` is also counted in words that use `"weight"`, such as `"overweight"` and `"underweight"`. However, when using `-o`, only the exact part of the word (`"weight"`) is printed out, instead of the entire word. This could be more useful when used with other commands to specify where the string is found or other variables, but used by itself, it doesn't seem to be very helpful or useful, other than using it to count how many times a certain string is found in a file.

**`-w` option**

The `-w` option prints out every instance of the specified string is used a word.

Example 1:
```bash
sarah@LAPTOP-QRLQI3VA MINGW64 ~/College/CSE 15L/Lab 4/docsearch (main)
$ grep -w "weight" technical/biomed/1468-6708-3-1.txt
        Older adults are frequently counseled to lose weight,
        Many healthy older adults report gradual weight gain
        gradual weight gain is normative and associated with the
        weight standards be adjusted upwards for age [ 8 ] . Such
        trials of weight modification might be more successful if
        would yield more powerful evaluations of weight
        ...
          underlying conditions that caused the low weight) could
          be more sensitive to change in weight than EVGFP. If YHL
          differences between the overweight and normal weight
        Recommendations for desirable weight have been
        determine desirable weight guidelines should include
```
In previous commands, I noted how using `"weight"` as the given string caused words such as `"overweight"` and `"underweight"` to also be printed out, since the string `"weight"` was part of the word. However, by using `-w`, only the lines with the specific word `"weight"` were printed out, which can be useful when you only want to see the specific places where the word specifically is used.

Example 2:
```bash
sarah@LAPTOP-QRLQI3VA MINGW64 ~/College/CSE 15L/Lab 4/docsearch (main)
$ grep -r -w "science" technical/plos
technical/plos/journal.pbio.0020001.txt:        the clear inequalities in science between developing and developed countries and to the
technical/plos/journal.pbio.0020001.txt:        importance of reducing the inequalities in science between developed and developing
technical/plos/journal.pbio.0020001.txt:        It is rather obvious that richer countries are able to invest more resources in science
technical/plos/journal.pbio.0020001.txt:        contributions to science, despite the fact that the average proportion of gross domestic
technical/plos/journal.pbio.0020001.txt:        product (GDP) invested in science in Latin America throughout this 10-year period was only
technical/plos/journal.pbio.0020001.txt:        productivity is remarkable when we compare it with the relatively low investment in science
technical/plos/journal.pbio.0020001.txt:        rate as well as in financial investment in science and technology. Some countries have
technical/plos/journal.pbio.0020001.txt:        funding to the most productive scientists from the national science development programs
...
technical/plos/pmed.0020209.txt:            “propaganda” than science.
technical/plos/pmed.0020209.txt:            she came to know over the years, had no science background at all.
technical/plos/pmed.0020209.txt:            say,” it was marketing, not science, that dominated. One of the techniques used by drug
technical/plos/pmed.0020212.txt:        mellitus, obesity, and Alzheimer's disease. These “discovery science” approaches have been
technical/plos/pmed.0020232.txt:        proof be used in science and science-based policy? Where should the burden of proof
technical/plos/pmed.0020232.txt:        Scientific assessments for policy should summarize the best state of the science,
```
When used in combination with `-r`, the `grep` command goes through every file in `technical/plos` and prints out the lines where the word `"science"` specifically appears. It also specifies which file the line comes from (although it doesn't specify the specific line). This can be useful to find the occurrence of a specific word throughout a directory, especially if you only want to find the specific word and not words that also happen to contain the specified word.
