# Server Misconfigurations

## Debugging Enabled

Some servers have debugging mode, which allows attackers to view errors, execute code, debug code, etc.

An indication of enabled debugging mode is that you might see a header like XDEBUG. Every debug library is different, but to connect to XDEBUG, you should open an xdebug listener (chromium has one), and send a GET request to the server like /?XDEBUG\_SESSION\_START=somesessionnameitdoesntmatter. Note that the server will connect to you, not the other way around.

This allows you to change server-side code, and you can get RCE.
