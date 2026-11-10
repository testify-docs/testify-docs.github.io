# mock

Package mock provides a system by which it is possible to mock your objects and verify calls are happening as expected.

### Example Usage

The mock package provides an object, Mock, that tracks activity on another object.  It is usually embedded into a test object as shown below:

	type MyTestObject struct {
	  // add a Mock object instance
	  mock.Mock

	  // other fields go here as normal
	}

When implementing the methods of an interface, you wire your functions up to call the Mock.Called(args...) method, and return the appropriate values.

For example, to mock a method that saves the name and age of a person and returns the year of their birth or an error, you might write this:

	func (o *MyTestObject) SavePersonDetails(firstname, lastname string, age int) (int, error) {
	  args := o.Called(firstname, lastname, age)
	  return args.Int(0), args.Error(1)
	}

The Int, Error and Bool methods are examples of strongly typed getters that take the argument index position. Given this argument list:

	(12, true, "Something")

You could read them out strongly typed like this:

	args.Int(0)
	args.Bool(1)
	args.String(2)

For objects of your own type, use the generic Arguments.Get(index) method and make a type assertion:

	return args.Get(0).(*MyObject), args.Get(1).(*AnotherObjectOfMine)

This may cause a panic if the object you are getting is nil (the type assertion will fail), in those cases you should check for nil first.

## Anything

```go
const (
	// Anything is used in Diff and Assert when the argument being tested
	// shouldn't be taken into consideration.
	Anything = "mock.Anything"
)
```

## AnythingOfType

```go
func AnythingOfType(t string) AnythingOfTypeArgument
```

AnythingOfType returns a special value containing the name of the type to check for. The type name will be matched against the type name returned by [reflect.Type.String](https://pkg.go.dev/reflect#Type.String).

Used in Diff and Assert.

For example:

	args.Assert(t, AnythingOfType("string"), AnythingOfType("int"))

## AssertExpectationsForObjects

```go
func AssertExpectationsForObjects(t TestingT, testObjects ...interface{}) bool
```

AssertExpectationsForObjects asserts that everything specified with [Mock.On](#method-Mock-On) of the specified objects was in fact called as expected.

Calls may have occurred in any order.

## FunctionalOptions

```go
func FunctionalOptions(values ...interface{}) *FunctionalOptionsArgument
```

FunctionalOptions returns an [FunctionalOptionsArgument](#type-FunctionalOptionsArgument) object containing the expected functional-options to check for.

For example:

	args.Assert(t, FunctionalOptions(foo.Opt1("strValue"), foo.Opt2(613)))

## InOrder

```go
func InOrder(calls ...*Call)
```

InOrder defines the order in which the calls should be made

	For example:

	InOrder(
		Mock.On("init").Return(nil),
		Mock.On("Do").Return(nil),
	)

## IsType

```go
func IsType(t interface{}) *IsTypeArgument
```

IsType returns an IsTypeArgument object containing the type to check for. You can provide a zero-value of the type to check.  This is an alternative to [AnythingOfType](#func-AnythingOfType).  Used in [Arguments.Diff](#method-Arguments-Diff) and [Arguments.Assert](#method-Arguments-Assert).

For example:

	args.Assert(t, IsType(""), IsType(0))

Mock cannot match interface types because the contained type will be  passed to both IsType and Mock.Called, for the zero value of all interfaces this will be \<nil> type.

## MatchedBy

```go
func MatchedBy(fn interface{}) argumentMatcher
```

MatchedBy can be used to match a mock call based on only certain properties from a complex struct or some calculation. It takes a function that will be evaluated with the called argument and will return true when there's a match and false otherwise.

Example:

	m.On("Do", MatchedBy(func(req *http.Request) bool { return req.Host == "example.com" }))

fn must be a function accepting a single argument (of the expected type) which returns a bool. If fn doesn't match the required signature, MatchedBy() panics.

## AnythingOfTypeArgument

```go
type AnythingOfTypeArgument = anythingOfTypeArgument
```

AnythingOfTypeArgument contains the type of an argument for use when type checking.  Used in [Arguments.Diff](#method-Arguments-Diff) and [Arguments.Assert](#method-Arguments-Assert).

Deprecated: this is an implementation detail that must not be used. Use the [AnythingOfType](#func-AnythingOfType) constructor instead, example:

	m.On("Do", mock.AnythingOfType("string"))

All explicit type declarations can be replaced with interface{} as is expected by [Mock.On](#method-Mock-On), example:

	func anyString interface{} {
		return mock.AnythingOfType("string")
	}

## Arguments

```go
type Arguments []interface{}
```

Arguments holds an array of method arguments or return values.

## Assert

```go
func (args Arguments) Assert(t TestingT, objects ...interface{}) bool
```

Assert compares the arguments with the specified objects and fails if they do not exactly match.

## Bool

```go
func (args Arguments) Bool(index int) bool
```

Bool gets the argument at the specified index. Panics if there is no argument, or if the argument is of the wrong type.

## Diff

```go
func (args Arguments) Diff(objects []interface{}) (string, int)
```

Diff gets a string describing the differences between the arguments and the specified objects.

Returns the diff string and number of differences found.

## Error

```go
func (args Arguments) Error(index int) error
```

Error gets the argument at the specified index. Panics if there is no argument, or if the argument is of the wrong type.

## Get

```go
func (args Arguments) Get(index int) interface{}
```

Get Returns the argument at the specified index.

## Int

```go
func (args Arguments) Int(index int) int
```

Int gets the argument at the specified index. Panics if there is no argument, or if the argument is of the wrong type.

## Is

```go
func (args Arguments) Is(objects ...interface{}) bool
```

Is gets whether the objects match the arguments specified.

## String

```go
func (args Arguments) String(indexOrNil ...int) string
```

String gets the argument at the specified index. Panics if there is no argument, or if the argument is of the wrong type.

If no index is provided, String() returns a complete string representation of the arguments.

## Call

```go
type Call struct {
	Parent *Mock

	// The name of the method that was or will be called.
	Method string

	// Holds the arguments of the method.
	Arguments Arguments

	// Holds the arguments that should be returned when
	// this method is called.
	ReturnArguments Arguments

	// The number of times to return the return arguments when setting
	// expectations. 0 means to always return the value.
	Repeatability int

	// Holds a channel that will be used to block the Return until it either
	// receives a message or is closed. nil means it returns immediately.
	WaitFor <-chan time.Time

	// Holds a handler used to manipulate arguments content that are passed by
	// reference. It's useful when mocking methods such as unmarshalers or
	// decoders.
	RunFn func(Arguments)

	// PanicMsg holds msg to be used to mock panic on the function call
	//  if the PanicMsg is set to a non nil string the function call will panic
	// irrespective of other settings
	PanicMsg *string
	// contains filtered or unexported fields
}
```

Call represents a method call and is used for setting expectations, as well as recording activity.

- `Parent: *Mock`: 
- `Method: string`: The name of the method that was or will be called.
- `Arguments: Arguments`: Holds the arguments of the method.
- `ReturnArguments: Arguments`: Holds the arguments that should be returned when this method is called.
- `Repeatability: int`: The number of times to return the return arguments when setting expectations. 0 means to always return the value.
- `WaitFor: <-chan time.Time`: Holds a channel that will be used to block the Return until it either receives a message or is closed. nil means it returns immediately.
- `RunFn: func(Arguments)`: Holds a handler used to manipulate arguments content that are passed by reference. It's useful when mocking methods such as unmarshalers or decoders.
- `PanicMsg: *string`: PanicMsg holds msg to be used to mock panic on the function call

	if the PanicMsg is set to a non nil string the function call will panic

irrespective of other settings

## After

```go
func (c *Call) After(d time.Duration) *Call
```

After sets how long to block until the call returns

	Mock.On("MyMethod", arg1, arg2).After(time.Second)

## Maybe

```go
func (c *Call) Maybe() *Call
```

Maybe allows the method call to be optional. Not calling an optional method will not cause an error while asserting expectations

## NotBefore

```go
func (c *Call) NotBefore(calls ...*Call) *Call
```

NotBefore indicates that the mock should only be called after the referenced calls have been called as expected. The referenced calls may be from the same mock instance and/or other mock instances.

	Mock.On("Do").Return(nil).NotBefore(
	    Mock.On("Init").Return(nil)
	)

## On

```go
func (c *Call) On(methodName string, arguments ...interface{}) *Call
```

On chains a new expectation description onto the mocked interface. This allows syntax like.

	Mock.
	   On("MyMethod", 1).Return(nil).
	   On("MyOtherMethod", 'a', 'b', 'c').Return(errors.New("Some Error"))

## Once

```go
func (c *Call) Once() *Call
```

Once indicates that the mock should only return the value once.

	Mock.On("MyMethod", arg1, arg2).Return(returnArg1, returnArg2).Once()

## Panic

```go
func (c *Call) Panic(msg string) *Call
```

Panic specifies if the function call should fail and the panic message

	Mock.On("DoSomething").Panic("test panic")

## Return

```go
func (c *Call) Return(returnArguments ...interface{}) *Call
```

Return specifies the return arguments for the expectation.

	Mock.On("DoSomething").Return(errors.New("failed"))

## Run

```go
func (c *Call) Run(fn func(args Arguments)) *Call
```

Run sets a handler to be called before returning. It can be used when mocking a method (such as an unmarshaler) that takes a pointer to a struct and sets properties in such struct

	Mock.On("Unmarshal", AnythingOfType("*map[string]interface{}")).Return().Run(func(args Arguments) {
		arg := args.Get(0).(*map[string]interface{})
		arg["foo"] = "bar"
	})

## Times

```go
func (c *Call) Times(i int) *Call
```

Times indicates that the mock should only return the indicated number of times.

	Mock.On("MyMethod", arg1, arg2).Return(returnArg1, returnArg2).Times(5)

## Twice

```go
func (c *Call) Twice() *Call
```

Twice indicates that the mock should only return the value twice.

	Mock.On("MyMethod", arg1, arg2).Return(returnArg1, returnArg2).Twice()

## Unset

```go
func (c *Call) Unset() *Call
```

Unset removes all mock handlers that satisfy the call instance arguments from being called. Only supported on call instances with static input arguments.

For example, the only handler remaining after the following would be "MyMethod(2, 2)":

	Mock.
	   On("MyMethod", 2, 2).Return(0).
	   On("MyMethod", 3, 3).Return(0).
	   On("MyMethod", Anything, Anything).Return(0)
	Mock.On("MyMethod", 3, 3).Unset()

## WaitUntil

```go
func (c *Call) WaitUntil(w <-chan time.Time) *Call
```

WaitUntil sets the channel that will block the mock's return until its closed or a message is received.

	Mock.On("MyMethod", arg1, arg2).WaitUntil(time.After(time.Second))

## FunctionalOptionsArgument

```go
type FunctionalOptionsArgument struct {
	// contains filtered or unexported fields
}
```

FunctionalOptionsArgument contains a list of functional options arguments expected for use when matching a list of arguments.

## String

```go
func (f *FunctionalOptionsArgument) String() string
```

String returns the string representation of FunctionalOptionsArgument

## IsTypeArgument

```go
type IsTypeArgument struct {
	// contains filtered or unexported fields
}
```

IsTypeArgument is a struct that contains the type of an argument for use when type checking.  This is an alternative to [AnythingOfType](#func-AnythingOfType). Used in [Arguments.Diff](#method-Arguments-Diff) and [Arguments.Assert](#method-Arguments-Assert).

## Mock

```go
type Mock struct {
	// Represents the calls that are expected of
	// an object.
	ExpectedCalls []*Call

	// Holds the calls that were made to this mocked object.
	Calls []Call
	// contains filtered or unexported fields
}
```

Mock is the workhorse used to track activity on another object. For an example of its usage, refer to the "Example Usage" section at the top of this document.

- `ExpectedCalls: []*Call`: Represents the calls that are expected of an object.
- `Calls: []Call`: Holds the calls that were made to this mocked object.

## AssertCalled

```go
func (m *Mock) AssertCalled(t TestingT, methodName string, arguments ...interface{}) bool
```

AssertCalled asserts that the method was called. It can produce a false result when an argument is a pointer type and the underlying value changed after calling the mocked method.

## AssertExpectations

```go
func (m *Mock) AssertExpectations(t TestingT) bool
```

AssertExpectations asserts that everything specified with [Mock.On](#method-Mock-On) was in fact called as expected.  Calls may have occurred in any order.

## AssertNotCalled

```go
func (m *Mock) AssertNotCalled(t TestingT, methodName string, arguments ...interface{}) bool
```

AssertNotCalled asserts that the method was not called. It can produce a false result when an argument is a pointer type and the underlying value changed after calling the mocked method.

## AssertNumberOfCalls

```go
func (m *Mock) AssertNumberOfCalls(t TestingT, methodName string, expectedCalls int) bool
```

AssertNumberOfCalls asserts that the method was called expectedCalls times.

## Called

```go
func (m *Mock) Called(arguments ...interface{}) Arguments
```

Called tells the mock object that a method has been called, and gets an array of arguments to return.  Panics if the call is unexpected (i.e. not preceded by appropriate [Mock.On](#method-Mock-On) calls) If Call.WaitFor is set, blocks until the channel is closed or receives a message.

## IsMethodCallable

```go
func (m *Mock) IsMethodCallable(t TestingT, methodName string, arguments ...interface{}) bool
```

IsMethodCallable returns true if given methodName and arguments have an unsatisfied expected call registered in the Mock.

## MethodCalled

```go
func (m *Mock) MethodCalled(methodName string, arguments ...interface{}) Arguments
```

MethodCalled tells the mock object that the given method has been called, and gets an array of arguments to return. Panics if the call is unexpected (i.e. not preceded by appropriate [Mock.On](#method-Mock-On) calls) If Call.WaitFor is set, blocks until the channel is closed or receives a message.

## On

```go
func (m *Mock) On(methodName string, arguments ...interface{}) *Call
```

On starts a description of an expectation of the specified method being called.

	Mock.On("MyMethod", arg1, arg2)

## String

```go
func (m *Mock) String() string
```

String provides a %v format string for Mock. Note: this is used implicitly by Arguments.Diff if a Mock is passed. It exists because go's default %v formatting traverses the struct without acquiring the mutex, which is detected by go test -race.

## Test

```go
func (m *Mock) Test(t TestingT)
```

Test sets the [TestingT](#type-TestingT) on which errors will be reported, otherwise errors will cause a panic. Test should not be called on an object that is going to be used in a goroutine other than the one running the test function.

## TestData

```go
func (m *Mock) TestData() objx.Map
```

TestData holds any data that might be useful for testing.  Testify ignores this data completely allowing you to do whatever you like with it.

## TestingT

```go
type TestingT interface {
	Logf(format string, args ...interface{})
	Errorf(format string, args ...interface{})
	FailNow()
}
```

TestingT is an interface wrapper around \*testing.T

- `Logf: func(format string, args ...interface{})`: 
- `Errorf: func(format string, args ...interface{})`: 
- `FailNow: func()`:
