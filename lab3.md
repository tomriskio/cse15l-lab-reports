# Lab Report 2

## Part 1

### Code for StringServer:

![StringServer.java](https://brookddd.github.io/cse15l-lab-reports/SS_code.png)

### 1st Screenshot of `/add-message`

![tomris](https://brookddd.github.io/cse15l-lab-reports/tomris.png)

1. Which methods are called? 
> `handleRequest(URI url)`
2. What are the relevant arguments to those methods, and the values of any relevant fields of the class
> the `URI` is `/add-message?s=tomris`. The String is `tomris`.
3. How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.
> With each repetition, I change the value of `arg`, so that it adds the URI's `String`. But initially, `arg` is empty, so only `tomris` is printed with a new line for the sake of simplicity.

#### 2nd Screenshot of `/add-message`

![tomrishello](https://brookddd.github.io/cse15l-lab-reports/tomrishello.png)

1. Which methods are called? 
> `handleRequest(URI url)`
2. What are the relevant arguments to those methods, and the values of any relevant fields of the class
> the `URI` is `/add-message?s=Hello`. The String is `Hello`.
3. How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.
> With each repetition, I change the value of `arg`, so that it adds the URI's `String`. Therefore, `Hello` is added to `arg` and gets printed with a new line before it.


## Part 2

### 1. Failure Inducing Input
* I did my tests with the ArrayExamples file. 
`@Test 
	public void testReverseInPlace2() {
	int[] input1 = { 1,2,3 };
	ArrayExamples.reverseInPlace(input1);
	assertArrayEquals(new int[]{ 3,2,1 }, input1);
	}	`
 * I input an array `{1, 2, 3}` I'm expecting the return to be `{3,2,1}`


### 2. Input That Doesn't Induce Failure

`@Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}`
* Here since there is only one element in the array, the reversed order is the same. So the test passes.

### 3. The Symptom:

`There was 1 failure:
testReverseInPlace2(ArrayTests)
arrays first differed at element [2]; expected:<1> but was:<3>
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:78)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)
        at org.junit.Assert.assertArrayEquals(Assert.java:418)
        at org.junit.Assert.assertArrayEquals(Assert.java:429)
        at ArrayTests.testReverseInPlace2(ArrayTests.java:16)
        ... 30 trimmed
Caused by: java.lang.AssertionError: expected:<1> but was:<3>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ExactComparisonCriteria.assertElementsEqual(ExactComparisonCriteria.java:8)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:76)
        ... 36 more
FAILURES!!!
Tests run: 2,  Failures: 1`

### 4. The bug

* Before 


`static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }`

* After 


`static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i += 1) {
      int j = arr[i];
      arr[i] = arr[arr.length -i-1];
      arr[arr.length - i - 1] = j;
    }
  }`
  
* By creating a temporary `int j` that takes over the value in `arr[i]`, I can later assign a new value to `arr[i]`. Thus, changing the values in the exact same array.


## Part 3

On week 2 I learned how to connect to a server from VSCode terminal. On week 3 I learned how to run tests with JUnit.
