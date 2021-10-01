# MySQL Port Change

If you are not able to start MySQL service in Xampp, conflicting ports might be the culprit. Some other applications might be using the default MySQL port `3306`. You can find which application is using this port using CMD command: `netstat -ano | findstr 3306`. If you get any result for this command, then the port `3306` is active. You can manually stop it by writing `services.msc` in RUN dialog, finding this service and then finally stopping it. However, this solution is temporary. After every restart, you'll have to manually stop this service. Other option is to change the port of MySQL Xampp from `3306` to something else (like `3308`). Here is how to do it:

Open Xampp.
Stop all the running services.
Go to "config" at top-right corner of the Xampp window, click on "service and port settings", go to "mysql" tab and change the "main port" to `3308` or something else.
Now, in Xampp, click on "config" in the MySQL row (click on MySQL's "config"), and open "my.ini".
"my.ini" will open in notepad. Go to Line 20 (Can be some other line also) and change the port to `3308`. Like this:

`# password = your_password`
`port = 3308`

Also, change the port to `3308` on line 28 of my.ini file, like this:
###### The MySQL server

[mysqld]

`port = 3308`

Save the changes.
Restart the Xampp. You might also have to restart your device.
Now go to C:\xampp\phpMyAdmin (Your directory where Xampp is installed) . Open the "config.inc.php" file.
Below the user, password and extension lines at the top of file(Below line 23), add this line:
`$cfg['Servers'][$i]['port'] = 3308;`

(Other wise this error will occur in while opening "phpmyadmin": (HY000/2002): No connection could be made because the target machine actively refused it.

Save the changes.

Now, you have to mention this new port in your project code :

// After adding the port:

`$conn = mysqli_connect("localhost:3308" , "root" , "", "database_name");`

That’s it.
