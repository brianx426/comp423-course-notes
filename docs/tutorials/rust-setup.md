# Setting up a dev container for Rust

* Primary author: [Brian Liu](https://github.com/brianx426)
* Reviewer: [Yuanyao Lin](https://github.com/yuanyaolin13)

# In this tutorial, you will learn how to set up a dev container for your Rust projects!

## First Things First, the Prerequisites
1. Install [Virtual Studio Code](https://code.visualstudio.com/download) (VS Code).
2. Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) for your operating system.
3. Create a [GitHub Account](https://github.com).
4. Install [Docker](https://www.docker.com/get-started/). This will provide our dev container.
5. Learn some Command-Line-Interface. Read some of the Learn a CLI text.

## Once you've done the above things, we move on to setting up your project
### Step 1. Create a Repository
(A) Open Terminal/Command Prompt<br>
(B) Run the following the commands<br>
  ```bash
  mkdir rust-project
  cd rust-project
  git init
  ```
!!! note "What do these commands do?"
    ```mkdir rust-project``` creates a new directory named ``rust-project``. ```cd rust-project``` makes ``rust-project`` the current working directory. ```git init``` initializes a new git repository

(C) Create the README file by running the following commands and make your first commit
  ```bash
  echo "# Rust Project" >> README.md
  echo "[Link to Tutorial](https://brianx426.github.io/comp423-course-notes/tutorials/rust-setup/)" >> README.md
  git add README.md
  git commit -m "Initial commit: added README.md"
  ```
!!! note "Command explanations"
    The `echo` commands appends the text after echo into the README file. After initializing our README file, we want to make our initial commit to GitHub using the `git add` and `git commit` commands.

### Step 2. Create a Remote Repository on GitHub
(A) Log in to your GitHub account and navigate to the [Create a New Repository](https://github.com/new) page.
(B) Fill in the details as follows:<br>

* **Repository Name**: `rust-project`
* **Description**: "Hello World using Rust"
* **Visibility**: Public

(C) Do not initialize the repository with a README, .gitignore, or license.

(D) Click **Create Repository**.

### Step 3: Link your Local Repository on Github
(A) Add the GitHub repository as a remote:

```bash
git remode add origin https://github.com/<your-username>/rust-project.git
```

Replace `<your-username>` with your GitHub username.

(B) Make `main` the default branch name. Run `git branch`, if you do not see `main`, run the following: `git branch -M main`

!!! note "Why do we do this?"
    Old versions of git use the name `master` for the primary branch, but nowadays, `main` is used as the standard primary branch name.

(C) Push your local commits to the GitHub Repository:
```bash
git push --set-upstream origin main
```

(D) Now, refresh your GitHub Repository on your web browser and you should see the same commit that you just made has been pushed to remote.

## Setting Up the Development Environment
### Step 1. Add Development Container Configuration
1. In VS Code, open the `rust-project` directory. You can do this via: File > Open Foler.
2. Install the **Dev Containers** extension for VS Code.
3. Create a `.devcontainer` directory in the root of your project with the following file inside of this "hidden" configuration directory:

```bash
.devcontainer/devcontainer.json
```

The `devcontainer.json` file defines the configuration for your development environment. We specify the following:

  * `name`: A descriptive name for your container
  * `image`: The Docker image to use, in this case, the latest version of a Rust environment. You can find a collection of base images maintained by Microsoft [here](https://hub.docker.com/r/microsoft/vscode-devcontainers).
  * `customizations`: Adds useful configurations to VS Code, like installing the Rust extension.
  * `postCreateCommand`: A command to run after the container is created. In our case, it will just run: `rustc --version` to check the version of rust we are using.

4\. In the `devcontainers.json` file, add the following:

```json
{
  "name": "Rust Project",
  "image": "mcr.microsoft.com/devcontainers/rust:latest",
  "customizations": {
    "vscode": {
      "settings: {},
      "extensions": ["rust-lang.rust-analyzer"]
    }
  },
  "postCreateCommand": "rustc --version"
}
```

### Step 2. Reopen the Project in a Dev Container
1. Press Ctrl(Cmd for mac) + Shift + p
2. Type and Select the option: "Dev Containers: Reopen in Container"
3. Wait until the image is downloaded
4. Once the image downloads, you can move on to creating the project!

## Creating the Project
You made it! We are in the home stretch of this tutorial now! Just a few more steps to go!
### Step 1. Create a new rust file by doing the following
(A) Open a new terminal in VS Code and run the following:

```bash
cargo new hello-comp423 --vcs none
cd hello-comp423
```

!!! note "I've ran these commands before!!!"
    Recall towards the beginning of this tutorial. We did something similar! The commands we just ran created a new directory called `hello-comp423` without initializing a VCS and made our current working directory `hello-comp423`

(B) Navigate to the `src/main.rs` file and open it.