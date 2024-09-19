---
layout: post

title: Java Coder Attempts GO | Ep1

imgCaption: Where To GO?
videoId: NH4zvUjNExM

date: 2024-09-19 12:00:00 -0400
categories:
- blog
- software
- video
---

I have heard many great things (and some odd things) about Golang, so I had to try it out. This video and post begin my journey to learning GO and hopefully making it my daily driver if I like it.

Before I begin, however, if you want a picture perfect set of tutorials or tips and tricks on GO, let me save you time. "GO" Check out these guys instead!
- [Melkey](https://www.youtube.com/@MelkeyDev)
- [Golang Dojo](https://www.youtube.com/@GolangDojo)

## Installing GO

I downloaded the installer [go.dev](https://go.dev). The installer should add GO to the path of your OS for running the appropriate commands.

Antivirus programs or Windows's built-in security may be upset with GO for various reasons, so you may need to tweak your security settings to run Go executables. Fortuantly that did not happen to me.

## Getting The Gist

First, I used the official GO site and various sources to get started.
- [go.dev Learn](https://go.dev/learn)
- [W3 Go](https://www.w3schools.com/go/index.php)

### Run Go Programs

I created a main.go file in the root of my project. Then ran the following commands.
```go
package main

import "fmt"

func main() {
  fmt.Println("Yo!")
}
```

Create the `go.mod` file.
```go
go mod init main
```
Run the go program.
```go
go run main.go
```
Create the exe.
```go
go  build main.go
```

To run the exe, try something like this.
```shell
./main.exe
```

## Import External Packages

I modified my `main.go` a bit, adding `"rsc.io/quote"` to the imports. Also, I wanted to make a function call as well to try it out.

```go
package main import (
  "fmt"
  "rsc.io/quote"
)

func main() {
  fmt.Println("Yo!")
  testThis()
}

func testThis() {
  fmt.Println(quote.Go())
}
```

I already had a `go.mod` file, so I just ran `tidy` to grab the new package.

```go
go mod tidy
```

## Project Structure

```
bin/...
project/cmd/name/main.go
project/pkg/yourpackage.go
go.mod
go.sum
```

I wanted to know what the `meta` project structure was before continuing so I didn't start any bad habits, but had a little trouble while making the video. Fortunately, there are tons of sources out there that go into depth for people like myself.

So I found that GO does not expect you to import files or pull directly from relative directories, instead, it expects modules to be defined and imported as packages of that module. (Which in hindsight makes sense, not sure why I struggled with this)

To start, put the `main.go` file in something like `/cmd/projectname/HERE`.

Then create a module.
```go
go mod init github.com/whatever/projectname
```

It seems like the general convention (not a requirement) is to prefix with `github.com/` and end with the `/projectname/yourpackages`, but I could be wrong about this depending on the project. Not sure yet.

From there, you can import packages from wherever, but I found typically projects use `pkg/` for this. I am intentionally not talking about `internal/...`, I will explore that later.

```go
import (
  "fmt"
  "github.com/whatever/projectname/pkg/yourpackage"
)

func main() {
  // USE STUFF IN /YOURPACKGE/...
}
```

Something I missed early on is how public and private work in GO. Upper case types and functions are considered "Public" and lower case is considered "Private". So in the video, I created a `junk.go` file in `pkg/junk/...` which had a function that retured a string. This function failed until I made it uppercase.
