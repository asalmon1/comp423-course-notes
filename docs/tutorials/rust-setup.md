# Setting up a dev container for Rust!

* Primary author: [Audrey Salmon](https://github.com/asalmon1)
* Reviewer: [Katie Brown](https://github.com/kgbrown5)

## Introduction

In the following tutorial, you'll learn how to set up a simple project from scratch in the Rust programming language. You don't need to know anything about Rust to complete this tutorial - in fact, you don't even need it installed on your host computer! 

Instead, we will be using a development environment (Dev Container). Dev Containers make it easy to set up an environment, even when you're using a new programming language.

## Prerequisites

Before starting this tutorial, ensure you have the following software installed on your host computer:

- **Visual Studio Code** (VSCode) with the **Remote - Containers** extension
- **Docker**
- **Git**

!!! warning
    Do not install any additional software onto your host computer. The dev container will handle all dependencies.

## Step 1: Create a Blank Directory & Initialize Git

1. Open your terminal.
2. Create a new directory for your project:
   ```bash
   mkdir rust-project
   cd rust-project
   ```
3. Initialize your git repository:
    ```bash
    git init
    ```

## Step 2: Configure Your Dev Container

1. In VSCode, open your `rust-project` directory. You can do this from the menu bar via *File > Open...*.
2. Inside the project directory, create the `.devcontainer` folder.
3. Create a file named `devcontainer.json` inside the `.devcontainer` folder, and add the following content:
    ```json
    {
        "name": "Rust Dev Container",
        "image": "mcr.microsoft.com/devcontainter/rust:latest",
        "features": {},
        "customizations": {
            "vscode": {
                "extensions": [
                    "rust-lang.rust-analyzer"
                ]
            }
        }
    }
    ```
    
    #### Parts of the `devcontainer.json` file

    * `name`: Sets the name of the container. This is especially important if you have more than one development environment, so you can differentiate between your various configurations.
    * `image`: If you wanted to customize your container more, you could provide the path to a `Dockerfile` here. To make this tutorial easier, we are using a prebuilt container image from Microsoft.
    * `customizations.vscode.extensions`: Ensures that the `rust-analyzer` VSCode plugin is installed.

## Step 3: Build and Open Your Dev Container

1. Ensure that you still have the project directory open in VSCode.
2. Use the **Command Palette** (`Ctrl+Shift+P` or *View > Command Palette* from the menu bar) and select **Dev Containers: Reopen in Container**.
3. Wait for the container to start. This may take a few minutes.

## Step 4: Check Your Environment

Once the Dev Container starts, check that `rustc` is installed.

1. Open a terminal in VSCode (*Terminal > New Terminal* from the menu bar).
2. Run `rustc --version`. If a recent version of Rust is printed, you're good to go!

## Step 5: Create a Rust Project

1. Create a new Rust project:
    ```bash
    cargo new hello_comp423 --vcs none
    ```

    !!! note
        The `--vcs none` flag tells Cargo not to create a new Git repository when setting up the project.

    This creates a folder called `hello_comp423` with the following structure:
        ```
        hello_comp423/
        ├── Cargo.toml
        └── src/
            └── main.rs
        ```

    #### Parts of your project folder

    * `Cargo.toml`: The project configuration file. You don't have to edit this.
    * `src/main.rs`: The entry point of your program.

    !!! note "What is Cargo?"
        [Cargo](https://doc.rust-lang.org/cargo/) is the Rust build system and package manager.

2. Navigate into your project directory using the VSCode explorer.

## Step 6: Write Your Rust Program

Open `src/main.rs` and replace its contents with:
    ```rust
    fn main() {
        println!("Hello COMP423");
    }
    ```

#### Parts of a Rust program
* `fn main()`: This defines the main function, the entry point of a Rust program.
* `println!`: This is a Rust [macro](https://doc.rust-lang.org/book/ch19-06-macros.html) (indicated by the `!`) which prints formatted text to the console, and automatically appends a newline to the end.
* `"Hello COMP423"`: This is a string literal passed as an argument to `println!`.

For more information on writing programs in Cargo, see the [Cargo documentation](https://doc.rust-lang.org/book/title-page.html).

## Step 7: Build and Run Your Project

You have two different options to run your project. Before you run any commands, make sure you cd into your `hello_comp423` directory. 

In the terminal:
```bash
cd hello_comp423
```

### Option 1: Building, then running the project

1. To build the project first, run `cargo build` in your terminal.
    * This command compiles the program and puts the output in the `target/debug` directory.
    * Compare this to running `gcc -o program program.c`, which allows you to explicitly name the output file when compiling a C program.
2. Run the binary:
    ```bash
    ./target/debug/hello_comp423
    ```

### Option 2: Running the project directly

Use the `cargo run` command to build and run the project in one step.

* This command compiles and immediately executes the program, which saves you an extra step!

Regardless of which method you choose, you should see the output:

```
Hello COMP423
```

## Conclusion

Congratulations! You've successfully set up your development environment, built a Rust project, and ran your program. 