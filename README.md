This repo is from tutum mysql docker. I have modified it to work with persistent storage on mysql 5.6.
tutum mysql repo: https://github.com/tutumcloud/mysql

For this to work both conf & data directories should be in persitent storage. ex: /master_conf & /master_data directories should be present and should have correct permissions.

Below are some example commands that can be used.

Build docker image as: 

    docker build -t mysql56 tutum_serv/5.6/

Run Master as:

    docker run -d -v /master_conf:/etc/mysql/conf.d -v /master_data:/var/lib/mysql -e MYSQL_USER=user -e MYSQL_PASS=test -e REPLICATION_MASTER=true -e REPLICATION_USER=repl -e REPLICATION_PASS=repl -p 23307:3306 --name mysql56master mysql56

Run Slave as:

    docker run -d -v /slave_conf:/etc/mysql/conf.d -v /slave_data:/var/lib/mysql -e MYSQL_USER=user -e MYSQL_PASS=test -e REPLICATION_SLAVE=true -p 23309:3306 --link mysql56master:mysql mysql56

If anyone can make it work on 5.7 let me know :)
