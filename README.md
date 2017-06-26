## Mezzanine + Mysql Master-slave replication + docker
### Prepare
1. one machine for master and one for slave
2. docker & docker-compose
3. open 3306 port
    * `iptables -t filter -A INPUT -p tcp --sport 3306 -j ACCEPT`
    * `iptables -t filter -A OUTPUT -p tcp --dport 3306 -j ACCEPT`
### Installation
1. Clone the project
    * `git clone https://github.com/duck105/mezzanine-docker.git projectdir`
    * `cd projectdir`
    * `git checkout feature/database_slave`
2. Set the local settings (docker-compose.yml)
    * need to set server_id & master's ip
    * master don't need to set MYSQL_MASTER_SERVER
3. Run Docker Compose
    * `docker-compose up`
### Create database & collect static file
1. Run bash interactively in the container
    * `docker exec -it CONTAINER_NAME /bin/bash`
2. command:
    * `python manage.py createdb --noinput`
    * `python manage.py collectstatic --noinput`
### Done
 * Then we have a set of master-slave web service
 * Open the browser and go to http://[master's ip] or http://[slave's ip]
 * Create blog on master's web & check it has been replicated to the slave 
