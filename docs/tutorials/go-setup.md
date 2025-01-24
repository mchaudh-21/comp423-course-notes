# Setting up a dev container for Go

* Primary author: [Manasi Chaudhary](https://github.com/mchaudh-21
)
* Reviewer: [Emma Coye](https://github.com/emmacoye)

## Prerequisites
* VS Code installed with Dev Containers extension 
* Docker Desktop installed and running 
* Git installed and configured
* Install [Go](https://go.dev/doc/install)

## Creating a New Project

### 1. Initialize Git Repository 

``` bash
# Create and enter new directory 
mkdir go-hello-423 
cd go-hello-423

# Initialize git repository 
git init 

# Create initial commit with empty README
echo "# Go Hello COMP423" > README.md
git add README.md
git commit -m "Initial Commit"
```

### 2. Configure Dev Container 
Create a new ```.devcontainer``` directory and add a ```devcontainer.json``` file, all inside the root of your project. This will be "hidden". 

Add the following configuration:
```
{
    "name": "Go development", 
    "image": "mcr.microsoft.com/devcontainers/go:latest",
    "customizations": {
        "vscode": {
            "extensions" : ["golang.go"]
        }
    }
}
```

### 3. Set up the project
A Go module is what manages the project's dependencies and provides package information. Create one for our project. 

First verify Go installation using ```go version```. 

Now initialize the module using ```go mod```:
```
go mod init hello-423
```

???+ warning "Verify setup"
    Use ```go mod verify``` to make sure the module was initialized. 

???+ abstract "Project Structure"
    A usual Go project includes

    * ```main.go``` -- entry point
    * ```go.mod``` -- dependencies
    * ```README.md``` -- documentation

### 4. Write Hello-423
In your project root, create a file called ```main.go``` and write the following in the file:

```
package main

import "fmt"

func main(){
    fmt.Println("Hello COMP423")
}
```

### 5. Build and run the program
We can compile and run the program with two different strategies 

* Write ```go run main.go``` in the terminal to compile and run the program in one step. 

* Use go build to compile the file, then run the compiled file. Input each line as follows in the terminal.
```
go build
./hello-423
```
???+ info "Understanding the compilation step"
    ```go build```: This command acts similarly to the ```gcc``` command that we used in COMP 211. ```gcc``` supports  a wide range of languages, including C and Go, but ```go build``` is designed specifically for Golang. ```go build``` is generally faster in compilation speed. 

## Conclusion
You've successfully created and run a program in Go!