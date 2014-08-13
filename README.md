bash-norman
===========
> A bash script for server layout and webapp management

I got tired of organizing webapps over and over again.  I wanted a simple way to spin up instances of *nix servers without worrying about where things should go.

While I have tried to stick with standard directory structures and locations, some of the decisions herein may not fit into a particular standard.

The target platform is `fedora`.  This should be the same for most `REHL` based OS's; however, it is not guaranteed.

## Goals
* logging
* safely store ssl certificates and credentials within your repository
* config
* init scripts
* focus on config at the app level, not at the system level

## System Requirements
Support for the following `appliances` shall be supported:

* nodejs
* nginx

## Directories
* `webapps` (`/usr/share/webapps`) - This is where your webapps go.  Webapp directories are named after the `TLD` of the webapp.  For instance, a webapp for `somefoo.com` would have a directory residing in `/usr/share/webapps/somefoo.com`.
* `logging` (`/var/logs/webapps`) - This is where webapp log files go.  Much like `/webapps`, the `TLD` is used herein to store log files I.E. `somefoo.com` would store it's log files in `/var/logs/webapps/somefoo.com`.


## Logging
`stderr` and `stdout` are logged separately and are managed by `logrotate`.  You can add a configuration for item for `logrotate` by adding `config/logrotate.conf` to your repository.  Logs are stored in the `logging` directory.
