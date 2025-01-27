# Setting up a Development Container for Go

* Primary author: [Katie Brown](https://github.com/kgbrown5)
* Reviewer: [Audrey Salmon](https://github.com/asalmon1)

## Introduction

In this tutorial, you will set up a new development environment using the language Go and learn how to make a simple starter program! You do not need to know anything about Go to complete this tutorial. In fact, you don't even need Go installed on your host computer. 

Instead, we will be using a Dev Container running Go. Dev Containers create a stable development environment, especially when you're using a new programming language, by making sure all collaborators have the same language version and extensions installed.The dev container will handle dependencies for you.

## Prerequisites

Before we get started, make sure you have installed the following:

* **Git**
* **Visual Studio Code**
* **Docker**

!!! warning
    Don't install Go on your computer! We will be implementing it in a Dev Container instead.

## Part 1: Setting up your Repository 

Instructions can also be found [here](https://comp423-25s.github.io/resources/MkDocs/tutorial/#part-1-project-setup-creating-the-repository) in *Part 1. Project Setup: Creating the Repository*

1. First, open a new terminal or command prompt.

2. Create a new directory by entering in these commands:
``` bash
mkdir comp423-ex00-go-tutorial
cd comp423-ex00-go-tutorial
```

3. Then initialize your repository using:
``` bash
git init
```

4. Finally, add a README using:
``` bash
echo "# COMP423 EX00 Go Tutorial" > README.md
git add README.md
git commit -m "Initial commit with README"
```

Congrats, you've just made the first commit on your new repository! Now you are going to link your repository to a remote repository.

1. Open GitHub and navigate to the **Create a New Repository** page.

2. Fill in the details as follows:
    - **Repository Name:** comp423-ex00-go-tutorial
    - **Description:** "Setting up a Go Dev Container for COMP423 EX00."
    - **Visibility:** Public

3. Then click **Create Repository**.

4. Now, navigate back to your terminal and add this new repository as a remote using:
``` bash
git remote add origin https://github.com/your-username/comp423-ex00-go-tutorial.git
```

    * Make sure to replace *your-username* with your GitHub username!

5. Finally, push your local commits to the remote using:
``` bash
git push --set-upstream origin main
```

!!! warning
    Make sure your default branch is named `main` using the subcommand `git branch`. Older versions of `git` name the default branch `master`. If this is the case, you can rename it to `main` by running the command `git branch -M main`.

## Part 2: Configuring the Dev Container

Now we need to actually set up the Dev Container! 

More info on Dev Containers can be found [here](https://comp423-25s.github.io/resources/MkDocs/tutorial/#part-2-setting-up-the-development-environment).

1. Open up VS Code and navigate to your `comp423-ex00-go-tutorial` repository.
2. Install the Dev Containers Extension for VS Code if you haven't already.
3. Then create a new folder in your repository named `.devcontainer`.
4. Next, create a new file named `devcontainer.json`.
This is the file that will hold all of your dev container configuration instructions, it should be the only file in your `.devcontainer` folder!

5. Now, paste the following info into your file:

``` json title=".devcontainer/devcontainer.json"
{
  "name": "COMP423 EX00 Go Tutorial",
  "image": "mcr.microsoft.com/devcontainers/go",
  "customizations": {
    "vscode": {
      "settings": {},
      "extensions": [
        "golang.go"
      ]
    }
  }
}
```

This is what we've just defined:

* `name`: The name of the dev container we are running. If you have many different development environments that you're using at one time, it's important to differentiate!
* `image`: What Docker image to use, in this case, the latest Go version environment. You can customize the image using a `Dockerfile` instead, but for simplicity here, we're using a base image provided by Microsoft.
* `customizations`: Adds useful configurations to VS Code. Here we are installing the Go extension made by the developers at Google so we can implement the language! Adding extensions here ensures other developers on your project have them installed in their dev containers automatically.

And now your Dev Container is configured! Check that everything is good to go by reopening the project in the container. 

You can do this by pressing `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac), typing "reopen", and selecting the `Dev Containers: Reopen in Container` option. At this point a new window will open and load up your dev container! This may take a few minutes, so don't be worried if you have to wait a bit for it.

Once your dev container fully loads open a new terminal within VS Code. Try running `go version` to see that your dev container is running a recent version of Go without you having to download and configure it!

## Part 3: Writing a Program

Now that we have our fully working dev container, let's use it!

1. Open a new terminal in VS Code and type in:
``` bash
go mod init hello
```
    - This initializes a new go.mod file in your current directory .
    - This .mod file serves as a module that tracks your imported package dependencies.
    - You should see the output `go: creating new go.mod: module hello`.

3. Next, create a new `hello.go` file.

4. Once you have this file, add in this code:
``` go title="hello.go"
package main

import "fmt"
```

This establishes that you are in the `main` package, and that you are importing the `fmt` package.

!!! note "fmt"
    `fmt` is a popular Go library that focuses on text formatting

5. Now you get to write your first function! Add this code to your file:
``` go title="hello.go"
func main() {
    fmt.Println("Hello COMP423!")
}
```
!!! note "main"
    We name our function `main` (instead of anything else) because in Go a `main` function will automatically execute when you run the `main` package.

6. You can then execute your file by either using the `run` command:
``` bash
go run hello.go
```
Or using the `build` command and running an executable file:
``` bash
go build hello.go
./hello
```

Try it out! You should now see `Hello COMP423!` printed in your terminal.

Even though they produce the same output, these commands have very different functionalities. `run` serves as a shortcut while developing to compile and execute your code in one quick step, while `build` compiles the full program (including packages) and creates an executable file that can then be sent elsewhere.

Running `build` is comparable to running `gcc -o hello hello.c`, which you used in COMP211! This is because they both compile your program and create an executable, but they don't run it. Instead you have to run the executable `./hello` separately.

## Congrats!

You have successfully set up a Go Dev Container, created a new Go project, and compiled and ran the program it to test it out!

Referenced [MkDocs Tutorial](https://comp423-25s.github.io/resources/MkDocs/tutorial/) by Kris Jordan