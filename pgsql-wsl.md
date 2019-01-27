# Here are the correct steps in order to set up a local postgresql database server.

- sudo apt install postgresql
- sudo service postgresql start
- sudo su - postgres
- createuser --superuser $USER where $USER is your username
- psql
- \\password \$USER is typed into the psql console to set up your account.
- \\q to exit
- createdb \$USER by convention
- exit and now you can run psql in your own console with your username.
