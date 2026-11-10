# http

Deprecated: Use [net/http/httptest](https://pkg.go.dev/net/http/httptest) instead.

## TestResponseWriter

```go
type TestResponseWriter struct {

	// StatusCode is the last int written by the call to WriteHeader(int)
	StatusCode int

	// Output is a string containing the written bytes using the Write([]byte) func.
	Output string
	// contains filtered or unexported fields
}
```

Deprecated: Use [net/http/httptest](https://pkg.go.dev/net/http/httptest) instead.

- `StatusCode: int`: StatusCode is the last int written by the call to WriteHeader(int)
- `Output: string`: Output is a string containing the written bytes using the Write(\[]byte) func.

## Header

```go
func (rw *TestResponseWriter) Header() http.Header
```

Deprecated: Use [net/http/httptest](https://pkg.go.dev/net/http/httptest) instead.

## Write

```go
func (rw *TestResponseWriter) Write(bytes []byte) (int, error)
```

Deprecated: Use [net/http/httptest](https://pkg.go.dev/net/http/httptest) instead.

## WriteHeader

```go
func (rw *TestResponseWriter) WriteHeader(i int)
```

Deprecated: Use [net/http/httptest](https://pkg.go.dev/net/http/httptest) instead.

## TestRoundTripper

```go
type TestRoundTripper struct {
	mock.Mock
}
```

Deprecated: Use [net/http/httptest](https://pkg.go.dev/net/http/httptest) instead.

- `mock.Mock: mock.Mock`: 

## RoundTrip

```go
func (t *TestRoundTripper) RoundTrip(req *http.Request) (*http.Response, error)
```

Deprecated: Use [net/http/httptest](https://pkg.go.dev/net/http/httptest) instead.
