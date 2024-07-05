the following are the steps to set up an Apache webserver from an existing EC2 instance, allowing HTTPS and HTTP traffic from the internet 
1. from your personal command line, ssh into the EC2 instance with the following command
     ssh -i COMP_370.pem ubuntu@3.93.64.75
     enter "yes" when prompted with authenticity 
2. update the server
    sudo apt update
3. install Apache
    sudo apt install apache2
    when prompted for use of additional disk space, enter Y
    sudo systemctl start apache2
4. check that this worked by typing the ip address, 3.93.64.75, into a browser
5. configure apache to listen on port 8008, firstly by adding an inbound rule to the security group in the EC2 instance
    custom TCP, port 8008, 0.0.0.0/0
6. configure apache to listen for port 8008 by the following commands
    sudo nano /etc/apache2/ports.conf
    change the Listen 80 to Listen 8008
    sudo nano /etc/apache2/sites-enabled/000-default.conf
    change the Virtual Host to 8008
7. restart the service and verify by typing the ip address and port into a browser
    sudo service apache2 restart
    in browser: http://3.93.64.75:8008/
8. to access the text file, cd into the directory containing the default html file and create a new txt file
    cd /var/www/html
    sudo vim comp370_hw2.txt
9. check that this works by typing http://3.93.64.75:8008/comp370_hw2.txt in a browser
10. can verify that this works for me! YAY
