# Criterion Setup

[Criterion](https://criterion.readthedocs.io/en/master/index.html) is a simple unit testing framework for C/C++

## Installation Instructions

Install the dependencies:

```
sudo apt update
sudo apt install meson ninja cmake pkg-config libffi-dev libgit2-dev
```

Clone the Criterion repository:

```
git clone --recursive https://github.com/Snaipe/Criterion
```

Build the project:

```
meson build
ninja -C build
```

Install the library:

```
sudo ninja -C build install
```

On Linux systems, update the dynamic linker runtime bindings:

```
sudo ldconfig
```

_Once installed we can delete the Criterion repository._
