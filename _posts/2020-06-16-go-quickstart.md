---
title: Set up a Go project
category: Go
---

This post explains how to quickly set up a Go project. Some of the content is adapted from the official documentation on [How to Write Go Code](https://golang.org/doc/code.html). If you're new to Go, that's worth reading.

The steps below assume that you'll host your repo on GitHub.

## Install Go

If you haven't already, [install the Go tools](https://golang.org/doc/install).

## Create a project

If you plan to host your project on GitHub, you probably want to start by creating a Go project there and cloning it. Alternatively, you can create the project root locally, replacing **myproj** with whatever name you want for your project:

    mkdir myproj && cd myproj

Once you've cloned or created the new project, create a new module in the root directory as shown below, replacing **myuser** and **myproj** with your GitHub user and the name of the repo:

    go mod init github.com/myuser/myproj

Go will create a **go.mod** file that declares the module path.

## Create library code

Create a library file (**pkg/myutils/adder.go**) by running the following from the root directory:

    mkdir -p pkg/myutils && touch pkg/myutils/adder.go

Add the following code to **adder.go**:

```go
package myutils

// Adder returns the result of adding two integers.
func Adder(n1 int, n2 int) int {
	return n1 + n2
}
```

## Create and run a test

Create a test file to accompany the library file. In the root directory, run:

    touch pkg/myutils/adder_test.go

Add the following code to **adder_test.go**.

```go
package myutils

import "testing"

func TestAdder(t *testing.T) {
	expected := 4
	actual := Adder(2, 2)

	if actual != expected {
		t.Errorf("actual == %d, expected %d", actual, expected)
	}
}
```

Run the test:

    go test ./pkg/myutils/

To run all the tests, you could use:

    go test ./...

## Create a main package

From the root directory, run: 

    mkdir -p cmd/myapp && touch cmd/myapp/main.go

Open the **main.go** file and add the following code:

```go
package main

import (
	"fmt"

	"github.com/myuser/myproj/pkg/myutils"
)

func main() {
	fmt.Println(myutils.Adder(2, 2))
}
```

## Build and run the app

    go install github.com/myuser/myproj/cmd/myapp
    ~/go/bin/myapp

## Resources

* [Ben Johnson: Structuring Applications in Go](https://medium.com/@benbjohnson/structuring-applications-in-go-3b04be4ff091)
* [Go: Command go](https://golang.org/cmd/go/)
* [Go: How to Write Go Code](https://golang.org/doc/code.html)
* [Go Blog: Using Go Modules](https://blog.golang.org/using-go-modules)
* [RunGo: Everything you need to know about Packages in Go](https://medium.com/rungo/everything-you-need-to-know-about-packages-in-go-b8bac62b74cc)
* [Standard Go Project Layout](https://github.com/golang-standards/project-layout)