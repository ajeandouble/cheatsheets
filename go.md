# Golang

# Resources

[Go for C++ Developpers - Presentation by Francescc Campoy](https://go.dev/talks/2015/go4cpp.slide#1)

[Go By Example](https://gobyexample.com)

[Concurrency and Channels in Go - Medium](https://medium.com/trendyol-tech/concurrency-and-channels-in-go-bbc4dea75286)


# History

Invented in 2007 in Particula by ***Ken Thompson***

# Characteristics

### Why go?

Go was created for:
- Scalability
- Concurrency
- Simplicity

# Notes

## Go vs C++

- Declared variables are initialized at the 0 of their type
-

## Slices and Arrays

>Go’s arrays are values. An array variable denotes the entire array; it is not a pointer to the first array element (as would be the case in C). This means that when you assign or pass around an array value you will make a copy of its contents. (To avoid the copy you could pass a pointer to the array, but then that’s a pointer to an array, not an array.) One way to think about arrays is as a sort of struct but with indexed rather than named fields: a fixed-size composite value.

[Slice Intro - Go Documentation](https://go.dev/blog/slices-intro)

[Go - Stack or Heap ?](https://medium.com/@yulang.chu/go-stack-or-heap-2-slices-which-keep-in-stack-have-limitation-of-size-b3f3adfd6190)

### Declaring Arrays and Slices

```go
var b[]string
b[0] = "Penn"
b[1] = "Teller"

b := [2]string
b := [2]string{"Penn", "Teller"}
b := [...]string{"Penn", "Teller"} // Make go count the array size for you

```

> We can modify the data of the slice in the literal function, however if the pointer to the data changes for any reason or the slice metadata is modified, the change can be partially or no visible at all to the outside function.

```go
	slice := string{"a", "b"}
	func(slice []string) {
		slice[0] = "Z"
		slice[1] = "Z"
		slice = append(slice, "a")
	}(slice)
	fmt.Print
```

## Pointers

>Go performs pointer escape analysis. If the pointer escapes the local stack, which it does in this case, the object is allocated on the heap. If it doesn't escape the local function, the compiler is free to allocate it on the stack (although it makes no guarantees; it depends on whether the pointer escape analysis can prove that the pointer stays local to this function).

[Return pointer local Structure - stackoverflow](https://stackoverflow.com/a/13715281)

## Structures

### Tags

[Tags - go.dev](https://go.dev/ref/spec#Tag)

## Concurency

>
In computer science, concurrency is the ability of different parts or units of a program, algorithm, or problem to be executed out-of-order or in partial order, without affecting the final outcome. (Wikipedia)

[Concurrency - Wikipedia](https://en.wikipedia.org/wiki/Concurrency_(computer_science))

>**Concurrency** is a way of composing independent tasks.
>Parallelism: is actually running multiple independent tasks at the same time.

>**Parallelism** is not the goal of concurency. Concurency goal is a good structure.

[Concurrency is not Parallelism - Rob Pike](https://www.youtube.com/watch?v=oV9rvDllKEg)

[Communicating Sequential Processes](https://www.cs.cmu.edu/~crary/819-f09/Hoare78.pdf)

### Channels

>The primitive we have for communication is channel. Channels are conduits through which data is passed using channel operator(<-). Channels can be used as shown in the block below:

```go
ch := make(chan int)/// channels must be typed
ch<-1 /// send value to channel
var a int
a<-ch ///get value from channel
///the arrow indicates the direction of data flow
```

>By default, reads and writes to channel block. i.e., if we try to read from a channel, we block till there is some value to read in it. Likewise write blocks till the receiver is ready.(Though we can overcome this by having buffered channels).Thus, channels provide a way to both communicate and synchronize.

[Go Concurrency - A Primer - Medium](https://medium.com/codezillas/go-concurrency-a-primer-de4e8eefd16e)

#### Select

```go
func main() {
 ch1 := make(chan int)
 ch2 := make(chan string)
 go foo(ch1)
 go bar(ch2)
 for i := 0; i < 5; i++ {
  select {
  case v1 := <-ch1:
   fmt.Printf("Channel 1 sent me %d\n", v1)
  case v2 := <-ch2:
   fmt.Printf("Channel 2 send me %s\n", v2)
  }
 }
 fmt.Println("Exiting main\n")
}
func foo(ch chan int) {
 for i := 0; ; i++ {
  ch <- i
  time.Sleep(time.Second * 3)
 }
}
func bar(ch chan string) {
 for i := 0; ; i++ {
  ch <- "Cheers!"
  time.Sleep(time.Second * 2)
 }
}
```

### Wait Groups

```go
func worker(id int) {
	fmt.Printf("Worker %d starting\n", id)

	time.Sleep(time.Second)
	fmt.Printf("Worker %d done\n", id)
}

func main() {

	var wg sync.WaitGroup

	for i := 1; i <= 5; i++ {
		wg.Add(1)

		i := i

		go func() {
			defer wg.Done()
			worker(i)
		}()
	}

	wg.Wait()
}
```

#### Atomic Operations

**Concurrent** execution can lead to race conditions. Even on a granular CPU instruction scale.


#### Interfaces

[Interfaces - Russ Cox](https://research.swtch.com/interfaces)

[How to use Intefaces in Go - Jordan Orelli](https://jordanorelli.com/post/32665860244/how-to-use-interfaces-in-go)

#### Misc

[Goroutines - Threads and Threads IDs](https://dunglas.dev/2022/05/goroutines-threads-and-thread-ids/)

## RAII

>**Resource Acquisition Is Initializaiton**

[What is meant by RAII - Stack Overflow](https://stackoverflow.com/questions/2321511/what-is-meant-by-resource-acquisition-is-initialization-raii)

## Standard Library

### Built-in

>Package builtin provides **only** documentation for Go's predeclared identifiers.

**In go true and false are predeclared untyped constants**

```go
const (
	true  = 0 == 0 // Untyped bool.
	false = 0 != 0 // Untyped bool.
)
```
### Iota

>**iota** is not a user-defined predeclared identifier that auto-increments and can only be used inside a const declaration scope.

```go
	const (
		a = iota	// 0
		b           // 1
		c           // 2
	)

	const (
		a = -1      // -1
		b = iota    // 1
		c           // 2
	)
```

[Ultimate Visual Guide to Go Enums and iota](https://blog.learngoprogramming.com/golang-const-type-enums-iota-bc4befd096d3)

## REST APIs

### Middleware

#### Logging Middleware


### Channels

[Principles of designing go APIs with channels](https://inconshreveable.com/07-08-2014/principles-of-designing-go-apis-with-channels/)

### JSON

[JSON Unmarshall vs JSON Decode - Stack Overflow](https://stackoverflow.com/a/21198571)

## Software Architecture

[RESTful API Folder Structure in Golang - youtube](https://www.youtube.com/watch?v=riR7fMkQvCM)

[How To Structure Your Go App - youtube](https://www.youtube.com/watch?v=MpFog2kZsHk)

# To sort

[When to use Pointers in GO](https://medium.com/@meeusdylan/when-to-use-pointers-in-go-44c15fe04eac)

[Make a debugger in golang - Medium](https://medium.com/golangspec/making-debugger-for-golang-part-i-53124284b7c8)

[Go - JSON Default values](https://www.orsolabs.com/post/go-json-default-values/)

[A complete Guide to JSON in Golang](https://www.sohamkamani.com/golang/json/)

Stringy?
https://go.dev/blog/slices-intro

https://pkg.go.dev/reflect


https://go.dev/doc/tutorial/generics
https://www.digitalocean.com/community/tutorials/how-to-use-generics-in-go

https://research.swtch.com/interfaces

