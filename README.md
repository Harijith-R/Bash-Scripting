# Bash-WordPress-DB

If you have worked with WordPress, you might have encountered this error, "ERROR ESTABLISHING A DATABASE CONNECTION". 

### Why do you get this error?

Well in short, you are getting this error because WordPress is unable to establish a database connection. Now the reason why WordPress is unable to establish a database connection can vary. It could be that your database login credentials are wrong or have been changed. It could be that your database server is unresponsive. It could be that your database has been corrupted. In our experience, majority of the times this error happens because of some sort of server error however there could be other factors as well.

## Script Usage:

WP-Config.php is probably the single most important file in your entire WordPress installation. This is where you specify the details for WordPress to connect your database. This script just creates a MySQL query which adds a database user and set the password of this user from the wp-config.php file and assign it to the database.

## Sample Usage:

Go to the root directory of wordpress installation and execute the below script to generate the MySQL query.
```
root@server [/home/clearosa/public_html]# for i in `find -iname wp-config.php` ; do j=$(grep 'DB_NAME' $i | awk -F "'" '{print $4}') ; k=$(grep 'DB_USER' $i | awk -F "'" '{print $4}') ;l=$(grep 'DB_PASSWORD' $i | awk -F "'" '{print $4}') ; echo GRANT ALL PRIVILEGES ON $j.* TO $k@"localhost" identified by "'$l'"";" ; done
```
Sample Output:
```
GRANT ALL PRIVILEGES ON kooid.* TO buhaha@localhost identified by 'koppan';
```

### General Usage:
```
root@meow [/home/kooi/public_html]# for i in `find -iname wp-config.php` ; do j=$(grep 'DB_NAME' $i | awk -F "'" '{print $4}') ; k=$(grep 'DB_USER' $i | awk -F "'" '{print $4}') ;l=$(grep 'DB_PASSWORD' $i | awk -F "'" '{print $4}') ; echo GRANT ALL PRIVILEGES ON $j.* TO $k@"localhost" identified by "'$l'"";" ; done
GRANT ALL PRIVILEGES ON kooid.* TO buhaha@localhost identified by 'koppan';
```

Now copy the MySQL query and execute it in MySQL prompt to fix this error.

