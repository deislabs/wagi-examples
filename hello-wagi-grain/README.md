# Hello Wagi for the Grain Language

[Grain](https://grain-lang.org) is a new programming language that targets WebAssembly.

This repository provides a simple module that works with [Wagi](https://github.com/deislabs/wagi).
It illustrates how easy it is to write HTTP responders with Grain and Wagi.

This version is built on Grain 0.3, and relies on Grain 0.3's static compiler.
Grain is a rapidly evolving language, and this code may not work on other versions of Grain.

## Building

There is already a `hello.gr.wasm` binary checked in.
To build from source, [install Grain]()
and then use this command to compile:

```console
$ grain compile hello.gr
```

You can test your program with `grain` or `wasmtime`:

```console
$ wasmtime hello.gr.wasm --env USER=mbutcher hello
==== Environment: ====
USER=mbutcher
==== Args: ====
hello.gr.wasm
hello
```

When deploying to Wagi, you will want to add an entry like this in WAGI's route TOML:

```toml
[[module]]
route = "/hello-grain"
module = "/path/to/hello-wagi-grain/hello.gr.wasm"

```

After reloading or restarting Wagi, you can execute this module:

```
$ curl localhost:3000/hello-grain?hello=world
==== Environment: ====
REMOTE_ADDR=127.0.0.1
SERVER_PORT=80
SERVER_PROTOCOL=http
REMOTE_USER=
HTTP_ACCEPT=*/*
X_MATCHED_ROUTE=/hello-grain
SERVER_NAME=localhost:3000
HTTP_USER_AGENT=curl/7.64.1
SCRIPT_NAME=/Users/technosophos/Code/Grain/hello-wagi-grain/hello.gr.wasm
PATH_INFO=/hello-grain
REQUEST_METHOD=GET
AUTH_TYPE=
REMOTE_HOST=127.0.0.1
HTTP_HOST=localhost:3000
QUERY_STRING=
GATEWAY_INTERFACE=CGI/1.1
PATH_TRANSLATED=/hello-grain
SERVER_SOFTWARE=WAGI/1
CONTENT_LENGTH=0
CONTENT_TYPE=
X_FULL_URL=http://localhost:3000/hello-grain
==== Args: ====
/hello-grain
hello=world
```
