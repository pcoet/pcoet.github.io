# Go quickstart

This tutorial shows you how to set up a basic Go project that includes a command
line application, a library, and a unit test.

To complete this tutorial, you need to have Go installed. To install Go, follow
the instructions at the [Go installation page](https://go.dev/doc/install).

## Create a Go module

Make a directory for your Go project and change into the directory:

    mkdir myproj && cd myproj

Initialize a Go module:

    go mod init myproj

You should see a new `go.mod` file. The content should look something like this:

```
module myproj

go 1.23.4
```

The `go.mod` file defines your module and helps you manage dependencies. The
module you just created is named `myproj`. In production code, you'd probably
want to use a repository location (e.g. `github.com/myuser/myproj`) as the name
for the module, so that other modules can use yours. To learn more, see
[Managing dependencies](https://go.dev/doc/modules/managing-dependencies).

## Create a library

Make a `pkg/utils` directory path:

    mkdir -p pkg/utils

Create a Go source file, `multiplier.go`, in the new directory path:

    touch pkg/utils/multiplier.go

Add the following content to the file:

```go
package utils

func Multiplier(m float64) func(float64) float64 {
	return func(n float64) float64 {
		return m * n
	}
}
```

The package name, `utils`, identifies the Go package. You'll use this name to
import the library. `Multiplier` is a higher-order function that returns
another function. The function begins with an uppercase letter (`M`), indicating
that it's part of the public API and can be imported by other Go files.

## Create a test

In the same directory (`pkg/utils`), create a test file:

    touch pkg/utils/multiplier_test.go

Add the following content to the test file:

```go
package utils

import (
	"testing"
)

func TestMultiplier(t *testing.T) {
	double := Multiplier(2)
	want := 20.0
	got := double(10)

	if got != want {
		t.Errorf("got %v; want %v", got, want)
	}
}
```

The `TestMultiplier` function uses the Go `testing` library to perform a simple
test of `Multiplier`. Run the test:

    go test ./pkg/...

You should see output like this:

    ok  	myproj/pkg/utils	0.250s

The `ok` indicates that the test completed successfully.

## Create an app

Make a directory path for your Go application:

    mkdir -p cmd/app

Create a `main.go` file:

    touch cmd/app/main.go

Add the following content to `main.go`:

```go
package main

import (
	"fmt"

	"myproj/pkg/utils"
)

func main() {
	double := utils.Multiplier(2)
	fmt.Println(double(2))
}
```

Here you're creating a `main` package that imports your `utils` library, and a
`main` function that uses `utils.Multiplier`.

Run the application:

    go run cmd/app/main.go

The `main` function is automaticaly invoked when you run the `main` package. The
output should be `4`.

You can also install the app and run it:

    go install myproj/cmd/app && ~/go/bin/app

And that's it! You now have a minimal Go project ready for development.

## Learn more

To learn more about setting up a Go project, see the following resources:

* [Tutorial: Get started with Go](https://go.dev/doc/tutorial/getting-started)
* [Tutorial: Create a Go module](https://go.dev/doc/tutorial/create-module)
* [Standard Go Project Layout](https://github.com/golang-standards/project-layout)
