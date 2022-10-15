# pyenv and pipenv

There have been many versions of python over the years. Occassionally a programmer can run into a
situation where a newer version of python breaks a program written for an older version. Python
modules also often have version dependencies.

[**`pyenv`**](https://github.com/pyenv/pyenv) and [**`pipenv`**](https://pipenv.pypa.io/en/latest/)
provide a mechanism to ensure a program specifies its dependencies so it will build and work
consistently over time and across different computers.

## Table of Contents

-   [Example](#example)
-   [pyenv](#pyenv)
-   [pipenv](#pipenv)

## Example

TODO

## pyenv

[top](#pyenv-and-pipenv)

### Installing pyenv

I used the [**`pyenv-installer`**](https://github.com/pyenv/pyenv-installer) project which makes it easy to install on Ubuntu.

1. Install all required prerequisite dependencies

    ```
    sudo apt-get update; sudo apt-get install make build-essential libssl-dev zlib1g-dev \
    libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
    libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
    ```

2. Download and execute the installation script

    ```
    curl https://pyenv.run | bash
    ```

3. Add the following lines to your **`.bashrc`** file

    ```
    # pyenv
    export PYENV_ROOT="$HOME/.pyenv"
    command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
    eval "$(pyenv init -)"
    ```

4. Restart your shell

    ```
    exec $SHELL
    ```

5. Validate the version
    ```
    pyenv --version
    ```

### Uninstall pyenv

1. Remove the **`~/.pyenv`** folder

    ```
    rm -fr ~/.pyenv
    ```

2. Delete the following lines from your **`~/.bashrc`** file

    ```
    # pyenv
    export PYENV_ROOT="$HOME/.pyenv"
    command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
    eval "$(pyenv init -)"
    ```

3. Restart your shell

    ```
    exec $SHELL
    ```

### Basic pyenv commands

1. List all the possible python version that can be installed

    ```
    pyenv install --list
    ```

2. Install python

    ```
    pyenv install 3.9.2
    ```

## pipenv

[top](#pyenv-and-pipenv)

This is a pipenv guide...
