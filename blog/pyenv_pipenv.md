# pyenv and pipenv

There have been many versions of python over the years. Occasionally a programmer can run into a
situation where a newer version of python breaks a program written for an older version. Python
packages also often have version dependencies.

[`pyenv`](https://github.com/pyenv/pyenv) and [`pipenv`](https://pipenv.pypa.io/en/latest/)
provide a mechanism to ensure a program specifies its dependencies so it will build and work
consistently over time and across different computers.

## Table of Contents

-   [pyenv](#pyenv)
-   [pipenv](#pipenv)

## pyenv

[top](#pyenv-and-pipenv)

### Installing pyenv

I used the [`pyenv-installer`](https://github.com/pyenv/pyenv-installer) project which makes it easy
to install on Ubuntu.

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

3. Add the following lines to your `.bashrc` file

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

1. Remove the `~/.pyenv` folder

    ```
    rm -fr ~/.pyenv
    ```

2. Delete the following lines from your `~/.bashrc` file

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

1. List all python versions that can be installed

    ```
    pyenv install --list
    ```

2. Install a specific version of python

    ```
    pyenv install 3.9.2
    ```

3. Set the _global_ (system-wide) version of python

    ```
    pyenv global 3.8.6
    ```

4. Set the local folder's (project-based) version of python

    ```
    pyenv local 3.9.2
    ```

    > This creates a file in the current folder named `.python_version`

5. You can also _uninstall_ an installed version of python

    ```
    pyenv uninstall 3.9.2
    ```

    > This works as long as `pyenv` was used to install that version...

6. Check all the install versions

    ```
    pyenv versions
    ```

## pipenv

[top](#pyenv-and-pipenv)

### Install pipenv

```
pip install --user pipenv
```

When using `pipenv` it is specific to a project folder. What happens next depends on whether the
files `Pipfile` and `Pipfile.lock` exist.

### The files exist

If the `Pipfile` and `Pipefile.lock` already exist we could install all the project dependencies
with the command:

```
pipenv install --dev
```

### They don't

When these files _don't_ exist, they will be created.

```
pipenv install
```

A newly created `Pipfile` will look something like:

```
[[source]]
url = "https://pypi.org/simple"
verify_ssl = true
name = "pypi"

[packages]

[dev-packages]

[requires]
python_version = "3.8"
```

Any installed packages show up under the `[packages]` category, and any development packages show
up under the `[dev-packages]` category.

### Basic pipenv commands

1. Installing a package

    ```
    pipenv install <package>
    ```

    For example to install `pygame`

    ```
    pipenv install pygame
    ```

2. Installing a development package

    To indicate a development package add `--dev` to the command

    ```
    pipenv install pytest --dev
    ```

    Now if we look at the `Pipfile` it contains:

    ```
    [[source]]
    url = "https://pypi.org/simple"
    verify_ssl = true
    name = "pypi"

    [packages]
    pygame = "*"

    [dev-packages]
    pytest = "*"

    [requires]
    python_version = "3.8"
    ```

> In both cases, we didn't specify a version for either package. The "\*" indicates the latest
> version was used.

3. Install a _specific_ package

    ```
    pipenv install tensorflow==2.7.0
    ```

    If we look at the `Pipfile` it now specifies this specific version of tensorflow.

    ```
    [[source]]
    url = "https://pypi.org/simple"
    verify_ssl = true
    name = "pypi"

    [packages]
    pygame = "*"
    tensorflow = "==2.7.0"

    [dev-packages]
    pytest = "*"

    [requires]
    python_version = "3.8"
    ```

4. Uninstall an installed package

    ```
    pipenv uninstall tensorflow
    ```

5. Remove a virtual environment

    We we ran the initial `pipenv install` this created a virtual environment in the project folder.
    If for some reason we want to remove the virtual environment we can run the command:

    ```
    pipenv --rm
    ```

    We can now create a new virtual environment which will install all the project dependencies which
    are defined in `Pipfile.lock`.

    ```
    pipenv install --dev
    ```

6. Run a python program in the virtual environment

    ```
    pipenv run python3 my-python-program.py
    ```

7. Detect security vulnerabilities

    ```
    pipenv check
    ```
