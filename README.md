# WordPress-Assignment
Docker WordPress Site with LEMP Stack on EC2 Ubuntu Server with using Subcommand to Enable/Disable the site.


*Firstly set up a EC2 Ubuntu server and be a root user.Using 
 <sudo su>
 
*Update and Install Docker on your Ubuntu Instance.Using
 <apt-get update -y>
 <apt-get install docker.io>



*Also ensure you have SSH access to your EC2 Ubuntu server .

*Make a repository in GitHub and clone it to the server.
 https://github.com/Pradeepbirmhan/WordPress-Assignment.git

<git clone https://github.com/Pradeepbirmhan/WordPress-Assignment.git>
  
*Now moving to project Directory.
<cd WordPress-Assignment>

*Now creating a new a.env file in the project directory with the following environment variables.

<MYSQL_ROOT_PASSWORD=Pradeepbirmhan
 MYSQL_DATABASE=wordpress
 MYSQL_USER=wordpress_user
 MYSQL_PASSWORD=wordpress_pradeepbirmhan>

*Install Docker Compose on the Instance.
 <sudo apt-get install docker-compose -y>
*Now adding a valid yaml file in docker-compose. using 
<vi docker-compose.yml>  

version: '3.9'

services:
  db:
    image: mysql:5.7
    container_name: db
    environment:
      MYSQL_ROOT_PASSWORD: Pradeepbirmhan
      MYSQL_DATABASE: wordpress_db
      MYSQL_USER: wordpress_user
      MYSQL_PASSWORD: wordpress_pradeepbirmhan
    volumes:
      - dbdata:/var/lib/mysql

  wordpress:
    image: wordpress:latest
    container_name: wordpress
    depends_on:
      - db
    ports:
      - "80:80"
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_NAME: wordpress_db
      WORDPRESS_DB_USER: wordpress_user
      WORDPRESS_DB_PASSWORD: wordpress_password
    volumes:
      - wpdata:/var/www/html

volumes:
  dbdata:
  wpdata:
--------

* Now lets start the WordPress Site with the LEMP stack.
<docker-compose up -d>

*Now to access the WordPress site with a custom domain (example.com), we need to add an entry to the /etc/hosts file on our local machine.
*Now opening the /etc/hosts file with a text editor and adding the following line.
<3.85.125.62   Example.com>
Save the file and close it.

a. Enable the Site
<docker-compose up>

b. Disable the Site
<docker-compose down>


*To stop and remove the Dockerized WordPress site and associated containers, run the following command:
<docker-compose down>

*Also making sure that no other services are running on the ports used by the Docker containers (on port 80, 8081 ,3306)
 to avoid conflicts.


