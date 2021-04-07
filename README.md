# Installing-LAMP-and-WP
This is documentation of installing a LAMP server and deploying Wordpress made by Ethan Farrell
For this documentation we are using Ubuntu 18.04 Server.

# Table of Contents:
1. [Installing LAMP Stack](#Installing-LAMP-Stack)
2. [Setting up the Database](#Setting-up-the-Database)


## Installing LAMP Stack

To Install the LAMP stack on Ubuntu you need to run this command below. This command will grab, download, and install all of what is needed to run the LAMP server. Once the installation of all of these is completed you can now move on to the next step of the process of configuring the LAMP server.

`sudo apt install apache2 mysql-server mysql-client php7.4 php7.4-dev php7.4-mysql`
![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%201%20Installing%20the%20Lamp%20Stack.PNG)

## Setting up the Database

The first thing you need to do to set up the database for the lamp server is to run this command: `sudo mysql` so that you can start to configuring things in the database. The below screenshot will show what it should look like if you have accessed the database properly.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%202%20Setting%20Up%20the%20database.PNG)
