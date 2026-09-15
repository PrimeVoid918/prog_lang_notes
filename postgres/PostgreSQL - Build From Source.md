## Clone repository

```bash
git clone https://github.com/postgres/postgres.git
cd postgres
```

---

## Create build directory

Keep compilation artifacts separate from the source tree.

```bash
mkdir build
cd build
```

---

## Configure

`../configure` because we are inside `build/`.

```bash
../configure \
    --prefix=$HOME/Desktop/Projects/databases/postgres/install \
    --enable-debug
```

### Flags

```text
--prefix=<dir>
```

Installation directory after `make install`.

Instead of:

```
/usr/local
```

everything will be installed into

```
~/Desktop/Projects/databases/postgres/install
```

This avoids modifying the system PostgreSQL.

---

```text
--enable-debug
```

Compiles PostgreSQL with debugging symbols.

Useful when using:

- gdb
- stack traces
- source-level debugging

Slightly slower than a release build.

---

## Compile

```bash
make -j$(nproc)
```

### Notes

```text
-j
```

Run multiple compilation jobs.

```bash
$(nproc)
```

Returns the number of CPU threads.

Example:

```
4
```

becomes

```bash
make -j4
```

---

## Install

```bash
make install
```

Installs PostgreSQL into the directory specified by `--prefix`.