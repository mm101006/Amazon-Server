# Project: Linux Server

## IP Address

18.216.67.242

## Running Code

1. Open up terminal within Linux Project.

2. In terminal type `vagrant up`.

3. Then type in `ssh grader@18.216.67.242 -p 2200 -i ~/.ssh/Amazon-Server`.

4. A window will pop up asking for the pass-phrase for the key-pair. Use the pass-phrase for the key-pair.

## Site Navigation

1. 18.216.67.242/login -- user is able to login in from here
2. 18.216.67.242/index -- user can view all authors within database
3. 18.216.67.242/index/int:author_id/books/ -- user can view all books by that author
4. 18.216.67.242/index/books -- user can view all books within database
5. 18.216.67.242/index/int:author_id/books/int:book_id/ -- user can view a particular book
6. 18.216.67.242/index/int:author_id/books/edit/int:book_id/ -- user can edit that book
7. 18.216.67.242/index/user/books -- user can view all of their books
8. 18.216.67.242/index/user/authors -- user can view all of their authors
9. 18.216.67.242/index -- if user is not logged in, user can still view all authors and books within database

## Software Used

1. Python 2.7.12
2. Vagrant 1.8.1
3. Apache2
4. postgresql
5. Finger
6. Git
7. Flask
8. sqlalchemy
9. oauth2.0
10. bleach
11. requests
12. libapache2-mod-wsgi
13. PIP
14. virtualenv

## Configuration Files

### Configuration of Ports
1. in terminal log in as user
2. type in `sudo nano /etc/ssh/sshd.config`
3. Change Row below What Ports, IPs and protocols we listen for

### Configuration of User account Passwords
1. in terminal sign into admin account
2. type in `cd /etc/ssh`
3. then `sudo nano sshd_config`
4. scroll down to Password Authentication no change no to yes
5. type in `sudo/etc/init.d/ssh restart`

### Enabling Site
1. in terminal type `sudo nano /etc/apache2/sites-enabled`
2. type in `sudo nano myLibrary.conf`
3. Update serverName to current in use ip address

## Steps Used to complete Project

### Create/Sign up for Server 
1. Sign into Amazon-Light Sail
2. Choose an image of Ubuntu operating system of OS
3. Chose a hostname 

### Signing into Server
1. In a new folder open up a terminal and type in `vagrant init /ubuntu/trusty64`
2. then type in `vagrant up`
3. In LightSail grab the ssh keys and save them in the folder. Renamed to ec2.pem
4. in terminal type in `sudo chmod 400 ec2.pem`
5. then type `ssh -i ec2.pem ubuntu@18.216.67.242 -p 2200`

### Updating Packages
1. in terminal type in `sudo apt-get update`
2. then type in `sudo apt-get upgrade`

### Configuring Ports
1. Deny every Port by typing in to terminal `sudo ufw default deny incoming` and `sudo ufw default allow outgoing`
2. Allow each port by typing in to terminal `sudo ufw allow 2200/tcp`, `sudo ufw allow http`, `sudo ufw allow out 123/udp`, and `sudo ufw allow out 53`
3. Start up firewall by typing in `sudo ufw enable`

*Other useful commands*
sudo ufw status, sudo ufw deny 80./tcp, sudo ufw delete deny 80/tcp

### Adding user and enabling password
1. Open up a terminal
2. Sign into Ubuntu account (admin)
3. Type in `sudo adduser grader` (a password is required)

### Grant sudo access to a user
1. sign in as ubuntu user
2. in terminal type in `sudo usermod -ag sudo grader`
3. then `sudo visudo`
4. below: %sudo All=(All:All) All add % grader All=(All:All) All

###Creating SSH Key Pair
1. generate a key-pair on local machine
2. open terminal fro root of your computer and type in `ssh-keygen /home/home/.ssh/Amazon-Server
enter in passphrase
3. sign in as grader
4. type in terminal `mkdir .ssh`
5. then `touch .ssh/authroized_keys`
6. sign back into grader
7. in terminal type `chmod 700 .ssh`
8. then type `chmod 644 .ssh/authorized_keys`

###Installing PostgreSQL
1. in terminal type in `sudo apt-get install postgresql postgresql-contrib
2. switch over to postgres account by typing in `sudo -i -u postgres`

###Creating a new user and Database in PostgreSQL
1. in terminal type in `createuser --interactive`
2. in terminal type in `createdb grader`
3. connect to database by typing in `sudo -u grader psql`

##Other

###Steps to drop Database
1. sign in as postgres by typing in `sudo -i -u postgres`
2. type in `dropdb grader`

###Deleting database Reset up
1. in terminal type in sudo nano `/etc/apache2/sites-enabled/myLibrary.conf` and type in the new ip address
2. then type in `sudo service apache2 restart`
3. Update the client_secrets.json file with new ip address
4. update the ip address in google console and facebook developer websites

###Running uploader for books to populate database
1. just run books.py 

###Checking for errors on Server
1. in terminal type in `cat /var/log/apache2/error.log`
