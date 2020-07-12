# Notes on 00_how_to_docker

## 12

Port 3306 is the default port for the MySQL Protocol (see [docs](https://dev.mysql.com/doc/mysql-port-reference/en/mysql-ports-reference-tables.html)).

If using MySQL >= 8.0 with older PHP releases, set MySQL Server's default password plugin to *mysql_native_password* as suggested [in PHP docs](https://www.php.net/manual/en/ref.pdo-mysql.php), [on Github](https://github.com/docker-library/mysql/issues/454) and [in Oracle docs](https://docs.oracle.com/cd/E17952_01/mysql-8.0-en/upgrading-from-previous-series.html). Can be done inline with *--default-authentication-plugin=mysql_native_password*

## 14

*--link* flag [is said to be a legacy feature](https://docs.docker.com/network/links/), so to connect [specify the hostname and port with WORDPRESS_DB_HOST](https://hub.docker.com/_/wordpress/) along with the password in WORDPRESS_DB_PASSWORD and the username in WORDPRESS_DB_USER (if it is something other than root).

## 19

Minimal Flask app - from Flask [quickstart guide](https://flask.palletsprojects.com/en/1.1.x/quickstart/).

Wiser to use *printf* instead of *echo*, as different implementations of *echo* differ on how they handle newlines.

>its /root folder will be bound to a HOME folder on your host

can mean different things. My opinion is that */root* folder of Abathur container should be bound to */home* directory of Char machine, hence using *scp* to copy hello.py there. On the other hand, VirtualBox driver on Linux seems to automount */hosthome* folder with user home folder and *lost+found* inside (different for [other drivers and OS](https://access.redhat.com/documentation/en-us/red_hat_container_development_kit/3.0/html/getting_started_guide/host-folders)).

## 22

Using Go templates to extract manager's address from *docker info* results. On Go templates: [intro](https://blog.container-solutions.com/docker-inspect-template-magic), [official docs](https://golang.org/pkg/text/template/).

First looked up the fields in a full json with `--format='{{json .}}'` (hinted in [docker docs](https://docs.docker.com/config/formatting/#hint)), then used `{{with (index .Swarm.RemoteManagers 0)}}{{.Addr}}{{end}}`. That is: `index .Swarm.RemoteManagers 0` sets context to the first element of `.Swarm.RemoteManagers` array, `{{with (...)}} something {{end}}` sets the context to `...` and executes `something`.

## 24

The dockerhub RabbitMQ image [docs](https://hub.docker.com/_/rabbitmq/) ask to specify a *--hostname*.
