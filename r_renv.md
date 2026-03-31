# Set up R and renv

The sections below detail the steps to implement a clean R install along with RENV for environment management.

- [Install required software](#install-required-software)
- [Project setup from scratch](#project-setup-from-scratch)
    - [Clone a repository and create an R project](#clone-a-repository-and-create-an-r-project)
    - [Create an environment using `renv`](#create-an-environment-using-renv)
    - [Install packages with `renv`](#install-packages-with-renv)
- [Project setup from existing repository](#project-setup-from-existing-repository)

---

## Install required software

* Download and install `R` from https://cran.rstudio.com/
* Download and install `Rstudio Desktop` from https://posit.co/download/rstudio-desktop/
* Download and install `Rtools` from https://cran.rstudio.com/bin/windows/Rtools/
* Download and install `Git` from https://git-scm.com/install/
* Download and install `GitHub Desktop` from https://desktop.github.com/download/
* Download and install `Docker Desktop` from https://www.docker.com/products/docker-desktop/

## Project setup from scratch

The following steps detail how to clone a newly created repository, create an R project **from scratch**, and set up an environment using `renv`.

You can use the `renv` R package to manage dependencies across projects (packages and libraries needed to run the different analyses). For more details on `renv` see https://rstudio.github.io/renv/articles/renv.html

> [!WARNING]
> Please note that if you are cloning a repository where an `renv` environment has already been created, you need to follow the steps in [Project Setup from existing repository](#project-setup-from-existing-repository). You can read this section for information purposes and then proceed to [Project Setup from existing repository](#project-setup-from-existing-repository) to get started.
>
> If you are not sure whether an `renv` environment has been created, you can check whether an `renv.lock` file exists at the root directory of the repository. If an `renv.lock` file exists, you can skip this section.

### Clone a repository and create an R project

Assuming we have just created a new repository in GitHub, follow these steps to clone it and set up the environment for the first time:

1. Go to your GitHub repository and under `Code -> HTTPS`, select the option `Open with GitHub Desktop`. This should open GitHub Desktop in your local machine.
2. In the `Clone a repository` window, ensure you are under `URL` and select a `Local path` (e.g. `C:\users\your-user\dev\repository-name`). Click on `Clone`.
3. Still in GitHub Desktop, click on `Fetch origin` to do a git pull. 
4. Open RStudio and select `File/New Project`, choosing the option `Existing Directory`. Select the path to where you just cloned your repository`Git` and click on `Create Project`. Once done, an `.Rproj` file should have appeared in the local folder.
5. In the RStudio Terminal, run `git pull` to ensure you have the latest version of the repository.
6. Before starting developing new code, it is advisable to create a new branch separate from `master`. You can do this with `git switch -c your-branch-name`.

### Create an environment using `renv`

To create an environment for the project using `renv`, do:

- Run `install.packages("renv")` from the R Console (not the Terminal) of RStudio.
    - If you need to install a previous `renv` version to match that of an existing project (check the updated `renv.lock` file for that), you can do `install.packages("remotes")` and then `remotes::install_version("renv", version = "1.1.1", repos = "https://cloud.r-project.org")`.
- Still in the RStudio Console, run `renv::init()` to create an `renv` folder and an `renv.lock` file in the project directory.
    - When doing this, `renv` may ask you to proceed acknowledging the changes it will implement (type `y` to proceed).
    - In addition, if the repository contains a `DESCRIPTION` file, it may ask you to confirm whether to use it for dependency discovery in this project.
- If you had a `DESCRIPTION` file and `renv` proceeded to install dependencies, run `renv::settings$snapshot.type("all")` and then `renv::snapshot()` to update the lockfile with metadata about the currently-used packages in the project library.
- Commit/push changes to the repo so other users get the updated `renv.lock` file.

### Install packages with `renv`

Any time you need to install a package, do so by running `renv::install("<package>")` or "`renv::install("bioc::<package>")` in the Console and then update the `renv.lock` file as follows:

- Run `renv::install("<package>")` to install new required packages.
- Run `renv::settings$snapshot.type("all")` and then `renv::snapshot()` to update the lockfile with metadata about the currently-used packages in the project library.
- Commit/push changes to the repo so other users get the updated `renv.lock` file.

## Project setup from existing repository

If instead of starting the project from scratch, you are joining after the repository has been created and an `renv.lock` file already exists, you can install the necessary packages as follows.

1. Create an R project and clone the repository following the steps described in [Clone a repository and create an R project](#clone-a-repository-and-create-an-r-project) and navigate to the project directory. Importantly, make sure that the `renv` version you install matches that in the `renv.lock` file (e.g. version `1.1.1`).

2. Run `renv::restore()` in the R Console (not the Terminal) to reinstall the exact package versions recorded in the lockfile `renv.lock`.

3. Any time you need to install a package, do so by running `renv::install("<package>")` or "`renv::install("bioc::<package>")` in the Console and then update the `renv.lock` file as follows:

    - Run `renv::install("<package>")` to install new required packages (or `renv::remove("<package>"`) to uninstall it).
    - Run `renv::settings$snapshot.type("all")` and then `renv::snapshot()` to update the lockfile with metadata about the currently-used packages in the project library.
    - Commit/push changes to the repo so other uses get the updated `renv.lock` file.
