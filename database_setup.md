the following are the steps to set up a MariaDB database from an existing EC2 instance, allowing HTTPS and HTTP traffic from the internet 
1. from your personal command line, ssh into the EC2 instance with the following command
     ssh -i COMP_370.pem ubuntu@3.93.64.75
2. update the server
    sudo apt update
3. install MariaDB database server and start the service
    sudo apt install mariadb-server
    when prompted for use of additional storage, hit Y
    sudo systemctl start mariadb.service
4. configure MariaDB
    sudo mysql_secure_installation
    for the questions that pop up, hit enter, n,n, y, y, y
5. configure the database to run on an external port, firstly by adding an inbound rule to the security group in the EC2 instance
    custom TCP, port 6002, 0.0.0.0/0
6. configure mariadb to listen for port 6002 by the following commands
    sudo vi /etc/mysql/mariadb.conf.d/50-s
erver.cnf
    add port = 6002 in basic settings
    change bind-address to 0.0.0.0
    sudo systemctl restart mysql
7. check that this worked to see the ports
    sudo apt install net-tools
    netstat -tlpn
8. enter MariaDB to create empty database
    sudo mariadb
    create database comp370_test;
9. create user with appropriate permissions in mariadb
    create user 'comp370'@'3.93.64.75' identified by '$ungl@ss3s';
    grant all on comp370_test.* to 'comp370'@'%' identified by '$ungl@ss3s' with grant option;
    flush privileges;
    exit;
10. to check work, download Dbeaver and connect to the ip address of the EC2 on port 6002 with the new username and password. this worked for me!

    


