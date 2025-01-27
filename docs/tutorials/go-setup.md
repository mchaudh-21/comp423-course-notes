# Setting up a dev container for Go

* Primary author: [Manasi Chaudhary](https://github.com/mchaudh-21
)
* Reviewer: [Emma Coye](https://github.com/emmacoye)

## Prerequisites
* VS Code installed with Dev Containers extension 
* Docker Desktop installed and running 
* Git installed and configured

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

#### Create a Remote Repository on GitHub
(1) Log in to your GitHub account and navigate to the Create a New Repository page.

(2) Fill in the details as follows:

- Repository Name: go-hello-comp423
- Description: Something releated to how this is a "Hello World" program.
- Visibility: Public

(3) Do not initialize the repository with a README, .gitignore, or license.

(4) Click Create Repository.

#### Link your Local Repository to GitHub
(1) Add the GitHub repository as a remote:


``` bash
git remote add origin https://github.com/<your-username>/go-hello-comp423.git
```
- Replace <your-username> with your GitHub username.

(2) Check your default branch name with the subcommand git branch. If it's not main, rename it to main with the following command: git branch -M main. Old versions of git choose the name master for the primary branch, but these days main is the standard primary branch name.

(3) Push your local commits to the GitHub repository:


``` bash
git push --set-upstream origin main
```

!!! Understanding the --set-upstream Flag
    git push --set-upstream origin main: This command pushes the main branch to the remote repository origin. The --set-upstream flag sets up the main branch to track the remote branch, meaning future pushes and pulls can be done without specifying the branch name and just writing git push origin when working on your local main branch. This long flag has a corresponding -u short flag.
(4) Back in your web browser, refresh your GitHub repository to see that the same commit you made locally has now been pushed to remote. You can use git log locally to see the commit ID and message which should match the ID of the most recent commit on GitHub. This is the result of pushing your changes to your remote repository.

!!! Reference
    These instructions are from COMP 423's [mkdocs tutorial](https://comp423-25s.github.io/resources/MkDocs/tutorial/#step-3-link-your-local-repository-to-github).

### 2. Configure Dev Container

Navigate to your new repository in VS Code.

Create a new ```.devcontainer``` directory and add a ```devcontainer.json``` file, all inside the root of your project. This will be "hidden". 

Add the following configuration:
```
{
    "name": "Go development", 
    "image": "mcr.microsoft.com/devcontainers/go:latest",
    "customizations": {
        "vscode": {
            "extensions" : ["ms-vscode.go"]
        }
    }
}
```

After adding the above configurations, we then want to reopen our project in a dev container.
To do so press Ctrl+Shift+P (or Cmd+Shift+P on macOS) and type: 
"Dev Containers: Reopen in Container," and selecting the option.

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
    
### 6. Push Changes
Now that your configuration is ready, let's test it out:

(1) Add and commit your changes:
``` bash
git add .
git commit -m "Program for 'Hello COMP423 in Go"
```

(2) Push the changes to GitHub:
``` bash
git push origin main
```

(3) Navigate to your GitHub repository to ensure that the changes have been committed and pushed.

## Conclusion
You've successfully created and run a program in Go!

## References

Details on dev containers and mkdocs can be further explored with this COMP 423 [mkdocs tutorial](https://comp423-25s.github.io/resources/MkDocs/tutorial/#what-is-a-development-dev-container).