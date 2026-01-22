<h1 align="center">
    Arturo's Mingw64 Package for MSYS2
</h1>

<p align="center">
<i>
  A Mingw64 package for the <a href="https://arturo-lang.io">Arturo programming language</a> on the
  <a href="https://www.msys2.org">MSYS2</a> platform.
</i>
<br>
<br><br>
<img 
    alt="Arturo logo" 
    width="20" 
    src="https://github.com/arturo-lang/arturo/raw/master/docs/images/logo.png#gh-light-mode-only"
/>
<img 
    alt="Arturo logo" 
    width="20" 
    src="https://github.com/arturo-lang/arturo/raw/master/docs/images/logo-lightgray.png#gh-dark-mode-only" 
/>
<br>
<b>~ CODE IS ART ~</b>
</p>

<p align="center">
    <img alt="GitHub License" src="https://img.shields.io/github/license/RickBarretto/mingw-w64-arturo?style=flat-square">
</p>
<p align="center">
    <img alt="GitHub branch status" src="https://img.shields.io/github/checks-status/RickBarretto/mingw-w64-arturo/main?style=flat-square">
</p>

## Prerequisites

- [MSYS2](https://www.msys2.org/) installed and updated.
- MSYS2 `mingw-w64-x86_64-toolchain` package installed.

## How to use

**Compiling from source**

```sh
$ git clone https://github.com/RickBarretto/mingw-w64-arturo
$ cd mingw-w64-arturo
$ makepkg -si
```

This will:

- Install dependencies from MSYS2's repository.
- Compile Nim 2.2.6 from source for build-only.
- Compile Arturo 0.10.0 (Arizona Bark) from source along with its dependencies.
- Install the `mingw-w64-x86_64-arturo` package system-wide.

## What you need to know

By installing this package, your system PATH will be modified
in order to add `~/.arturo/bin` and `~/.arturo/packages/bin` into your `$PATH`.

Don't worry too much, we also have made scripts to uninstall Arturo
and to clean up your PATH from those entries. :wink:


## Update and Remove

### Update

**Recompiling from source**

```sh
$ cd mingw-w64-arturo
$ git pull
$ makepkg -si
```

### Remove

```sh
$ pacman -R mingw-w64-x86_64-arturo
```