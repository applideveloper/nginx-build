# nginx-build

[![Build Status](https://drone.io/github.com/cubicdaiya/nginx-build/status.png)](https://drone.io/github.com/cubicdaiya/nginx-build/latest)

`nginx-build` - provides a command to build nginx seamlessly.

## Requirements

 * [wget](https://www.gnu.org/software/wget/) for downloading nginx and external libraries
 * [git](http://git-scm.com/) for downloading 3rd party modules

## Build Support

 * [nginx](http://nginx.org/)
 * [OpenResty](http://www.openresty.com/)
 * [Tengine](http://tengine.taobao.org/)

## Installation

```bash
go get -u github.com/cubicdaiya/nginx-build
```

If you don't have go-runtime, you may download the binary from [here](https://github.com/cubicdaiya/nginx-build/releases).


If you are Mac OS X user, you can use [Homebrew](http://brew.sh/).

```
brew tap cubicdaiya/nginx-build
brew install nginx-build
```

## Quick Start

```bash
nginx-build -d work
cd work/1.9.1/nginx-1.9.1
objs/bin/nginx -V
```

## Custom Configuration

### Configuration for building nginx

`nginx-build` provides a mechanism for customizing configuration for building nginx.
Prepare a configure script like the following.

```bash
#!/bin/sh

./configure \
--sbin-path=/usr/sbin/nginx \
--conf-path=/etc/nginx/nginx.conf \
```

Give this file to `nginx-build` with `-c`.

```bash
$ nginx-build -d work -c configure.example
```

### Embedding ZLIB statically

Give `-zlib` to `nginx-build`.

```bash
$ nginx-build -d work -zlib
```

`-zlibversion` is an option to set a version of ZLIB.

```bash
$ nginx-build -d work -zlib -zlibversion=1.2.8
```

### Embedding PCRE statically

Give `-pcre` to `nginx-build`.

```bash
$ nginx-build -d work -pcre
```

`-pcreversion` is an option to set a version of PCRE.

```bash
$ nginx-build -d work -pcre -pcreversion=8.37
```

### Embedding OpenSSL statically

Give `-openssl` to `nginx-build`.

```bash
$ nginx-build -d work -openssl
```

`-opensslversion` is an option to set a version of OPENSSL.

```bash
$ nginx-build -d work -openssl -opensslversion=1.0.2a
```

### Embedding 3rd-party modules

`nginx-build` provides a mechanism for embedding 3rd-party modules.
Prepare a ini-file below.

```ini
[echo-nginx-module]
form=git
url=https://github.com/openresty/echo-nginx-module.git
rev=v0.57

[ngx_devel_kit]
form=git
url=https://github.com/simpl/ngx_devel_kit
rev=v0.2.19
```

Give this file to `nginx-build` with `-m`.

```bash
$ nginx-build -d work -m modules.cfg.example
```
