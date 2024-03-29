# Lab Report 5
## Part 1
### Student
Student: I'm testing my merge method for ListExamples, but I'm getting a timeout error for just one of the tests. Since this is a timeout error, I think the bug might have to do with wrong incrementing of the loop variables. However, I double-checked my merge method and it seems like both index variables are being updated when they should be?
This what my terminal shows after running `bash test.sh`.  
![Image](/images/bug.png) 

Here's my file directory and the contents of potentially relevant files:  
**File directory**
```
lab7/
|- lib/
	|- hamcrest-core-1.3.jar
	|- junit-4.13.2.jar
|- ListExamples.class
|- ListExamples.java
|- ListExamplesTests.class
|- ListExamplesTests.java
|- StringChecker.class
|- test.sh
```
**ListExamples.java**
```
import java.util.ArrayList;
import java.util.List;

interface StringChecker { boolean checkString(String s); }

class ListExamples {
  // Returns a new list that has all the elements of the input list for which
  // the StringChecker returns true, and not the elements that return false, in
  // the same order they appeared in the input list;
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(s);
      }
    }
    return result;
  }

  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else if(list1.get(index1).compareTo(list2.get(index2)) > 0)  {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      // change index1 below to index2 to fix test
      index2 += 1;
    }
    return result;
  }

}
```
**ListExamplesTests.java**
```
import static org.junit.Assert.*;
import org.junit.*;
import java.util.*;
import java.util.ArrayList;

public class ListExamplesTests {
	@Test(timeout = 500)
	public void testMerge1() {
    	List<String> l1 = new ArrayList<String>(Arrays.asList("x", "y"));
		List<String> l2 = new ArrayList<String>(Arrays.asList("a", "b"));
		assertArrayEquals(new String[]{ "a", "b", "x", "y"}, ListExamples.merge(l1, l2).toArray());
	}
	
	@Test(timeout = 500)
        public void testMerge2() {
		List<String> l1 = new ArrayList<String>(Arrays.asList("a", "b", "c"));
		List<String> l2 = new ArrayList<String>(Arrays.asList("c", "d", "e"));
		assertArrayEquals(new String[]{ "a", "b", "c", "c", "d", "e" }, ListExamples.merge(l1, l2).toArray());
        }

}
```
**test.sh**
```
javac -cp ".;lib/hamcrest-core-1.3.jar;lib/junit-4.13.2.jar" *.java
java -cp ".;lib/hamcrest-core-1.3.jar;lib/junit-4.13.2.jar" org.junit.runner.JUnitCore ListExamplesTests
```

### TA
TA: Yes, you are correct about the bug being caused by issues with the loop variables. You might want to check if the loop variables are guaranteed to be updated in each of the loops, more specifically ensure that the index variables are being incremented in each if-else branch of the loops. Also, note the differences between what's being tested in the two test methods. The second test method is testing for something the first one doesn't include, which is what is triggering the bug.

### Student
Student: Thank you, I looked at the if-else statements in the first while loop of my merge method and realized that incrementing the index variables in the if and else if branches did not guarantee that an index variable would be updated because my conditions didn't catch the possibility of two strings being equal to each other. I fixed the bug by switching the else if statement into just an else branch, so that the loop variable would still be updated when `list1.get(index1).compareTo(list2.get(index2)) == 0`. My merge method now passes both tests.  
![Image](/images/bugFixed.png)

**ListExamples.java merge()**
```
static List<String> merge(List<String> list1, List<String> list2) {
  List<String> result = new ArrayList<>();
  int index1 = 0, index2 = 0;
  while(index1 < list1.size() && index2 < list2.size()) {
    if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    else  {
      result.add(list2.get(index2));
      index2 += 1;
    }
  }
  while(index1 < list1.size()) {
    result.add(list1.get(index1));
    index1 += 1;
  }
  while(index2 < list2.size()) {
    result.add(list2.get(index2));
    // change index1 below to index2 to fix test
    index2 += 1;
  }
  return result;
}
```

## Part 2
During the second half of this quarter, something knew I learned was how to use the Java debugger. This was particularly interesting to me because I'd heard of it prior to this class, but never learned how to actually use it. I found that being able to access variables from outside of the class itself very helpful because I no longer have to figure out where to put a bunch of print statements in multiple code files that I have to later clean up, and instead have access to these values all within the debugger.
