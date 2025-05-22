# MinilibX Linux

[![Build Status](https://github.com/42Paris/minilibx-linux/actions/workflows/ci.yml/badge.svg)](https://github.com/42Paris/minilibx-linux/actions/workflows/ci.yml)

A minimal X11 (X11R6) programming API in C, designed for students and X-beginners.

---

## Table of Contents

- [MinilibX Linux](#minilibx-linux)
  - [Table of Contents](#table-of-contents)
  - [Features](#features)
  - [Requirements](#requirements)
    - [Linux](#linux)
    - [macOS](#macos)
  - [Installation](#installation)
    - [Compile from Source](#compile-from-source)
    - [Manual Installation](#manual-installation)
  - [Usage](#usage)
  - [API Reference](#api-reference)
  - [License](#license)

---

## Features

- Create windows, handle events, draw pixels, images, and text
- Minimal dependencies: X11 and XShm
- Includes man pages and a sample test program

---

## Requirements

### Linux

- TrueColor visual type (8, 15, 16, 24, or 32 bits)
- `gcc`
- `make`
- X11 development files (`xorg`)
- XShm extension (`libxext-dev`)
- BSD utility functions (`libbsd-dev`)

```bash
sudo apt-get install gcc make xorg libxext-dev libbsd-dev
```

### macOS

- [Quartz](https://www.xquartz.org/)

```bash
brew install --cask xquartz
sudo reboot
xeyes  # verify X11
```

---

## Installation

### Compile from Source

```bash
git clone https://github.com/42Paris/minilibx-linux.git
cd minilibx-linux
./configure   # generates Makefile.gen and builds everything
# or simply:
make
```

This produces:

- `libmlx.a` and `libmlx_$(HOSTTYPE).a`
- `test/mlx-test` sample binary

### Manual Installation

Copy the library, headers, and man-pages to your system paths:

```bash
sudo cp libmlx.a libmlx_$(HOSTTYPE).a /usr/local/lib/
sudo cp mlx.h             /usr/local/include/
sudo cp man/man3/mlx*.1   /usr/local/share/man/man3/
sudo mandb  # update man database
```

---

## Usage

Include the header and link against `libmlx.a`:

```c
#include <mlx.h>

int main(void)
{
    void *mlx = mlx_init();
    void *win = mlx_new_window(mlx, 800, 600, "Hello MinilibX");
    mlx_loop(mlx);
    return 0;
}
```

Compile:

```bash
gcc main.c -L. -lmlx -lXext -lX11 -lm -o my_app
```

---

## API Reference

Consult the man pages under `man/man3/`:

```bash
man mlx
man mlx_loop
man mlx_new_window
man mlx_pixel_put
```

---

## License

This project is licensed under the [MIT License](LICENSE).
Olivier CROUZET – January 6, 2014
