# setup-openresty

This is just a small bash script for downloading + installing OpenResty.

It will install OpenResty to `/opt/openresty-${OPENRESTY_VERSION}` (or to a prefix
of your choosing). It can use it's own copy
of LibreSSL or OpenSSL. For other libraries (like zlib and PCRE), it will use your system libraries.

It also downloads and installs Lua 5.1.5 + LuaRocks into `/opt/openresty-${OPENRESTY_VERSION}/luajit`.
This provides compatibility when installing modules with LuaRocks. For example,
the `lua-cjson` module fails to build with LuaJIT + LuaRocks, which makes it
hard to install rocks like Lapis.

If your system has `update-alternatives`, then it will
add `/opt/openresty-${OPENRESTY_VERSION}/luajit/bin/lua` as an alternative for `/usr/bin/lua`,
and `/opt/openresty-${OPENRESTY_VERSION}/luajit/bin/luac` as an alternative for `usr/bin/luac`.

You can pass options to the script to enable/disable features - they mostly
follow the OpenResty configure script options, with a few changes:

* You can get pretty sloppy with dashes vs underscores. All these
  accomplish the same thing
  * `--with-http_dav_module`
  * `--with-http-dav_module`
  * `--with_http_dav_module`
* You can get pretty sloppy about having the `_module` in your command line,
so these also all do the same thing:
  * `--with-http_dav`
  * `--with-http-dav`
* There's a few extra options for enabling some 3rd-party nginx modules not included with OpenResty
  * `--with-stream-echo` -- enables [echo in TCP connections](https://github.com/openresty/stream-echo-nginx-module)
  * `--with-rtmp` - enables [rtmp](https://github.com/arut/nginx-rtmp-module)
  * `--with-nchan` - enables [nchan](https://github.com/slact/nchan)
  * `--with-ngx-lua-ipc` - enables [ngx_lua_ipc](https://github.com/slact/ngx_lua_ipc)
  * `--with-flv` - enables [ngx-http-flv](https://github.com/winshining/nginx-http-flv-module), a fork of the rtmp module
  * `--with-lua-io` - enables [lua-io-nginx-module](https://github.com/tokers/lua-io-nginx-module)
* Choosing the SSL implementation can be accomplished a few ways:
  * `--use-libressl` - (default) use a self-contained LibreSSL build
  * `--use-libressl=x.x.x` - use a self-contained LibreSSL build, with a specific version
  * `--use-openssl` - use a self-contained OpenSSL build
  * `--use-openssl=x.x.x` - use a self-contained OpenSSL build, with a specific version
  * `--use-system-ssl` - use your default SSL implementation.
* You can also pass `--minimal` to disable all non-essential modules/features (`http` is still enabled, though),
then use `--with-(x)` to explicitly enable the features/modules you want
* Alternatively, you can pass `--large` to enable all the modules/features, *except* the drizzle, iconv, and postgres
modules. You'll still need to use `--with-iconv` etc to use those.
* `--prefix=/some/path` - change the prefix from the default `/opt/openresty-${OPENRESTY_VERSION}` to some other path
* `--symlink` This will create symlinks under `/usr/local/bin` for convenience:
  * `/usr/local/bin/lua-openresty      -> /opt/openresty-${OPENRESTY_VERSION}/luajit/bin/lua`
  * `/usr/local/bin/luac-openresty     -> /opt/openresty-${OPENRESTY_VERSION}/luajit/bin/luac`
  * `/usr/local/bin/luajit-openresty   -> /opt/openresty-${OPENRESTY_VERSION}/luajit/bin/luajit`
  * `/usr/local/bin/luarocks-openresty -> /opt/openresty-${OPENRESTY_VERSION}/luajit/bin/luarocks`
  * `/usr/local/bin/openresty      -> /opt/openresty-${OPENRESTY_VERSION}/bin/openresty`
  * `/usr/local/bin/opm            -> /opt/openresty-${OPENRESTY_VERSION}/bin/opm`
  * `/usr/local/bin/resty          -> /opt/openresty-${OPENRESTY_VERSION}/bin/resty`
  * `/usr/local/bin/restydoc       -> /opt/openresty-${OPENRESTY_VERSION}/bin/restydoc`
  * `/usr/local/bin/restydoc-index -> /opt/openresty/bin/restydoc-index`

## Compatibility

All these distros were tested via Docker:

* Debian Wheezy (7)
* Debian Jessie (8)
* Debian Stretch (9)
* Ubuntu Precise (12.04)
* Ubuntu Trusty (14.04)
* Ubuntu Xenial (16.04)
* CentOS 7
* Fedora 25
* Fedora 26
* Alpine 3.5
* Alpine 3.6
* OpenSUSE 42.3

## License

MIT license (see LICENSE)
