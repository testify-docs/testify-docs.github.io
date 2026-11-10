# assert

Package assert provides a set of comprehensive testing tools for use with the normal Go testing system.

### Note

All functions in this package return a bool value indicating whether the assertion has passed.

### Example Usage

The following is a complete example using assert in a standard test function:

	import (
	  "testing"
	  "github.com/stretchr/testify/assert"
	)

	func TestSomething(t *testing.T) {

	  var a string = "Hello"
	  var b string = "Hello"

	  assert.Equal(t, a, b, "The two words should be the same.")

	}

if you assert many times, use the format below:

	import (
	  "testing"
	  "github.com/stretchr/testify/assert"
	)

	func TestSomething(t *testing.T) {
	  assert := assert.New(t)

	  var a string = "Hello"
	  var b string = "Hello"

	  assert.Equal(a, b, "The two words should be the same.")
	}

### Assertions

Assertions allow you to easily write test code, and are global funcs in the assert package. All assertion functions take, as the first argument, the [\*testing.T](https://pkg.go.dev/testing#T) object provided by the testing framework. This allows the assertion funcs to write the failings and other details to the correct place.

Every assertion function also takes an optional string message as the final argument, allowing custom error messages to be appended to the message the assertion method outputs.

## AnError

```go
var AnError = errors.New("assert.AnError general error for testing")
```

AnError is an error instance useful for testing.  If the code does not care about error specifics, and only needs to return the error for example, this error should be used to make the test code more readable.

## CallerInfo

```go
func CallerInfo() []string
```

CallerInfo returns an array of strings containing the file and line number of each stack frame leading from the current test to the assert call that failed.

## Condition

```go
func Condition(t TestingT, comp Comparison, msgAndArgs ...interface{}) bool
```

Condition uses a Comparison to assert a complex condition.

## Conditionf

```go
func Conditionf(t TestingT, comp Comparison, msg string, args ...interface{}) bool
```

Conditionf uses a Comparison to assert a complex condition.

## Contains

```go
func Contains(t TestingT, s, contains interface{}, msgAndArgs ...interface{}) bool
```

Contains asserts that the specified string, list(array, slice...) or map contains the specified substring or element.

	assert.Contains(t, "Hello World", "World")
	assert.Contains(t, ["Hello", "World"], "World")
	assert.Contains(t, {"Hello": "World"}, "Hello")

## Containsf

```go
func Containsf(t TestingT, s interface{}, contains interface{}, msg string, args ...interface{}) bool
```

Containsf asserts that the specified string, list(array, slice...) or map contains the specified substring or element.

	assert.Containsf(t, "Hello World", "World", "error message %s", "formatted")
	assert.Containsf(t, ["Hello", "World"], "World", "error message %s", "formatted")
	assert.Containsf(t, {"Hello": "World"}, "Hello", "error message %s", "formatted")

## DirExists

```go
func DirExists(t TestingT, path string, msgAndArgs ...interface{}) bool
```

DirExists checks whether a directory exists in the given path. It also fails if the path is a file rather a directory or there is an error checking whether it exists.

## DirExistsf

```go
func DirExistsf(t TestingT, path string, msg string, args ...interface{}) bool
```

DirExistsf checks whether a directory exists in the given path. It also fails if the path is a file rather a directory or there is an error checking whether it exists.

## ElementsMatch

```go
func ElementsMatch(t TestingT, listA, listB interface{}, msgAndArgs ...interface{}) (ok bool)
```

ElementsMatch asserts that the specified listA(array, slice...) is equal to specified listB(array, slice...) ignoring the order of the elements. If there are duplicate elements, the number of appearances of each of them in both lists should match.

assert.ElementsMatch(t, \[1, 3, 2, 3], \[1, 3, 3, 2])

## ElementsMatchf

```go
func ElementsMatchf(t TestingT, listA interface{}, listB interface{}, msg string, args ...interface{}) bool
```

ElementsMatchf asserts that the specified listA(array, slice...) is equal to specified listB(array, slice...) ignoring the order of the elements. If there are duplicate elements, the number of appearances of each of them in both lists should match.

assert.ElementsMatchf(t, \[1, 3, 2, 3], \[1, 3, 3, 2], "error message %s", "formatted")

## Empty

```go
func Empty(t TestingT, object interface{}, msgAndArgs ...interface{}) bool
```

Empty asserts that the given value is "empty".

[Zero values](https://go.dev/ref/spec#The_zero_value) are "empty".

Arrays are "empty" if every element is the zero value of the type (stricter than "empty").

Slices, maps and channels with zero length are "empty".

Pointer values are "empty" if the pointer is nil or if the pointed value is "empty".

	assert.Empty(t, obj)

## Emptyf

```go
func Emptyf(t TestingT, object interface{}, msg string, args ...interface{}) bool
```

Emptyf asserts that the given value is "empty".

[Zero values](https://go.dev/ref/spec#The_zero_value) are "empty".

Arrays are "empty" if every element is the zero value of the type (stricter than "empty").

Slices, maps and channels with zero length are "empty".

Pointer values are "empty" if the pointer is nil or if the pointed value is "empty".

	assert.Emptyf(t, obj, "error message %s", "formatted")

## Equal

```go
func Equal(t TestingT, expected, actual interface{}, msgAndArgs ...interface{}) bool
```

Equal asserts that two objects are equal.

	assert.Equal(t, 123, 123)

Pointer variable equality is determined based on the equality of the referenced values (as opposed to the memory addresses). Function equality cannot be determined and will always fail.

## EqualError

```go
func EqualError(t TestingT, theError error, errString string, msgAndArgs ...interface{}) bool
```

EqualError asserts that a function returned a non-nil error (i.e. an error) and that it is equal to the provided error.

	actualObj, err := SomeFunction()
	assert.EqualError(t, err,  expectedErrorString)

## EqualErrorf

```go
func EqualErrorf(t TestingT, theError error, errString string, msg string, args ...interface{}) bool
```

EqualErrorf asserts that a function returned a non-nil error (i.e. an error) and that it is equal to the provided error.

	actualObj, err := SomeFunction()
	assert.EqualErrorf(t, err,  expectedErrorString, "error message %s", "formatted")

## EqualExportedValues

```go
func EqualExportedValues(t TestingT, expected, actual interface{}, msgAndArgs ...interface{}) bool
```

EqualExportedValues asserts that the types of two objects are equal and their public fields are also equal. This is useful for comparing structs that have private fields that could potentially differ.

	 type S struct {
		Exported     	int
		notExported   	int
	 }
	 assert.EqualExportedValues(t, S{1, 2}, S{1, 3}) => true
	 assert.EqualExportedValues(t, S{1, 2}, S{2, 3}) => false

## EqualExportedValuesf

```go
func EqualExportedValuesf(t TestingT, expected interface{}, actual interface{}, msg string, args ...interface{}) bool
```

EqualExportedValuesf asserts that the types of two objects are equal and their public fields are also equal. This is useful for comparing structs that have private fields that could potentially differ.

	 type S struct {
		Exported     	int
		notExported   	int
	 }
	 assert.EqualExportedValuesf(t, S{1, 2}, S{1, 3}, "error message %s", "formatted") => true
	 assert.EqualExportedValuesf(t, S{1, 2}, S{2, 3}, "error message %s", "formatted") => false

## EqualValues

```go
func EqualValues(t TestingT, expected, actual interface{}, msgAndArgs ...interface{}) bool
```

EqualValues asserts that two objects are equal or convertible to the larger type and equal.

	assert.EqualValues(t, uint32(123), int32(123))

## EqualValuesf

```go
func EqualValuesf(t TestingT, expected interface{}, actual interface{}, msg string, args ...interface{}) bool
```

EqualValuesf asserts that two objects are equal or convertible to the larger type and equal.

	assert.EqualValuesf(t, uint32(123), int32(123), "error message %s", "formatted")

## Equalf

```go
func Equalf(t TestingT, expected interface{}, actual interface{}, msg string, args ...interface{}) bool
```

Equalf asserts that two objects are equal.

	assert.Equalf(t, 123, 123, "error message %s", "formatted")

Pointer variable equality is determined based on the equality of the referenced values (as opposed to the memory addresses). Function equality cannot be determined and will always fail.

## Error

```go
func Error(t TestingT, err error, msgAndArgs ...interface{}) bool
```

Error asserts that a function returned a non-nil error (ie. an error).

	actualObj, err := SomeFunction()
	assert.Error(t, err)

## ErrorAs

```go
func ErrorAs(t TestingT, err error, target interface{}, msgAndArgs ...interface{}) bool
```

ErrorAs asserts that at least one of the errors in err's chain matches target, and if so, sets target to that error value. This is a wrapper for errors.As.

## ErrorAsf

```go
func ErrorAsf(t TestingT, err error, target interface{}, msg string, args ...interface{}) bool
```

ErrorAsf asserts that at least one of the errors in err's chain matches target, and if so, sets target to that error value. This is a wrapper for errors.As.

## ErrorContains

```go
func ErrorContains(t TestingT, theError error, contains string, msgAndArgs ...interface{}) bool
```

ErrorContains asserts that a function returned a non-nil error (i.e. an error) and that the error contains the specified substring.

	actualObj, err := SomeFunction()
	assert.ErrorContains(t, err,  expectedErrorSubString)

## ErrorContainsf

```go
func ErrorContainsf(t TestingT, theError error, contains string, msg string, args ...interface{}) bool
```

ErrorContainsf asserts that a function returned a non-nil error (i.e. an error) and that the error contains the specified substring.

	actualObj, err := SomeFunction()
	assert.ErrorContainsf(t, err,  expectedErrorSubString, "error message %s", "formatted")

## ErrorIs

```go
func ErrorIs(t TestingT, err, target error, msgAndArgs ...interface{}) bool
```

ErrorIs asserts that at least one of the errors in err's chain matches target. This is a wrapper for errors.Is.

## ErrorIsf

```go
func ErrorIsf(t TestingT, err error, target error, msg string, args ...interface{}) bool
```

ErrorIsf asserts that at least one of the errors in err's chain matches target. This is a wrapper for errors.Is.

## Errorf

```go
func Errorf(t TestingT, err error, msg string, args ...interface{}) bool
```

Errorf asserts that a function returned a non-nil error (ie. an error).

	actualObj, err := SomeFunction()
	assert.Errorf(t, err, "error message %s", "formatted")

## Eventually

```go
func Eventually(t TestingT, condition func() bool, waitFor time.Duration, tick time.Duration, msgAndArgs ...interface{}) bool
```

Eventually asserts that given condition will be met in waitFor time, periodically checking target function each tick.

	assert.Eventually(t, func() bool { return true; }, time.Second, 10*time.Millisecond)

## EventuallyWithT

```go
func EventuallyWithT(t TestingT, condition func(collect *CollectT), waitFor time.Duration, tick time.Duration, msgAndArgs ...interface{}) bool
```

EventuallyWithT asserts that given condition will be met in waitFor time, periodically checking target function each tick. In contrast to Eventually, it supplies a CollectT to the condition function, so that the condition function can use the CollectT to call other assertions. The condition is considered "met" if no errors are raised in a tick. The supplied CollectT collects all errors from one tick (if there are any). If the condition is not met before waitFor, the collected errors of the last tick are copied to t.

	externalValue := false
	go func() {
		time.Sleep(8*time.Second)
		externalValue = true
	}()
	assert.EventuallyWithT(t, func(c *assert.CollectT) {
		// add assertions as needed; any assertion failure will fail the current tick
		assert.True(c, externalValue, "expected 'externalValue' to be true")
	}, 10*time.Second, 1*time.Second, "external state has not changed to 'true'; still false")

## EventuallyWithTf

```go
func EventuallyWithTf(t TestingT, condition func(collect *CollectT), waitFor time.Duration, tick time.Duration, msg string, args ...interface{}) bool
```

EventuallyWithTf asserts that given condition will be met in waitFor time, periodically checking target function each tick. In contrast to Eventually, it supplies a CollectT to the condition function, so that the condition function can use the CollectT to call other assertions. The condition is considered "met" if no errors are raised in a tick. The supplied CollectT collects all errors from one tick (if there are any). If the condition is not met before waitFor, the collected errors of the last tick are copied to t.

	externalValue := false
	go func() {
		time.Sleep(8*time.Second)
		externalValue = true
	}()
	assert.EventuallyWithTf(t, func(c *assert.CollectT) {
		// add assertions as needed; any assertion failure will fail the current tick
		assert.True(c, externalValue, "expected 'externalValue' to be true")
	}, 10*time.Second, 1*time.Second, "error message %s", "formatted")

## Eventuallyf

```go
func Eventuallyf(t TestingT, condition func() bool, waitFor time.Duration, tick time.Duration, msg string, args ...interface{}) bool
```

Eventuallyf asserts that given condition will be met in waitFor time, periodically checking target function each tick.

	assert.Eventuallyf(t, func() bool { return true; }, time.Second, 10*time.Millisecond, "error message %s", "formatted")

## Exactly

```go
func Exactly(t TestingT, expected, actual interface{}, msgAndArgs ...interface{}) bool
```

Exactly asserts that two objects are equal in value and type.

	assert.Exactly(t, int32(123), int64(123))

## Exactlyf

```go
func Exactlyf(t TestingT, expected interface{}, actual interface{}, msg string, args ...interface{}) bool
```

Exactlyf asserts that two objects are equal in value and type.

	assert.Exactlyf(t, int32(123), int64(123), "error message %s", "formatted")

## Fail

```go
func Fail(t TestingT, failureMessage string, msgAndArgs ...interface{}) bool
```

Fail reports a failure through

## FailNow

```go
func FailNow(t TestingT, failureMessage string, msgAndArgs ...interface{}) bool
```

FailNow fails test

## FailNowf

```go
func FailNowf(t TestingT, failureMessage string, msg string, args ...interface{}) bool
```

FailNowf fails test

## Failf

```go
func Failf(t TestingT, failureMessage string, msg string, args ...interface{}) bool
```

Failf reports a failure through

## False

```go
func False(t TestingT, value bool, msgAndArgs ...interface{}) bool
```

False asserts that the specified value is false.

	assert.False(t, myBool)

## Falsef

```go
func Falsef(t TestingT, value bool, msg string, args ...interface{}) bool
```

Falsef asserts that the specified value is false.

	assert.Falsef(t, myBool, "error message %s", "formatted")

## FileExists

```go
func FileExists(t TestingT, path string, msgAndArgs ...interface{}) bool
```

FileExists checks whether a file exists in the given path. It also fails if the path points to a directory or there is an error when trying to check the file.

## FileExistsf

```go
func FileExistsf(t TestingT, path string, msg string, args ...interface{}) bool
```

FileExistsf checks whether a file exists in the given path. It also fails if the path points to a directory or there is an error when trying to check the file.

## Greater

```go
func Greater(t TestingT, e1 interface{}, e2 interface{}, msgAndArgs ...interface{}) bool
```

Greater asserts that the first element is greater than the second

	assert.Greater(t, 2, 1)
	assert.Greater(t, float64(2), float64(1))
	assert.Greater(t, "b", "a")

## GreaterOrEqual

```go
func GreaterOrEqual(t TestingT, e1 interface{}, e2 interface{}, msgAndArgs ...interface{}) bool
```

GreaterOrEqual asserts that the first element is greater than or equal to the second

	assert.GreaterOrEqual(t, 2, 1)
	assert.GreaterOrEqual(t, 2, 2)
	assert.GreaterOrEqual(t, "b", "a")
	assert.GreaterOrEqual(t, "b", "b")

## GreaterOrEqualf

```go
func GreaterOrEqualf(t TestingT, e1 interface{}, e2 interface{}, msg string, args ...interface{}) bool
```

GreaterOrEqualf asserts that the first element is greater than or equal to the second

	assert.GreaterOrEqualf(t, 2, 1, "error message %s", "formatted")
	assert.GreaterOrEqualf(t, 2, 2, "error message %s", "formatted")
	assert.GreaterOrEqualf(t, "b", "a", "error message %s", "formatted")
	assert.GreaterOrEqualf(t, "b", "b", "error message %s", "formatted")

## Greaterf

```go
func Greaterf(t TestingT, e1 interface{}, e2 interface{}, msg string, args ...interface{}) bool
```

Greaterf asserts that the first element is greater than the second

	assert.Greaterf(t, 2, 1, "error message %s", "formatted")
	assert.Greaterf(t, float64(2), float64(1), "error message %s", "formatted")
	assert.Greaterf(t, "b", "a", "error message %s", "formatted")

## HTTPBody

```go
func HTTPBody(handler http.HandlerFunc, method, url string, values url.Values) string
```

HTTPBody is a helper that returns HTTP body of the response. It returns empty string if building a new request fails.

## HTTPBodyContains

```go
func HTTPBodyContains(t TestingT, handler http.HandlerFunc, method, url string, values url.Values, str interface{}, msgAndArgs ...interface{}) bool
```

HTTPBodyContains asserts that a specified handler returns a body that contains a string.

	assert.HTTPBodyContains(t, myHandler, "GET", "www.google.com", nil, "I'm Feeling Lucky")

Returns whether the assertion was successful (true) or not (false).

## HTTPBodyContainsf

```go
func HTTPBodyContainsf(t TestingT, handler http.HandlerFunc, method string, url string, values url.Values, str interface{}, msg string, args ...interface{}) bool
```

HTTPBodyContainsf asserts that a specified handler returns a body that contains a string.

	assert.HTTPBodyContainsf(t, myHandler, "GET", "www.google.com", nil, "I'm Feeling Lucky", "error message %s", "formatted")

Returns whether the assertion was successful (true) or not (false).

## HTTPBodyNotContains

```go
func HTTPBodyNotContains(t TestingT, handler http.HandlerFunc, method, url string, values url.Values, str interface{}, msgAndArgs ...interface{}) bool
```

HTTPBodyNotContains asserts that a specified handler returns a body that does not contain a string.

	assert.HTTPBodyNotContains(t, myHandler, "GET", "www.google.com", nil, "I'm Feeling Lucky")

Returns whether the assertion was successful (true) or not (false).

## HTTPBodyNotContainsf

```go
func HTTPBodyNotContainsf(t TestingT, handler http.HandlerFunc, method string, url string, values url.Values, str interface{}, msg string, args ...interface{}) bool
```

HTTPBodyNotContainsf asserts that a specified handler returns a body that does not contain a string.

	assert.HTTPBodyNotContainsf(t, myHandler, "GET", "www.google.com", nil, "I'm Feeling Lucky", "error message %s", "formatted")

Returns whether the assertion was successful (true) or not (false).

## HTTPError

```go
func HTTPError(t TestingT, handler http.HandlerFunc, method, url string, values url.Values, msgAndArgs ...interface{}) bool
```

HTTPError asserts that a specified handler returns an error status code.

	assert.HTTPError(t, myHandler, "POST", "/a/b/c", url.Values{"a": []string{"b", "c"}}

Returns whether the assertion was successful (true) or not (false).

## HTTPErrorf

```go
func HTTPErrorf(t TestingT, handler http.HandlerFunc, method string, url string, values url.Values, msg string, args ...interface{}) bool
```

HTTPErrorf asserts that a specified handler returns an error status code.

	assert.HTTPErrorf(t, myHandler, "POST", "/a/b/c", url.Values{"a": []string{"b", "c"}}

Returns whether the assertion was successful (true) or not (false).

## HTTPRedirect

```go
func HTTPRedirect(t TestingT, handler http.HandlerFunc, method, url string, values url.Values, msgAndArgs ...interface{}) bool
```

HTTPRedirect asserts that a specified handler returns a redirect status code.

	assert.HTTPRedirect(t, myHandler, "GET", "/a/b/c", url.Values{"a": []string{"b", "c"}}

Returns whether the assertion was successful (true) or not (false).

## HTTPRedirectf

```go
func HTTPRedirectf(t TestingT, handler http.HandlerFunc, method string, url string, values url.Values, msg string, args ...interface{}) bool
```

HTTPRedirectf asserts that a specified handler returns a redirect status code.

	assert.HTTPRedirectf(t, myHandler, "GET", "/a/b/c", url.Values{"a": []string{"b", "c"}}

Returns whether the assertion was successful (true) or not (false).

## HTTPStatusCode

```go
func HTTPStatusCode(t TestingT, handler http.HandlerFunc, method, url string, values url.Values, statuscode int, msgAndArgs ...interface{}) bool
```

HTTPStatusCode asserts that a specified handler returns a specified status code.

	assert.HTTPStatusCode(t, myHandler, "GET", "/notImplemented", nil, 501)

Returns whether the assertion was successful (true) or not (false).

## HTTPStatusCodef

```go
func HTTPStatusCodef(t TestingT, handler http.HandlerFunc, method string, url string, values url.Values, statuscode int, msg string, args ...interface{}) bool
```

HTTPStatusCodef asserts that a specified handler returns a specified status code.

	assert.HTTPStatusCodef(t, myHandler, "GET", "/notImplemented", nil, 501, "error message %s", "formatted")

Returns whether the assertion was successful (true) or not (false).

## HTTPSuccess

```go
func HTTPSuccess(t TestingT, handler http.HandlerFunc, method, url string, values url.Values, msgAndArgs ...interface{}) bool
```

HTTPSuccess asserts that a specified handler returns a success status code.

	assert.HTTPSuccess(t, myHandler, "POST", "http://www.google.com", nil)

Returns whether the assertion was successful (true) or not (false).

## HTTPSuccessf

```go
func HTTPSuccessf(t TestingT, handler http.HandlerFunc, method string, url string, values url.Values, msg string, args ...interface{}) bool
```

HTTPSuccessf asserts that a specified handler returns a success status code.

	assert.HTTPSuccessf(t, myHandler, "POST", "http://www.google.com", nil, "error message %s", "formatted")

Returns whether the assertion was successful (true) or not (false).

## Implements

```go
func Implements(t TestingT, interfaceObject interface{}, object interface{}, msgAndArgs ...interface{}) bool
```

Implements asserts that an object is implemented by the specified interface.

	assert.Implements(t, (*MyInterface)(nil), new(MyObject))

## Implementsf

```go
func Implementsf(t TestingT, interfaceObject interface{}, object interface{}, msg string, args ...interface{}) bool
```

Implementsf asserts that an object is implemented by the specified interface.

	assert.Implementsf(t, (*MyInterface)(nil), new(MyObject), "error message %s", "formatted")

## InDelta

```go
func InDelta(t TestingT, expected, actual interface{}, delta float64, msgAndArgs ...interface{}) bool
```

InDelta asserts that the two numerals are within delta of each other.

	assert.InDelta(t, math.Pi, 22/7.0, 0.01)

## InDeltaMapValues

```go
func InDeltaMapValues(t TestingT, expected, actual interface{}, delta float64, msgAndArgs ...interface{}) bool
```

InDeltaMapValues is the same as InDelta, but it compares all values between two maps. Both maps must have exactly the same keys.

## InDeltaMapValuesf

```go
func InDeltaMapValuesf(t TestingT, expected interface{}, actual interface{}, delta float64, msg string, args ...interface{}) bool
```

InDeltaMapValuesf is the same as InDelta, but it compares all values between two maps. Both maps must have exactly the same keys.

## InDeltaSlice

```go
func InDeltaSlice(t TestingT, expected, actual interface{}, delta float64, msgAndArgs ...interface{}) bool
```

InDeltaSlice is the same as InDelta, except it compares two slices.

## InDeltaSlicef

```go
func InDeltaSlicef(t TestingT, expected interface{}, actual interface{}, delta float64, msg string, args ...interface{}) bool
```

InDeltaSlicef is the same as InDelta, except it compares two slices.

## InDeltaf

```go
func InDeltaf(t TestingT, expected interface{}, actual interface{}, delta float64, msg string, args ...interface{}) bool
```

InDeltaf asserts that the two numerals are within delta of each other.

	assert.InDeltaf(t, math.Pi, 22/7.0, 0.01, "error message %s", "formatted")

## InEpsilon

```go
func InEpsilon(t TestingT, expected, actual interface{}, epsilon float64, msgAndArgs ...interface{}) bool
```

InEpsilon asserts that expected and actual have a relative error less than epsilon

## InEpsilonSlice

```go
func InEpsilonSlice(t TestingT, expected, actual interface{}, epsilon float64, msgAndArgs ...interface{}) bool
```

InEpsilonSlice is the same as InEpsilon, except it compares each value from two slices.

## InEpsilonSlicef

```go
func InEpsilonSlicef(t TestingT, expected interface{}, actual interface{}, epsilon float64, msg string, args ...interface{}) bool
```

InEpsilonSlicef is the same as InEpsilon, except it compares each value from two slices.

## InEpsilonf

```go
func InEpsilonf(t TestingT, expected interface{}, actual interface{}, epsilon float64, msg string, args ...interface{}) bool
```

InEpsilonf asserts that expected and actual have a relative error less than epsilon

## IsDecreasing

```go
func IsDecreasing(t TestingT, object interface{}, msgAndArgs ...interface{}) bool
```

IsDecreasing asserts that the collection is decreasing

	assert.IsDecreasing(t, []int{2, 1, 0})
	assert.IsDecreasing(t, []float{2, 1})
	assert.IsDecreasing(t, []string{"b", "a"})

## IsDecreasingf

```go
func IsDecreasingf(t TestingT, object interface{}, msg string, args ...interface{}) bool
```

IsDecreasingf asserts that the collection is decreasing

	assert.IsDecreasingf(t, []int{2, 1, 0}, "error message %s", "formatted")
	assert.IsDecreasingf(t, []float{2, 1}, "error message %s", "formatted")
	assert.IsDecreasingf(t, []string{"b", "a"}, "error message %s", "formatted")

## IsIncreasing

```go
func IsIncreasing(t TestingT, object interface{}, msgAndArgs ...interface{}) bool
```

IsIncreasing asserts that the collection is increasing

	assert.IsIncreasing(t, []int{1, 2, 3})
	assert.IsIncreasing(t, []float{1, 2})
	assert.IsIncreasing(t, []string{"a", "b"})

## IsIncreasingf

```go
func IsIncreasingf(t TestingT, object interface{}, msg string, args ...interface{}) bool
```

IsIncreasingf asserts that the collection is increasing

	assert.IsIncreasingf(t, []int{1, 2, 3}, "error message %s", "formatted")
	assert.IsIncreasingf(t, []float{1, 2}, "error message %s", "formatted")
	assert.IsIncreasingf(t, []string{"a", "b"}, "error message %s", "formatted")

## IsNonDecreasing

```go
func IsNonDecreasing(t TestingT, object interface{}, msgAndArgs ...interface{}) bool
```

IsNonDecreasing asserts that the collection is not decreasing

	assert.IsNonDecreasing(t, []int{1, 1, 2})
	assert.IsNonDecreasing(t, []float{1, 2})
	assert.IsNonDecreasing(t, []string{"a", "b"})

## IsNonDecreasingf

```go
func IsNonDecreasingf(t TestingT, object interface{}, msg string, args ...interface{}) bool
```

IsNonDecreasingf asserts that the collection is not decreasing

	assert.IsNonDecreasingf(t, []int{1, 1, 2}, "error message %s", "formatted")
	assert.IsNonDecreasingf(t, []float{1, 2}, "error message %s", "formatted")
	assert.IsNonDecreasingf(t, []string{"a", "b"}, "error message %s", "formatted")

## IsNonIncreasing

```go
func IsNonIncreasing(t TestingT, object interface{}, msgAndArgs ...interface{}) bool
```

IsNonIncreasing asserts that the collection is not increasing

	assert.IsNonIncreasing(t, []int{2, 1, 1})
	assert.IsNonIncreasing(t, []float{2, 1})
	assert.IsNonIncreasing(t, []string{"b", "a"})

## IsNonIncreasingf

```go
func IsNonIncreasingf(t TestingT, object interface{}, msg string, args ...interface{}) bool
```

IsNonIncreasingf asserts that the collection is not increasing

	assert.IsNonIncreasingf(t, []int{2, 1, 1}, "error message %s", "formatted")
	assert.IsNonIncreasingf(t, []float{2, 1}, "error message %s", "formatted")
	assert.IsNonIncreasingf(t, []string{"b", "a"}, "error message %s", "formatted")

## IsNotType

```go
func IsNotType(t TestingT, theType, object interface{}, msgAndArgs ...interface{}) bool
```

IsNotType asserts that the specified objects are not of the same type.

	assert.IsNotType(t, &NotMyStruct{}, &MyStruct{})

## IsNotTypef

```go
func IsNotTypef(t TestingT, theType interface{}, object interface{}, msg string, args ...interface{}) bool
```

IsNotTypef asserts that the specified objects are not of the same type.

	assert.IsNotTypef(t, &NotMyStruct{}, &MyStruct{}, "error message %s", "formatted")

## IsType

```go
func IsType(t TestingT, expectedType, object interface{}, msgAndArgs ...interface{}) bool
```

IsType asserts that the specified objects are of the same type.

	assert.IsType(t, &MyStruct{}, &MyStruct{})

## IsTypef

```go
func IsTypef(t TestingT, expectedType interface{}, object interface{}, msg string, args ...interface{}) bool
```

IsTypef asserts that the specified objects are of the same type.

	assert.IsTypef(t, &MyStruct{}, &MyStruct{}, "error message %s", "formatted")

## JSONEq

```go
func JSONEq(t TestingT, expected string, actual string, msgAndArgs ...interface{}) bool
```

JSONEq asserts that two JSON strings are equivalent.

	assert.JSONEq(t, `{"hello": "world", "foo": "bar"}`, `{"foo": "bar", "hello": "world"}`)

## JSONEqf

```go
func JSONEqf(t TestingT, expected string, actual string, msg string, args ...interface{}) bool
```

JSONEqf asserts that two JSON strings are equivalent.

	assert.JSONEqf(t, `{"hello": "world", "foo": "bar"}`, `{"foo": "bar", "hello": "world"}`, "error message %s", "formatted")

## Len

```go
func Len(t TestingT, object interface{}, length int, msgAndArgs ...interface{}) bool
```

Len asserts that the specified object has specific length. Len also fails if the object has a type that len() not accept.

	assert.Len(t, mySlice, 3)

## Lenf

```go
func Lenf(t TestingT, object interface{}, length int, msg string, args ...interface{}) bool
```

Lenf asserts that the specified object has specific length. Lenf also fails if the object has a type that len() not accept.

	assert.Lenf(t, mySlice, 3, "error message %s", "formatted")

## Less

```go
func Less(t TestingT, e1 interface{}, e2 interface{}, msgAndArgs ...interface{}) bool
```

Less asserts that the first element is less than the second

	assert.Less(t, 1, 2)
	assert.Less(t, float64(1), float64(2))
	assert.Less(t, "a", "b")

## LessOrEqual

```go
func LessOrEqual(t TestingT, e1 interface{}, e2 interface{}, msgAndArgs ...interface{}) bool
```

LessOrEqual asserts that the first element is less than or equal to the second

	assert.LessOrEqual(t, 1, 2)
	assert.LessOrEqual(t, 2, 2)
	assert.LessOrEqual(t, "a", "b")
	assert.LessOrEqual(t, "b", "b")

## LessOrEqualf

```go
func LessOrEqualf(t TestingT, e1 interface{}, e2 interface{}, msg string, args ...interface{}) bool
```

LessOrEqualf asserts that the first element is less than or equal to the second

	assert.LessOrEqualf(t, 1, 2, "error message %s", "formatted")
	assert.LessOrEqualf(t, 2, 2, "error message %s", "formatted")
	assert.LessOrEqualf(t, "a", "b", "error message %s", "formatted")
	assert.LessOrEqualf(t, "b", "b", "error message %s", "formatted")

## Lessf

```go
func Lessf(t TestingT, e1 interface{}, e2 interface{}, msg string, args ...interface{}) bool
```

Lessf asserts that the first element is less than the second

	assert.Lessf(t, 1, 2, "error message %s", "formatted")
	assert.Lessf(t, float64(1), float64(2), "error message %s", "formatted")
	assert.Lessf(t, "a", "b", "error message %s", "formatted")

## Negative

```go
func Negative(t TestingT, e interface{}, msgAndArgs ...interface{}) bool
```

Negative asserts that the specified element is negative

	assert.Negative(t, -1)
	assert.Negative(t, -1.23)

## Negativef

```go
func Negativef(t TestingT, e interface{}, msg string, args ...interface{}) bool
```

Negativef asserts that the specified element is negative

	assert.Negativef(t, -1, "error message %s", "formatted")
	assert.Negativef(t, -1.23, "error message %s", "formatted")

## Never

```go
func Never(t TestingT, condition func() bool, waitFor time.Duration, tick time.Duration, msgAndArgs ...interface{}) bool
```

Never asserts that the given condition doesn't satisfy in waitFor time, periodically checking the target function each tick.

	assert.Never(t, func() bool { return false; }, time.Second, 10*time.Millisecond)

## Neverf

```go
func Neverf(t TestingT, condition func() bool, waitFor time.Duration, tick time.Duration, msg string, args ...interface{}) bool
```

Neverf asserts that the given condition doesn't satisfy in waitFor time, periodically checking the target function each tick.

	assert.Neverf(t, func() bool { return false; }, time.Second, 10*time.Millisecond, "error message %s", "formatted")

## New

```go
func New(t TestingT) *Assertions
```

New makes a new Assertions object for the specified TestingT.

## Nil

```go
func Nil(t TestingT, object interface{}, msgAndArgs ...interface{}) bool
```

Nil asserts that the specified object is nil.

	assert.Nil(t, err)

## Nilf

```go
func Nilf(t TestingT, object interface{}, msg string, args ...interface{}) bool
```

Nilf asserts that the specified object is nil.

	assert.Nilf(t, err, "error message %s", "formatted")

## NoDirExists

```go
func NoDirExists(t TestingT, path string, msgAndArgs ...interface{}) bool
```

NoDirExists checks whether a directory does not exist in the given path. It fails if the path points to an existing \_directory\_ only.

## NoDirExistsf

```go
func NoDirExistsf(t TestingT, path string, msg string, args ...interface{}) bool
```

NoDirExistsf checks whether a directory does not exist in the given path. It fails if the path points to an existing \_directory\_ only.

## NoError

```go
func NoError(t TestingT, err error, msgAndArgs ...interface{}) bool
```

NoError asserts that a function returned a nil error (ie. no error).

	  actualObj, err := SomeFunction()
	  if assert.NoError(t, err) {
		   assert.Equal(t, expectedObj, actualObj)
	  }

## NoErrorf

```go
func NoErrorf(t TestingT, err error, msg string, args ...interface{}) bool
```

NoErrorf asserts that a function returned a nil error (ie. no error).

	  actualObj, err := SomeFunction()
	  if assert.NoErrorf(t, err, "error message %s", "formatted") {
		   assert.Equal(t, expectedObj, actualObj)
	  }

## NoFileExists

```go
func NoFileExists(t TestingT, path string, msgAndArgs ...interface{}) bool
```

NoFileExists checks whether a file does not exist in a given path. It fails if the path points to an existing \_file\_ only.

## NoFileExistsf

```go
func NoFileExistsf(t TestingT, path string, msg string, args ...interface{}) bool
```

NoFileExistsf checks whether a file does not exist in a given path. It fails if the path points to an existing \_file\_ only.

## NotContains

```go
func NotContains(t TestingT, s, contains interface{}, msgAndArgs ...interface{}) bool
```

NotContains asserts that the specified string, list(array, slice...) or map does NOT contain the specified substring or element.

	assert.NotContains(t, "Hello World", "Earth")
	assert.NotContains(t, ["Hello", "World"], "Earth")
	assert.NotContains(t, {"Hello": "World"}, "Earth")

## NotContainsf

```go
func NotContainsf(t TestingT, s interface{}, contains interface{}, msg string, args ...interface{}) bool
```

NotContainsf asserts that the specified string, list(array, slice...) or map does NOT contain the specified substring or element.

	assert.NotContainsf(t, "Hello World", "Earth", "error message %s", "formatted")
	assert.NotContainsf(t, ["Hello", "World"], "Earth", "error message %s", "formatted")
	assert.NotContainsf(t, {"Hello": "World"}, "Earth", "error message %s", "formatted")

## NotElementsMatch

```go
func NotElementsMatch(t TestingT, listA, listB interface{}, msgAndArgs ...interface{}) (ok bool)
```

NotElementsMatch asserts that the specified listA(array, slice...) is NOT equal to specified listB(array, slice...) ignoring the order of the elements. If there are duplicate elements, the number of appearances of each of them in both lists should not match. This is an inverse of ElementsMatch.

assert.NotElementsMatch(t, \[1, 1, 2, 3], \[1, 1, 2, 3]) -> false

assert.NotElementsMatch(t, \[1, 1, 2, 3], \[1, 2, 3]) -> true

assert.NotElementsMatch(t, \[1, 2, 3], \[1, 2, 4]) -> true

## NotElementsMatchf

```go
func NotElementsMatchf(t TestingT, listA interface{}, listB interface{}, msg string, args ...interface{}) bool
```

NotElementsMatchf asserts that the specified listA(array, slice...) is NOT equal to specified listB(array, slice...) ignoring the order of the elements. If there are duplicate elements, the number of appearances of each of them in both lists should not match. This is an inverse of ElementsMatch.

assert.NotElementsMatchf(t, \[1, 1, 2, 3], \[1, 1, 2, 3], "error message %s", "formatted") -> false

assert.NotElementsMatchf(t, \[1, 1, 2, 3], \[1, 2, 3], "error message %s", "formatted") -> true

assert.NotElementsMatchf(t, \[1, 2, 3], \[1, 2, 4], "error message %s", "formatted") -> true

## NotEmpty

```go
func NotEmpty(t TestingT, object interface{}, msgAndArgs ...interface{}) bool
```

NotEmpty asserts that the specified object is NOT [Empty](#func-Empty).

	if assert.NotEmpty(t, obj) {
	  assert.Equal(t, "two", obj[1])
	}

## NotEmptyf

```go
func NotEmptyf(t TestingT, object interface{}, msg string, args ...interface{}) bool
```

NotEmptyf asserts that the specified object is NOT [Empty](#func-Empty).

	if assert.NotEmptyf(t, obj, "error message %s", "formatted") {
	  assert.Equal(t, "two", obj[1])
	}

## NotEqual

```go
func NotEqual(t TestingT, expected, actual interface{}, msgAndArgs ...interface{}) bool
```

NotEqual asserts that the specified values are NOT equal.

	assert.NotEqual(t, obj1, obj2)

Pointer variable equality is determined based on the equality of the referenced values (as opposed to the memory addresses).

## NotEqualValues

```go
func NotEqualValues(t TestingT, expected, actual interface{}, msgAndArgs ...interface{}) bool
```

NotEqualValues asserts that two objects are not equal even when converted to the same type

	assert.NotEqualValues(t, obj1, obj2)

## NotEqualValuesf

```go
func NotEqualValuesf(t TestingT, expected interface{}, actual interface{}, msg string, args ...interface{}) bool
```

NotEqualValuesf asserts that two objects are not equal even when converted to the same type

	assert.NotEqualValuesf(t, obj1, obj2, "error message %s", "formatted")

## NotEqualf

```go
func NotEqualf(t TestingT, expected interface{}, actual interface{}, msg string, args ...interface{}) bool
```

NotEqualf asserts that the specified values are NOT equal.

	assert.NotEqualf(t, obj1, obj2, "error message %s", "formatted")

Pointer variable equality is determined based on the equality of the referenced values (as opposed to the memory addresses).

## NotErrorAs

```go
func NotErrorAs(t TestingT, err error, target interface{}, msgAndArgs ...interface{}) bool
```

NotErrorAs asserts that none of the errors in err's chain matches target, but if so, sets target to that error value.

## NotErrorAsf

```go
func NotErrorAsf(t TestingT, err error, target interface{}, msg string, args ...interface{}) bool
```

NotErrorAsf asserts that none of the errors in err's chain matches target, but if so, sets target to that error value.

## NotErrorIs

```go
func NotErrorIs(t TestingT, err, target error, msgAndArgs ...interface{}) bool
```

NotErrorIs asserts that none of the errors in err's chain matches target. This is a wrapper for errors.Is.

## NotErrorIsf

```go
func NotErrorIsf(t TestingT, err error, target error, msg string, args ...interface{}) bool
```

NotErrorIsf asserts that none of the errors in err's chain matches target. This is a wrapper for errors.Is.

## NotImplements

```go
func NotImplements(t TestingT, interfaceObject interface{}, object interface{}, msgAndArgs ...interface{}) bool
```

NotImplements asserts that an object does not implement the specified interface.

	assert.NotImplements(t, (*MyInterface)(nil), new(MyObject))

## NotImplementsf

```go
func NotImplementsf(t TestingT, interfaceObject interface{}, object interface{}, msg string, args ...interface{}) bool
```

NotImplementsf asserts that an object does not implement the specified interface.

	assert.NotImplementsf(t, (*MyInterface)(nil), new(MyObject), "error message %s", "formatted")

## NotNil

```go
func NotNil(t TestingT, object interface{}, msgAndArgs ...interface{}) bool
```

NotNil asserts that the specified object is not nil.

	assert.NotNil(t, err)

## NotNilf

```go
func NotNilf(t TestingT, object interface{}, msg string, args ...interface{}) bool
```

NotNilf asserts that the specified object is not nil.

	assert.NotNilf(t, err, "error message %s", "formatted")

## NotPanics

```go
func NotPanics(t TestingT, f PanicTestFunc, msgAndArgs ...interface{}) bool
```

NotPanics asserts that the code inside the specified PanicTestFunc does NOT panic.

	assert.NotPanics(t, func(){ RemainCalm() })

## NotPanicsf

```go
func NotPanicsf(t TestingT, f PanicTestFunc, msg string, args ...interface{}) bool
```

NotPanicsf asserts that the code inside the specified PanicTestFunc does NOT panic.

	assert.NotPanicsf(t, func(){ RemainCalm() }, "error message %s", "formatted")

## NotRegexp

```go
func NotRegexp(t TestingT, rx interface{}, str interface{}, msgAndArgs ...interface{}) bool
```

NotRegexp asserts that a specified regexp does not match a string.

	assert.NotRegexp(t, regexp.MustCompile("starts"), "it's starting")
	assert.NotRegexp(t, "^start", "it's not starting")

## NotRegexpf

```go
func NotRegexpf(t TestingT, rx interface{}, str interface{}, msg string, args ...interface{}) bool
```

NotRegexpf asserts that a specified regexp does not match a string.

	assert.NotRegexpf(t, regexp.MustCompile("starts"), "it's starting", "error message %s", "formatted")
	assert.NotRegexpf(t, "^start", "it's not starting", "error message %s", "formatted")

## NotSame

```go
func NotSame(t TestingT, expected, actual interface{}, msgAndArgs ...interface{}) bool
```

NotSame asserts that two pointers do not reference the same object.

	assert.NotSame(t, ptr1, ptr2)

Both arguments must be pointer variables. Pointer variable sameness is determined based on the equality of both type and value.

## NotSamef

```go
func NotSamef(t TestingT, expected interface{}, actual interface{}, msg string, args ...interface{}) bool
```

NotSamef asserts that two pointers do not reference the same object.

	assert.NotSamef(t, ptr1, ptr2, "error message %s", "formatted")

Both arguments must be pointer variables. Pointer variable sameness is determined based on the equality of both type and value.

## NotSubset

```go
func NotSubset(t TestingT, list, subset interface{}, msgAndArgs ...interface{}) (ok bool)
```

NotSubset asserts that the list (array, slice, or map) does NOT contain all elements given in the subset (array, slice, or map). Map elements are key-value pairs unless compared with an array or slice where only the map key is evaluated.

	assert.NotSubset(t, [1, 3, 4], [1, 2])
	assert.NotSubset(t, {"x": 1, "y": 2}, {"z": 3})
	assert.NotSubset(t, [1, 3, 4], {1: "one", 2: "two"})
	assert.NotSubset(t, {"x": 1, "y": 2}, ["z"])

## NotSubsetf

```go
func NotSubsetf(t TestingT, list interface{}, subset interface{}, msg string, args ...interface{}) bool
```

NotSubsetf asserts that the list (array, slice, or map) does NOT contain all elements given in the subset (array, slice, or map). Map elements are key-value pairs unless compared with an array or slice where only the map key is evaluated.

	assert.NotSubsetf(t, [1, 3, 4], [1, 2], "error message %s", "formatted")
	assert.NotSubsetf(t, {"x": 1, "y": 2}, {"z": 3}, "error message %s", "formatted")
	assert.NotSubsetf(t, [1, 3, 4], {1: "one", 2: "two"}, "error message %s", "formatted")
	assert.NotSubsetf(t, {"x": 1, "y": 2}, ["z"], "error message %s", "formatted")

## NotZero

```go
func NotZero(t TestingT, i interface{}, msgAndArgs ...interface{}) bool
```

NotZero asserts that i is not the zero value for its type.

## NotZerof

```go
func NotZerof(t TestingT, i interface{}, msg string, args ...interface{}) bool
```

NotZerof asserts that i is not the zero value for its type.

## ObjectsAreEqual

```go
func ObjectsAreEqual(expected, actual interface{}) bool
```

ObjectsAreEqual determines if two objects are considered equal.

This function does no assertion of any kind.

## ObjectsAreEqualValues

```go
func ObjectsAreEqualValues(expected, actual interface{}) bool
```

ObjectsAreEqualValues gets whether two objects are equal, or if their values are equal.

## ObjectsExportedFieldsAreEqual

```go
func ObjectsExportedFieldsAreEqual(expected, actual interface{}) bool
```

ObjectsExportedFieldsAreEqual determines if the exported (public) fields of two objects are considered equal. This comparison of only exported fields is applied recursively to nested data structures.

This function does no assertion of any kind.

Deprecated: Use [EqualExportedValues](#func-EqualExportedValues) instead.

## Panics

```go
func Panics(t TestingT, f PanicTestFunc, msgAndArgs ...interface{}) bool
```

Panics asserts that the code inside the specified PanicTestFunc panics.

	assert.Panics(t, func(){ GoCrazy() })

## PanicsWithError

```go
func PanicsWithError(t TestingT, errString string, f PanicTestFunc, msgAndArgs ...interface{}) bool
```

PanicsWithError asserts that the code inside the specified PanicTestFunc panics, and that the recovered panic value is an error that satisfies the EqualError comparison.

	assert.PanicsWithError(t, "crazy error", func(){ GoCrazy() })

## PanicsWithErrorf

```go
func PanicsWithErrorf(t TestingT, errString string, f PanicTestFunc, msg string, args ...interface{}) bool
```

PanicsWithErrorf asserts that the code inside the specified PanicTestFunc panics, and that the recovered panic value is an error that satisfies the EqualError comparison.

	assert.PanicsWithErrorf(t, "crazy error", func(){ GoCrazy() }, "error message %s", "formatted")

## PanicsWithValue

```go
func PanicsWithValue(t TestingT, expected interface{}, f PanicTestFunc, msgAndArgs ...interface{}) bool
```

PanicsWithValue asserts that the code inside the specified PanicTestFunc panics, and that the recovered panic value equals the expected panic value.

	assert.PanicsWithValue(t, "crazy error", func(){ GoCrazy() })

## PanicsWithValuef

```go
func PanicsWithValuef(t TestingT, expected interface{}, f PanicTestFunc, msg string, args ...interface{}) bool
```

PanicsWithValuef asserts that the code inside the specified PanicTestFunc panics, and that the recovered panic value equals the expected panic value.

	assert.PanicsWithValuef(t, "crazy error", func(){ GoCrazy() }, "error message %s", "formatted")

## Panicsf

```go
func Panicsf(t TestingT, f PanicTestFunc, msg string, args ...interface{}) bool
```

Panicsf asserts that the code inside the specified PanicTestFunc panics.

	assert.Panicsf(t, func(){ GoCrazy() }, "error message %s", "formatted")

## Positive

```go
func Positive(t TestingT, e interface{}, msgAndArgs ...interface{}) bool
```

Positive asserts that the specified element is positive

	assert.Positive(t, 1)
	assert.Positive(t, 1.23)

## Positivef

```go
func Positivef(t TestingT, e interface{}, msg string, args ...interface{}) bool
```

Positivef asserts that the specified element is positive

	assert.Positivef(t, 1, "error message %s", "formatted")
	assert.Positivef(t, 1.23, "error message %s", "formatted")

## Regexp

```go
func Regexp(t TestingT, rx interface{}, str interface{}, msgAndArgs ...interface{}) bool
```

Regexp asserts that a specified regexp matches a string.

	assert.Regexp(t, regexp.MustCompile("start"), "it's starting")
	assert.Regexp(t, "start...$", "it's not starting")

## Regexpf

```go
func Regexpf(t TestingT, rx interface{}, str interface{}, msg string, args ...interface{}) bool
```

Regexpf asserts that a specified regexp matches a string.

	assert.Regexpf(t, regexp.MustCompile("start"), "it's starting", "error message %s", "formatted")
	assert.Regexpf(t, "start...$", "it's not starting", "error message %s", "formatted")

## Same

```go
func Same(t TestingT, expected, actual interface{}, msgAndArgs ...interface{}) bool
```

Same asserts that two pointers reference the same object.

	assert.Same(t, ptr1, ptr2)

Both arguments must be pointer variables. Pointer variable sameness is determined based on the equality of both type and value.

## Samef

```go
func Samef(t TestingT, expected interface{}, actual interface{}, msg string, args ...interface{}) bool
```

Samef asserts that two pointers reference the same object.

	assert.Samef(t, ptr1, ptr2, "error message %s", "formatted")

Both arguments must be pointer variables. Pointer variable sameness is determined based on the equality of both type and value.

## Subset

```go
func Subset(t TestingT, list, subset interface{}, msgAndArgs ...interface{}) (ok bool)
```

Subset asserts that the list (array, slice, or map) contains all elements given in the subset (array, slice, or map). Map elements are key-value pairs unless compared with an array or slice where only the map key is evaluated.

	assert.Subset(t, [1, 2, 3], [1, 2])
	assert.Subset(t, {"x": 1, "y": 2}, {"x": 1})
	assert.Subset(t, [1, 2, 3], {1: "one", 2: "two"})
	assert.Subset(t, {"x": 1, "y": 2}, ["x"])

## Subsetf

```go
func Subsetf(t TestingT, list interface{}, subset interface{}, msg string, args ...interface{}) bool
```

Subsetf asserts that the list (array, slice, or map) contains all elements given in the subset (array, slice, or map). Map elements are key-value pairs unless compared with an array or slice where only the map key is evaluated.

	assert.Subsetf(t, [1, 2, 3], [1, 2], "error message %s", "formatted")
	assert.Subsetf(t, {"x": 1, "y": 2}, {"x": 1}, "error message %s", "formatted")
	assert.Subsetf(t, [1, 2, 3], {1: "one", 2: "two"}, "error message %s", "formatted")
	assert.Subsetf(t, {"x": 1, "y": 2}, ["x"], "error message %s", "formatted")

## True

```go
func True(t TestingT, value bool, msgAndArgs ...interface{}) bool
```

True asserts that the specified value is true.

	assert.True(t, myBool)

## Truef

```go
func Truef(t TestingT, value bool, msg string, args ...interface{}) bool
```

Truef asserts that the specified value is true.

	assert.Truef(t, myBool, "error message %s", "formatted")

## WithinDuration

```go
func WithinDuration(t TestingT, expected, actual time.Time, delta time.Duration, msgAndArgs ...interface{}) bool
```

WithinDuration asserts that the two times are within duration delta of each other.

	assert.WithinDuration(t, time.Now(), time.Now(), 10*time.Second)

## WithinDurationf

```go
func WithinDurationf(t TestingT, expected time.Time, actual time.Time, delta time.Duration, msg string, args ...interface{}) bool
```

WithinDurationf asserts that the two times are within duration delta of each other.

	assert.WithinDurationf(t, time.Now(), time.Now(), 10*time.Second, "error message %s", "formatted")

## WithinRange

```go
func WithinRange(t TestingT, actual, start, end time.Time, msgAndArgs ...interface{}) bool
```

WithinRange asserts that a time is within a time range (inclusive).

	assert.WithinRange(t, time.Now(), time.Now().Add(-time.Second), time.Now().Add(time.Second))

## WithinRangef

```go
func WithinRangef(t TestingT, actual time.Time, start time.Time, end time.Time, msg string, args ...interface{}) bool
```

WithinRangef asserts that a time is within a time range (inclusive).

	assert.WithinRangef(t, time.Now(), time.Now().Add(-time.Second), time.Now().Add(time.Second), "error message %s", "formatted")

## YAMLEq

```go
func YAMLEq(t TestingT, expected string, actual string, msgAndArgs ...interface{}) bool
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
	assert.YAMLEq(t, expected, actual)

## YAMLEqf

```go
func YAMLEqf(t TestingT, expected string, actual string, msg string, args ...interface{}) bool
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
	assert.YAMLEqf(t, expected, actual, "error message %s", "formatted")

## Zero

```go
func Zero(t TestingT, i interface{}, msgAndArgs ...interface{}) bool
```

Zero asserts that i is the zero value for its type.

## Zerof

```go
func Zerof(t TestingT, i interface{}, msg string, args ...interface{}) bool
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
func (a *Assertions) Condition(comp Comparison, msgAndArgs ...interface{}) bool
```

Condition uses a Comparison to assert a complex condition.

## Conditionf

```go
func (a *Assertions) Conditionf(comp Comparison, msg string, args ...interface{}) bool
```

Conditionf uses a Comparison to assert a complex condition.

## Contains

```go
func (a *Assertions) Contains(s interface{}, contains interface{}, msgAndArgs ...interface{}) bool
```

Contains asserts that the specified string, list(array, slice...) or map contains the specified substring or element.

	a.Contains("Hello World", "World")
	a.Contains(["Hello", "World"], "World")
	a.Contains({"Hello": "World"}, "Hello")

## Containsf

```go
func (a *Assertions) Containsf(s interface{}, contains interface{}, msg string, args ...interface{}) bool
```

Containsf asserts that the specified string, list(array, slice...) or map contains the specified substring or element.

	a.Containsf("Hello World", "World", "error message %s", "formatted")
	a.Containsf(["Hello", "World"], "World", "error message %s", "formatted")
	a.Containsf({"Hello": "World"}, "Hello", "error message %s", "formatted")

## DirExists

```go
func (a *Assertions) DirExists(path string, msgAndArgs ...interface{}) bool
```

DirExists checks whether a directory exists in the given path. It also fails if the path is a file rather a directory or there is an error checking whether it exists.

## DirExistsf

```go
func (a *Assertions) DirExistsf(path string, msg string, args ...interface{}) bool
```

DirExistsf checks whether a directory exists in the given path. It also fails if the path is a file rather a directory or there is an error checking whether it exists.

## ElementsMatch

```go
func (a *Assertions) ElementsMatch(listA interface{}, listB interface{}, msgAndArgs ...interface{}) bool
```

ElementsMatch asserts that the specified listA(array, slice...) is equal to specified listB(array, slice...) ignoring the order of the elements. If there are duplicate elements, the number of appearances of each of them in both lists should match.

a.ElementsMatch(\[1, 3, 2, 3], \[1, 3, 3, 2])

## ElementsMatchf

```go
func (a *Assertions) ElementsMatchf(listA interface{}, listB interface{}, msg string, args ...interface{}) bool
```

ElementsMatchf asserts that the specified listA(array, slice...) is equal to specified listB(array, slice...) ignoring the order of the elements. If there are duplicate elements, the number of appearances of each of them in both lists should match.

a.ElementsMatchf(\[1, 3, 2, 3], \[1, 3, 3, 2], "error message %s", "formatted")

## Empty

```go
func (a *Assertions) Empty(object interface{}, msgAndArgs ...interface{}) bool
```

Empty asserts that the given value is "empty".

[Zero values](https://go.dev/ref/spec#The_zero_value) are "empty".

Arrays are "empty" if every element is the zero value of the type (stricter than "empty").

Slices, maps and channels with zero length are "empty".

Pointer values are "empty" if the pointer is nil or if the pointed value is "empty".

	a.Empty(obj)

## Emptyf

```go
func (a *Assertions) Emptyf(object interface{}, msg string, args ...interface{}) bool
```

Emptyf asserts that the given value is "empty".

[Zero values](https://go.dev/ref/spec#The_zero_value) are "empty".

Arrays are "empty" if every element is the zero value of the type (stricter than "empty").

Slices, maps and channels with zero length are "empty".

Pointer values are "empty" if the pointer is nil or if the pointed value is "empty".

	a.Emptyf(obj, "error message %s", "formatted")

## Equal

```go
func (a *Assertions) Equal(expected interface{}, actual interface{}, msgAndArgs ...interface{}) bool
```

Equal asserts that two objects are equal.

	a.Equal(123, 123)

Pointer variable equality is determined based on the equality of the referenced values (as opposed to the memory addresses). Function equality cannot be determined and will always fail.

## EqualError

```go
func (a *Assertions) EqualError(theError error, errString string, msgAndArgs ...interface{}) bool
```

EqualError asserts that a function returned a non-nil error (i.e. an error) and that it is equal to the provided error.

	actualObj, err := SomeFunction()
	a.EqualError(err,  expectedErrorString)

## EqualErrorf

```go
func (a *Assertions) EqualErrorf(theError error, errString string, msg string, args ...interface{}) bool
```

EqualErrorf asserts that a function returned a non-nil error (i.e. an error) and that it is equal to the provided error.

	actualObj, err := SomeFunction()
	a.EqualErrorf(err,  expectedErrorString, "error message %s", "formatted")

## EqualExportedValues

```go
func (a *Assertions) EqualExportedValues(expected interface{}, actual interface{}, msgAndArgs ...interface{}) bool
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
func (a *Assertions) EqualExportedValuesf(expected interface{}, actual interface{}, msg string, args ...interface{}) bool
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
func (a *Assertions) EqualValues(expected interface{}, actual interface{}, msgAndArgs ...interface{}) bool
```

EqualValues asserts that two objects are equal or convertible to the larger type and equal.

	a.EqualValues(uint32(123), int32(123))

## EqualValuesf

```go
func (a *Assertions) EqualValuesf(expected interface{}, actual interface{}, msg string, args ...interface{}) bool
```

EqualValuesf asserts that two objects are equal or convertible to the larger type and equal.

	a.EqualValuesf(uint32(123), int32(123), "error message %s", "formatted")

## Equalf

```go
func (a *Assertions) Equalf(expected interface{}, actual interface{}, msg string, args ...interface{}) bool
```

Equalf asserts that two objects are equal.

	a.Equalf(123, 123, "error message %s", "formatted")

Pointer variable equality is determined based on the equality of the referenced values (as opposed to the memory addresses). Function equality cannot be determined and will always fail.

## Error

```go
func (a *Assertions) Error(err error, msgAndArgs ...interface{}) bool
```

Error asserts that a function returned a non-nil error (ie. an error).

	actualObj, err := SomeFunction()
	a.Error(err)

## ErrorAs

```go
func (a *Assertions) ErrorAs(err error, target interface{}, msgAndArgs ...interface{}) bool
```

ErrorAs asserts that at least one of the errors in err's chain matches target, and if so, sets target to that error value. This is a wrapper for errors.As.

## ErrorAsf

```go
func (a *Assertions) ErrorAsf(err error, target interface{}, msg string, args ...interface{}) bool
```

ErrorAsf asserts that at least one of the errors in err's chain matches target, and if so, sets target to that error value. This is a wrapper for errors.As.

## ErrorContains

```go
func (a *Assertions) ErrorContains(theError error, contains string, msgAndArgs ...interface{}) bool
```

ErrorContains asserts that a function returned a non-nil error (i.e. an error) and that the error contains the specified substring.

	actualObj, err := SomeFunction()
	a.ErrorContains(err,  expectedErrorSubString)

## ErrorContainsf

```go
func (a *Assertions) ErrorContainsf(theError error, contains string, msg string, args ...interface{}) bool
```

ErrorContainsf asserts that a function returned a non-nil error (i.e. an error) and that the error contains the specified substring.

	actualObj, err := SomeFunction()
	a.ErrorContainsf(err,  expectedErrorSubString, "error message %s", "formatted")

## ErrorIs

```go
func (a *Assertions) ErrorIs(err error, target error, msgAndArgs ...interface{}) bool
```

ErrorIs asserts that at least one of the errors in err's chain matches target. This is a wrapper for errors.Is.

## ErrorIsf

```go
func (a *Assertions) ErrorIsf(err error, target error, msg string, args ...interface{}) bool
```

ErrorIsf asserts that at least one of the errors in err's chain matches target. This is a wrapper for errors.Is.

## Errorf

```go
func (a *Assertions) Errorf(err error, msg string, args ...interface{}) bool
```

Errorf asserts that a function returned a non-nil error (ie. an error).

	actualObj, err := SomeFunction()
	a.Errorf(err, "error message %s", "formatted")

## Eventually

```go
func (a *Assertions) Eventually(condition func() bool, waitFor time.Duration, tick time.Duration, msgAndArgs ...interface{}) bool
```

Eventually asserts that given condition will be met in waitFor time, periodically checking target function each tick.

	a.Eventually(func() bool { return true; }, time.Second, 10*time.Millisecond)

## EventuallyWithT

```go
func (a *Assertions) EventuallyWithT(condition func(collect *CollectT), waitFor time.Duration, tick time.Duration, msgAndArgs ...interface{}) bool
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
func (a *Assertions) EventuallyWithTf(condition func(collect *CollectT), waitFor time.Duration, tick time.Duration, msg string, args ...interface{}) bool
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
func (a *Assertions) Eventuallyf(condition func() bool, waitFor time.Duration, tick time.Duration, msg string, args ...interface{}) bool
```

Eventuallyf asserts that given condition will be met in waitFor time, periodically checking target function each tick.

	a.Eventuallyf(func() bool { return true; }, time.Second, 10*time.Millisecond, "error message %s", "formatted")

## Exactly

```go
func (a *Assertions) Exactly(expected interface{}, actual interface{}, msgAndArgs ...interface{}) bool
```

Exactly asserts that two objects are equal in value and type.

	a.Exactly(int32(123), int64(123))

## Exactlyf

```go
func (a *Assertions) Exactlyf(expected interface{}, actual interface{}, msg string, args ...interface{}) bool
```

Exactlyf asserts that two objects are equal in value and type.

	a.Exactlyf(int32(123), int64(123), "error message %s", "formatted")

## Fail

```go
func (a *Assertions) Fail(failureMessage string, msgAndArgs ...interface{}) bool
```

Fail reports a failure through

## FailNow

```go
func (a *Assertions) FailNow(failureMessage string, msgAndArgs ...interface{}) bool
```

FailNow fails test

## FailNowf

```go
func (a *Assertions) FailNowf(failureMessage string, msg string, args ...interface{}) bool
```

FailNowf fails test

## Failf

```go
func (a *Assertions) Failf(failureMessage string, msg string, args ...interface{}) bool
```

Failf reports a failure through

## False

```go
func (a *Assertions) False(value bool, msgAndArgs ...interface{}) bool
```

False asserts that the specified value is false.

	a.False(myBool)

## Falsef

```go
func (a *Assertions) Falsef(value bool, msg string, args ...interface{}) bool
```

Falsef asserts that the specified value is false.

	a.Falsef(myBool, "error message %s", "formatted")

## FileExists

```go
func (a *Assertions) FileExists(path string, msgAndArgs ...interface{}) bool
```

FileExists checks whether a file exists in the given path. It also fails if the path points to a directory or there is an error when trying to check the file.

## FileExistsf

```go
func (a *Assertions) FileExistsf(path string, msg string, args ...interface{}) bool
```

FileExistsf checks whether a file exists in the given path. It also fails if the path points to a directory or there is an error when trying to check the file.

## Greater

```go
func (a *Assertions) Greater(e1 interface{}, e2 interface{}, msgAndArgs ...interface{}) bool
```

Greater asserts that the first element is greater than the second

	a.Greater(2, 1)
	a.Greater(float64(2), float64(1))
	a.Greater("b", "a")

## GreaterOrEqual

```go
func (a *Assertions) GreaterOrEqual(e1 interface{}, e2 interface{}, msgAndArgs ...interface{}) bool
```

GreaterOrEqual asserts that the first element is greater than or equal to the second

	a.GreaterOrEqual(2, 1)
	a.GreaterOrEqual(2, 2)
	a.GreaterOrEqual("b", "a")
	a.GreaterOrEqual("b", "b")

## GreaterOrEqualf

```go
func (a *Assertions) GreaterOrEqualf(e1 interface{}, e2 interface{}, msg string, args ...interface{}) bool
```

GreaterOrEqualf asserts that the first element is greater than or equal to the second

	a.GreaterOrEqualf(2, 1, "error message %s", "formatted")
	a.GreaterOrEqualf(2, 2, "error message %s", "formatted")
	a.GreaterOrEqualf("b", "a", "error message %s", "formatted")
	a.GreaterOrEqualf("b", "b", "error message %s", "formatted")

## Greaterf

```go
func (a *Assertions) Greaterf(e1 interface{}, e2 interface{}, msg string, args ...interface{}) bool
```

Greaterf asserts that the first element is greater than the second

	a.Greaterf(2, 1, "error message %s", "formatted")
	a.Greaterf(float64(2), float64(1), "error message %s", "formatted")
	a.Greaterf("b", "a", "error message %s", "formatted")

## HTTPBodyContains

```go
func (a *Assertions) HTTPBodyContains(handler http.HandlerFunc, method string, url string, values url.Values, str interface{}, msgAndArgs ...interface{}) bool
```

HTTPBodyContains asserts that a specified handler returns a body that contains a string.

	a.HTTPBodyContains(myHandler, "GET", "www.google.com", nil, "I'm Feeling Lucky")

Returns whether the assertion was successful (true) or not (false).

## HTTPBodyContainsf

```go
func (a *Assertions) HTTPBodyContainsf(handler http.HandlerFunc, method string, url string, values url.Values, str interface{}, msg string, args ...interface{}) bool
```

HTTPBodyContainsf asserts that a specified handler returns a body that contains a string.

	a.HTTPBodyContainsf(myHandler, "GET", "www.google.com", nil, "I'm Feeling Lucky", "error message %s", "formatted")

Returns whether the assertion was successful (true) or not (false).

## HTTPBodyNotContains

```go
func (a *Assertions) HTTPBodyNotContains(handler http.HandlerFunc, method string, url string, values url.Values, str interface{}, msgAndArgs ...interface{}) bool
```

HTTPBodyNotContains asserts that a specified handler returns a body that does not contain a string.

	a.HTTPBodyNotContains(myHandler, "GET", "www.google.com", nil, "I'm Feeling Lucky")

Returns whether the assertion was successful (true) or not (false).

## HTTPBodyNotContainsf

```go
func (a *Assertions) HTTPBodyNotContainsf(handler http.HandlerFunc, method string, url string, values url.Values, str interface{}, msg string, args ...interface{}) bool
```

HTTPBodyNotContainsf asserts that a specified handler returns a body that does not contain a string.

	a.HTTPBodyNotContainsf(myHandler, "GET", "www.google.com", nil, "I'm Feeling Lucky", "error message %s", "formatted")

Returns whether the assertion was successful (true) or not (false).

## HTTPError

```go
func (a *Assertions) HTTPError(handler http.HandlerFunc, method string, url string, values url.Values, msgAndArgs ...interface{}) bool
```

HTTPError asserts that a specified handler returns an error status code.

	a.HTTPError(myHandler, "POST", "/a/b/c", url.Values{"a": []string{"b", "c"}}

Returns whether the assertion was successful (true) or not (false).

## HTTPErrorf

```go
func (a *Assertions) HTTPErrorf(handler http.HandlerFunc, method string, url string, values url.Values, msg string, args ...interface{}) bool
```

HTTPErrorf asserts that a specified handler returns an error status code.

	a.HTTPErrorf(myHandler, "POST", "/a/b/c", url.Values{"a": []string{"b", "c"}}

Returns whether the assertion was successful (true) or not (false).

## HTTPRedirect

```go
func (a *Assertions) HTTPRedirect(handler http.HandlerFunc, method string, url string, values url.Values, msgAndArgs ...interface{}) bool
```

HTTPRedirect asserts that a specified handler returns a redirect status code.

	a.HTTPRedirect(myHandler, "GET", "/a/b/c", url.Values{"a": []string{"b", "c"}}

Returns whether the assertion was successful (true) or not (false).

## HTTPRedirectf

```go
func (a *Assertions) HTTPRedirectf(handler http.HandlerFunc, method string, url string, values url.Values, msg string, args ...interface{}) bool
```

HTTPRedirectf asserts that a specified handler returns a redirect status code.

	a.HTTPRedirectf(myHandler, "GET", "/a/b/c", url.Values{"a": []string{"b", "c"}}

Returns whether the assertion was successful (true) or not (false).

## HTTPStatusCode

```go
func (a *Assertions) HTTPStatusCode(handler http.HandlerFunc, method string, url string, values url.Values, statuscode int, msgAndArgs ...interface{}) bool
```

HTTPStatusCode asserts that a specified handler returns a specified status code.

	a.HTTPStatusCode(myHandler, "GET", "/notImplemented", nil, 501)

Returns whether the assertion was successful (true) or not (false).

## HTTPStatusCodef

```go
func (a *Assertions) HTTPStatusCodef(handler http.HandlerFunc, method string, url string, values url.Values, statuscode int, msg string, args ...interface{}) bool
```

HTTPStatusCodef asserts that a specified handler returns a specified status code.

	a.HTTPStatusCodef(myHandler, "GET", "/notImplemented", nil, 501, "error message %s", "formatted")

Returns whether the assertion was successful (true) or not (false).

## HTTPSuccess

```go
func (a *Assertions) HTTPSuccess(handler http.HandlerFunc, method string, url string, values url.Values, msgAndArgs ...interface{}) bool
```

HTTPSuccess asserts that a specified handler returns a success status code.

	a.HTTPSuccess(myHandler, "POST", "http://www.google.com", nil)

Returns whether the assertion was successful (true) or not (false).

## HTTPSuccessf

```go
func (a *Assertions) HTTPSuccessf(handler http.HandlerFunc, method string, url string, values url.Values, msg string, args ...interface{}) bool
```

HTTPSuccessf asserts that a specified handler returns a success status code.

	a.HTTPSuccessf(myHandler, "POST", "http://www.google.com", nil, "error message %s", "formatted")

Returns whether the assertion was successful (true) or not (false).

## Implements

```go
func (a *Assertions) Implements(interfaceObject interface{}, object interface{}, msgAndArgs ...interface{}) bool
```

Implements asserts that an object is implemented by the specified interface.

	a.Implements((*MyInterface)(nil), new(MyObject))

## Implementsf

```go
func (a *Assertions) Implementsf(interfaceObject interface{}, object interface{}, msg string, args ...interface{}) bool
```

Implementsf asserts that an object is implemented by the specified interface.

	a.Implementsf((*MyInterface)(nil), new(MyObject), "error message %s", "formatted")

## InDelta

```go
func (a *Assertions) InDelta(expected interface{}, actual interface{}, delta float64, msgAndArgs ...interface{}) bool
```

InDelta asserts that the two numerals are within delta of each other.

	a.InDelta(math.Pi, 22/7.0, 0.01)

## InDeltaMapValues

```go
func (a *Assertions) InDeltaMapValues(expected interface{}, actual interface{}, delta float64, msgAndArgs ...interface{}) bool
```

InDeltaMapValues is the same as InDelta, but it compares all values between two maps. Both maps must have exactly the same keys.

## InDeltaMapValuesf

```go
func (a *Assertions) InDeltaMapValuesf(expected interface{}, actual interface{}, delta float64, msg string, args ...interface{}) bool
```

InDeltaMapValuesf is the same as InDelta, but it compares all values between two maps. Both maps must have exactly the same keys.

## InDeltaSlice

```go
func (a *Assertions) InDeltaSlice(expected interface{}, actual interface{}, delta float64, msgAndArgs ...interface{}) bool
```

InDeltaSlice is the same as InDelta, except it compares two slices.

## InDeltaSlicef

```go
func (a *Assertions) InDeltaSlicef(expected interface{}, actual interface{}, delta float64, msg string, args ...interface{}) bool
```

InDeltaSlicef is the same as InDelta, except it compares two slices.

## InDeltaf

```go
func (a *Assertions) InDeltaf(expected interface{}, actual interface{}, delta float64, msg string, args ...interface{}) bool
```

InDeltaf asserts that the two numerals are within delta of each other.

	a.InDeltaf(math.Pi, 22/7.0, 0.01, "error message %s", "formatted")

## InEpsilon

```go
func (a *Assertions) InEpsilon(expected interface{}, actual interface{}, epsilon float64, msgAndArgs ...interface{}) bool
```

InEpsilon asserts that expected and actual have a relative error less than epsilon

## InEpsilonSlice

```go
func (a *Assertions) InEpsilonSlice(expected interface{}, actual interface{}, epsilon float64, msgAndArgs ...interface{}) bool
```

InEpsilonSlice is the same as InEpsilon, except it compares each value from two slices.

## InEpsilonSlicef

```go
func (a *Assertions) InEpsilonSlicef(expected interface{}, actual interface{}, epsilon float64, msg string, args ...interface{}) bool
```

InEpsilonSlicef is the same as InEpsilon, except it compares each value from two slices.

## InEpsilonf

```go
func (a *Assertions) InEpsilonf(expected interface{}, actual interface{}, epsilon float64, msg string, args ...interface{}) bool
```

InEpsilonf asserts that expected and actual have a relative error less than epsilon

## IsDecreasing

```go
func (a *Assertions) IsDecreasing(object interface{}, msgAndArgs ...interface{}) bool
```

IsDecreasing asserts that the collection is decreasing

	a.IsDecreasing([]int{2, 1, 0})
	a.IsDecreasing([]float{2, 1})
	a.IsDecreasing([]string{"b", "a"})

## IsDecreasingf

```go
func (a *Assertions) IsDecreasingf(object interface{}, msg string, args ...interface{}) bool
```

IsDecreasingf asserts that the collection is decreasing

	a.IsDecreasingf([]int{2, 1, 0}, "error message %s", "formatted")
	a.IsDecreasingf([]float{2, 1}, "error message %s", "formatted")
	a.IsDecreasingf([]string{"b", "a"}, "error message %s", "formatted")

## IsIncreasing

```go
func (a *Assertions) IsIncreasing(object interface{}, msgAndArgs ...interface{}) bool
```

IsIncreasing asserts that the collection is increasing

	a.IsIncreasing([]int{1, 2, 3})
	a.IsIncreasing([]float{1, 2})
	a.IsIncreasing([]string{"a", "b"})

## IsIncreasingf

```go
func (a *Assertions) IsIncreasingf(object interface{}, msg string, args ...interface{}) bool
```

IsIncreasingf asserts that the collection is increasing

	a.IsIncreasingf([]int{1, 2, 3}, "error message %s", "formatted")
	a.IsIncreasingf([]float{1, 2}, "error message %s", "formatted")
	a.IsIncreasingf([]string{"a", "b"}, "error message %s", "formatted")

## IsNonDecreasing

```go
func (a *Assertions) IsNonDecreasing(object interface{}, msgAndArgs ...interface{}) bool
```

IsNonDecreasing asserts that the collection is not decreasing

	a.IsNonDecreasing([]int{1, 1, 2})
	a.IsNonDecreasing([]float{1, 2})
	a.IsNonDecreasing([]string{"a", "b"})

## IsNonDecreasingf

```go
func (a *Assertions) IsNonDecreasingf(object interface{}, msg string, args ...interface{}) bool
```

IsNonDecreasingf asserts that the collection is not decreasing

	a.IsNonDecreasingf([]int{1, 1, 2}, "error message %s", "formatted")
	a.IsNonDecreasingf([]float{1, 2}, "error message %s", "formatted")
	a.IsNonDecreasingf([]string{"a", "b"}, "error message %s", "formatted")

## IsNonIncreasing

```go
func (a *Assertions) IsNonIncreasing(object interface{}, msgAndArgs ...interface{}) bool
```

IsNonIncreasing asserts that the collection is not increasing

	a.IsNonIncreasing([]int{2, 1, 1})
	a.IsNonIncreasing([]float{2, 1})
	a.IsNonIncreasing([]string{"b", "a"})

## IsNonIncreasingf

```go
func (a *Assertions) IsNonIncreasingf(object interface{}, msg string, args ...interface{}) bool
```

IsNonIncreasingf asserts that the collection is not increasing

	a.IsNonIncreasingf([]int{2, 1, 1}, "error message %s", "formatted")
	a.IsNonIncreasingf([]float{2, 1}, "error message %s", "formatted")
	a.IsNonIncreasingf([]string{"b", "a"}, "error message %s", "formatted")

## IsNotType

```go
func (a *Assertions) IsNotType(theType interface{}, object interface{}, msgAndArgs ...interface{}) bool
```

IsNotType asserts that the specified objects are not of the same type.

	a.IsNotType(&NotMyStruct{}, &MyStruct{})

## IsNotTypef

```go
func (a *Assertions) IsNotTypef(theType interface{}, object interface{}, msg string, args ...interface{}) bool
```

IsNotTypef asserts that the specified objects are not of the same type.

	a.IsNotTypef(&NotMyStruct{}, &MyStruct{}, "error message %s", "formatted")

## IsType

```go
func (a *Assertions) IsType(expectedType interface{}, object interface{}, msgAndArgs ...interface{}) bool
```

IsType asserts that the specified objects are of the same type.

	a.IsType(&MyStruct{}, &MyStruct{})

## IsTypef

```go
func (a *Assertions) IsTypef(expectedType interface{}, object interface{}, msg string, args ...interface{}) bool
```

IsTypef asserts that the specified objects are of the same type.

	a.IsTypef(&MyStruct{}, &MyStruct{}, "error message %s", "formatted")

## JSONEq

```go
func (a *Assertions) JSONEq(expected string, actual string, msgAndArgs ...interface{}) bool
```

JSONEq asserts that two JSON strings are equivalent.

	a.JSONEq(`{"hello": "world", "foo": "bar"}`, `{"foo": "bar", "hello": "world"}`)

## JSONEqf

```go
func (a *Assertions) JSONEqf(expected string, actual string, msg string, args ...interface{}) bool
```

JSONEqf asserts that two JSON strings are equivalent.

	a.JSONEqf(`{"hello": "world", "foo": "bar"}`, `{"foo": "bar", "hello": "world"}`, "error message %s", "formatted")

## Len

```go
func (a *Assertions) Len(object interface{}, length int, msgAndArgs ...interface{}) bool
```

Len asserts that the specified object has specific length. Len also fails if the object has a type that len() not accept.

	a.Len(mySlice, 3)

## Lenf

```go
func (a *Assertions) Lenf(object interface{}, length int, msg string, args ...interface{}) bool
```

Lenf asserts that the specified object has specific length. Lenf also fails if the object has a type that len() not accept.

	a.Lenf(mySlice, 3, "error message %s", "formatted")

## Less

```go
func (a *Assertions) Less(e1 interface{}, e2 interface{}, msgAndArgs ...interface{}) bool
```

Less asserts that the first element is less than the second

	a.Less(1, 2)
	a.Less(float64(1), float64(2))
	a.Less("a", "b")

## LessOrEqual

```go
func (a *Assertions) LessOrEqual(e1 interface{}, e2 interface{}, msgAndArgs ...interface{}) bool
```

LessOrEqual asserts that the first element is less than or equal to the second

	a.LessOrEqual(1, 2)
	a.LessOrEqual(2, 2)
	a.LessOrEqual("a", "b")
	a.LessOrEqual("b", "b")

## LessOrEqualf

```go
func (a *Assertions) LessOrEqualf(e1 interface{}, e2 interface{}, msg string, args ...interface{}) bool
```

LessOrEqualf asserts that the first element is less than or equal to the second

	a.LessOrEqualf(1, 2, "error message %s", "formatted")
	a.LessOrEqualf(2, 2, "error message %s", "formatted")
	a.LessOrEqualf("a", "b", "error message %s", "formatted")
	a.LessOrEqualf("b", "b", "error message %s", "formatted")

## Lessf

```go
func (a *Assertions) Lessf(e1 interface{}, e2 interface{}, msg string, args ...interface{}) bool
```

Lessf asserts that the first element is less than the second

	a.Lessf(1, 2, "error message %s", "formatted")
	a.Lessf(float64(1), float64(2), "error message %s", "formatted")
	a.Lessf("a", "b", "error message %s", "formatted")

## Negative

```go
func (a *Assertions) Negative(e interface{}, msgAndArgs ...interface{}) bool
```

Negative asserts that the specified element is negative

	a.Negative(-1)
	a.Negative(-1.23)

## Negativef

```go
func (a *Assertions) Negativef(e interface{}, msg string, args ...interface{}) bool
```

Negativef asserts that the specified element is negative

	a.Negativef(-1, "error message %s", "formatted")
	a.Negativef(-1.23, "error message %s", "formatted")

## Never

```go
func (a *Assertions) Never(condition func() bool, waitFor time.Duration, tick time.Duration, msgAndArgs ...interface{}) bool
```

Never asserts that the given condition doesn't satisfy in waitFor time, periodically checking the target function each tick.

	a.Never(func() bool { return false; }, time.Second, 10*time.Millisecond)

## Neverf

```go
func (a *Assertions) Neverf(condition func() bool, waitFor time.Duration, tick time.Duration, msg string, args ...interface{}) bool
```

Neverf asserts that the given condition doesn't satisfy in waitFor time, periodically checking the target function each tick.

	a.Neverf(func() bool { return false; }, time.Second, 10*time.Millisecond, "error message %s", "formatted")

## Nil

```go
func (a *Assertions) Nil(object interface{}, msgAndArgs ...interface{}) bool
```

Nil asserts that the specified object is nil.

	a.Nil(err)

## Nilf

```go
func (a *Assertions) Nilf(object interface{}, msg string, args ...interface{}) bool
```

Nilf asserts that the specified object is nil.

	a.Nilf(err, "error message %s", "formatted")

## NoDirExists

```go
func (a *Assertions) NoDirExists(path string, msgAndArgs ...interface{}) bool
```

NoDirExists checks whether a directory does not exist in the given path. It fails if the path points to an existing \_directory\_ only.

## NoDirExistsf

```go
func (a *Assertions) NoDirExistsf(path string, msg string, args ...interface{}) bool
```

NoDirExistsf checks whether a directory does not exist in the given path. It fails if the path points to an existing \_directory\_ only.

## NoError

```go
func (a *Assertions) NoError(err error, msgAndArgs ...interface{}) bool
```

NoError asserts that a function returned a nil error (ie. no error).

	  actualObj, err := SomeFunction()
	  if a.NoError(err) {
		   assert.Equal(t, expectedObj, actualObj)
	  }

## NoErrorf

```go
func (a *Assertions) NoErrorf(err error, msg string, args ...interface{}) bool
```

NoErrorf asserts that a function returned a nil error (ie. no error).

	  actualObj, err := SomeFunction()
	  if a.NoErrorf(err, "error message %s", "formatted") {
		   assert.Equal(t, expectedObj, actualObj)
	  }

## NoFileExists

```go
func (a *Assertions) NoFileExists(path string, msgAndArgs ...interface{}) bool
```

NoFileExists checks whether a file does not exist in a given path. It fails if the path points to an existing \_file\_ only.

## NoFileExistsf

```go
func (a *Assertions) NoFileExistsf(path string, msg string, args ...interface{}) bool
```

NoFileExistsf checks whether a file does not exist in a given path. It fails if the path points to an existing \_file\_ only.

## NotContains

```go
func (a *Assertions) NotContains(s interface{}, contains interface{}, msgAndArgs ...interface{}) bool
```

NotContains asserts that the specified string, list(array, slice...) or map does NOT contain the specified substring or element.

	a.NotContains("Hello World", "Earth")
	a.NotContains(["Hello", "World"], "Earth")
	a.NotContains({"Hello": "World"}, "Earth")

## NotContainsf

```go
func (a *Assertions) NotContainsf(s interface{}, contains interface{}, msg string, args ...interface{}) bool
```

NotContainsf asserts that the specified string, list(array, slice...) or map does NOT contain the specified substring or element.

	a.NotContainsf("Hello World", "Earth", "error message %s", "formatted")
	a.NotContainsf(["Hello", "World"], "Earth", "error message %s", "formatted")
	a.NotContainsf({"Hello": "World"}, "Earth", "error message %s", "formatted")

## NotElementsMatch

```go
func (a *Assertions) NotElementsMatch(listA interface{}, listB interface{}, msgAndArgs ...interface{}) bool
```

NotElementsMatch asserts that the specified listA(array, slice...) is NOT equal to specified listB(array, slice...) ignoring the order of the elements. If there are duplicate elements, the number of appearances of each of them in both lists should not match. This is an inverse of ElementsMatch.

a.NotElementsMatch(\[1, 1, 2, 3], \[1, 1, 2, 3]) -> false

a.NotElementsMatch(\[1, 1, 2, 3], \[1, 2, 3]) -> true

a.NotElementsMatch(\[1, 2, 3], \[1, 2, 4]) -> true

## NotElementsMatchf

```go
func (a *Assertions) NotElementsMatchf(listA interface{}, listB interface{}, msg string, args ...interface{}) bool
```

NotElementsMatchf asserts that the specified listA(array, slice...) is NOT equal to specified listB(array, slice...) ignoring the order of the elements. If there are duplicate elements, the number of appearances of each of them in both lists should not match. This is an inverse of ElementsMatch.

a.NotElementsMatchf(\[1, 1, 2, 3], \[1, 1, 2, 3], "error message %s", "formatted") -> false

a.NotElementsMatchf(\[1, 1, 2, 3], \[1, 2, 3], "error message %s", "formatted") -> true

a.NotElementsMatchf(\[1, 2, 3], \[1, 2, 4], "error message %s", "formatted") -> true

## NotEmpty

```go
func (a *Assertions) NotEmpty(object interface{}, msgAndArgs ...interface{}) bool
```

NotEmpty asserts that the specified object is NOT [Empty](#func-Empty).

	if a.NotEmpty(obj) {
	  assert.Equal(t, "two", obj[1])
	}

## NotEmptyf

```go
func (a *Assertions) NotEmptyf(object interface{}, msg string, args ...interface{}) bool
```

NotEmptyf asserts that the specified object is NOT [Empty](#func-Empty).

	if a.NotEmptyf(obj, "error message %s", "formatted") {
	  assert.Equal(t, "two", obj[1])
	}

## NotEqual

```go
func (a *Assertions) NotEqual(expected interface{}, actual interface{}, msgAndArgs ...interface{}) bool
```

NotEqual asserts that the specified values are NOT equal.

	a.NotEqual(obj1, obj2)

Pointer variable equality is determined based on the equality of the referenced values (as opposed to the memory addresses).

## NotEqualValues

```go
func (a *Assertions) NotEqualValues(expected interface{}, actual interface{}, msgAndArgs ...interface{}) bool
```

NotEqualValues asserts that two objects are not equal even when converted to the same type

	a.NotEqualValues(obj1, obj2)

## NotEqualValuesf

```go
func (a *Assertions) NotEqualValuesf(expected interface{}, actual interface{}, msg string, args ...interface{}) bool
```

NotEqualValuesf asserts that two objects are not equal even when converted to the same type

	a.NotEqualValuesf(obj1, obj2, "error message %s", "formatted")

## NotEqualf

```go
func (a *Assertions) NotEqualf(expected interface{}, actual interface{}, msg string, args ...interface{}) bool
```

NotEqualf asserts that the specified values are NOT equal.

	a.NotEqualf(obj1, obj2, "error message %s", "formatted")

Pointer variable equality is determined based on the equality of the referenced values (as opposed to the memory addresses).

## NotErrorAs

```go
func (a *Assertions) NotErrorAs(err error, target interface{}, msgAndArgs ...interface{}) bool
```

NotErrorAs asserts that none of the errors in err's chain matches target, but if so, sets target to that error value.

## NotErrorAsf

```go
func (a *Assertions) NotErrorAsf(err error, target interface{}, msg string, args ...interface{}) bool
```

NotErrorAsf asserts that none of the errors in err's chain matches target, but if so, sets target to that error value.

## NotErrorIs

```go
func (a *Assertions) NotErrorIs(err error, target error, msgAndArgs ...interface{}) bool
```

NotErrorIs asserts that none of the errors in err's chain matches target. This is a wrapper for errors.Is.

## NotErrorIsf

```go
func (a *Assertions) NotErrorIsf(err error, target error, msg string, args ...interface{}) bool
```

NotErrorIsf asserts that none of the errors in err's chain matches target. This is a wrapper for errors.Is.

## NotImplements

```go
func (a *Assertions) NotImplements(interfaceObject interface{}, object interface{}, msgAndArgs ...interface{}) bool
```

NotImplements asserts that an object does not implement the specified interface.

	a.NotImplements((*MyInterface)(nil), new(MyObject))

## NotImplementsf

```go
func (a *Assertions) NotImplementsf(interfaceObject interface{}, object interface{}, msg string, args ...interface{}) bool
```

NotImplementsf asserts that an object does not implement the specified interface.

	a.NotImplementsf((*MyInterface)(nil), new(MyObject), "error message %s", "formatted")

## NotNil

```go
func (a *Assertions) NotNil(object interface{}, msgAndArgs ...interface{}) bool
```

NotNil asserts that the specified object is not nil.

	a.NotNil(err)

## NotNilf

```go
func (a *Assertions) NotNilf(object interface{}, msg string, args ...interface{}) bool
```

NotNilf asserts that the specified object is not nil.

	a.NotNilf(err, "error message %s", "formatted")

## NotPanics

```go
func (a *Assertions) NotPanics(f PanicTestFunc, msgAndArgs ...interface{}) bool
```

NotPanics asserts that the code inside the specified PanicTestFunc does NOT panic.

	a.NotPanics(func(){ RemainCalm() })

## NotPanicsf

```go
func (a *Assertions) NotPanicsf(f PanicTestFunc, msg string, args ...interface{}) bool
```

NotPanicsf asserts that the code inside the specified PanicTestFunc does NOT panic.

	a.NotPanicsf(func(){ RemainCalm() }, "error message %s", "formatted")

## NotRegexp

```go
func (a *Assertions) NotRegexp(rx interface{}, str interface{}, msgAndArgs ...interface{}) bool
```

NotRegexp asserts that a specified regexp does not match a string.

	a.NotRegexp(regexp.MustCompile("starts"), "it's starting")
	a.NotRegexp("^start", "it's not starting")

## NotRegexpf

```go
func (a *Assertions) NotRegexpf(rx interface{}, str interface{}, msg string, args ...interface{}) bool
```

NotRegexpf asserts that a specified regexp does not match a string.

	a.NotRegexpf(regexp.MustCompile("starts"), "it's starting", "error message %s", "formatted")
	a.NotRegexpf("^start", "it's not starting", "error message %s", "formatted")

## NotSame

```go
func (a *Assertions) NotSame(expected interface{}, actual interface{}, msgAndArgs ...interface{}) bool
```

NotSame asserts that two pointers do not reference the same object.

	a.NotSame(ptr1, ptr2)

Both arguments must be pointer variables. Pointer variable sameness is determined based on the equality of both type and value.

## NotSamef

```go
func (a *Assertions) NotSamef(expected interface{}, actual interface{}, msg string, args ...interface{}) bool
```

NotSamef asserts that two pointers do not reference the same object.

	a.NotSamef(ptr1, ptr2, "error message %s", "formatted")

Both arguments must be pointer variables. Pointer variable sameness is determined based on the equality of both type and value.

## NotSubset

```go
func (a *Assertions) NotSubset(list interface{}, subset interface{}, msgAndArgs ...interface{}) bool
```

NotSubset asserts that the list (array, slice, or map) does NOT contain all elements given in the subset (array, slice, or map). Map elements are key-value pairs unless compared with an array or slice where only the map key is evaluated.

	a.NotSubset([1, 3, 4], [1, 2])
	a.NotSubset({"x": 1, "y": 2}, {"z": 3})
	a.NotSubset([1, 3, 4], {1: "one", 2: "two"})
	a.NotSubset({"x": 1, "y": 2}, ["z"])

## NotSubsetf

```go
func (a *Assertions) NotSubsetf(list interface{}, subset interface{}, msg string, args ...interface{}) bool
```

NotSubsetf asserts that the list (array, slice, or map) does NOT contain all elements given in the subset (array, slice, or map). Map elements are key-value pairs unless compared with an array or slice where only the map key is evaluated.

	a.NotSubsetf([1, 3, 4], [1, 2], "error message %s", "formatted")
	a.NotSubsetf({"x": 1, "y": 2}, {"z": 3}, "error message %s", "formatted")
	a.NotSubsetf([1, 3, 4], {1: "one", 2: "two"}, "error message %s", "formatted")
	a.NotSubsetf({"x": 1, "y": 2}, ["z"], "error message %s", "formatted")

## NotZero

```go
func (a *Assertions) NotZero(i interface{}, msgAndArgs ...interface{}) bool
```

NotZero asserts that i is not the zero value for its type.

## NotZerof

```go
func (a *Assertions) NotZerof(i interface{}, msg string, args ...interface{}) bool
```

NotZerof asserts that i is not the zero value for its type.

## Panics

```go
func (a *Assertions) Panics(f PanicTestFunc, msgAndArgs ...interface{}) bool
```

Panics asserts that the code inside the specified PanicTestFunc panics.

	a.Panics(func(){ GoCrazy() })

## PanicsWithError

```go
func (a *Assertions) PanicsWithError(errString string, f PanicTestFunc, msgAndArgs ...interface{}) bool
```

PanicsWithError asserts that the code inside the specified PanicTestFunc panics, and that the recovered panic value is an error that satisfies the EqualError comparison.

	a.PanicsWithError("crazy error", func(){ GoCrazy() })

## PanicsWithErrorf

```go
func (a *Assertions) PanicsWithErrorf(errString string, f PanicTestFunc, msg string, args ...interface{}) bool
```

PanicsWithErrorf asserts that the code inside the specified PanicTestFunc panics, and that the recovered panic value is an error that satisfies the EqualError comparison.

	a.PanicsWithErrorf("crazy error", func(){ GoCrazy() }, "error message %s", "formatted")

## PanicsWithValue

```go
func (a *Assertions) PanicsWithValue(expected interface{}, f PanicTestFunc, msgAndArgs ...interface{}) bool
```

PanicsWithValue asserts that the code inside the specified PanicTestFunc panics, and that the recovered panic value equals the expected panic value.

	a.PanicsWithValue("crazy error", func(){ GoCrazy() })

## PanicsWithValuef

```go
func (a *Assertions) PanicsWithValuef(expected interface{}, f PanicTestFunc, msg string, args ...interface{}) bool
```

PanicsWithValuef asserts that the code inside the specified PanicTestFunc panics, and that the recovered panic value equals the expected panic value.

	a.PanicsWithValuef("crazy error", func(){ GoCrazy() }, "error message %s", "formatted")

## Panicsf

```go
func (a *Assertions) Panicsf(f PanicTestFunc, msg string, args ...interface{}) bool
```

Panicsf asserts that the code inside the specified PanicTestFunc panics.

	a.Panicsf(func(){ GoCrazy() }, "error message %s", "formatted")

## Positive

```go
func (a *Assertions) Positive(e interface{}, msgAndArgs ...interface{}) bool
```

Positive asserts that the specified element is positive

	a.Positive(1)
	a.Positive(1.23)

## Positivef

```go
func (a *Assertions) Positivef(e interface{}, msg string, args ...interface{}) bool
```

Positivef asserts that the specified element is positive

	a.Positivef(1, "error message %s", "formatted")
	a.Positivef(1.23, "error message %s", "formatted")

## Regexp

```go
func (a *Assertions) Regexp(rx interface{}, str interface{}, msgAndArgs ...interface{}) bool
```

Regexp asserts that a specified regexp matches a string.

	a.Regexp(regexp.MustCompile("start"), "it's starting")
	a.Regexp("start...$", "it's not starting")

## Regexpf

```go
func (a *Assertions) Regexpf(rx interface{}, str interface{}, msg string, args ...interface{}) bool
```

Regexpf asserts that a specified regexp matches a string.

	a.Regexpf(regexp.MustCompile("start"), "it's starting", "error message %s", "formatted")
	a.Regexpf("start...$", "it's not starting", "error message %s", "formatted")

## Same

```go
func (a *Assertions) Same(expected interface{}, actual interface{}, msgAndArgs ...interface{}) bool
```

Same asserts that two pointers reference the same object.

	a.Same(ptr1, ptr2)

Both arguments must be pointer variables. Pointer variable sameness is determined based on the equality of both type and value.

## Samef

```go
func (a *Assertions) Samef(expected interface{}, actual interface{}, msg string, args ...interface{}) bool
```

Samef asserts that two pointers reference the same object.

	a.Samef(ptr1, ptr2, "error message %s", "formatted")

Both arguments must be pointer variables. Pointer variable sameness is determined based on the equality of both type and value.

## Subset

```go
func (a *Assertions) Subset(list interface{}, subset interface{}, msgAndArgs ...interface{}) bool
```

Subset asserts that the list (array, slice, or map) contains all elements given in the subset (array, slice, or map). Map elements are key-value pairs unless compared with an array or slice where only the map key is evaluated.

	a.Subset([1, 2, 3], [1, 2])
	a.Subset({"x": 1, "y": 2}, {"x": 1})
	a.Subset([1, 2, 3], {1: "one", 2: "two"})
	a.Subset({"x": 1, "y": 2}, ["x"])

## Subsetf

```go
func (a *Assertions) Subsetf(list interface{}, subset interface{}, msg string, args ...interface{}) bool
```

Subsetf asserts that the list (array, slice, or map) contains all elements given in the subset (array, slice, or map). Map elements are key-value pairs unless compared with an array or slice where only the map key is evaluated.

	a.Subsetf([1, 2, 3], [1, 2], "error message %s", "formatted")
	a.Subsetf({"x": 1, "y": 2}, {"x": 1}, "error message %s", "formatted")
	a.Subsetf([1, 2, 3], {1: "one", 2: "two"}, "error message %s", "formatted")
	a.Subsetf({"x": 1, "y": 2}, ["x"], "error message %s", "formatted")

## True

```go
func (a *Assertions) True(value bool, msgAndArgs ...interface{}) bool
```

True asserts that the specified value is true.

	a.True(myBool)

## Truef

```go
func (a *Assertions) Truef(value bool, msg string, args ...interface{}) bool
```

Truef asserts that the specified value is true.

	a.Truef(myBool, "error message %s", "formatted")

## WithinDuration

```go
func (a *Assertions) WithinDuration(expected time.Time, actual time.Time, delta time.Duration, msgAndArgs ...interface{}) bool
```

WithinDuration asserts that the two times are within duration delta of each other.

	a.WithinDuration(time.Now(), time.Now(), 10*time.Second)

## WithinDurationf

```go
func (a *Assertions) WithinDurationf(expected time.Time, actual time.Time, delta time.Duration, msg string, args ...interface{}) bool
```

WithinDurationf asserts that the two times are within duration delta of each other.

	a.WithinDurationf(time.Now(), time.Now(), 10*time.Second, "error message %s", "formatted")

## WithinRange

```go
func (a *Assertions) WithinRange(actual time.Time, start time.Time, end time.Time, msgAndArgs ...interface{}) bool
```

WithinRange asserts that a time is within a time range (inclusive).

	a.WithinRange(time.Now(), time.Now().Add(-time.Second), time.Now().Add(time.Second))

## WithinRangef

```go
func (a *Assertions) WithinRangef(actual time.Time, start time.Time, end time.Time, msg string, args ...interface{}) bool
```

WithinRangef asserts that a time is within a time range (inclusive).

	a.WithinRangef(time.Now(), time.Now().Add(-time.Second), time.Now().Add(time.Second), "error message %s", "formatted")

## YAMLEq

```go
func (a *Assertions) YAMLEq(expected string, actual string, msgAndArgs ...interface{}) bool
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
func (a *Assertions) YAMLEqf(expected string, actual string, msg string, args ...interface{}) bool
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
func (a *Assertions) Zero(i interface{}, msgAndArgs ...interface{}) bool
```

Zero asserts that i is the zero value for its type.

## Zerof

```go
func (a *Assertions) Zerof(i interface{}, msg string, args ...interface{}) bool
```

Zerof asserts that i is the zero value for its type.

## BoolAssertionFunc

```go
type BoolAssertionFunc = func(TestingT, bool, ...interface{}) bool
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

## CollectT

```go
type CollectT struct {
	// contains filtered or unexported fields
}
```

CollectT implements the TestingT interface and collects all errors.

## Copy

```go
func (*CollectT) Copy(TestingT)
```

Deprecated: That was a method for internal usage that should not have been published. Now just panics.

## Errorf

```go
func (c *CollectT) Errorf(format string, args ...interface{})
```

Errorf collects the error.

## FailNow

```go
func (c *CollectT) FailNow()
```

FailNow stops execution by calling runtime.Goexit.

## Helper

```go
func (CollectT) Helper()
```

Helper is like [testing.T.Helper](https://pkg.go.dev/testing#T.Helper) but does nothing.

## Reset

```go
func (*CollectT) Reset()
```

Deprecated: That was a method for internal usage that should not have been published. Now just panics.

## CompareType

```go
type CompareType = compareResult
```

Deprecated: CompareType has only ever been for internal use and has accidentally been published since v1.6.0. Do not use it.

## Comparison

```go
type Comparison func() (success bool)
```

Comparison is a custom function that returns true on success and false on failure

## ComparisonAssertionFunc

```go
type ComparisonAssertionFunc = func(TestingT, interface{}, interface{}, ...interface{}) bool
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
type ErrorAssertionFunc = func(TestingT, error, ...interface{}) bool
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

## PanicAssertionFunc

```go
type PanicAssertionFunc = func(t TestingT, f PanicTestFunc, msgAndArgs ...interface{}) bool
```

PanicAssertionFunc is a common function prototype when validating a panic value.  Can be useful for table driven tests.

### Example: PanicAssertionFunc

```go
{
	t := &testing.T{}

	tests := []struct {
		name      string
		panicFn   PanicTestFunc
		assertion PanicAssertionFunc
	}{
		{"with panic", func() { panic(nil) }, Panics},
		{"without panic", func() {}, NotPanics},
	}

	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			tt.assertion(t, tt.panicFn)
		})
	}
}
```

## PanicTestFunc

```go
type PanicTestFunc func()
```

PanicTestFunc defines a func that should be passed to the assert.Panics and assert.NotPanics methods, and represents a simple func that takes no arguments, and returns nothing.

## TestingT

```go
type TestingT interface {
	Errorf(format string, args ...interface{})
}
```

TestingT is an interface wrapper around \*testing.T

- `Errorf: func(format string, args ...interface{})`: 

## ValueAssertionFunc

```go
type ValueAssertionFunc = func(TestingT, interface{}, ...interface{}) bool
```

ValueAssertionFunc is a common function prototype when validating a single value.  Can be useful for table driven tests.

### Example: ValueAssertionFunc

```go
{
	t := &testing.T{}

	dumbParse := func(input string) interface{} {
		var x interface{}
		_ = json.Unmarshal([]byte(input), &x)
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
