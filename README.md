### Installing both Postgresql and PGAdmin using docker

## Purpose

This repository is for my CyberDeck project and is meant to streamline the installation of
both Postgresql and PGAdmin.  This is setup for quick and easy access to pgadmin so you can create additional databases
for other applications like Joplin-Server.

## Features
* Pre-configured pgAdmin: Quick access to pgAdmin with pre-set environment variables and automatic server configuration via entrypoint.sh.
* No pgAdmin Login Page: When accessing pgAdmin, you are automatically logged in with the credentials you set in the .env file.

## Installation

```bash
cd source
git clone https://github.com/mikepaxton/postgres-pgadmin.git
cd postgres-pgadmin
mv .env.exampmle .env
```

Edit the .env file to reflect the needed information for your install.

Next, we need to edit the docker-compose.yml file.

1. Change the directory where you want to store the postgres.db files by modifying volumes:
    * In my case I use /data/postgres_data

Once the changes have been made to both .env and the compose files, we need to start the container.
On first install, I like to start the container without running the container in the background by not passing the -d option.
```bash
docker compose up
```
When the container start you will probably get an error indicating there is no "admin" database.
To fix this go to your browser and enter the pgadmin url.
http://localhost:8110 (or the port you setup)
You should be automatically logged into pgadmin.  On the left, click on the "My Postgres" and then click on "database".
Right click "database" and choose "Create -> Database".
For the database name, enter admin and leave the owner as admin.
Click Save.
This should create the admin database and the error message back in terminal should disappear.

Now, we can stop postgres by typing ctrl+c to cancel the container.
At this point, if everything is working we can restart the containers and leave them running in the background.
```bash
docker compose up -d
```
Both postgres and pgadmin should be up and running.

## Notes

Use the .env file to configure sensitive data such as passwords.

The postgres_data folder permissions will be shown as 999:root.  Leave it as that or postgres will not run.
By default the admin account will not be able to access that directory.  If for some reason you need to get into it
you can either use:

```bash
sudo su
```
When done, type exit to switch back to the admin account.




