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
![Image](/images/ChatLog2.png) 

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

## Part 2 - Researching Commands
**Path to private key**

![Image](/images/private key.png) 

**Path to public key**

