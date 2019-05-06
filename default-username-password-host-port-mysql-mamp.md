# What is the default username, password, host and port for MySQL on MAMP?

The default username and password for MySQL on MAMP (and other details) are the following:

* Hostname: `127.0.0.1`
* Username: `root`
* Password: `root`
* Port: `8889`

You can see the [MAMP start page here](http://localhost:8888/MAMP/?language=English) which will show you these details as well.

### How do I change the default password in MAMP MySQL?

On a Mac, you can change your MySQL password on MAMP with the following command:

```shell
/Applications/MAMP/Library/bin/mysqladmin -u root -p password newpassword
```
