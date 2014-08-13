bash-norman
===========
> A bash script for server layout and webapp management

I got tired of organizing webapps over and over again.  I wanted a simple way to spin up instances of *nix servers without worrying about where things should go.

While I have attempted adherence with standard directory structures and locations, some of the decisions herein may not fit into your standard of choice.

The target platform is `fedora`.  This should be the same for most `REHL` based OS's; however, it is not guaranteed.

## Goals
While these would suffice just fine for a single webapp on a system, they allow for multiple webapps to be installed on the same system as well.

* logging
* safely store ssl certificates and credentials within your repository
* system'less configuration
* init scripts
* run webapps as their own user
* scp based deployments

## Getting Started
1. `scp bootstrap.bash norman.bash root@myserver:~`
2. `ssh root@myserver bootstrap.bash`

You should then be able to deploy webapps to `myserver`!  `norman` will use your system package manager to install packages required by the supported appliances.

## Supported appliances
The following `appliances` are supported:

* nodejs
* nginx
* mongo

## Directories
* `webapps` (`/usr/share/webapps`) - This is where your webapps go.  Webapp directories are named after the `TLD` of the webapp.  For instance, a webapp for `somefoo.com` would have a directory residing in `/usr/share/webapps/somefoo.com`.
* `logging` (`/var/logs/webapps`) - This is where webapp log files go.  Much like `/webapps`, the `TLD` is used herein to store log files I.E. `somefoo.com` would store it's log files in `/var/logs/webapps/somefoo.com`.


## Logging
`stderr` and `stdout` are logged separately and are managed by `logrotate`.  You can add a configuration item for `logrotate` by adding `config/logrotate.conf` to your repository.  Logs are stored in the `logging` directory.

## User accounts
Isolating a running process with the correct user permissions is important.  A user with the name of the `webapp` is created whenever your `webapp` is created I.E. `somefoo.com` would have a username of `somefoo.com`.  Pretty simple.   Your app will run under this account.  The corresponding directories shall be owned by this user and grouped by `nobody`.

Webapp users are permitted to login via ssh keys.  Webapp users are not given passwords.  You can control the ssh keys by adding `config/authorized_keys` to your repository.  This will enable others on your team to have separate ssh keys for deployment.

## Deployment
Deploying a webapp is as simple as uploading a `.tar.gz` file to the `webapps` directory.  For instance, if you were to `scp somefoo.com.tar.gz myServer:/usr/share/webapps`, `norman` would notice and set everything up.
