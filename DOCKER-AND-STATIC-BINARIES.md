# Running Static binaries generated with Rust in Docker containers

## Source used

Actix repository examples used:

https://github.com/actix/actix


## Glibc

Generating the binary with glibc

### Compiling and running

Compile with x86_64-unknown-linux-gnu as target

```bash
RUSTFLAGS='-C target-feature=+crt-static' cargo build --example ping --release --target x86_64-unknown-linux-gnu
```

Executing the binary using alpine-glibc image

```bash
docker run --rm -it -v $PWD/target/x86_64-unknown-linux-gnu/release/examples/ping:/bin/ping frolvlad/alpine-glibc /bin/ash
```


## Musl

Added muslc target

```bash
rustup target add x86_64-unknown-linux-musl
```

### Compiling and running


Compiling with x86_64-unknown-linux-musl as target:

```bash
cargo build --example ping --release --target x86_64-unknown-linux-musl
```

Running using alpine docker image:

```bash
docker run --rm -it -v $PWD/target/x86_64-unknown-linux-musl/release/examples/ping:/usr/bin/ping alpine:3.12 /bin/sh
```

