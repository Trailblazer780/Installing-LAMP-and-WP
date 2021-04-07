# Installing-LAMP-and-WP
This is documentation of installing a LAMP server and deploying Wordpress made by Ethan Farrell
For this documentation we are using Ubuntu 18.04 Server.

# Table of Contents:
1. [Installing LAMP Stack](#Installing-LAMP-Stack)
2. [Setting up the Database](#Setting-up-the-Database)
3. [Downloading Wordpress](#Downloading-Wordpress)
4. [Setting up Wordpress](#Setting-up-Wordpress)


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

The first thing we want to do when getting wordpress is to get the latest version. This link is the download link for the latest version of wordpress: `https://wordpress.org/latest.tar.gz`

After we have that link we can now download wordpress onto our Ubuntu machine via the command line. You will want to be inside of your home directory when you are downloading wordpress. The command that you need to run is: `wget https://wordpress.org/latest.tar.gz` If it downloaded correctly your terminal should look like the screenshot below:

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%207%20Downloading%20Wordpress.PNG)

To check and make sure that the file is there you can preform a long listing of your home directory by simply running the `ll` command. The screenshot below is what should be in your home directory if it downloaded properly.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%208%20Checking%20that%20wordpress%20is%20there.PNG)


## Setting up Wordpress

The first thing we need to do to setup Wordpress is to create a directory that we can put it in. To do this you can run the following command (You can replace the `ethan.nscctruro.ca` with whatever you would like to call your website):

`sudo mkdir /var/www/html/ethan.nscctruro.ca`

After running that command we can now extract the Wordpress files from the latest.tar.gz file. To do this run the following command:
`sudo tar -xvzf latest.tar.gz`

When it is done extracting you can perform a long listing on your home directory and you will now see that wordpress has been extracted. To do this run the following command: `ll`

Your terminal should look like the screenshot below and you should see a wordpress directory.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%209%20Extracted%20wordpress.PNG)

The next step is to move all of the contents inside off that wordpress folder to where you website file is located in the Ubuntu system. To do this run the following command(if you called your directory something else you need to replace the `ethan.nscctruro.ca` with whatever you nameds the directory):

`sudo mv wordpress/* /var/www/html/ethan.nscctruro.ca/`

To confirm that the files moved to that directory properly we can now switch to that directory by running the following command:

`cd /var/www/html/ethan.nscctruro.ca`

Once you have switched the that directory we can now perform a long listing of that directory by running the `ll` command. The screenshot below is what it should look like if all of the files moved to the directory properly.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%2010%20Checking%20wordpress%20moved%20files.PNG)
