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
