# mysqltunnel

A simple wrapper script for running a local mysql client over an SSH tunnel.

1. Creates an SSH tunnel
1. Forwards a random local port to a remote mysqld port
1. Starts a local mysql client on the forwarded port
1. Cleans up afterwards

The simplest usage just mimics the SSH and mysql clients:

	mysqltunnel user@host -u root -p

## HOWTO

Connect to a non-standard SSH port:

	mysqltunnel user@host:port

Connect to a non-standard MySQL port:

	mysqltunnel user@host -P 3307

Tunnel through one SSH server to another MySQL server:

	mysqltunnel user@host -h myhost

Connect to a remote MySQL unix socket:

	mysqltunnel user@host --socket=/var/run/mysqld/mysqld.sock

Use explicit DSN strings for clarity:

	mysqltunnel ssh://user@host[:port] mysql://myuser[:mypass]@myhost[:myport]

Or go to town with separate arguments:

	mysqltunnel -sh host -su user -sP port -h myhost -u myuser -P myport -p[mypass]

## Defaults

### SSH

* Compression is turned on: `-C`
* Agent is forwarded: `-A`
* User defaults to the *local* system $USER
	* Same as SSH client
* When using a user@host DSN the user portion *must* be specified
	* A lone host-name conflicts with a MySQL database name

### MySQL Client

* A sane prompt is set: `mysql $host $database >`
* User defaults to the *local* system $USER
	* Same as MySQL client
