# Installing-LAMP-and-WP
This is documentation of installing a LAMP server and deploying Wordpress made by Ethan Farrell
For this documentation we are using Ubuntu 18.04 Server.

# Table of Contents:
1. [Installing LAMP Stack](#Installing-LAMP-Stack)
2. [Setting up the Database](#Setting-up-the-Database)
3. [Downloading Wordpress](#Downloading-Wordpress)


## Installing LAMP Stack

To Install the LAMP stack on Ubuntu you need to run this command below. This command will grab, download, and install all of what is needed to run the LAMP server. Once the installation of all of these is completed you can now move on to the next step of the process of configuring the LAMP server.

`sudo apt install apache2 mysql-server mysql-client php7.4 php7.4-dev php7.4-mysql`
![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%201%20Installing%20the%20Lamp%20Stack.PNG)

## Setting up the Database

The first thing you need to do to set up the database for the lamp server is to run this command: `sudo mysql` so that you can start to configuring things in the database. The below screenshot will show what it should look like if you have accessed the database properly.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%202%20Setting%20Up%20the%20database.PNG)

First we will need to create a user that the database is going to use. To do this run the following command:
`CREATE USER 'wordpress'@'localhost' IDENTIFIED BY 'Password123.';`

If the command was run correctly it should look like the screenshot below. Remember that for the user `wordpress` can be substituted with whatever you want in the command. The password can also be substituted with whatever you would like but if this is going to be a publical;ly acessable server you are going to want a more complex password than what I have used in the example.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%203%20Create%20Database%20user.PNG)

Now that we have created a user that can manage the databases we can now create the database that you are going to use with wordpress later on with this documentation you need to run the following command: 
`CREATE DATABASE wordpressDB;`

If you created the database correctly your terminal should now look like the following screenshot below:

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%204%20Creating%20Database.PNG)

To make sure that the database was created sucessfully run the following command:
`SHOW DATABASES;`

Your terminal should look like the screenshot below and you should see the database you created in the table.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%205%20Show%20Databases.PNG)

After the database has been created we can now go and give the user that we created in the earlier step full access to the database that we have just created. To do this run the following command:
`GRANT ALL PRIVILEGES ON *.* TO 'wordpress'@'localhost';`

If the command was run successfully your terminal should look the screenshot below.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%206%20Grant%20permissions%20to%20DB%20User.PNG)

Now that we have completed the setup of the database and its user we can now go back to our regular terminal and to do this you simply need to run the command: `exit` and you will be brought back to your Ubuntu terminal.


## Downloading Wordpress
