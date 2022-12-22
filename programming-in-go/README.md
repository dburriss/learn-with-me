# Learning Go lang

This is a short overview of the building blocks of the Go programming language. It is intended as a short primer for someone experienced with other programming languages, who would like to start writing Go.

- [Learning Go lang](#learning-go-lang)
	- [Language features](#language-features)
	- [Getting started](#getting-started)
	- [Running code](#running-code)
	- [Comments](#comments)
	- [Types](#types)
	- [Assigning a value](#assigning-a-value)
	- [Collections](#collections)
	- [Control flow](#control-flow)
	- [Errors](#errors)
	- [Behavior](#behavior)
	- [Generics](#generics)
	- [Concurrency](#concurrency)
	- [Testing](#testing)
	- [Importing packages](#importing-packages)


## Language features

Go is a multi-paradigm language that is primarily imperative. It supports some OOP features like encapsulation (convention based) but thankfully does not support the more damaging OOP ideas like inheritance. Go strives for simplicity and so lacks some capabilities of other programming languages. It has a strong focus on concurrency, exposing low-level constructs simply, and being performant even though it is garbage collected. 

The type system is statically typed with type inference and structural typing. 

## Getting started

First step is [downloading and installing Go](https://go.dev/dl/).

Next, we need an IDE. Probably the easiest to get started with is using [VS Code](https://code.visualstudio.com/) and the [Go extension](https://code.visualstudio.com/docs/languages/go).

## Running code

First, we need to define a module so we run the command:

```bash
go mod init github.com/dburriss/learn-with-me
```

This creates a _go.mod_ file at the root of our application. 

Let's create a file called *hello.go* to contain our code:

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

Our application is a single module with all our source code in it. A module can have many packages in it. As you can see above, our hello.go code is declared in a package called "main". Package `main` has special meaning in Go as it is used as the entrypoint to an application. The recommended practice is to have other packages contained in a folder with the same package name.

Then we can build and run with the `run` command.

```bash
go run .
```

Read more about [managing dependencies](https://go.dev/doc/modules/managing-dependencies#naming_module).

## Comments

```go
// a single line comment

/*
a multiline package
looks like this
*/
```

Comments can be turned into documentation, so it is common to comment on `package` and `func` declarations. You can [read more here](https://go.dev/doc/comment).

The [godoc](https://pkg.go.dev/golang.org/x/tools/cmd/godoc) tool extracts comments from source code and runs as a server.



## Types

Go has many [Built-in primitive types](https://pkg.go.dev/builtin#pkg-types) such as `bool`, `int32`, and `string`.

You can create your own types.

```go
type World struct {
    name string
    moons int32
}
```

## Assigning a value

As with all languages that use `nil`, you can declare a variable without a value very easily (footgun).

```go
var world string
world = "Earth"
fmt.Printf("Hello, %s!", world)
```

If you have a sensible default, this can be declared in a single line.

```go
var world string = "World"
fmt.Printf("Hello, %s!", world)
```

We can ask the Go compiler to *infer* the type by using the `:=` operator.

```go
world := "World"
fmt.Printf("Hello, %s!", world)
```

As the keyword `var` indicates, the value of the variable can indeed vary.

```go
var world = "World"
world = "Mars"
fmt.Printf("Hello, %s!", world)
```

If you do not want the value to vary, you can declare it as a `const`.

> You can move a `const` up to the package scope.

```go
const world = "World"
world = "Mars" // compiler error: cannot assign to world (constant "World" of type string)
fmt.Printf("Hello, %s!", world)
```

There are multiple ways of declaring more complex types, like using `new(T)`. The way in the code below demonstrates explicitly setting each field.

```go
type World struct {
	name  string
	moons int32
}

func main() {
	var world = World{name: "Earth", moons: 1}
	fmt.Printf("Hello, %s with %d moon(s).", world.name, world.moons)
}
```

The values so far have been value types. Go also allows the use of pointers. To use a pointer you use `*T` when declaring the variable and you need to assign a value at declaration for it to be usable. The pointer variable contains the address where the value is found, rather than the actual value.

The dereference operator `*` is used to access the value the pointer is addressed to.

> Note: Go does not allow pointer arithmetic.

```go
// declare a pointer using *string and the `new` function
var namePtr *string = new(string)
// use deference operator to assign a string value
*namePtr = "Bob"
// use dereference operator to get value the pointer is addressing
name := *namePtr
// print values
fmt.Print(namePtr, " ", name)
// output: <pointer address> Bob
// eg. 0xc000070270 Bob
```

Another operator used with pointers is the *address of* operator `&`. This allows us to get a pointer to the memory address of an existing variable.

```go
name := "Bob"
// use "address of" operator & to get a pointer to an existing variable
address := &name
// print values
fmt.Print(address, " ", name)
// output: <pointer address> Bob
// eg. 0xc000070270 Bob
```

## Collections

An **array** in Go is declared backwards to most other languages, with the syntax `[size]T`. They use a zero-based index and elements are indexed just like in many other languages. The compiler will complain if you try reference an index that is out of bounds.

```go
var intArr [3]int
intArr[0] = 1
intArr[1] = 2
intArr[2] = 3
intArr[3] = 4 // compile error

fmt.Println(intArr[0])
fmt.Println(intArr)
```

It is possible to inline the initialization of the array values.

```go
intArr := [3]int{1, 2, 3}
```

If you need a dynamically sized structure, or a subset of the elements in an array, you can use the **slice** datatype. The slice datatype sits over an array and can point to ranges in it.

```go
intArr := [3]int{1, 2, 3}
slice := intArr[:]
slice[3] = 4 // runtime error: index out of range
fmt.Println(intArr, slice)
```

As you can see from above, using a slice with an existing array does not allow us to extend the array but it does allow us to work with a specific slice of the array without copying the elements to a new array.

```go
intArr := [3]int{1, 2, 3}
slice := intArr[0:1]// a range of index 0 and up to but not including 1
fmt.Println(intArr, slice) // output: [1 2 3] [1]
```

If you do not want to worry about the underlying array, you can declare the slice directly like so. There are functions to use with a `slice` like `append` that allow you to operate on the array (and get a copy back).

```go
var dynamicSlice []int
dynamicSlice = append(dynamicSlice, 1)
fmt.Println(dynamicSlice)
// output: [1]
```

If you need dynamic key value pairs you can use a **map**.

```go
ages := map[string]int{"Bob": 42, "Alice": 31}
ages["Alice"] = 29
delete(ages, "Alice")
fmt.Println(ages)
```

## Control flow

Go has the usual `if-else`, `switch`, and `for` control structures common in most languages.

The `if-else` is pretty standard. The `else` of course is optional.

```go
// create the variable `value` with type `any` which is an alias for `interface{}`
var value any = "Bob"
// to a type test on `value` which returns the instance of the type being tested
// and a boolean of whether successful
str, ok := value.(string)
// check if indeed is a string
if ok {
	fmt.Printf("value is a string: %s\n", str)
} else {
	fmt.Printf("value is not a string\n")
}
```

**Switch** statements are also pretty standard with a nice ability to be able to test both conditions like an `if`, as well as type assertions as seen below.

```go
var value any = "Bob"
switch value.(type) {
case int:
	fmt.Println("value is an int")
case string:
	fmt.Println("value is an string")
default:
	fmt.Println("unknown type")
}
```

> Note: `break` is supported in Go cases.

**For** loops have a few different variations.  
The usual C style `for` loop.

```go
for i := 0; i < 10; i++ {
	fmt.Println(i)
}
```

You can use the `range` clause to loop over `string`, `array`, `slice`, `map`, or `chan`(explained later). This is sometimes known as a foreach in other languages.

```go
arr := [10]int{0, 1, 2, 3, 4, 5, 6, 7, 8, 9}
for el := range arr {
	fmt.Println(el)
}
```

Go does not have a `while` statement but `for` can take a condition which is equivalent.

```go
arr := [10]int{0, 1, 2, 3, 4, 5, 6, 7, 8, 9}
index := 0
for index < 5 {
	fmt.Println(arr[index])
	index++
}
```

> Note: Go does not have an equivalent to `do-while`.

## Errors

Error handling is handled using a feature of the Go programming language, namely **multiple return types**. In the code snippet below you can see how the builtin [os.OpenFile](https://pkg.go.dev/os#OpenFile) has the return type `*File, error`. So it returns a pointer to a `File` and an `error`. It is on the developer to check that no error ocurred. If an error did occur, the developer must decide how to handle this.

In the case below, we just panic if the file does not exist.

```go
fileName := "i-dont-exist.txt"
file, err := os.OpenFile(fileName, os.O_RDONLY, 0644)
if err != nil {
	fmt.Println(err)
}
var text = make([]byte, 1024)
n, err := file.Read(text)
if n > 0 && err == nil {
	println(string(text))
} else {
	println("No content")
}
```

> Note: It is common to reuse the `error` return variable, here labeled as `err`.

## Behavior

Go does not have constructors, so the convention is to create a function called `newT` to construct type `T`. In the example below `newWorld` creates a new instance of `World`.

```go
type World struct {
	name  string
	moons int
}

func newWorld(name string, moons int) World {
	return World{name, moons}
}

func main() {
	world := newWorld("Earth", 1)
	fmt.Println(world)
}
```

Go has first class support for functions. This means functions can be assigned to variables and passed into other functions as arguments.

```go
arr := []int{0, 1, 3, 4}
var odd = func(i int) bool { return i%2 != 0 }
filtered := filter(odd, arr)
fmt.Println("Original", arr)
// output: Original [0 1 3 4]
fmt.Println("Filtered", filtered)
// output: Filtered [1 3]

func filter(predicate func(int) bool, arr []int) []int {
	newArr := []int{}
	n := 0
	for _, x := range arr {
		if predicate(x) {
			newArr = append(newArr, x)
			n++
		}
	}
	return newArr
}
```

We could even create a type for our function signature.

```go
type IntPredicate func(i int) bool
```

Functions can be attached to types as methods by signifying the type to attach to at the start of the signature.

```go
func (world World) IsHospitable() bool {
	return world.name == "Earth"
}

//usage
world := newWorld("Earth", 1)
world.IsHospitable()
```

Now that we understand how to add methods to a type it is a good time to talk about Go interfaces. A type does not explicitly implement an interface in Go. If it implements the members of the interface, then it implicitly implements that type.

As an example, lets look at the [Formatter](https://pkg.go.dev/fmt#Formatter) interface from the standard Go `fmt` package.

```go
type Formatter interface {
	Format(f State, verb rune)
}
```

In the past, when calling `fmt.Println` we got a default printout of a `World` type.

```go
world := newWorld("Earth", 1)
fmt.Println(world)
// output: {Earth 1}
```

If we implement the [Formatter](https://pkg.go.dev/fmt#Formatter) interface we can control the output of the printout. We do this by adding the `Format` method with the exact signature as the interface above.

```go
func (world World) Format(f fmt.State, verb rune) {
	f.Write([]byte(fmt.Sprintf("World{name: %s, moons: %d}", world.name, world.moons)))
}
```

Now when we call `fmt.Println` we get a differently formatted `World` value.

```go
world := newWorld("Earth", 1)
fmt.Println(world)
// output: World{name: Earth, moons: 1}
```

## Generics

Go 1.18 introduced generics as a language feature. As the name suggests, this allows you to write generic functions.

Let's take the `filter` function that was specific to `int` and make it generic. We do this by adding the generic type and its constraint after the function name. In this case we have no constraint on the type `K`.

This `filter` function will continue to work for filtering `int`s for **odd** numbers.

```go
func filter[K any](predicate func(K) bool, arr []K) []K {
	newArr := []K{}
	n := 0
	for _, x := range arr {
		if predicate(x) {
			newArr = append(newArr, x)
			n++
		}
	}
	return newArr
}
```

We can now also use it for other types. In the example below we use it to filter to the names that are less than or equal to 3 characters.

```go
arr := []string{"Bob", "Tracy", "Wu"}
var shortNames = func(x string) bool { return len(x) <= 3 }
filtered := filter(shortNames, arr)
fmt.Println("Original", arr)
// output: [Bob Tracy Wu]
fmt.Println("Filtered", filtered)
// output: [Bob Wu]
```

## Concurrency

One of the core design principles of Go is to have primitives for concurrent programming baked into the language. Let's start with this non-concurrent program that prints out the number of moons for each planet in the Solar system.

```go
func scan(planet string) {
	var printInfo = func(planet string, moons int) {
		fmt.Printf("%s has %d moon(s).\n", planet, moons)
	}
	switch planet {
	case "Mercury":
		printInfo(planet, 0)
	case "Venus":
		printInfo(planet, 0)
	case "Earth":
		printInfo(planet, 1)
	case "Mars":
		printInfo(planet, 2)
	case "Jupiter":
		printInfo(planet, 80)
	case "Saturn":
		printInfo(planet, 83)
	case "Uranus":
		printInfo(planet, 27)
	case "Neptune":
		printInfo(planet, 14)
	default:
		printInfo(fmt.Sprintf("%s is unknown", planet), 0)
	}
}

func main() {
	planets := [8]string{"Mercury", "Venus", "Earth", "Mars", "Saturn", "Jupiter", "Uranus", "Neptune"}
	for _, planet := range planets {
		scan(planet)
	}
}
```

When you run the above program you get the planets printed out in the order they appear in the array (and our solar system).

```
Mercury has 0 moon(s).
Venus has 0 moon(s).
Earth has 1 moon(s).
Mars has 2 moon(s).
Saturn has 83 moon(s).
Jupiter has 80 moon(s).
Uranus has 27 moon(s).
Neptune has 14 moon(s).
```

Now what if we want the scans to happen concurrently? When we run a Go application it is running on something called the main Goroutine. You can think of a Goroutine like a thread but it is super lightweight.

We can then use the `go` keyword to spawn a new Goroutine. This will run each scan of each planet in it's own Goroutine. The only line that changes is the single line within the `for` loop.

```go
go scan(planet)
```

When you run the application now you may notice something weird. Nothing is output to the console. The reason for this is because after spawning the *goroutines*, the main one keeps executing. It reaches the end of the program and then shuts down. Those child *goroutines* never finish executing before the main Goroutine finishes.

We can "fix" this by making the main Goroutine sleep for a bit before exiting.

```go
func main() {
	planets := [8]string{"Mercury", "Venus", "Earth", "Mars", "Saturn", "Jupiter", "Uranus", "Neptune"}
	for _, planet := range planets {
		// use to `go` keyword
		go scan(planet)
	}
	// sleep so all child goroutines finish
	time.Sleep(500 * time.Microsecond)
}
```

By playing with the range of how long the main *goroutine* sleeps for, you can get none, some, or all of the planet info to print out. Try play with ranges from 100 microseconds to 2000 microseconds. On my machine anything over 800 microseconds printed out all planet info.

Let's look at a less hacky way of waiting for all child *goroutines* to finish.
We will make use of a `sync.WaitGroup`. 

Each time we spawn a new Goroutine, we will increment the state of the `WaitGroup` using the `Add` method. Then in each *goroutine*, we pass a reference to the `WaitGroup`. We can then call the `Done()` method on the `WaitGroup` at the end of each `scan`. 

The final step is to use the `Wait` method on the `WaitGroup` instance to wait for all `Done` calls. There is no magic here. `Wait` will just wait until the number accumulated with the `Add` calls equals the number of `Done` calls.

```go
// now scan takes `WaitGroup` reference
func scan(wg *sync.WaitGroup, planet string) {
	var printInfo = func(planet string, moons int) {
		fmt.Printf("%s has %d moon(s).\n", planet, moons)
	}
	switch planet {
	case "Mercury":
		printInfo(planet, 0)
	case "Venus":
		printInfo(planet, 0)
	case "Earth":
		printInfo(planet, 1)
	case "Mars":
		printInfo(planet, 2)
	case "Jupiter":
		printInfo(planet, 80)
	case "Saturn":
		printInfo(planet, 83)
	case "Uranus":
		printInfo(planet, 27)
	case "Neptune":
		printInfo(planet, 14)
	default:
		printInfo(fmt.Sprintf("%s is unknown", planet), 0)
	}
	// added a sleep and call to Done
	time.Sleep(1000 * time.Millisecond)
	wg.Done()
}

func main() {
	planets := [8]string{"Mercury", "Venus", "Earth", "Mars", "Saturn", "Jupiter", "Uranus", "Neptune"}
	var wg sync.WaitGroup
	for _, planet := range planets {
		// increment wg
		wg.Add(1)
		go scan(&wg, planet)
	}
	// wait for all calls to Done
	wg.Wait()
}
```

> Note: I placed a 1 second `Sleep` call in the `scan` function so you can tell that the Goroutines are indeed running concurrently, else it would take over 8 seconds to execute.

The final piece to concurrent programming is **channels**. These are the mechanism that *goroutines* use to communicate with one another. Channels behave a bit like message queues except they block until the other side is ready to send or receive. Like *goroutines* these are built into the language and use the `chan` keyword and make use of the `<-` operator to send and receive messages on the channel.

Below is a simple example of 2 *goroutines* communicating via a channel.

```go
func main() {
	var wg sync.WaitGroup
	// create a channel that sends type `World`
	ch := make(chan World)

	wg.Add(1)
	// async create world and send on channel
	go func() {
		// put the new world instance on channel `ch`
		ch <- newWorld("Earth")
	}()

	// listen on channel
	go func() {
		// will block until a World message is available
		planet := <-ch
		fmt.Println(planet)
		wg.Done()
	}()
	// wait for goroutines to finish
	wg.Wait()
}
```

The first *goroutine* is sending on a channel and another is receiving on that same channel. We still use all the same techniques we learned about previously using `WaitGroup`.

In many programs we will have a dynamic list of goroutines kicking off and we will need to get communication back via a channel. If the application is processing a finite list (ie. not listening indefinitely) we might want to loop over all messages in the channel.

> Important bits are commented.

```go
package main

import (
	"fmt"
	"sync"
	"time"
)

type World struct {
	name    string
	moons   int
	scanned bool
}

func newWorld(name string) World {
	return World{name, 0, false}
}

func scan(ch chan World, wg *sync.WaitGroup, world World) {
	var scanPlanet = func(planet *World, moons int) {
		planet.moons = moons
		planet.scanned = true
	}
	// perform scan of moons
	switch world.name {
	case "Mercury":
		scanPlanet(&world, 0)
	case "Venus":
		scanPlanet(&world, 0)
	case "Earth":
		scanPlanet(&world, 1)
	case "Mars":
		scanPlanet(&world, 2)
	case "Jupiter":
		scanPlanet(&world, 80)
	case "Saturn":
		scanPlanet(&world, 83)
	case "Uranus":
		scanPlanet(&world, 27)
	case "Neptune":
		scanPlanet(&world, 14)
	}
	time.Sleep(1000 * time.Millisecond)
	// send world with updated scan data
	ch <- world
	// notify that work is done
	wg.Done()
}

func printInfo(w World) {
	if w.scanned {
		fmt.Printf("%s has %d moon(s).\n", w.name, w.moons)
	} else {
		fmt.Printf("%s was not scanned.\n", w.name)
	}
}

func main() {

	var wg sync.WaitGroup
	// now we create channel
	ch := make(chan World)

	planets := [8]string{"Mercury", "Venus", "Earth", "Mars", "Saturn", "Jupiter", "Uranus", "Neptune"}
	for _, name := range planets {
		wg.Add(1)
		// pass the channel into the goroutine
		go scan(ch, &wg, newWorld(name))
	}
	// anonymous goroutine that will wait for others to finish and then close the channel
	go func() {
		println("Closing channel connection...") // always prints before planets
		wg.Wait()
		// after all goroutines finished sending on channel, close it
		close(ch)
	}()
	// since closed, has a known number of messages so can iterate over those
	for world := range ch {
		printInfo(world)
	}
}
```

Let's look at the important parts.

At the start we create our `WaitGroup` and `chan World`.

```go
var wg sync.WaitGroup
ch := make(chan World)
```

For each *goroutine* of `scan` that we kick off, we increment the `wg WaitGroup`.

```go
wg.Add(1)
go scan(ch, &wg, newWorld(name))
```

Within the `scan` function that is running as a *goroutine*, we put a message on the channel and then tell the `WaitGroup` the asynchronous work is done.

```go
ch <- world
wg.Done()
```

We start a *goroutine* using an anonymous function to wait for the `WaitGroup` to reach zero and then close the channel.

```go
go func() {
	wg.Wait()
	close(ch)
}()
```

We can now loop over the range of the closed channel and process the messages.

```go
for world := range ch {
	printInfo(world)
}
```

## Testing

Go supports testing out of the box. You can run the following command to learn more about the `test` command. 

```bash
go help test
```
It supports many types of tests like fuzzing and benchmarks. This will only cover code "unit" style tests.

The first thing to know is the Go uses conventions. Tests have to be in a source file with a name ending in suffix `_test` eg. `hello_test.go`.

Tests are normal functions that start with the prefix `Test` eg. `func TestScan(t *testing.T)`. The test function take a type `testing.T` which is used to interact with the test runner.

Below is a simple test that checks whether a constructor function sets the name of the `World` as expected. The Go test tooling does not have native assertions like many other languages so it is up to the developer to assert and then use the `testing.T` instance to interact with the test runner.

```go
package main

import "testing"

func TestNewWorldSetsName(t *testing.T) {
	name := "Earth"

	result := newWorld(name)

	if result.name != name {
		t.Errorf("Expected World to have name %s but instead has %s", name, result.name)
	}
}
```

> Check out [Testing](https://pkg.go.dev/testing) documentation for more types of tests.


## Importing packages

Importing 3rd-party packages is done using the `go get` command.

As an example, [Gin](https://github.com/gin-gonic/gin#installation) is a popular Go Web Framework. Installing that in your environment is done via:

```bash
go get -u github.com/gin-gonic/gin
```

This pulls the package to your local environment, determined by you [GOPATH](https://go.dev/doc/gopath_code#remote).