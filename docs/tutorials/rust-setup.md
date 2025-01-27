# Setting Up a Dev Container for Rust

* Primary author: [Boluwatife Adeshina](https://github.com/boluwatifeda)
* Reviewer: [Miguel Alvarado Dorado](https://github.com/miguelaa123)

---

!!! warning
    Do not install Rust or Cargo directly on your computer. The Dev Container handles everything for you, ensuring a consistent and isolated environment. Additionally, the Dev Container runs on Linux, so if you see an .exe file, that may mean that you are running commands outside the Dev Container on your host machine.


Follow these steps to create and configure a Rust DevContainer for your project.

---

## Prerequisites
- **Tools Required**:
    - [Docker](https://www.docker.com/)
    - [Visual Studio Code](https://code.visualstudio.com/)
    - **VSCode Extensions**:
        - [Remote - Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

---

## Steps to Create a Rust Dev Container

### 1. Create a New Project Directory
Start by creating a new folder for your project:
```bash
mkdir rust-devcontainer
cd rust-devcontainer
git init
```

### 2. Add Dev Container Configuration
Inside the ```rust-devcontainer```, create a new directory named ```.devcontainer```:
```bash 
mkdir .devcontainer
```
Then create the file with pathway ```.devcontainer/devcontainer.json``` by writing to your terminal:
```bash
touch .devcontainer/devcontainer.json
```
Add the following content to our JSON File:
```json
{
  "name": "Rust DevContainer",
  "image": "mcr.microsoft.com/devcontainers/rust:latest",
  "customizations": {
    "vscode": {
      "extensions": ["rust-lang.rust-analyzer"]
    }
  } 
}
```
!!! note
    - "name" is simply what you are calling your dev container
    - "image" defines the Docker image to use, in this case the latest version of a Go environment
    - "customizations" is useful when you want to add any important extenisions to make sure your project works for anyone using your dev container

### 3. Opening the Dev Container
Reopen the project in the container by pressing ```Ctrl+Shift+P``` (or ```Cmd+Shift+P``` on Mac), typing "Dev Containers: Reopen in Container," and selecting the option.

Verify that Rust has been installed by opening a terminal and running the command: 
```bash
rustc --version
```
This command should return: ```rustc 1.83.0 (90b35a623 2024-11-26)```

### 4. Executing a Rust Program
To ensure functionality, lets create a basic Rust program.

1. Create a new Rust project and enter it by writing the following to the command line:
```bash
cargo new hello-comp423 --vcs none #The --vcs option ensures that we create a new project without automatically creating a new git repository
cd hello-comp423
```

2. Open ```src/main.rs``` and write over its contents with this function:
    ```rust
    fn main() {
        println!("Hello COMP423");
    }
    ```
    and save the file.

3. There are two ways we can run the file:

    === "```cargo build```"

    The first way utilizes ```cargo build```. This command creates an ELF (Executable and Linked File) within a new ```target``` directory which allows you to manually run the program from your terminal. You run the program by running the command ```./target/debug/<your-program-name>``` in your terminal. (```./``` tells the terminal to look for an executable in the current directory while the rest specifies the pathname of the ELF file) In this instance we would run ```./target/debug/hello-comp423```. Once this is completed your program should output:
    ```bash
    Hello COMP423
    ```
    ```cargo build``` is useful because it compiles and builds your Rust project, downloads and manages all dependencies, and allows you to run it at any time of your choosing. Ultimately this gives you a lot of control over your program.

    !!! tip
        ```cargo clean``` will remove the ```target``` directory, deleting all build artifacts. You can run this command to free up disk space, ensure a fresh build, or fix build issues.

    === "```cargo run```"

    The second way, ```cargo run``` builds and executes your program in a single action. Whereas if you alter your process, you would have to rerun ```cargo build```, ```cargo run``` automatically rebuilds your project if your make changes everytime you execute it. Again, your project build remains in the ```target``` directory, and consists of compiled binaries (The ELF files) and dependencies.

    !!! note
        Note that ```cargo build``` allows you to build your project once and then run it multiple times. It can be useful for performance-sensitive tasks as it allows you to inspect or manipulate the compiled output. ```cargo run``` streamlines the process by automatically handling both tasks, which is more convenient for regular development.

---
### Key Concepts for Setting Up a Dev Container Project

Dev Container
: A configuration for containerized development environments in Visual Studio Code. It includes tools, dependencies, and settings.

Docker
: A platform that enables you to develop, ship, and run applications inside containers. Required for using DevContainers.

`devcontainer.json`
: A configuration file that defines the settings, extensions, and commands for the DevContainer.

Rust DevContainer
: A pre-configured DevContainer for Rust development. Includes Rust tools like `cargo` and the Rust Analyzer extension.

---
## References
1. [Starting a Static Website Project with MkDocs](https://comp423-25s.github.io/resources/MkDocs/tutorial/#step-2-add-requirementstxt-python-dependency-configuration)