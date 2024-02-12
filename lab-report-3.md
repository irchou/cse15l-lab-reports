# Lab Report 3

## Part 1 - Bugs
**Failure-inducing input**
```
@Test
public void testReversedFail() {
    int[] input1 = {1, 2, 3, 4, 5};
    assertArrayEquals(new int[]{5, 4, 3, 2, 1}, ArrayExamples.reversed(input1));

    int[] input2 = {1, 1, 2, 2};
    assertArrayEquals(new int[]{2, 2, 1, 1}, ArrayExamples.reversed(input2));
}
```

**Input that doesn't induce failure**
```
@Test
public void testReversedPass() {
    int[] input1 = { };
    assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));

    int[] input2 = {0, 0, 0};
    assertArrayEquals(new int[]{0, 0, 0}, ArrayExamples.reversed(input2));
}
```

**The Symptom**
![Image](/images/ArrayExamplesReversedBugSymptom.png) 

**The Bug**  
Before
```
static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
        arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
}
```
After
```
static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
        newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
}
```

In the original code, the values of the newly created empty array `newArray` were the ones being copied into the original array `arr`. This meant that the original array `arr` got filled with 0's (Java' default intialization value for integers) and the method returned an array of only 0's. To fix this, the order was swapped around so that the values of the original array `arr` became the ones being added to the new empty array `newArray`. Then, after `newArray` is properly filled with the reverse values of `arr`, it gets returned by the method.

## Part 2 - Researching Commands
**Path to private key**

![Image](/images/private key.png) 

**Path to public key**

