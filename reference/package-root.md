# github.com/stretchr/testify

Module testify is a set of packages that provide many tools for testifying that your code will behave as you intend.

Testify contains the following packages:

The [github.com/stretchr/testify/assert](https://pkg.go.dev/github.com/stretchr/testify/assert) package provides a comprehensive set of assertion functions that tie in to [the Go testing system](https://go.dev/doc/code#Testing). The [github.com/stretchr/testify/require](https://pkg.go.dev/github.com/stretchr/testify/require) package provides the same assertions but as fatal checks.

The [github.com/stretchr/testify/mock](https://pkg.go.dev/github.com/stretchr/testify/mock) package provides a system by which it is possible to mock your objects and verify calls are happening as expected.

The [github.com/stretchr/testify/suite](https://pkg.go.dev/github.com/stretchr/testify/suite) package provides a basic structure for using structs as testing suites, and methods on those structs as tests.  It includes setup/teardown functionality in the way of interfaces.

A [golangci-lint](https://golangci-lint.run/) compatible linter for testify is available called [testifylint](https://github.com/Antonboom/testifylint).
