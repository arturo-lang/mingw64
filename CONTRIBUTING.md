# Contribution Guide

If you want to contribute, We would be extremely greatful. 😊

Contributing could mean a few different things:

- Bug report
- Discuss the current state of the source code
- Submit bug fixes and updates
- Documentation
- Fix grammar and typos
- Propose new features
- Become a maintainer
- Donations

In a few words: all contributions (even if they are just ideas or suggestions) are 💯% welcome!

## What you need to know

This package also exists in the official MSYS2 repository.
What you’ll find here is a mirror of that package.

The goal of this repository is isolation and control: a dedicated place where we can keep the package separate from others, apply changes, and test updates or patches before submitting them upstream.

Continuous integration is enabled, so every change is checked to ensure the package builds correctly and ships with all required runtime dependencies.

Beyond packaging and testing, this repository also serves as a central place for documentation and user support.

## Setup

In order to contribute for this project, make sure you have
MSYS2 installed in your system.

Then Clone our repository:

```sh
% git clone https://github.com/arturo-lang/mingw64 mingw-w64-arturo
% cd mingw-w64-arturo
```

## Patching

1. **Getting the source code**

In order to create patches, you need to get our source code, first.
So, use the following command:

```sh
% makepkg-mingw -o
```

This will download our source code and apply the previous patches.

2. **Copy the target**

Rename `src/arturo-*/` to `a/` and mock the structure of the file 
you want to modify inside `b/`.

Example:

```diff
-  src/
-  ├─ a/
-  │  └─ src/
-  │     └─ extras/
-  │        └─ db_connector/
+  │           └─ sqlite3.nim
-  └─ b/
-    └─ src/
-       └─ extras/
-          └─ db_connector/
+             └─ sqlite3.nim
```

You need to mock exactly the same file-path. 
Preferably, make a real copy this of this file, 
don't copy & paste its content, but the file itself.

3. **Make changes**

Then, change what you wish to change.

4. **Create the patch**

```sh
% cd src
% diff --unified --recursive --new-file \
    path/to/original                    \
    path/to/modified                    \
    > ../<id>-<description>.patch
```

In our example:

```sh
% cd src
% diff --unified --recursive --new-file        \
    a/src/extras/db_connector/sqlite3.nim      \
    b/src/extras/db_connector/sqlite3.nim      \
    > ../002-fix-sqlite3-dependency-name.patch
```

5. **Apply patches**

Add your patch to the `source` at `PKGBUILD`, e.g.:

```sh
source=(
  "https://github.com/arturo-lang/arturo/archive/v${pkgver}/${_realname}-${pkgver}.tar.gz"
  "001-no-static-linking.patch"
  "002-fix-sqlite3-dependency-name.patch"
  # Add 003 here
)
```

And also apply the patch inside `prepare` in `PKGBUILD`:

```sh
prepare() {
    ...
    patch -p1 -i "${srcdir}"/<your-patch-here>.patch
}
```

6. **Regenerate checksums**

```sh
% makepkg-mingw -g >> PKGBUILD
```

Manually adjust the `sha256sums` as you wish.
Preferably, put it right after `source`
and adjust its indentation.

7. **Update the release**

Increment `pkgrel` at `PKGBUILD`.


## New Versions

New versions should be compatible with the current one,
but dependencies may change. Make sure it's synced with
our need, with all of them updated and with the strictly
necessary ones only.

Also, make sure to increment `pkgrel` if you modify our package.
