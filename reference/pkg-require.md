# require

Package require implements the same assertions as the assert package but stops test execution when a test fails.

### Example Usage

The following is a complete example using require in a standard test function:

	import (
	  "testing"
	  "github.com/stretchr/testify/require"
	)

	func TestSomething(t *testing.T) {

	  var a string = "Hello"
	  var b string = "Hello"

	  require.Equal(t, a, b, "The two words should be the same.")

	}

### Assertions

The require package have same global functions as in the assert package, but instead of returning a boolean result they call [testing.T.FailNow](https://pkg.go.dev/testing#T.FailNow). A consequence of this is that it must be called from the goroutine running the test function, not from other goroutines created during the test.

Every assertion function also takes an optional string message as the final argument, allowing custom error messages to be appended to the message the assertion method outputs.

## Condition

```go
func Condition(t TestingT, comp assert.Comparison, msgAndArgs ...interface{})
```

Condition uses a Comparison to assert a complex condition.

## Conditionf

```go
func Conditionf(t TestingT, comp assert.Comparison, msg string, args ...interface{})
```

Conditionf uses a Comparison to assert a complex condition.

## Contains

```go
func Contains(t TestingT, s interface{}, contains interface{}, msgAndArgs ...interface{})
```

Contains asserts that the specified string, list(array, slice...) or map contains the specified substring or element.

	require.Contains(t, "Hello World", "World")
	require.Contains(t, ["Hello", "World"], "World")
	require.Contains(t, {"Hello": "World"}, "Hello")

## Containsf

```go
func Containsf(t TestingT, s interface{}, contains interface{}, msg string, args ...interface{})
```

Containsf asserts that the specified string, list(array, slice...) or map contains the specified substring or element.

	require.Containsf(t, "Hello World", "World", "error message %s", "formatted")
	require.Containsf(t, ["Hello", "World"], "World", "error message %s", "formatted")
	require.Containsf(t, {"Hello": "World"}, "Hello", "error message %s", "formatted")

## DirExists

```go
func DirExists(t TestingT, path string, msgAndArgs ...interface{})
```

DirExists checks whether a directory exists in the given path. It also fails if the path is a file rather a directory or there is an error checking whether it exists.

## DirExistsf

```go
func DirExistsf(t TestingT, path string, msg string, args ...interface{})
```

DirExistsf checks whether a directory exists in the given path. It also fails if the path is a file rather a directory or there is an error checking whether it exists.

## ElementsMatch

```go
func ElementsMatch(t TestingT, listA interface{}, listB interface{}, msgAndArgs ...interface{})
```

ElementsMatch asserts that the specified listA(array, slice...) is equal to specified listB(array, slice...) ignoring the order of the elements. If there are duplicate elements, the number of appearances of each of them in both lists should match.

require.ElementsMatch(t, \[1, 3, 2, 3], \[1, 3, 3, 2])

## ElementsMatchf

```go
func ElementsMatchf(t TestingT, listA interface{}, listB interface{}, msg string, args ...interface{})
```

ElementsMatchf asserts that the specified listA(array, slice...) is equal to specified listB(array, slice...) ignoring the order of the elements. If there are duplicate elements, the number of appearances of each of them in both lists should match.

require.ElementsMatchf(t, \[1, 3, 2, 3], \[1, 3, 3, 2], "error message %s", "formatted")

## Empty

```go
func Empty(t TestingT, object interface{}, msgAndArgs ...interface{})
```

Empty asserts that the given value is "empty".

[Zero values](https://go.dev/ref/spec#The_zero_value) are "empty".

Arrays are "empty" if every element is the zero value of the type (stricter than "empty").

Slices, maps and channels with zero length are "empty".

Pointer values are "empty" if the pointer is nil or if the pointed value is "empty".

	require.Empty(t, obj)

## Emptyf

```go
func Emptyf(t TestingT, object interface{}, msg string, args ...interface{})
```

Emptyf asserts that the given value is "empty".

[Zero values](https://go.dev/ref/spec#The_zero_value) are "empty".

Arrays are "empty" if every element is the zero value of the type (stricter than "empty").

Slices, maps and channels with zero length are "empty".

Pointer values are "empty" if the pointer is nil or if the pointed value is "empty".

	require.Emptyf(t, obj, "error message %s", "formatted")

## Equal

```go
func Equal(t TestingT, expected interface{}, actual interface{}, msgAndArgs ...interface{})
```

Equal asserts that two objects are equal.

	require.Equal(t, 123, 123)

Pointer variable equality is determined based on the equality of the referenced values (as opposed to the memory addresses). Function equality cannot be determined and will always fail.

## EqualError

```go
func EqualError(t TestingT, theError error, errString string, msgAndArgs ...interface{})
```

EqualError asserts that a function returned a non-nil error (i.e. an error) and that it is equal to the provided error.

	actualObj, err := SomeFunction()
	require.EqualError(t, err,  expectedErrorString)

## EqualErrorf

```go
func EqualErrorf(t TestingT, theError error, errString string, msg string, args ...interface{})
```

EqualErrorf asserts that a function returned a non-nil error (i.e. an error) and that it is equal to the provided error.

	actualObj, err := SomeFunction()
	require.EqualErrorf(t, err,  expectedErrorString, "error message %s", "formatted")

## EqualExportedValues

```go
func EqualExportedValues(t TestingT, expected interface{}, actual interface{}, msgAndArgs ...interface{})
```

EqualExportedValues asserts that the types of two objects are equal and their public fields are also equal. This is useful for comparing structs that have private fields that could potentially differ.

	 type S struct {
		Exported     	int
		notExported   	int
	 }
	 require.EqualExportedValues(t, S{1, 2}, S{1, 3}) => true
	 require.EqualExportedValues(t, S{1, 2}, S{2, 3}) => false

## EqualExportedValuesf

```go
func EqualExportedValuesf(t TestingT, expected interface{}, actual interface{}, msg string, args ...interface{})
```

EqualExportedValuesf asserts that the types of two objects are equal and their public fields are also equal. This is useful for comparing structs that have private fields that could potentially differ.

	 type S struct {
		Exported     	int
		notExported   	int
	 }
	 require.EqualExportedValuesf(t, S{1, 2}, S{1, 3}, "error message %s", "formatted") => true
	 require.EqualExportedValuesf(t, S{1, 2}, S{2, 3}, "error message %s", "formatted") => false

## EqualValues

```go
func EqualValues(t TestingT, expected interface{}, actual interface{}, msgAndArgs ...interface{})
```

EqualValues asserts that two objects are equal or convertible to the larger type and equal.

	require.EqualValues(t, uint32(123), int32(123))

## EqualValuesf

```go
func EqualValuesf(t TestingT, expected interface{}, actual interface{}, msg string, args ...interface{})
```

EqualValuesf asserts that two objects are equal or convertible to the larger type and equal.

	require.EqualValuesf(t, uint32(123), int32(123), "error message %s", "formatted")

## Equalf

```go
func Equalf(t TestingT, expected interface{}, actual interface{}, msg string, args ...interface{})
```

Equalf asserts that two objects are equal.

	require.Equalf(t, 123, 123, "error message %s", "formatted")

Pointer variable equality is determined based on the equality of the referenced values (as opposed to the memory addresses). Function equality cannot be determined and will always fail.

## Error

```go
func Error(t TestingT, err error, msgAndArgs ...interface{})
```

Error asserts that a function returned a non-nil error (ie. an error).

	actualObj, err := SomeFunction()
	require.Error(t, err)

## ErrorAs

```go
func ErrorAs(t TestingT, err error, target interface{}, msgAndArgs ...interface{})
```

ErrorAs asserts that at least one of the errors in err's chain matches target, and if so, sets target to that error value. This is a wrapper for errors.As.

## ErrorAsf

```go
func ErrorAsf(t TestingT, err error, target interface{}, msg string, args ...interface{})
```

ErrorAsf asserts that at least one of the errors in err's chain matches target, and if so, sets target to that error value. This is a wrapper for errors.As.

## ErrorContains

```go
func ErrorContains(t TestingT, theError error, contains string, msgAndArgs ...interface{})
```

ErrorContains asserts that a function returned a non-nil error (i.e. an error) and that the error contains the specified substring.

	actualObj, err := SomeFunction()
	require.ErrorContains(t, err,  expectedErrorSubString)

## ErrorContainsf

```go
func ErrorContainsf(t TestingT, theError error, contains string, msg string, args ...interface{})
```

ErrorContainsf asserts that a function returned a non-nil error (i.e. an error) and that the error contains the specified substring.

	actualObj, err := SomeFunction()
	require.ErrorContainsf(t, err,  expectedErrorSubString, "error message %s", "formatted")

## ErrorIs

```go
func ErrorIs(t TestingT, err error, target error, msgAndArgs ...interface{})
```

ErrorIs asserts that at least one of the errors in err's chain matches target. This is a wrapper for errors.Is.

## ErrorIsf

```go
func ErrorIsf(t TestingT, err error, target error, msg string, args ...interface{})
```

ErrorIsf asserts that at least one of the errors in err's chain matches target. This is a wrapper for errors.Is.

## Errorf

```go
func Errorf(t TestingT, err error, msg string, args ...interface{})
```

Errorf asserts that a function returned a non-nil error (ie. an error).

	actualObj, err := SomeFunction()
	require.Errorf(t, err, "error message %s", "formatted")

## Eventually

```go
func Eventually(t TestingT, condition func() bool, waitFor time.Duration, tick time.Duration, msgAndArgs ...interface{})
```

Eventually asserts that given condition will be met in waitFor time, periodically checking target function each tick.

	require.Eventually(t, func() bool { return true; }, time.Second, 10*time.Millisecond)

## EventuallyWithT

```go
func EventuallyWithT(t TestingT, condition func(collect *assert.CollectT), waitFor time.Duration, tick time.Duration, msgAndArgs ...interface{})
```

EventuallyWithT asserts that given condition will be met in waitFor time, periodically checking target function each tick. In contrast to Eventually, it supplies a CollectT to the condition function, so that the condition function can use the CollectT to call other assertions. The condition is considered "met" if no errors are raised in a tick. The supplied CollectT collects all errors from one tick (if there are any). If the condition is not met before waitFor, the collected errors of the last tick are copied to t.

	externalValue := false
	go func() {
		time.Sleep(8*time.Second)
		externalValue = true
	}()
	require.EventuallyWithT(t, func(c *assert.CollectT) {
		// add assertions as needed; any assertion failure will fail the current tick
		require.True(c, externalValue, "expected 'externalValue' to be true")
	}, 10*time.Second, 1*time.Second, "external state has not changed to 'true'; still false")

## EventuallyWithTf

```go
func EventuallyWithTf(t TestingT, condition func(collect *assert.CollectT), waitFor time.Duration, tick time.Duration, msg string, args ...interface{})
```

EventuallyWithTf asserts that given condition will be met in waitFor time, periodically checking target function each tick. In contrast to Eventually, it supplies a CollectT to the condition function, so that the condition function can use the CollectT to call other assertions. The condition is considered "met" if no errors are raised in a tick. The supplied CollectT collects all errors from one tick (if there are any). If the condition is not met before waitFor, the collected errors of the last tick are copied to t.

	externalValue := false
	go func() {
		time.Sleep(8*time.Second)
		externalValue = true
	}()
	require.EventuallyWithTf(t, func(c *assert.CollectT) {
		// add assertions as needed; any assertion failure will fail the current tick
		require.True(c, externalValue, "expected 'externalValue' to be true")
	}, 10*time.Second, 1*time.Second, "error message %s", "formatted")

## Eventuallyf

```go
func Eventuallyf(t TestingT, condition func() bool, waitFor time.Duration, tick time.Duration, msg string, args ...interface{})
```

Eventuallyf asserts that given condition will be met in waitFor time, periodically checking target function each tick.

	require.Eventuallyf(t, func() bool { return true; }, time.Second, 10*time.Millisecond, "error message %s", "formatted")

## Exactly

```go
func Exactly(t TestingT, expected interface{}, actual interface{}, msgAndArgs ...interface{})
```

Exactly asserts that two objects are equal in value and type.

	require.Exactly(t, int32(123), int64(123))

## Exactlyf

```go
func Exactlyf(t TestingT, expected interface{}, actual interface{}, msg string, args ...interface{})
```

Exactlyf asserts that two objects are equal in value and type.

	require.Exactlyf(t, int32(123), int64(123), "error message %s", "formatted")

## Fail

```go
func Fail(t TestingT, failureMessage string, msgAndArgs ...interface{})
```

Fail reports a failure through

## FailNow

```go
func FailNow(t TestingT, failureMessage string, msgAndArgs ...interface{})
```

FailNow fails test

## FailNowf

```go
func FailNowf(t TestingT, failureMessage string, msg string, args ...interface{})
```

FailNowf fails test

## Failf

```go
func Failf(t TestingT, failureMessage string, msg string, args ...interface{})
```

Failf reports a failure through

## False

```go
func False(t TestingT, value bool, msgAndArgs ...interface{})
```

False asserts that the specified value is false.

	require.False(t, myBool)

## Falsef

```go
func Falsef(t TestingT, value bool, msg string, args ...interface{})
```

Falsef asserts that the specified value is false.

	require.Falsef(t, myBool, "error message %s", "formatted")

## FileExists

```go
func FileExists(t TestingT, path string, msgAndArgs ...interface{})
```

FileExists checks whether a file exists in the given path. It also fails if the path points to a directory or there is an error when trying to check the file.

## FileExistsf

```go
func FileExistsf(t TestingT, path string, msg string, args ...interface{})
```

FileExistsf checks whether a file exists in the given path. It also fails if the path points to a directory or there is an error when trying to check the file.

## Greater

```go
func Greater(t TestingT, e1 interface{}, e2 interface{}, msgAndArgs ...interface{})
```

Greater asserts that the first element is greater than the second

	require.Greater(t, 2, 1)
	require.Greater(t, float64(2), float64(1))
	require.Greater(t, "b", "a")

## GreaterOrEqual

```go
func GreaterOrEqual(t TestingT, e1 interface{}, e2 interface{}, msgAndArgs ...interface{})
```

GreaterOrEqual asserts that the first element is greater than or equal to the second

	require.GreaterOrEqual(t, 2, 1)
	require.GreaterOrEqual(t, 2, 2)
	require.GreaterOrEqual(t, "b", "a")
	require.GreaterOrEqual(t, "b", "b")

## GreaterOrEqualf

```go
func GreaterOrEqualf(t TestingT, e1 interface{}, e2 interface{}, msg string, args ...interface{})
```

GreaterOrEqualf asserts that the first element is greater than or equal to the second

	require.GreaterOrEqualf(t, 2, 1, "error message %s", "formatted")
	require.GreaterOrEqualf(t, 2, 2, "error message %s", "formatted")
	require.GreaterOrEqualf(t, "b", "a", "error message %s", "formatted")
	require.GreaterOrEqualf(t, "b", "b", "error message %s", "formatted")

## Greaterf

```go
func Greaterf(t TestingT, e1 interface{}, e2 interface{}, msg string, args ...interface{})
```

Greaterf asserts that the first element is greater than the second

	require.Greaterf(t, 2, 1, "error message %s", "formatted")
	require.Greaterf(t, float64(2), float64(1), "error message %s", "formatted")
	require.Greaterf(t, "b", "a", "error message %s", "formatted")

## HTTPBodyContains

```go
func HTTPBodyContains(t TestingT, handler http.HandlerFunc, method string, url string, values url.Values, str interface{}, msgAndArgs ...interface{})
```

HTTPBodyContains asserts that a specified handler returns a body that contains a string.

	require.HTTPBodyContains(t, myHandler, "GET", "www.google.com", nil, "I'm Feeling Lucky")

## HTTPBodyContainsf

```go
func HTTPBodyContainsf(t TestingT, handler http.HandlerFunc, method string, url string, values url.Values, str interface{}, msg string, args ...interface{})
```

HTTPBodyContainsf asserts that a specified handler returns a body that contains a string.

	require.HTTPBodyContainsf(t, myHandler, "GET", "www.google.com", nil, "I'm Feeling Lucky", "error message %s", "formatted")

## HTTPBodyNotContains

```go
func HTTPBodyNotContains(t TestingT, handler http.HandlerFunc, method string, url string, values url.Values, str interface{}, msgAndArgs ...interface{})
```

HTTPBodyNotContains asserts that a specified handler returns a body that does not contain a string.

	require.HTTPBodyNotContains(t, myHandler, "GET", "www.google.com", nil, "I'm Feeling Lucky")

## HTTPBodyNotContainsf

```go
func HTTPBodyNotContainsf(t TestingT, handler http.HandlerFunc, method string, url string, values url.Values, str interface{}, msg string, args ...interface{})
```

HTTPBodyNotContainsf asserts that a specified handler returns a body that does not contain a string.

	require.HTTPBodyNotContainsf(t, myHandler, "GET", "www.google.com", nil, "I'm Feeling Lucky", "error message %s", "formatted")

## HTTPError

```go
func HTTPError(t TestingT, handler http.HandlerFunc, method string, url string, values url.Values, msgAndArgs ...interface{})
```

HTTPError asserts that a specified handler returns an error status code.

	require.HTTPError(t, myHandler, "POST", "/a/b/c", url.Values{"a": []string{"b", "c"}}

## HTTPErrorf

```go
func HTTPErrorf(t TestingT, handler http.HandlerFunc, method string, url string, values url.Values, msg string, args ...interface{})
```

HTTPErrorf asserts that a specified handler returns an error status code.

	require.HTTPErrorf(t, myHandler, "POST", "/a/b/c", url.Values{"a": []string{"b", "c"}}

## HTTPRedirect

```go
func HTTPRedirect(t TestingT, handler http.HandlerFunc, method string, url string, values url.Values, msgAndArgs ...interface{})
```

HTTPRedirect asserts that a specified handler returns a redirect status code.

	require.HTTPRedirect(t, myHandler, "GET", "/a/b/c", url.Values{"a": []string{"b", "c"}}

## HTTPRedirectf

```go
func HTTPRedirectf(t TestingT, handler http.HandlerFunc, method string, url string, values url.Values, msg string, args ...interface{})
```

HTTPRedirectf asserts that a specified handler returns a redirect status code.

	require.HTTPRedirectf(t, myHandler, "GET", "/a/b/c", url.Values{"a": []string{"b", "c"}}

## HTTPStatusCode

```go
func HTTPStatusCode(t TestingT, handler http.HandlerFunc, method string, url string, values url.Values, statuscode int, msgAndArgs ...interface{})
```

HTTPStatusCode asserts that a specified handler returns a specified status code.

	require.HTTPStatusCode(t, myHandler, "GET", "/notImplemented", nil, 501)

## HTTPStatusCodef

```go
func HTTPStatusCodef(t TestingT, handler http.HandlerFunc, method string, url string, values url.Values, statuscode int, msg string, args ...interface{})
```

HTTPStatusCodef asserts that a specified handler returns a specified status code.

	require.HTTPStatusCodef(t, myHandler, "GET", "/notImplemented", nil, 501, "error message %s", "formatted")

## HTTPSuccess

```go
func HTTPSuccess(t TestingT, handler http.HandlerFunc, method string, url string, values url.Values, msgAndArgs ...interface{})
```

HTTPSuccess asserts that a specified handler returns a success status code.

	require.HTTPSuccess(t, myHandler, "POST", "http://www.google.com", nil)

## HTTPSuccessf

```go
func HTTPSuccessf(t TestingT, handler http.HandlerFunc, method string, url string, values url.Values, msg string, args ...interface{})
```

HTTPSuccessf asserts that a specified handler returns a success status code.

	require.HTTPSuccessf(t, myHandler, "POST", "http://www.google.com", nil, "error message %s", "formatted")

## Implements

```go
func Implements(t TestingT, interfaceObject interface{}, object interface{}, msgAndArgs ...interface{})
```

Implements asserts that an object is implemented by the specified interface.

	require.Implements(t, (*MyInterface)(nil), new(MyObject))

## Implementsf

```go
func Implementsf(t TestingT, interfaceObject interface{}, object interface{}, msg string, args ...interface{})
```

Implementsf asserts that an object is implemented by the specified interface.

	require.Implementsf(t, (*MyInterface)(nil), new(MyObject), "error message %s", "formatted")

## InDelta

```go
func InDelta(t TestingT, expected interface{}, actual interface{}, delta float64, msgAndArgs ...interface{})
```

InDelta asserts that the two numerals are within delta of each other.

	require.InDelta(t, math.Pi, 22/7.0, 0.01)

## InDeltaMapValues

```go
func InDeltaMapValues(t TestingT, expected interface{}, actual interface{}, delta float64, msgAndArgs ...interface{})
```

InDeltaMapValues is the same as InDelta, but it compares all values between two maps. Both maps must have exactly the same keys.

## InDeltaMapValuesf

```go
func InDeltaMapValuesf(t TestingT, expected interface{}, actual interface{}, delta float64, msg string, args ...interface{})
```

InDeltaMapValuesf is the same as InDelta, but it compares all values between two maps. Both maps must have exactly the same keys.

## InDeltaSlice

```go
func InDeltaSlice(t TestingT, expected interface{}, actual interface{}, delta float64, msgAndArgs ...interface{})
```

InDeltaSlice is the same as InDelta, except it compares two slices.

## InDeltaSlicef

```go
func InDeltaSlicef(t TestingT, expected interface{}, actual interface{}, delta float64, msg string, args ...interface{})
```

InDeltaSlicef is the same as InDelta, except it compares two slices.

## InDeltaf

```go
func InDeltaf(t TestingT, expected interface{}, actual interface{}, delta float64, msg string, args ...interface{})
```

InDeltaf asserts that the two numerals are within delta of each other.

	require.InDeltaf(t, math.Pi, 22/7.0, 0.01, "error message %s", "formatted")

## InEpsilon

```go
func InEpsilon(t TestingT, expected interface{}, actual interface{}, epsilon float64, msgAndArgs ...interface{})
```

InEpsilon asserts that expected and actual have a relative error less than epsilon

## InEpsilonSlice

```go
func InEpsilonSlice(t TestingT, expected interface{}, actual interface{}, epsilon float64, msgAndArgs ...interface{})
```

InEpsilonSlice is the same as InEpsilon, except it compares each value from two slices.

## InEpsilonSlicef

```go
func InEpsilonSlicef(t TestingT, expected interface{}, actual interface{}, epsilon float64, msg string, args ...interface{})
```

InEpsilonSlicef is the same as InEpsilon, except it compares each value from two slices.

## InEpsilonf

```go
func InEpsilonf(t TestingT, expected interface{}, actual interface{}, epsilon float64, msg string, args ...interface{})
```

InEpsilonf asserts that expected and actual have a relative error less than epsilon

## IsDecreasing

```go
func IsDecreasing(t TestingT, object interface{}, msgAndArgs ...interface{})
```

IsDecreasing asserts that the collection is decreasing

	require.IsDecreasing(t, []int{2, 1, 0})
	require.IsDecreasing(t, []float{2, 1})
	require.IsDecreasing(t, []string{"b", "a"})

## IsDecreasingf

```go
func IsDecreasingf(t TestingT, object interface{}, msg string, args ...interface{})
```

IsDecreasingf asserts that the collection is decreasing

	require.IsDecreasingf(t, []int{2, 1, 0}, "error message %s", "formatted")
	require.IsDecreasingf(t, []float{2, 1}, "error message %s", "formatted")
	require.IsDecreasingf(t, []string{"b", "a"}, "error message %s", "formatted")

## IsIncreasing

```go
func IsIncreasing(t TestingT, object interface{}, msgAndArgs ...interface{})
```

IsIncreasing asserts that the collection is increasing

	require.IsIncreasing(t, []int{1, 2, 3})
	require.IsIncreasing(t, []float{1, 2})
	require.IsIncreasing(t, []string{"a", "b"})

## IsIncreasingf

```go
func IsIncreasingf(t TestingT, object interface{}, msg string, args ...interface{})
```

IsIncreasingf asserts that the collection is increasing

	require.IsIncreasingf(t, []int{1, 2, 3}, "error message %s", "formatted")
	require.IsIncreasingf(t, []float{1, 2}, "error message %s", "formatted")
	require.IsIncreasingf(t, []string{"a", "b"}, "error message %s", "formatted")

## IsNonDecreasing

```go
func IsNonDecreasing(t TestingT, object interface{}, msgAndArgs ...interface{})
```

IsNonDecreasing asserts that the collection is not decreasing

	require.IsNonDecreasing(t, []int{1, 1, 2})
	require.IsNonDecreasing(t, []float{1, 2})
	require.IsNonDecreasing(t, []string{"a", "b"})

## IsNonDecreasingf

```go
func IsNonDecreasingf(t TestingT, object interface{}, msg string, args ...interface{})
```

IsNonDecreasingf asserts that the collection is not decreasing

	require.IsNonDecreasingf(t, []int{1, 1, 2}, "error message %s", "formatted")
	require.IsNonDecreasingf(t, []float{1, 2}, "error message %s", "formatted")
	require.IsNonDecreasingf(t, []string{"a", "b"}, "error message %s", "formatted")

## IsNonIncreasing

```go
func IsNonIncreasing(t TestingT, object interface{}, msgAndArgs ...interface{})
```

IsNonIncreasing asserts that the collection is not increasing

	require.IsNonIncreasing(t, []int{2, 1, 1})
	require.IsNonIncreasing(t, []float{2, 1})
	require.IsNonIncreasing(t, []string{"b", "a"})

## IsNonIncreasingf

```go
func IsNonIncreasingf(t TestingT, object interface{}, msg string, args ...interface{})
```

IsNonIncreasingf asserts that the collection is not increasing

	require.IsNonIncreasingf(t, []int{2, 1, 1}, "error message %s", "formatted")
	require.IsNonIncreasingf(t, []float{2, 1}, "error message %s", "formatted")
	require.IsNonIncreasingf(t, []string{"b", "a"}, "error message %s", "formatted")

## IsNotType

```go
func IsNotType(t TestingT, theType interface{}, object interface{}, msgAndArgs ...interface{})
```

IsNotType asserts that the specified objects are not of the same type.

	require.IsNotType(t, &NotMyStruct{}, &MyStruct{})

## IsNotTypef

```go
func IsNotTypef(t TestingT, theType interface{}, object interface{}, msg string, args ...interface{})
```

IsNotTypef asserts that the specified objects are not of the same type.

	require.IsNotTypef(t, &NotMyStruct{}, &MyStruct{}, "error message %s", "formatted")

## IsType

```go
func IsType(t TestingT, expectedType interface{}, object interface{}, msgAndArgs ...interface{})
```

IsType asserts that the specified objects are of the same type.

	require.IsType(t, &MyStruct{}, &MyStruct{})

## IsTypef

```go
func IsTypef(t TestingT, expectedType interface{}, object interface{}, msg string, args ...interface{})
```

IsTypef asserts that the specified objects are of the same type.

	require.IsTypef(t, &MyStruct{}, &MyStruct{}, "error message %s", "formatted")

## JSONEq

```go
func JSONEq(t TestingT, expected string, actual string, msgAndArgs ...interface{})
```

JSONEq asserts that two JSON strings are equivalent.

	require.JSONEq(t, `{"hello": "world", "foo": "bar"}`, `{"foo": "bar", "hello": "world"}`)

## JSONEqf

```go
func JSONEqf(t TestingT, expected string, actual string, msg string, args ...interface{})
```

JSONEqf asserts that two JSON strings are equivalent.

	require.JSONEqf(t, `{"hello": "world", "foo": "bar"}`, `{"foo": "bar", "hello": "world"}`, "error message %s", "formatted")

## Len

```go
func Len(t TestingT, object interface{}, length int, msgAndArgs ...interface{})
```

Len asserts that the specified object has specific length. Len also fails if the object has a type that len() not accept.

	require.Len(t, mySlice, 3)

## Lenf

```go
func Lenf(t TestingT, object interface{}, length int, msg string, args ...interface{})
```

Lenf asserts that the specified object has specific length. Lenf also fails if the object has a type that len() not accept.

	require.Lenf(t, mySlice, 3, "error message %s", "formatted")

## Less

```go
func Less(t TestingT, e1 interface{}, e2 interface{}, msgAndArgs ...interface{})
```

Less asserts that the first element is less than the second

	require.Less(t, 1, 2)
	require.Less(t, float64(1), float64(2))
	require.Less(t, "a", "b")

## LessOrEqual

```go
func LessOrEqual(t TestingT, e1 interface{}, e2 interface{}, msgAndArgs ...interface{})
```

LessOrEqual asserts that the first element is less than or equal to the second

	require.LessOrEqual(t, 1, 2)
	require.LessOrEqual(t, 2, 2)
	require.LessOrEqual(t, "a", "b")
	require.LessOrEqual(t, "b", "b")

## LessOrEqualf

```go
func LessOrEqualf(t TestingT, e1 interface{}, e2 interface{}, msg string, args ...interface{})
```

LessOrEqualf asserts that the first element is less than or equal to the second

	require.LessOrEqualf(t, 1, 2, "error message %s", "formatted")
	require.LessOrEqualf(t, 2, 2, "error message %s", "formatted")
	require.LessOrEqualf(t, "a", "b", "error message %s", "formatted")
	require.LessOrEqualf(t, "b", "b", "error message %s", "formatted")

## Lessf

```go
func Lessf(t TestingT, e1 interface{}, e2 interface{}, msg string, args ...interface{})
```

Lessf asserts that the first element is less than the second

	require.Lessf(t, 1, 2, "error message %s", "formatted")
	require.Lessf(t, float64(1), float64(2), "error message %s", "formatted")
	require.Lessf(t, "a", "b", "error message %s", "formatted")

## Negative

```go
func Negative(t TestingT, e interface{}, msgAndArgs ...interface{})
```

Negative asserts that the specified element is negative

	require.Negative(t, -1)
	require.Negative(t, -1.23)

## Negativef

```go
func Negativef(t TestingT, e interface{}, msg string, args ...interface{})
```

Negativef asserts that the specified element is negative

	require.Negativef(t, -1, "error message %s", "formatted")
	require.Negativef(t, -1.23, "error message %s", "formatted")

## Never

```go
func Never(t TestingT, condition func() bool, waitFor time.Duration, tick time.Duration, msgAndArgs ...interface{})
```

Never asserts that the given condition doesn't satisfy in waitFor time, periodically checking the target function each tick.

	require.Never(t, func() bool { return false; }, time.Second, 10*time.Millisecond)

## Neverf

```go
func Neverf(t TestingT, condition func() bool, waitFor time.Duration, tick time.Duration, msg string, args ...interface{})
```

Neverf asserts that the given condition doesn't satisfy in waitFor time, periodically checking the target function each tick.

	require.Neverf(t, func() bool { return false; }, time.Second, 10*time.Millisecond, "error message %s", "formatted")

## New

```go
func New(t TestingT) *Assertions
```

New makes a new Assertions object for the specified TestingT.

## Nil

```go
func Nil(t TestingT, object interface{}, msgAndArgs ...interface{})
```

Nil asserts that the specified object is nil.

	require.Nil(t, err)

## Nilf

```go
func Nilf(t TestingT, object interface{}, msg string, args ...interface{})
```

Nilf asserts that the specified object is nil.

	require.Nilf(t, err, "error message %s", "formatted")

## NoDirExists

```go
func NoDirExists(t TestingT, path string, msgAndArgs ...interface{})
```

NoDirExists checks whether a directory does not exist in the given path. It fails if the path points to an existing \_directory\_ only.

## NoDirExistsf

```go
func NoDirExistsf(t TestingT, path string, msg string, args ...interface{})
```

NoDirExistsf checks whether a directory does not exist in the given path. It fails if the path points to an existing \_directory\_ only.

## NoError

```go
func NoError(t TestingT, err error, msgAndArgs ...interface{})
```

NoError asserts that a function returned a nil error (ie. no error).

	actualObj, err := SomeFunction()
	require.NoError(t, err)
	require.Equal(t, expectedObj, actualObj)

## NoErrorf

```go
func NoErrorf(t TestingT, err error, msg string, args ...interface{})
```

NoErrorf asserts that a function returned a nil error (ie. no error).

	actualObj, err := SomeFunction()
	require.NoErrorf(t, err, "error message %s", "formatted")
	require.Equal(t, expectedObj, actualObj)

## NoFileExists

```go
func NoFileExists(t TestingT, path string, msgAndArgs ...interface{})
```

NoFileExists checks whether a file does not exist in a given path. It fails if the path points to an existing \_file\_ only.

## NoFileExistsf

```go
func NoFileExistsf(t TestingT, path string, msg string, args ...interface{})
```

NoFileExistsf checks whether a file does not exist in a given path. It fails if the path points to an existing \_file\_ only.

## NotContains

```go
func NotContains(t TestingT, s interface{}, contains interface{}, msgAndArgs ...interface{})
```

NotContains asserts that the specified string, list(array, slice...) or map does NOT contain the specified substring or element.

	require.NotContains(t, "Hello World", "Earth")
	require.NotContains(t, ["Hello", "World"], "Earth")
	require.NotContains(t, {"Hello": "World"}, "Earth")

## NotContainsf

```go
func NotContainsf(t TestingT, s interface{}, contains interface{}, msg string, args ...interface{})
```

NotContainsf asserts that the specified string, list(array, slice...) or map does NOT contain the specified substring or element.

	require.NotContainsf(t, "Hello World", "Earth", "error message %s", "formatted")
	require.NotContainsf(t, ["Hello", "World"], "Earth", "error message %s", "formatted")
	require.NotContainsf(t, {"Hello": "World"}, "Earth", "error message %s", "formatted")

## NotElementsMatch

```go
func NotElementsMatch(t TestingT, listA interface{}, listB interface{}, msgAndArgs ...interface{})
```

NotElementsMatch asserts that the specified listA(array, slice...) is NOT equal to specified listB(array, slice...) ignoring the order of the elements. If there are duplicate elements, the number of appearances of each of them in both lists should not match. This is an inverse of ElementsMatch.

require.NotElementsMatch(t, \[1, 1, 2, 3], \[1, 1, 2, 3]) -> false

require.NotElementsMatch(t, \[1, 1, 2, 3], \[1, 2, 3]) -> true

require.NotElementsMatch(t, \[1, 2, 3], \[1, 2, 4]) -> true

## NotElementsMatchf

```go
func NotElementsMatchf(t TestingT, listA interface{}, listB interface{}, msg string, args ...interface{})
```

NotElementsMatchf asserts that the specified listA(array, slice...) is NOT equal to specified listB(array, slice...) ignoring the order of the elements. If there are duplicate elements, the number of appearances of each of them in both lists should not match. This is an inverse of ElementsMatch.

require.NotElementsMatchf(t, \[1, 1, 2, 3], \[1, 1, 2, 3], "error message %s", "formatted") -> false

require.NotElementsMatchf(t, \[1, 1, 2, 3], \[1, 2, 3], "error message %s", "formatted") -> true

require.NotElementsMatchf(t, \[1, 2, 3], \[1, 2, 4], "error message %s", "formatted") -> true

## NotEmpty

```go
func NotEmpty(t TestingT, object interface{}, msgAndArgs ...interface{})
```

NotEmpty asserts that the specified object is NOT [Empty](#func-Empty).

	require.NotEmpty(t, obj)
	require.Equal(t, "two", obj[1])

## NotEmptyf

```go
func NotEmptyf(t TestingT, object interface{}, msg string, args ...interface{})
```

NotEmptyf asserts that the specified object is NOT [Empty](#func-Empty).

	require.NotEmptyf(t, obj, "error message %s", "formatted")
	require.Equal(t, "two", obj[1])

## NotEqual

```go
func NotEqual(t TestingT, expected interface{}, actual interface{}, msgAndArgs ...interface{})
```

NotEqual asserts that the specified values are NOT equal.

	require.NotEqual(t, obj1, obj2)

Pointer variable equality is determined based on the equality of the referenced values (as opposed to the memory addresses).

## NotEqualValues

```go
func NotEqualValues(t TestingT, expected interface{}, actual interface{}, msgAndArgs ...interface{})
```

NotEqualValues asserts that two objects are not equal even when converted to the same type

	require.NotEqualValues(t, obj1, obj2)

## NotEqualValuesf

```go
func NotEqualValuesf(t TestingT, expected interface{}, actual interface{}, msg string, args ...interface{})
```

NotEqualValuesf asserts that two objects are not equal even when converted to the same type

	require.NotEqualValuesf(t, obj1, obj2, "error message %s", "formatted")

## NotEqualf

```go
func NotEqualf(t TestingT, expected interface{}, actual interface{}, msg string, args ...interface{})
```

NotEqualf asserts that the specified values are NOT equal.

	require.NotEqualf(t, obj1, obj2, "error message %s", "formatted")

Pointer variable equality is determined based on the equality of the referenced values (as opposed to the memory addresses).

## NotErrorAs

```go
func NotErrorAs(t TestingT, err error, target interface{}, msgAndArgs ...interface{})
```

NotErrorAs asserts that none of the errors in err's chain matches target, but if so, sets target to that error value.

## NotErrorAsf

```go
func NotErrorAsf(t TestingT, err error, target interface{}, msg string, args ...interface{})
```

NotErrorAsf asserts that none of the errors in err's chain matches target, but if so, sets target to that error value.

## NotErrorIs

```go
func NotErrorIs(t TestingT, err error, target error, msgAndArgs ...interface{})
```

NotErrorIs asserts that none of the errors in err's chain matches target. This is a wrapper for errors.Is.

## NotErrorIsf

```go
func NotErrorIsf(t TestingT, err error, target error, msg string, args ...interface{})
```

NotErrorIsf asserts that none of the errors in err's chain matches target. This is a wrapper for errors.Is.

## NotImplements

```go
func NotImplements(t TestingT, interfaceObject interface{}, object interface{}, msgAndArgs ...interface{})
```

NotImplements asserts that an object does not implement the specified interface.

	require.NotImplements(t, (*MyInterface)(nil), new(MyObject))

## NotImplementsf

```go
func NotImplementsf(t TestingT, interfaceObject interface{}, object interface{}, msg string, args ...interface{})
```

NotImplementsf asserts that an object does not implement the specified interface.

	require.NotImplementsf(t, (*MyInterface)(nil), new(MyObject), "error message %s", "formatted")

## NotNil

```go
func NotNil(t TestingT, object interface{}, msgAndArgs ...interface{})
```

NotNil asserts that the specified object is not nil.

	require.NotNil(t, err)

## NotNilf

```go
func NotNilf(t TestingT, object interface{}, msg string, args ...interface{})
```

NotNilf asserts that the specified object is not nil.

	require.NotNilf(t, err, "error message %s", "formatted")

## NotPanics

```go
func NotPanics(t TestingT, f assert.PanicTestFunc, msgAndArgs ...interface{})
```

NotPanics asserts that the code inside the specified PanicTestFunc does NOT panic.

	require.NotPanics(t, func(){ RemainCalm() })

## NotPanicsf

```go
func NotPanicsf(t TestingT, f assert.PanicTestFunc, msg string, args ...interface{})
```

NotPanicsf asserts that the code inside the specified PanicTestFunc does NOT panic.

	require.NotPanicsf(t, func(){ RemainCalm() }, "error message %s", "formatted")

## NotRegexp

```go
func NotRegexp(t TestingT, rx interface{}, str interface{}, msgAndArgs ...interface{})
```

NotRegexp asserts that a specified regexp does not match a string.

	require.NotRegexp(t, regexp.MustCompile("starts"), "it's starting")
	require.NotRegexp(t, "^start", "it's not starting")

## NotRegexpf

```go
func NotRegexpf(t TestingT, rx interface{}, str interface{}, msg string, args ...interface{})
```

NotRegexpf asserts that a specified regexp does not match a string.

	require.NotRegexpf(t, regexp.MustCompile("starts"), "it's starting", "error message %s", "formatted")
	require.NotRegexpf(t, "^start", "it's not starting", "error message %s", "formatted")

## NotSame

```go
func NotSame(t TestingT, expected interface{}, actual interface{}, msgAndArgs ...interface{})
```

NotSame asserts that two pointers do not reference the same object.

	require.NotSame(t, ptr1, ptr2)

Both arguments must be pointer variables. Pointer variable sameness is determined based on the equality of both type and value.

## NotSamef

```go
func NotSamef(t TestingT, expected interface{}, actual interface{}, msg string, args ...interface{})
```

NotSamef asserts that two pointers do not reference the same object.

	require.NotSamef(t, ptr1, ptr2, "error message %s", "formatted")

Both arguments must be pointer variables. Pointer variable sameness is determined based on the equality of both type and value.

## NotSubset

```go
func NotSubset(t TestingT, list interface{}, subset interface{}, msgAndArgs ...interface{})
```

NotSubset asserts that the list (array, slice, or map) does NOT contain all elements given in the subset (array, slice, or map). Map elements are key-value pairs unless compared with an array or slice where only the map key is evaluated.

	require.NotSubset(t, [1, 3, 4], [1, 2])
	require.NotSubset(t, {"x": 1, "y": 2}, {"z": 3})
	require.NotSubset(t, [1, 3, 4], {1: "one", 2: "two"})
	require.NotSubset(t, {"x": 1, "y": 2}, ["z"])

## NotSubsetf

```go
func NotSubsetf(t TestingT, list interface{}, subset interface{}, msg string, args ...interface{})
```

NotSubsetf asserts that the list (array, slice, or map) does NOT contain all elements given in the subset (array, slice, or map). Map elements are key-value pairs unless compared with an array or slice where only the map key is evaluated.

	require.NotSubsetf(t, [1, 3, 4], [1, 2], "error message %s", "formatted")
	require.NotSubsetf(t, {"x": 1, "y": 2}, {"z": 3}, "error message %s", "formatted")
	require.NotSubsetf(t, [1, 3, 4], {1: "one", 2: "two"}, "error message %s", "formatted")
	require.NotSubsetf(t, {"x": 1, "y": 2}, ["z"], "error message %s", "formatted")

## NotZero

```go
func NotZero(t TestingT, i interface{}, msgAndArgs ...interface{})
```

NotZero asserts that i is not the zero value for its type.

## NotZerof

```go
func NotZerof(t TestingT, i interface{}, msg string, args ...interface{})
```

NotZerof asserts that i is not the zero value for its type.

## Panics

```go
func Panics(t TestingT, f assert.PanicTestFunc, msgAndArgs ...interface{})
```

Panics asserts that the code inside the specified PanicTestFunc panics.

	require.Panics(t, func(){ GoCrazy() })

## PanicsWithError

```go
func PanicsWithError(t TestingT, errString string, f assert.PanicTestFunc, msgAndArgs ...interface{})
```

PanicsWithError asserts that the code inside the specified PanicTestFunc panics, and that the recovered panic value is an error that satisfies the EqualError comparison.

	require.PanicsWithError(t, "crazy error", func(){ GoCrazy() })

## PanicsWithErrorf

```go
func PanicsWithErrorf(t TestingT, errString string, f assert.PanicTestFunc, msg string, args ...interface{})
```

PanicsWithErrorf asserts that the code inside the specified PanicTestFunc panics, and that the recovered panic value is an error that satisfies the EqualError comparison.

	require.PanicsWithErrorf(t, "crazy error", func(){ GoCrazy() }, "error message %s", "formatted")

## PanicsWithValue

```go
func PanicsWithValue(t TestingT, expected interface{}, f assert.PanicTestFunc, msgAndArgs ...interface{})
```

PanicsWithValue asserts that the code inside the specified PanicTestFunc panics, and that the recovered panic value equals the expected panic value.

	require.PanicsWithValue(t, "crazy error", func(){ GoCrazy() })

## PanicsWithValuef

```go
func PanicsWithValuef(t TestingT, expected interface{}, f assert.PanicTestFunc, msg string, args ...interface{})
```

PanicsWithValuef asserts that the code inside the specified PanicTestFunc panics, and that the recovered panic value equals the expected panic value.

	require.PanicsWithValuef(t, "crazy error", func(){ GoCrazy() }, "error message %s", "formatted")

## Panicsf

```go
func Panicsf(t TestingT, f assert.PanicTestFunc, msg string, args ...interface{})
```

Panicsf asserts that the code inside the specified PanicTestFunc panics.

	require.Panicsf(t, func(){ GoCrazy() }, "error message %s", "formatted")

## Positive

```go
func Positive(t TestingT, e interface{}, msgAndArgs ...interface{})
```

Positive asserts that the specified element is positive

	require.Positive(t, 1)
	require.Positive(t, 1.23)

## Positivef

```go
func Positivef(t TestingT, e interface{}, msg string, args ...interface{})
```

Positivef asserts that the specified element is positive

	require.Positivef(t, 1, "error message %s", "formatted")
	require.Positivef(t, 1.23, "error message %s", "formatted")

## Regexp

```go
func Regexp(t TestingT, rx interface{}, str interface{}, msgAndArgs ...interface{})
```

Regexp asserts that a specified regexp matches a string.

	require.Regexp(t, regexp.MustCompile("start"), "it's starting")
	require.Regexp(t, "start...$", "it's not starting")

## Regexpf

```go
func Regexpf(t TestingT, rx interface{}, str interface{}, msg string, args ...interface{})
```

Regexpf asserts that a specified regexp matches a string.

	require.Regexpf(t, regexp.MustCompile("start"), "it's starting", "error message %s", "formatted")
	require.Regexpf(t, "start...$", "it's not starting", "error message %s", "formatted")

## Same

```go
func Same(t TestingT, expected interface{}, actual interface{}, msgAndArgs ...interface{})
```

Same asserts that two pointers reference the same object.

	require.Same(t, ptr1, ptr2)

Both arguments must be pointer variables. Pointer variable sameness is determined based on the equality of both type and value.

## Samef

```go
func Samef(t TestingT, expected interface{}, actual interface{}, msg string, args ...interface{})
```

Samef asserts that two pointers reference the same object.

	require.Samef(t, ptr1, ptr2, "error message %s", "formatted")

Both arguments must be pointer variables. Pointer variable sameness is determined based on the equality of both type and value.

## Subset

```go
func Subset(t TestingT, list interface{}, subset interface{}, msgAndArgs ...interface{})
```

Subset asserts that the list (array, slice, or map) contains all elements given in the subset (array, slice, or map). Map elements are key-value pairs unless compared with an array or slice where only the map key is evaluated.

	require.Subset(t, [1, 2, 3], [1, 2])
	require.Subset(t, {"x": 1, "y": 2}, {"x": 1})
	require.Subset(t, [1, 2, 3], {1: "one", 2: "two"})
	require.Subset(t, {"x": 1, "y": 2}, ["x"])

## Subsetf

```go
func Subsetf(t TestingT, list interface{}, subset interface{}, msg string, args ...interface{})
```

Subsetf asserts that the list (array, slice, or map) contains all elements given in the subset (array, slice, or map). Map elements are key-value pairs unless compared with an array or slice where only the map key is evaluated.

	require.Subsetf(t, [1, 2, 3], [1, 2], "error message %s", "formatted")
	require.Subsetf(t, {"x": 1, "y": 2}, {"x": 1}, "error message %s", "formatted")
	require.Subsetf(t, [1, 2, 3], {1: "one", 2: "two"}, "error message %s", "formatted")
	require.Subsetf(t, {"x": 1, "y": 2}, ["x"], "error message %s", "formatted")

## True

```go
func True(t TestingT, value bool, msgAndArgs ...interface{})
```

True asserts that the specified value is true.

	require.True(t, myBool)

## Truef

```go
func Truef(t TestingT, value bool, msg string, args ...interface{})
```

Truef asserts that the specified value is true.

	require.Truef(t, myBool, "error message %s", "formatted")

## WithinDuration

```go
func WithinDuration(t TestingT, expected time.Time, actual time.Time, delta time.Duration, msgAndArgs ...interface{})
```

WithinDuration asserts that the two times are within duration delta of each other.

	require.WithinDuration(t, time.Now(), time.Now(), 10*time.Second)

## WithinDurationf

```go
func WithinDurationf(t TestingT, expected time.Time, actual time.Time, delta time.Duration, msg string, args ...interface{})
```

WithinDurationf asserts that the two times are within duration delta of each other.

	require.WithinDurationf(t, time.Now(), time.Now(), 10*time.Second, "error message %s", "formatted")

## WithinRange

```go
func WithinRange(t TestingT, actual time.Time, start time.Time, end time.Time, msgAndArgs ...interface{})
```

WithinRange asserts that a time is within a time range (inclusive).

	require.WithinRange(t, time.Now(), time.Now().Add(-time.Second), time.Now().Add(time.Second))

## WithinRangef

```go
func WithinRangef(t TestingT, actual time.Time, start time.Time, end time.Time, msg string, args ...interface{})
```

WithinRangef asserts that a time is within a time range (inclusive).

	require.WithinRangef(t, time.Now(), time.Now().Add(-time.Second), time.Now().Add(time.Second), "error message %s", "formatted")

## YAMLEq

```go
func YAMLEq(t TestingT, expected string, actual string, msgAndArgs ...interface{})
```

YAMLEq asserts that the first documents in the two YAML strings are equivalent.

	expected := `---
	key: value
	---
	key: this is a second document, it is not evaluated
	`
	actual := `---
	key: value
	---
	key: this is a subsequent document, it is not evaluated
	`
	require.YAMLEq(t, expected, actual)

## YAMLEqf

```go
func YAMLEqf(t TestingT, expected string, actual string, msg string, args ...interface{})
```

YAMLEqf asserts that the first documents in the two YAML strings are equivalent.

	expected := `---
	key: value
	---
	key: this is a second document, it is not evaluated
	`
	actual := `---
	key: value
	---
	key: this is a subsequent document, it is not evaluated
	`
	require.YAMLEqf(t, expected, actual, "error message %s", "formatted")

## Zero

```go
func Zero(t TestingT, i interface{}, msgAndArgs ...interface{})
```

Zero asserts that i is the zero value for its type.

## Zerof

```go
func Zerof(t TestingT, i interface{}, msg string, args ...interface{})
```

Zerof asserts that i is the zero value for its type.

## Assertions

```go
type Assertions struct {
	// contains filtered or unexported fields
}
```

Assertions provides assertion methods around the TestingT interface.

## Condition

```go
func (a *Assertions) Condition(comp assert.Comparison, msgAndArgs ...interface{})
```

Condition uses a Comparison to assert a complex condition.

## Conditionf

```go
func (a *Assertions) Conditionf(comp assert.Comparison, msg string, args ...interface{})
```

Conditionf uses a Comparison to assert a complex condition.

## Contains

```go
func (a *Assertions) Contains(s interface{}, contains interface{}, msgAndArgs ...interface{})
```

Contains asserts that the specified string, list(array, slice...) or map contains the specified substring or element.

	a.Contains("Hello World", "World")
	a.Contains(["Hello", "World"], "World")
	a.Contains({"Hello": "World"}, "Hello")

## Containsf

```go
func (a *Assertions) Containsf(s interface{}, contains interface{}, msg string, args ...interface{})
```

Containsf asserts that the specified string, list(array, slice...) or map contains the specified substring or element.

	a.Containsf("Hello World", "World", "error message %s", "formatted")
	a.Containsf(["Hello", "World"], "World", "error message %s", "formatted")
	a.Containsf({"Hello": "World"}, "Hello", "error message %s", "formatted")

## DirExists

```go
func (a *Assertions) DirExists(path string, msgAndArgs ...interface{})
```

DirExists checks whether a directory exists in the given path. It also fails if the path is a file rather a directory or there is an error checking whether it exists.

## DirExistsf

```go
func (a *Assertions) DirExistsf(path string, msg string, args ...interface{})
```

DirExistsf checks whether a directory exists in the given path. It also fails if the path is a file rather a directory or there is an error checking whether it exists.

## ElementsMatch

```go
func (a *Assertions) ElementsMatch(listA interface{}, listB interface{}, msgAndArgs ...interface{})
```

ElementsMatch asserts that the specified listA(array, slice...) is equal to specified listB(array, slice...) ignoring the order of the elements. If there are duplicate elements, the number of appearances of each of them in both lists should match.

a.ElementsMatch(\[1, 3, 2, 3], \[1, 3, 3, 2])

## ElementsMatchf

```go
func (a *Assertions) ElementsMatchf(listA interface{}, listB interface{}, msg string, args ...interface{})
```

ElementsMatchf asserts that the specified listA(array, slice...) is equal to specified listB(array, slice...) ignoring the order of the elements. If there are duplicate elements, the number of appearances of each of them in both lists should match.

a.ElementsMatchf(\[1, 3, 2, 3], \[1, 3, 3, 2], "error message %s", "formatted")

## Empty

```go
func (a *Assertions) Empty(object interface{}, msgAndArgs ...interface{})
```

Empty asserts that the given value is "empty".

[Zero values](https://go.dev/ref/spec#The_zero_value) are "empty".

Arrays are "empty" if every element is the zero value of the type (stricter than "empty").

Slices, maps and channels with zero length are "empty".

Pointer values are "empty" if the pointer is nil or if the pointed value is "empty".

	a.Empty(obj)

## Emptyf

```go
func (a *Assertions) Emptyf(object interface{}, msg string, args ...interface{})
```

Emptyf asserts that the given value is "empty".

[Zero values](https://go.dev/ref/spec#The_zero_value) are "empty".

Arrays are "empty" if every element is the zero value of the type (stricter than "empty").

Slices, maps and channels with zero length are "empty".

Pointer values are "empty" if the pointer is nil or if the pointed value is "empty".

	a.Emptyf(obj, "error message %s", "formatted")

## Equal

```go
func (a *Assertions) Equal(expected interface{}, actual interface{}, msgAndArgs ...interface{})
```

Equal asserts that two objects are equal.

	a.Equal(123, 123)

Pointer variable equality is determined based on the equality of the referenced values (as opposed to the memory addresses). Function equality cannot be determined and will always fail.

## EqualError

```go
func (a *Assertions) EqualError(theError error, errString string, msgAndArgs ...interface{})
```

EqualError asserts that a function returned a non-nil error (i.e. an error) and that it is equal to the provided error.

	actualObj, err := SomeFunction()
	a.EqualError(err,  expectedErrorString)

## EqualErrorf

```go
func (a *Assertions) EqualErrorf(theError error, errString string, msg string, args ...interface{})
```

EqualErrorf asserts that a function returned a non-nil error (i.e. an error) and that it is equal to the provided error.

	actualObj, err := SomeFunction()
	a.EqualErrorf(err,  expectedErrorString, "error message %s", "formatted")

## EqualExportedValues

```go
func (a *Assertions) EqualExportedValues(expected interface{}, actual interface{}, msgAndArgs ...interface{})
```

EqualExportedValues asserts that the types of two objects are equal and their public fields are also equal. This is useful for comparing structs that have private fields that could potentially differ.

	 type S struct {
		Exported     	int
		notExported   	int
	 }
	 a.EqualExportedValues(S{1, 2}, S{1, 3}) => true
	 a.EqualExportedValues(S{1, 2}, S{2, 3}) => false

## EqualExportedValuesf

```go
func (a *Assertions) EqualExportedValuesf(expected interface{}, actual interface{}, msg string, args ...interface{})
```

EqualExportedValuesf asserts that the types of two objects are equal and their public fields are also equal. This is useful for comparing structs that have private fields that could potentially differ.

	 type S struct {
		Exported     	int
		notExported   	int
	 }
	 a.EqualExportedValuesf(S{1, 2}, S{1, 3}, "error message %s", "formatted") => true
	 a.EqualExportedValuesf(S{1, 2}, S{2, 3}, "error message %s", "formatted") => false

## EqualValues

```go
func (a *Assertions) EqualValues(expected interface{}, actual interface{}, msgAndArgs ...interface{})
```

EqualValues asserts that two objects are equal or convertible to the larger type and equal.

	a.EqualValues(uint32(123), int32(123))

## EqualValuesf

```go
func (a *Assertions) EqualValuesf(expected interface{}, actual interface{}, msg string, args ...interface{})
```

EqualValuesf asserts that two objects are equal or convertible to the larger type and equal.

	a.EqualValuesf(uint32(123), int32(123), "error message %s", "formatted")

## Equalf

```go
func (a *Assertions) Equalf(expected interface{}, actual interface{}, msg string, args ...interface{})
```

Equalf asserts that two objects are equal.

	a.Equalf(123, 123, "error message %s", "formatted")

Pointer variable equality is determined based on the equality of the referenced values (as opposed to the memory addresses). Function equality cannot be determined and will always fail.

## Error

```go
func (a *Assertions) Error(err error, msgAndArgs ...interface{})
```

Error asserts that a function returned a non-nil error (ie. an error).

	actualObj, err := SomeFunction()
	a.Error(err)

## ErrorAs

```go
func (a *Assertions) ErrorAs(err error, target interface{}, msgAndArgs ...interface{})
```

ErrorAs asserts that at least one of the errors in err's chain matches target, and if so, sets target to that error value. This is a wrapper for errors.As.

## ErrorAsf

```go
func (a *Assertions) ErrorAsf(err error, target interface{}, msg string, args ...interface{})
```

ErrorAsf asserts that at least one of the errors in err's chain matches target, and if so, sets target to that error value. This is a wrapper for errors.As.

## ErrorContains

```go
func (a *Assertions) ErrorContains(theError error, contains string, msgAndArgs ...interface{})
```

ErrorContains asserts that a function returned a non-nil error (i.e. an error) and that the error contains the specified substring.

	actualObj, err := SomeFunction()
	a.ErrorContains(err,  expectedErrorSubString)

## ErrorContainsf

```go
func (a *Assertions) ErrorContainsf(theError error, contains string, msg string, args ...interface{})
```

ErrorContainsf asserts that a function returned a non-nil error (i.e. an error) and that the error contains the specified substring.

	actualObj, err := SomeFunction()
	a.ErrorContainsf(err,  expectedErrorSubString, "error message %s", "formatted")

## ErrorIs

```go
func (a *Assertions) ErrorIs(err error, target error, msgAndArgs ...interface{})
```

ErrorIs asserts that at least one of the errors in err's chain matches target. This is a wrapper for errors.Is.

## ErrorIsf

```go
func (a *Assertions) ErrorIsf(err error, target error, msg string, args ...interface{})
```

ErrorIsf asserts that at least one of the errors in err's chain matches target. This is a wrapper for errors.Is.

## Errorf

```go
func (a *Assertions) Errorf(err error, msg string, args ...interface{})
```

Errorf asserts that a function returned a non-nil error (ie. an error).

	actualObj, err := SomeFunction()
	a.Errorf(err, "error message %s", "formatted")

## Eventually

```go
func (a *Assertions) Eventually(condition func() bool, waitFor time.Duration, tick time.Duration, msgAndArgs ...interface{})
```

Eventually asserts that given condition will be met in waitFor time, periodically checking target function each tick.

	a.Eventually(func() bool { return true; }, time.Second, 10*time.Millisecond)

## EventuallyWithT

```go
func (a *Assertions) EventuallyWithT(condition func(collect *assert.CollectT), waitFor time.Duration, tick time.Duration, msgAndArgs ...interface{})
```

EventuallyWithT asserts that given condition will be met in waitFor time, periodically checking target function each tick. In contrast to Eventually, it supplies a CollectT to the condition function, so that the condition function can use the CollectT to call other assertions. The condition is considered "met" if no errors are raised in a tick. The supplied CollectT collects all errors from one tick (if there are any). If the condition is not met before waitFor, the collected errors of the last tick are copied to t.

	externalValue := false
	go func() {
		time.Sleep(8*time.Second)
		externalValue = true
	}()
	a.EventuallyWithT(func(c *assert.CollectT) {
		// add assertions as needed; any assertion failure will fail the current tick
		assert.True(c, externalValue, "expected 'externalValue' to be true")
	}, 10*time.Second, 1*time.Second, "external state has not changed to 'true'; still false")

## EventuallyWithTf

```go
func (a *Assertions) EventuallyWithTf(condition func(collect *assert.CollectT), waitFor time.Duration, tick time.Duration, msg string, args ...interface{})
```

EventuallyWithTf asserts that given condition will be met in waitFor time, periodically checking target function each tick. In contrast to Eventually, it supplies a CollectT to the condition function, so that the condition function can use the CollectT to call other assertions. The condition is considered "met" if no errors are raised in a tick. The supplied CollectT collects all errors from one tick (if there are any). If the condition is not met before waitFor, the collected errors of the last tick are copied to t.

	externalValue := false
	go func() {
		time.Sleep(8*time.Second)
		externalValue = true
	}()
	a.EventuallyWithTf(func(c *assert.CollectT) {
		// add assertions as needed; any assertion failure will fail the current tick
		assert.True(c, externalValue, "expected 'externalValue' to be true")
	}, 10*time.Second, 1*time.Second, "error message %s", "formatted")

## Eventuallyf

```go
func (a *Assertions) Eventuallyf(condition func() bool, waitFor time.Duration, tick time.Duration, msg string, args ...interface{})
```

Eventuallyf asserts that given condition will be met in waitFor time, periodically checking target function each tick.

	a.Eventuallyf(func() bool { return true; }, time.Second, 10*time.Millisecond, "error message %s", "formatted")

## Exactly

```go
func (a *Assertions) Exactly(expected interface{}, actual interface{}, msgAndArgs ...interface{})
```

Exactly asserts that two objects are equal in value and type.

	a.Exactly(int32(123), int64(123))

## Exactlyf

```go
func (a *Assertions) Exactlyf(expected interface{}, actual interface{}, msg string, args ...interface{})
```

Exactlyf asserts that two objects are equal in value and type.

	a.Exactlyf(int32(123), int64(123), "error message %s", "formatted")

## Fail

```go
func (a *Assertions) Fail(failureMessage string, msgAndArgs ...interface{})
```

Fail reports a failure through

## FailNow

```go
func (a *Assertions) FailNow(failureMessage string, msgAndArgs ...interface{})
```

FailNow fails test

## FailNowf

```go
func (a *Assertions) FailNowf(failureMessage string, msg string, args ...interface{})
```

FailNowf fails test

## Failf

```go
func (a *Assertions) Failf(failureMessage string, msg string, args ...interface{})
```

Failf reports a failure through

## False

```go
func (a *Assertions) False(value bool, msgAndArgs ...interface{})
```

False asserts that the specified value is false.

	a.False(myBool)

## Falsef

```go
func (a *Assertions) Falsef(value bool, msg string, args ...interface{})
```

Falsef asserts that the specified value is false.

	a.Falsef(myBool, "error message %s", "formatted")

## FileExists

```go
func (a *Assertions) FileExists(path string, msgAndArgs ...interface{})
```

FileExists checks whether a file exists in the given path. It also fails if the path points to a directory or there is an error when trying to check the file.

## FileExistsf

```go
func (a *Assertions) FileExistsf(path string, msg string, args ...interface{})
```

FileExistsf checks whether a file exists in the given path. It also fails if the path points to a directory or there is an error when trying to check the file.

## Greater

```go
func (a *Assertions) Greater(e1 interface{}, e2 interface{}, msgAndArgs ...interface{})
```

Greater asserts that the first element is greater than the second

	a.Greater(2, 1)
	a.Greater(float64(2), float64(1))
	a.Greater("b", "a")

## GreaterOrEqual

```go
func (a *Assertions) GreaterOrEqual(e1 interface{}, e2 interface{}, msgAndArgs ...interface{})
```

GreaterOrEqual asserts that the first element is greater than or equal to the second

	a.GreaterOrEqual(2, 1)
	a.GreaterOrEqual(2, 2)
	a.GreaterOrEqual("b", "a")
	a.GreaterOrEqual("b", "b")

## GreaterOrEqualf

```go
func (a *Assertions) GreaterOrEqualf(e1 interface{}, e2 interface{}, msg string, args ...interface{})
```

GreaterOrEqualf asserts that the first element is greater than or equal to the second

	a.GreaterOrEqualf(2, 1, "error message %s", "formatted")
	a.GreaterOrEqualf(2, 2, "error message %s", "formatted")
	a.GreaterOrEqualf("b", "a", "error message %s", "formatted")
	a.GreaterOrEqualf("b", "b", "error message %s", "formatted")

## Greaterf

```go
func (a *Assertions) Greaterf(e1 interface{}, e2 interface{}, msg string, args ...interface{})
```

Greaterf asserts that the first element is greater than the second

	a.Greaterf(2, 1, "error message %s", "formatted")
	a.Greaterf(float64(2), float64(1), "error message %s", "formatted")
	a.Greaterf("b", "a", "error message %s", "formatted")

## HTTPBodyContains

```go
func (a *Assertions) HTTPBodyContains(handler http.HandlerFunc, method string, url string, values url.Values, str interface{}, msgAndArgs ...interface{})
```

HTTPBodyContains asserts that a specified handler returns a body that contains a string.

	a.HTTPBodyContains(myHandler, "GET", "www.google.com", nil, "I'm Feeling Lucky")

## HTTPBodyContainsf

```go
func (a *Assertions) HTTPBodyContainsf(handler http.HandlerFunc, method string, url string, values url.Values, str interface{}, msg string, args ...interface{})
```

HTTPBodyContainsf asserts that a specified handler returns a body that contains a string.

	a.HTTPBodyContainsf(myHandler, "GET", "www.google.com", nil, "I'm Feeling Lucky", "error message %s", "formatted")

## HTTPBodyNotContains

```go
func (a *Assertions) HTTPBodyNotContains(handler http.HandlerFunc, method string, url string, values url.Values, str interface{}, msgAndArgs ...interface{})
```

HTTPBodyNotContains asserts that a specified handler returns a body that does not contain a string.

	a.HTTPBodyNotContains(myHandler, "GET", "www.google.com", nil, "I'm Feeling Lucky")

## HTTPBodyNotContainsf

```go
func (a *Assertions) HTTPBodyNotContainsf(handler http.HandlerFunc, method string, url string, values url.Values, str interface{}, msg string, args ...interface{})
```

HTTPBodyNotContainsf asserts that a specified handler returns a body that does not contain a string.

	a.HTTPBodyNotContainsf(myHandler, "GET", "www.google.com", nil, "I'm Feeling Lucky", "error message %s", "formatted")

## HTTPError

```go
func (a *Assertions) HTTPError(handler http.HandlerFunc, method string, url string, values url.Values, msgAndArgs ...interface{})
```

HTTPError asserts that a specified handler returns an error status code.

	a.HTTPError(myHandler, "POST", "/a/b/c", url.Values{"a": []string{"b", "c"}}

## HTTPErrorf

```go
func (a *Assertions) HTTPErrorf(handler http.HandlerFunc, method string, url string, values url.Values, msg string, args ...interface{})
```

HTTPErrorf asserts that a specified handler returns an error status code.

	a.HTTPErrorf(myHandler, "POST", "/a/b/c", url.Values{"a": []string{"b", "c"}}

## HTTPRedirect

```go
func (a *Assertions) HTTPRedirect(handler http.HandlerFunc, method string, url string, values url.Values, msgAndArgs ...interface{})
```

HTTPRedirect asserts that a specified handler returns a redirect status code.

	a.HTTPRedirect(myHandler, "GET", "/a/b/c", url.Values{"a": []string{"b", "c"}}

## HTTPRedirectf

```go
func (a *Assertions) HTTPRedirectf(handler http.HandlerFunc, method string, url string, values url.Values, msg string, args ...interface{})
```

HTTPRedirectf asserts that a specified handler returns a redirect status code.

	a.HTTPRedirectf(myHandler, "GET", "/a/b/c", url.Values{"a": []string{"b", "c"}}

## HTTPStatusCode

```go
func (a *Assertions) HTTPStatusCode(handler http.HandlerFunc, method string, url string, values url.Values, statuscode int, msgAndArgs ...interface{})
```

HTTPStatusCode asserts that a specified handler returns a specified status code.

	a.HTTPStatusCode(myHandler, "GET", "/notImplemented", nil, 501)

## HTTPStatusCodef

```go
func (a *Assertions) HTTPStatusCodef(handler http.HandlerFunc, method string, url string, values url.Values, statuscode int, msg string, args ...interface{})
```

HTTPStatusCodef asserts that a specified handler returns a specified status code.

	a.HTTPStatusCodef(myHandler, "GET", "/notImplemented", nil, 501, "error message %s", "formatted")

## HTTPSuccess

```go
func (a *Assertions) HTTPSuccess(handler http.HandlerFunc, method string, url string, values url.Values, msgAndArgs ...interface{})
```

HTTPSuccess asserts that a specified handler returns a success status code.

	a.HTTPSuccess(myHandler, "POST", "http://www.google.com", nil)

## HTTPSuccessf

```go
func (a *Assertions) HTTPSuccessf(handler http.HandlerFunc, method string, url string, values url.Values, msg string, args ...interface{})
```

HTTPSuccessf asserts that a specified handler returns a success status code.

	a.HTTPSuccessf(myHandler, "POST", "http://www.google.com", nil, "error message %s", "formatted")

## Implements

```go
func (a *Assertions) Implements(interfaceObject interface{}, object interface{}, msgAndArgs ...interface{})
```

Implements asserts that an object is implemented by the specified interface.

	a.Implements((*MyInterface)(nil), new(MyObject))

## Implementsf

```go
func (a *Assertions) Implementsf(interfaceObject interface{}, object interface{}, msg string, args ...interface{})
```

Implementsf asserts that an object is implemented by the specified interface.

	a.Implementsf((*MyInterface)(nil), new(MyObject), "error message %s", "formatted")

## InDelta

```go
func (a *Assertions) InDelta(expected interface{}, actual interface{}, delta float64, msgAndArgs ...interface{})
```

InDelta asserts that the two numerals are within delta of each other.

	a.InDelta(math.Pi, 22/7.0, 0.01)

## InDeltaMapValues

```go
func (a *Assertions) InDeltaMapValues(expected interface{}, actual interface{}, delta float64, msgAndArgs ...interface{})
```

InDeltaMapValues is the same as InDelta, but it compares all values between two maps. Both maps must have exactly the same keys.

## InDeltaMapValuesf

```go
func (a *Assertions) InDeltaMapValuesf(expected interface{}, actual interface{}, delta float64, msg string, args ...interface{})
```

InDeltaMapValuesf is the same as InDelta, but it compares all values between two maps. Both maps must have exactly the same keys.

## InDeltaSlice

```go
func (a *Assertions) InDeltaSlice(expected interface{}, actual interface{}, delta float64, msgAndArgs ...interface{})
```

InDeltaSlice is the same as InDelta, except it compares two slices.

## InDeltaSlicef

```go
func (a *Assertions) InDeltaSlicef(expected interface{}, actual interface{}, delta float64, msg string, args ...interface{})
```

InDeltaSlicef is the same as InDelta, except it compares two slices.

## InDeltaf

```go
func (a *Assertions) InDeltaf(expected interface{}, actual interface{}, delta float64, msg string, args ...interface{})
```

InDeltaf asserts that the two numerals are within delta of each other.

	a.InDeltaf(math.Pi, 22/7.0, 0.01, "error message %s", "formatted")

## InEpsilon

```go
func (a *Assertions) InEpsilon(expected interface{}, actual interface{}, epsilon float64, msgAndArgs ...interface{})
```

InEpsilon asserts that expected and actual have a relative error less than epsilon

## InEpsilonSlice

```go
func (a *Assertions) InEpsilonSlice(expected interface{}, actual interface{}, epsilon float64, msgAndArgs ...interface{})
```

InEpsilonSlice is the same as InEpsilon, except it compares each value from two slices.

## InEpsilonSlicef

```go
func (a *Assertions) InEpsilonSlicef(expected interface{}, actual interface{}, epsilon float64, msg string, args ...interface{})
```

InEpsilonSlicef is the same as InEpsilon, except it compares each value from two slices.

## InEpsilonf

```go
func (a *Assertions) InEpsilonf(expected interface{}, actual interface{}, epsilon float64, msg string, args ...interface{})
```

InEpsilonf asserts that expected and actual have a relative error less than epsilon

## IsDecreasing

```go
func (a *Assertions) IsDecreasing(object interface{}, msgAndArgs ...interface{})
```

IsDecreasing asserts that the collection is decreasing

	a.IsDecreasing([]int{2, 1, 0})
	a.IsDecreasing([]float{2, 1})
	a.IsDecreasing([]string{"b", "a"})

## IsDecreasingf

```go
func (a *Assertions) IsDecreasingf(object interface{}, msg string, args ...interface{})
```

IsDecreasingf asserts that the collection is decreasing

	a.IsDecreasingf([]int{2, 1, 0}, "error message %s", "formatted")
	a.IsDecreasingf([]float{2, 1}, "error message %s", "formatted")
	a.IsDecreasingf([]string{"b", "a"}, "error message %s", "formatted")

## IsIncreasing

```go
func (a *Assertions) IsIncreasing(object interface{}, msgAndArgs ...interface{})
```

IsIncreasing asserts that the collection is increasing

	a.IsIncreasing([]int{1, 2, 3})
	a.IsIncreasing([]float{1, 2})
	a.IsIncreasing([]string{"a", "b"})

## IsIncreasingf

```go
func (a *Assertions) IsIncreasingf(object interface{}, msg string, args ...interface{})
```

IsIncreasingf asserts that the collection is increasing

	a.IsIncreasingf([]int{1, 2, 3}, "error message %s", "formatted")
	a.IsIncreasingf([]float{1, 2}, "error message %s", "formatted")
	a.IsIncreasingf([]string{"a", "b"}, "error message %s", "formatted")

## IsNonDecreasing

```go
func (a *Assertions) IsNonDecreasing(object interface{}, msgAndArgs ...interface{})
```

IsNonDecreasing asserts that the collection is not decreasing

	a.IsNonDecreasing([]int{1, 1, 2})
	a.IsNonDecreasing([]float{1, 2})
	a.IsNonDecreasing([]string{"a", "b"})

## IsNonDecreasingf

```go
func (a *Assertions) IsNonDecreasingf(object interface{}, msg string, args ...interface{})
```

IsNonDecreasingf asserts that the collection is not decreasing

	a.IsNonDecreasingf([]int{1, 1, 2}, "error message %s", "formatted")
	a.IsNonDecreasingf([]float{1, 2}, "error message %s", "formatted")
	a.IsNonDecreasingf([]string{"a", "b"}, "error message %s", "formatted")

## IsNonIncreasing

```go
func (a *Assertions) IsNonIncreasing(object interface{}, msgAndArgs ...interface{})
```

IsNonIncreasing asserts that the collection is not increasing

	a.IsNonIncreasing([]int{2, 1, 1})
	a.IsNonIncreasing([]float{2, 1})
	a.IsNonIncreasing([]string{"b", "a"})

## IsNonIncreasingf

```go
func (a *Assertions) IsNonIncreasingf(object interface{}, msg string, args ...interface{})
```

IsNonIncreasingf asserts that the collection is not increasing

	a.IsNonIncreasingf([]int{2, 1, 1}, "error message %s", "formatted")
	a.IsNonIncreasingf([]float{2, 1}, "error message %s", "formatted")
	a.IsNonIncreasingf([]string{"b", "a"}, "error message %s", "formatted")

## IsNotType

```go
func (a *Assertions) IsNotType(theType interface{}, object interface{}, msgAndArgs ...interface{})
```

IsNotType asserts that the specified objects are not of the same type.

	a.IsNotType(&NotMyStruct{}, &MyStruct{})

## IsNotTypef

```go
func (a *Assertions) IsNotTypef(theType interface{}, object interface{}, msg string, args ...interface{})
```

IsNotTypef asserts that the specified objects are not of the same type.

	a.IsNotTypef(&NotMyStruct{}, &MyStruct{}, "error message %s", "formatted")

## IsType

```go
func (a *Assertions) IsType(expectedType interface{}, object interface{}, msgAndArgs ...interface{})
```

IsType asserts that the specified objects are of the same type.

	a.IsType(&MyStruct{}, &MyStruct{})

## IsTypef

```go
func (a *Assertions) IsTypef(expectedType interface{}, object interface{}, msg string, args ...interface{})
```

IsTypef asserts that the specified objects are of the same type.

	a.IsTypef(&MyStruct{}, &MyStruct{}, "error message %s", "formatted")

## JSONEq

```go
func (a *Assertions) JSONEq(expected string, actual string, msgAndArgs ...interface{})
```

JSONEq asserts that two JSON strings are equivalent.

	a.JSONEq(`{"hello": "world", "foo": "bar"}`, `{"foo": "bar", "hello": "world"}`)

## JSONEqf

```go
func (a *Assertions) JSONEqf(expected string, actual string, msg string, args ...interface{})
```

JSONEqf asserts that two JSON strings are equivalent.

	a.JSONEqf(`{"hello": "world", "foo": "bar"}`, `{"foo": "bar", "hello": "world"}`, "error message %s", "formatted")

## Len

```go
func (a *Assertions) Len(object interface{}, length int, msgAndArgs ...interface{})
```

Len asserts that the specified object has specific length. Len also fails if the object has a type that len() not accept.

	a.Len(mySlice, 3)

## Lenf

```go
func (a *Assertions) Lenf(object interface{}, length int, msg string, args ...interface{})
```

Lenf asserts that the specified object has specific length. Lenf also fails if the object has a type that len() not accept.

	a.Lenf(mySlice, 3, "error message %s", "formatted")

## Less

```go
func (a *Assertions) Less(e1 interface{}, e2 interface{}, msgAndArgs ...interface{})
```

Less asserts that the first element is less than the second

	a.Less(1, 2)
	a.Less(float64(1), float64(2))
	a.Less("a", "b")

## LessOrEqual

```go
func (a *Assertions) LessOrEqual(e1 interface{}, e2 interface{}, msgAndArgs ...interface{})
```

LessOrEqual asserts that the first element is less than or equal to the second

	a.LessOrEqual(1, 2)
	a.LessOrEqual(2, 2)
	a.LessOrEqual("a", "b")
	a.LessOrEqual("b", "b")

## LessOrEqualf

```go
func (a *Assertions) LessOrEqualf(e1 interface{}, e2 interface{}, msg string, args ...interface{})
```

LessOrEqualf asserts that the first element is less than or equal to the second

	a.LessOrEqualf(1, 2, "error message %s", "formatted")
	a.LessOrEqualf(2, 2, "error message %s", "formatted")
	a.LessOrEqualf("a", "b", "error message %s", "formatted")
	a.LessOrEqualf("b", "b", "error message %s", "formatted")

## Lessf

```go
func (a *Assertions) Lessf(e1 interface{}, e2 interface{}, msg string, args ...interface{})
```

Lessf asserts that the first element is less than the second

	a.Lessf(1, 2, "error message %s", "formatted")
	a.Lessf(float64(1), float64(2), "error message %s", "formatted")
	a.Lessf("a", "b", "error message %s", "formatted")

## Negative

```go
func (a *Assertions) Negative(e interface{}, msgAndArgs ...interface{})
```

Negative asserts that the specified element is negative

	a.Negative(-1)
	a.Negative(-1.23)

## Negativef

```go
func (a *Assertions) Negativef(e interface{}, msg string, args ...interface{})
```

Negativef asserts that the specified element is negative

	a.Negativef(-1, "error message %s", "formatted")
	a.Negativef(-1.23, "error message %s", "formatted")

## Never

```go
func (a *Assertions) Never(condition func() bool, waitFor time.Duration, tick time.Duration, msgAndArgs ...interface{})
```

Never asserts that the given condition doesn't satisfy in waitFor time, periodically checking the target function each tick.

	a.Never(func() bool { return false; }, time.Second, 10*time.Millisecond)

## Neverf

```go
func (a *Assertions) Neverf(condition func() bool, waitFor time.Duration, tick time.Duration, msg string, args ...interface{})
```

Neverf asserts that the given condition doesn't satisfy in waitFor time, periodically checking the target function each tick.

	a.Neverf(func() bool { return false; }, time.Second, 10*time.Millisecond, "error message %s", "formatted")

## Nil

```go
func (a *Assertions) Nil(object interface{}, msgAndArgs ...interface{})
```

Nil asserts that the specified object is nil.

	a.Nil(err)

## Nilf

```go
func (a *Assertions) Nilf(object interface{}, msg string, args ...interface{})
```

Nilf asserts that the specified object is nil.

	a.Nilf(err, "error message %s", "formatted")

## NoDirExists

```go
func (a *Assertions) NoDirExists(path string, msgAndArgs ...interface{})
```

NoDirExists checks whether a directory does not exist in the given path. It fails if the path points to an existing \_directory\_ only.

## NoDirExistsf

```go
func (a *Assertions) NoDirExistsf(path string, msg string, args ...interface{})
```

NoDirExistsf checks whether a directory does not exist in the given path. It fails if the path points to an existing \_directory\_ only.

## NoError

```go
func (a *Assertions) NoError(err error, msgAndArgs ...interface{})
```

NoError asserts that a function returned a nil error (ie. no error).

	actualObj, err := SomeFunction()
	a.NoError(err)
	a.Equal(expectedObj, actualObj)

## NoErrorf

```go
func (a *Assertions) NoErrorf(err error, msg string, args ...interface{})
```

NoErrorf asserts that a function returned a nil error (ie. no error).

	actualObj, err := SomeFunction()
	a.NoErrorf(err, "error message %s", "formatted")
	a.Equal(expectedObj, actualObj)

## NoFileExists

```go
func (a *Assertions) NoFileExists(path string, msgAndArgs ...interface{})
```

NoFileExists checks whether a file does not exist in a given path. It fails if the path points to an existing \_file\_ only.

## NoFileExistsf

```go
func (a *Assertions) NoFileExistsf(path string, msg string, args ...interface{})
```

NoFileExistsf checks whether a file does not exist in a given path. It fails if the path points to an existing \_file\_ only.

## NotContains

```go
func (a *Assertions) NotContains(s interface{}, contains interface{}, msgAndArgs ...interface{})
```

NotContains asserts that the specified string, list(array, slice...) or map does NOT contain the specified substring or element.

	a.NotContains("Hello World", "Earth")
	a.NotContains(["Hello", "World"], "Earth")
	a.NotContains({"Hello": "World"}, "Earth")

## NotContainsf

```go
func (a *Assertions) NotContainsf(s interface{}, contains interface{}, msg string, args ...interface{})
```

NotContainsf asserts that the specified string, list(array, slice...) or map does NOT contain the specified substring or element.

	a.NotContainsf("Hello World", "Earth", "error message %s", "formatted")
	a.NotContainsf(["Hello", "World"], "Earth", "error message %s", "formatted")
	a.NotContainsf({"Hello": "World"}, "Earth", "error message %s", "formatted")

## NotElementsMatch

```go
func (a *Assertions) NotElementsMatch(listA interface{}, listB interface{}, msgAndArgs ...interface{})
```

NotElementsMatch asserts that the specified listA(array, slice...) is NOT equal to specified listB(array, slice...) ignoring the order of the elements. If there are duplicate elements, the number of appearances of each of them in both lists should not match. This is an inverse of ElementsMatch.

a.NotElementsMatch(\[1, 1, 2, 3], \[1, 1, 2, 3]) -> false

a.NotElementsMatch(\[1, 1, 2, 3], \[1, 2, 3]) -> true

a.NotElementsMatch(\[1, 2, 3], \[1, 2, 4]) -> true

## NotElementsMatchf

```go
func (a *Assertions) NotElementsMatchf(listA interface{}, listB interface{}, msg string, args ...interface{})
```

NotElementsMatchf asserts that the specified listA(array, slice...) is NOT equal to specified listB(array, slice...) ignoring the order of the elements. If there are duplicate elements, the number of appearances of each of them in both lists should not match. This is an inverse of ElementsMatch.

a.NotElementsMatchf(\[1, 1, 2, 3], \[1, 1, 2, 3], "error message %s", "formatted") -> false

a.NotElementsMatchf(\[1, 1, 2, 3], \[1, 2, 3], "error message %s", "formatted") -> true

a.NotElementsMatchf(\[1, 2, 3], \[1, 2, 4], "error message %s", "formatted") -> true

## NotEmpty

```go
func (a *Assertions) NotEmpty(object interface{}, msgAndArgs ...interface{})
```

NotEmpty asserts that the specified object is NOT [Empty](#func-Empty).

	a.NotEmpty(obj)
	a.Equal("two", obj[1])

## NotEmptyf

```go
func (a *Assertions) NotEmptyf(object interface{}, msg string, args ...interface{})
```

NotEmptyf asserts that the specified object is NOT [Empty](#func-Empty).

	a.NotEmptyf(obj, "error message %s", "formatted")
	a.Equal("two", obj[1])

## NotEqual

```go
func (a *Assertions) NotEqual(expected interface{}, actual interface{}, msgAndArgs ...interface{})
```

NotEqual asserts that the specified values are NOT equal.

	a.NotEqual(obj1, obj2)

Pointer variable equality is determined based on the equality of the referenced values (as opposed to the memory addresses).

## NotEqualValues

```go
func (a *Assertions) NotEqualValues(expected interface{}, actual interface{}, msgAndArgs ...interface{})
```

NotEqualValues asserts that two objects are not equal even when converted to the same type

	a.NotEqualValues(obj1, obj2)

## NotEqualValuesf

```go
func (a *Assertions) NotEqualValuesf(expected interface{}, actual interface{}, msg string, args ...interface{})
```

NotEqualValuesf asserts that two objects are not equal even when converted to the same type

	a.NotEqualValuesf(obj1, obj2, "error message %s", "formatted")

## NotEqualf

```go
func (a *Assertions) NotEqualf(expected interface{}, actual interface{}, msg string, args ...interface{})
```

NotEqualf asserts that the specified values are NOT equal.

	a.NotEqualf(obj1, obj2, "error message %s", "formatted")

Pointer variable equality is determined based on the equality of the referenced values (as opposed to the memory addresses).

## NotErrorAs

```go
func (a *Assertions) NotErrorAs(err error, target interface{}, msgAndArgs ...interface{})
```

NotErrorAs asserts that none of the errors in err's chain matches target, but if so, sets target to that error value.

## NotErrorAsf

```go
func (a *Assertions) NotErrorAsf(err error, target interface{}, msg string, args ...interface{})
```

NotErrorAsf asserts that none of the errors in err's chain matches target, but if so, sets target to that error value.

## NotErrorIs

```go
func (a *Assertions) NotErrorIs(err error, target error, msgAndArgs ...interface{})
```

NotErrorIs asserts that none of the errors in err's chain matches target. This is a wrapper for errors.Is.

## NotErrorIsf

```go
func (a *Assertions) NotErrorIsf(err error, target error, msg string, args ...interface{})
```

NotErrorIsf asserts that none of the errors in err's chain matches target. This is a wrapper for errors.Is.

## NotImplements

```go
func (a *Assertions) NotImplements(interfaceObject interface{}, object interface{}, msgAndArgs ...interface{})
```

NotImplements asserts that an object does not implement the specified interface.

	a.NotImplements((*MyInterface)(nil), new(MyObject))

## NotImplementsf

```go
func (a *Assertions) NotImplementsf(interfaceObject interface{}, object interface{}, msg string, args ...interface{})
```

NotImplementsf asserts that an object does not implement the specified interface.

	a.NotImplementsf((*MyInterface)(nil), new(MyObject), "error message %s", "formatted")

## NotNil

```go
func (a *Assertions) NotNil(object interface{}, msgAndArgs ...interface{})
```

NotNil asserts that the specified object is not nil.

	a.NotNil(err)

## NotNilf

```go
func (a *Assertions) NotNilf(object interface{}, msg string, args ...interface{})
```

NotNilf asserts that the specified object is not nil.

	a.NotNilf(err, "error message %s", "formatted")

## NotPanics

```go
func (a *Assertions) NotPanics(f assert.PanicTestFunc, msgAndArgs ...interface{})
```

NotPanics asserts that the code inside the specified PanicTestFunc does NOT panic.

	a.NotPanics(func(){ RemainCalm() })

## NotPanicsf

```go
func (a *Assertions) NotPanicsf(f assert.PanicTestFunc, msg string, args ...interface{})
```

NotPanicsf asserts that the code inside the specified PanicTestFunc does NOT panic.

	a.NotPanicsf(func(){ RemainCalm() }, "error message %s", "formatted")

## NotRegexp

```go
func (a *Assertions) NotRegexp(rx interface{}, str interface{}, msgAndArgs ...interface{})
```

NotRegexp asserts that a specified regexp does not match a string.

	a.NotRegexp(regexp.MustCompile("starts"), "it's starting")
	a.NotRegexp("^start", "it's not starting")

## NotRegexpf

```go
func (a *Assertions) NotRegexpf(rx interface{}, str interface{}, msg string, args ...interface{})
```

NotRegexpf asserts that a specified regexp does not match a string.

	a.NotRegexpf(regexp.MustCompile("starts"), "it's starting", "error message %s", "formatted")
	a.NotRegexpf("^start", "it's not starting", "error message %s", "formatted")

## NotSame

```go
func (a *Assertions) NotSame(expected interface{}, actual interface{}, msgAndArgs ...interface{})
```

NotSame asserts that two pointers do not reference the same object.

	a.NotSame(ptr1, ptr2)

Both arguments must be pointer variables. Pointer variable sameness is determined based on the equality of both type and value.

## NotSamef

```go
func (a *Assertions) NotSamef(expected interface{}, actual interface{}, msg string, args ...interface{})
```

NotSamef asserts that two pointers do not reference the same object.

	a.NotSamef(ptr1, ptr2, "error message %s", "formatted")

Both arguments must be pointer variables. Pointer variable sameness is determined based on the equality of both type and value.

## NotSubset

```go
func (a *Assertions) NotSubset(list interface{}, subset interface{}, msgAndArgs ...interface{})
```

NotSubset asserts that the list (array, slice, or map) does NOT contain all elements given in the subset (array, slice, or map). Map elements are key-value pairs unless compared with an array or slice where only the map key is evaluated.

	a.NotSubset([1, 3, 4], [1, 2])
	a.NotSubset({"x": 1, "y": 2}, {"z": 3})
	a.NotSubset([1, 3, 4], {1: "one", 2: "two"})
	a.NotSubset({"x": 1, "y": 2}, ["z"])

## NotSubsetf

```go
func (a *Assertions) NotSubsetf(list interface{}, subset interface{}, msg string, args ...interface{})
```

NotSubsetf asserts that the list (array, slice, or map) does NOT contain all elements given in the subset (array, slice, or map). Map elements are key-value pairs unless compared with an array or slice where only the map key is evaluated.

	a.NotSubsetf([1, 3, 4], [1, 2], "error message %s", "formatted")
	a.NotSubsetf({"x": 1, "y": 2}, {"z": 3}, "error message %s", "formatted")
	a.NotSubsetf([1, 3, 4], {1: "one", 2: "two"}, "error message %s", "formatted")
	a.NotSubsetf({"x": 1, "y": 2}, ["z"], "error message %s", "formatted")

## NotZero

```go
func (a *Assertions) NotZero(i interface{}, msgAndArgs ...interface{})
```

NotZero asserts that i is not the zero value for its type.

## NotZerof

```go
func (a *Assertions) NotZerof(i interface{}, msg string, args ...interface{})
```

NotZerof asserts that i is not the zero value for its type.

## Panics

```go
func (a *Assertions) Panics(f assert.PanicTestFunc, msgAndArgs ...interface{})
```

Panics asserts that the code inside the specified PanicTestFunc panics.

	a.Panics(func(){ GoCrazy() })

## PanicsWithError

```go
func (a *Assertions) PanicsWithError(errString string, f assert.PanicTestFunc, msgAndArgs ...interface{})
```

PanicsWithError asserts that the code inside the specified PanicTestFunc panics, and that the recovered panic value is an error that satisfies the EqualError comparison.

	a.PanicsWithError("crazy error", func(){ GoCrazy() })

## PanicsWithErrorf

```go
func (a *Assertions) PanicsWithErrorf(errString string, f assert.PanicTestFunc, msg string, args ...interface{})
```

PanicsWithErrorf asserts that the code inside the specified PanicTestFunc panics, and that the recovered panic value is an error that satisfies the EqualError comparison.

	a.PanicsWithErrorf("crazy error", func(){ GoCrazy() }, "error message %s", "formatted")

## PanicsWithValue

```go
func (a *Assertions) PanicsWithValue(expected interface{}, f assert.PanicTestFunc, msgAndArgs ...interface{})
```

PanicsWithValue asserts that the code inside the specified PanicTestFunc panics, and that the recovered panic value equals the expected panic value.

	a.PanicsWithValue("crazy error", func(){ GoCrazy() })

## PanicsWithValuef

```go
func (a *Assertions) PanicsWithValuef(expected interface{}, f assert.PanicTestFunc, msg string, args ...interface{})
```

PanicsWithValuef asserts that the code inside the specified PanicTestFunc panics, and that the recovered panic value equals the expected panic value.

	a.PanicsWithValuef("crazy error", func(){ GoCrazy() }, "error message %s", "formatted")

## Panicsf

```go
func (a *Assertions) Panicsf(f assert.PanicTestFunc, msg string, args ...interface{})
```

Panicsf asserts that the code inside the specified PanicTestFunc panics.

	a.Panicsf(func(){ GoCrazy() }, "error message %s", "formatted")

## Positive

```go
func (a *Assertions) Positive(e interface{}, msgAndArgs ...interface{})
```

Positive asserts that the specified element is positive

	a.Positive(1)
	a.Positive(1.23)

## Positivef

```go
func (a *Assertions) Positivef(e interface{}, msg string, args ...interface{})
```

Positivef asserts that the specified element is positive

	a.Positivef(1, "error message %s", "formatted")
	a.Positivef(1.23, "error message %s", "formatted")

## Regexp

```go
func (a *Assertions) Regexp(rx interface{}, str interface{}, msgAndArgs ...interface{})
```

Regexp asserts that a specified regexp matches a string.

	a.Regexp(regexp.MustCompile("start"), "it's starting")
	a.Regexp("start...$", "it's not starting")

## Regexpf

```go
func (a *Assertions) Regexpf(rx interface{}, str interface{}, msg string, args ...interface{})
```

Regexpf asserts that a specified regexp matches a string.

	a.Regexpf(regexp.MustCompile("start"), "it's starting", "error message %s", "formatted")
	a.Regexpf("start...$", "it's not starting", "error message %s", "formatted")

## Same

```go
func (a *Assertions) Same(expected interface{}, actual interface{}, msgAndArgs ...interface{})
```

Same asserts that two pointers reference the same object.

	a.Same(ptr1, ptr2)

Both arguments must be pointer variables. Pointer variable sameness is determined based on the equality of both type and value.

## Samef

```go
func (a *Assertions) Samef(expected interface{}, actual interface{}, msg string, args ...interface{})
```

Samef asserts that two pointers reference the same object.

	a.Samef(ptr1, ptr2, "error message %s", "formatted")

Both arguments must be pointer variables. Pointer variable sameness is determined based on the equality of both type and value.

## Subset

```go
func (a *Assertions) Subset(list interface{}, subset interface{}, msgAndArgs ...interface{})
```

Subset asserts that the list (array, slice, or map) contains all elements given in the subset (array, slice, or map). Map elements are key-value pairs unless compared with an array or slice where only the map key is evaluated.

	a.Subset([1, 2, 3], [1, 2])
	a.Subset({"x": 1, "y": 2}, {"x": 1})
	a.Subset([1, 2, 3], {1: "one", 2: "two"})
	a.Subset({"x": 1, "y": 2}, ["x"])

## Subsetf

```go
func (a *Assertions) Subsetf(list interface{}, subset interface{}, msg string, args ...interface{})
```

Subsetf asserts that the list (array, slice, or map) contains all elements given in the subset (array, slice, or map). Map elements are key-value pairs unless compared with an array or slice where only the map key is evaluated.

	a.Subsetf([1, 2, 3], [1, 2], "error message %s", "formatted")
	a.Subsetf({"x": 1, "y": 2}, {"x": 1}, "error message %s", "formatted")
	a.Subsetf([1, 2, 3], {1: "one", 2: "two"}, "error message %s", "formatted")
	a.Subsetf({"x": 1, "y": 2}, ["x"], "error message %s", "formatted")

## True

```go
func (a *Assertions) True(value bool, msgAndArgs ...interface{})
```

True asserts that the specified value is true.

	a.True(myBool)

## Truef

```go
func (a *Assertions) Truef(value bool, msg string, args ...interface{})
```

Truef asserts that the specified value is true.

	a.Truef(myBool, "error message %s", "formatted")

## WithinDuration

```go
func (a *Assertions) WithinDuration(expected time.Time, actual time.Time, delta time.Duration, msgAndArgs ...interface{})
```

WithinDuration asserts that the two times are within duration delta of each other.

	a.WithinDuration(time.Now(), time.Now(), 10*time.Second)

## WithinDurationf

```go
func (a *Assertions) WithinDurationf(expected time.Time, actual time.Time, delta time.Duration, msg string, args ...interface{})
```

WithinDurationf asserts that the two times are within duration delta of each other.

	a.WithinDurationf(time.Now(), time.Now(), 10*time.Second, "error message %s", "formatted")

## WithinRange

```go
func (a *Assertions) WithinRange(actual time.Time, start time.Time, end time.Time, msgAndArgs ...interface{})
```

WithinRange asserts that a time is within a time range (inclusive).

	a.WithinRange(time.Now(), time.Now().Add(-time.Second), time.Now().Add(time.Second))

## WithinRangef

```go
func (a *Assertions) WithinRangef(actual time.Time, start time.Time, end time.Time, msg string, args ...interface{})
```

WithinRangef asserts that a time is within a time range (inclusive).

	a.WithinRangef(time.Now(), time.Now().Add(-time.Second), time.Now().Add(time.Second), "error message %s", "formatted")

## YAMLEq

```go
func (a *Assertions) YAMLEq(expected string, actual string, msgAndArgs ...interface{})
```

YAMLEq asserts that the first documents in the two YAML strings are equivalent.

	expected := `---
	key: value
	---
	key: this is a second document, it is not evaluated
	`
	actual := `---
	key: value
	---
	key: this is a subsequent document, it is not evaluated
	`
	a.YAMLEq(expected, actual)

## YAMLEqf

```go
func (a *Assertions) YAMLEqf(expected string, actual string, msg string, args ...interface{})
```

YAMLEqf asserts that the first documents in the two YAML strings are equivalent.

	expected := `---
	key: value
	---
	key: this is a second document, it is not evaluated
	`
	actual := `---
	key: value
	---
	key: this is a subsequent document, it is not evaluated
	`
	a.YAMLEqf(expected, actual, "error message %s", "formatted")

## Zero

```go
func (a *Assertions) Zero(i interface{}, msgAndArgs ...interface{})
```

Zero asserts that i is the zero value for its type.

## Zerof

```go
func (a *Assertions) Zerof(i interface{}, msg string, args ...interface{})
```

Zerof asserts that i is the zero value for its type.

## BoolAssertionFunc

```go
type BoolAssertionFunc = func(TestingT, bool, ...interface{})
```

BoolAssertionFunc is a common function prototype when validating a bool value.  Can be useful for table driven tests.

### Example: BoolAssertionFunc

```go
{
	t := &testing.T{}

	isOkay := func(x int) bool {
		return x >= 42
	}

	tests := []struct {
		name      string
		arg       int
		assertion BoolAssertionFunc
	}{
		{"-1 is bad", -1, False},
		{"42 is good", 42, True},
		{"41 is bad", 41, False},
		{"45 is cool", 45, True},
	}

	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			tt.assertion(t, isOkay(tt.arg))
		})
	}
}
```

## ComparisonAssertionFunc

```go
type ComparisonAssertionFunc = func(TestingT, interface{}, interface{}, ...interface{})
```

ComparisonAssertionFunc is a common function prototype when comparing two values.  Can be useful for table driven tests.

### Example: ComparisonAssertionFunc

```go
{
	t := &testing.T{}

	adder := func(x, y int) int {
		return x + y
	}

	type args struct {
		x int
		y int
	}

	tests := []struct {
		name      string
		args      args
		expect    int
		assertion ComparisonAssertionFunc
	}{
		{"2+2=4", args{2, 2}, 4, Equal},
		{"2+2!=5", args{2, 2}, 5, NotEqual},
		{"2+3==5", args{2, 3}, 5, Exactly},
	}

	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			tt.assertion(t, tt.expect, adder(tt.args.x, tt.args.y))
		})
	}
}
```

## ErrorAssertionFunc

```go
type ErrorAssertionFunc = func(TestingT, error, ...interface{})
```

ErrorAssertionFunc is a common function prototype when validating an error value.  Can be useful for table driven tests.

### Example: ErrorAssertionFunc

```go
{
	t := &testing.T{}

	dumbParseNum := func(input string, v interface{}) error {
		return json.Unmarshal([]byte(input), v)
	}

	tests := []struct {
		name      string
		arg       string
		assertion ErrorAssertionFunc
	}{
		{"1.2 is number", "1.2", NoError},
		{"1.2.3 not number", "1.2.3", Error},
		{"true is not number", "true", Error},
		{"3 is number", "3", NoError},
	}

	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			var x float64
			tt.assertion(t, dumbParseNum(tt.arg, &x))
		})
	}
}
```

## TestingT

```go
type TestingT interface {
	Errorf(format string, args ...interface{})
	FailNow()
}
```

TestingT is an interface wrapper around \*testing.T

- `Errorf: func(format string, args ...interface{})`: 
- `FailNow: func()`: 

## ValueAssertionFunc

```go
type ValueAssertionFunc = func(TestingT, interface{}, ...interface{})
```

ValueAssertionFunc is a common function prototype when validating a single value.  Can be useful for table driven tests.

### Example: ValueAssertionFunc

```go
{
	t := &testing.T{}

	dumbParse := func(input string) interface{} {
		var x interface{}
		json.Unmarshal([]byte(input), &x)
		return x
	}

	tests := []struct {
		name      string
		arg       string
		assertion ValueAssertionFunc
	}{
		{"true is not nil", "true", NotNil},
		{"empty string is nil", "", Nil},
		{"zero is not nil", "0", NotNil},
		{"zero is zero", "0", Zero},
		{"false is zero", "false", Zero},
	}

	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			tt.assertion(t, dumbParse(tt.arg))
		})
	}
}
```
