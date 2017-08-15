# setup-openresty

This is just a small bash script for downloading + installing OpenResty.

It will install OpenResty to `/opt/openresty-${OPENRESTY_VERSION}`, then
creating a symlink at `/opt/openresty`

It also downloads + installs Lua 5.1.5 + LuaRocks into `/opt/openresty/luajit`.
This provides compatibility when installing modules with LuaRocks. For example,
the `lua-cjson` module fails to build with LuaJIT + LuaRocks, which makes it
hard to install rocks like Lapis.

Using Lua + LuaRocks allows rocks to install as normal.

## Compatibility

Tested with Debian Squeeze + Ubuntu 16.04, nothing else, YMMV

## License

MIT license (see LICENSE)
