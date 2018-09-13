# PHP7 + Xdebug in PhpStorm Guide

Really short guide to setup php7's built in server + xdebug to work with PhpStorm on windows. No XAMPP, no extra stuff, only the things you really need.

1. Install PhpStorm
2. Install php7.x (https://windows.php.net/download#php-7.2) in `c:\php` (or whatever)
3. Go to `c:\php` and rename php.ini-development to `php.ini`
4. Add `c:\php` to PATH env var.
5. Exec `php -i > info.txt` and copy/paste it here (https://xdebug.org/wizard.php)
6. Download xdebug extension file from step 5 result and place it in `c:\php\ext`
7. Add this at the bottom of your `php.ini`
```
[Xdebug]
zend_extension=c:\php\ext\php_xdebug-(whatever version it is).dll
xdebug.remote_autostart=1
xdebug.remote_enable=1
xdebug.remote_port="9000"
xdebug.remote_host="localhost"
xdebug.profiler_enable=1
xdebug.profiler_output_dir="C:\php\tmp"
xdebug.idekey=PHPSTORM
```
8. Start PhpStorm and go to Settings -> Languages & Frameworks -> PHP
9. Add a new CLI interpreter and use your path (`c:\php\php.exe` in this case). Click on validate and you´ll see your configuration path (`c:\php\php.ini`) and your current xdebug version (you dont need to add any more info here)
10. Create a new project with simple index.php with a few lines to test
11. In the topbar, click on Edit configurations and add a new PHP Built-in Web Server. You can use localhost as host and the `/public` folder as Document Root.
12. In the same topbar, click on the telephone icon to start listening xdebug stuff and run your newly created server.
13. Add a breakpoint somewhere in your index.php and try to access localhost in your browser.
14. Voila!

## (Optional) PHP Code Sniffer configuration ##

1. Install composer. You can download the exe in https://getcomposer.org/ or directly in PhpStorm -> Settings -> Languages & Frameworks -> PHP -> Composer and download composer.phar in your project directory or maybe in c:\php.
2. Run "composer global require squizlabs/php_codesniffer" in cmd or add the following if you want it at project level.
```
"require-dev": {
  "squizlabs/php_codesniffer": "3.*"
}
```
3. Go to Settings -> Languages & Frameworks -> PHP -> Code Sniffer and click on the three dots button to add a new configuration.
4. In the path look for your global or local composer path and check \vendor\bin\phpcs.bat (use the .bat in windows). The validate button should return a green message.
5. Go to Settings -> Editor -> Inspections -> PHP and you'll see PHP Code Sniffer validator and PHP Mess Detector validation, check both (I usually also change the severity to Warning).
6. (Optional) You can (should) select PSR-2 as Coding standard in php-cs. If is not in the list, click on refresh button.

## (Optional) MySQL configuration ##

This php configuration works great with sqlite databases, but for some projects MySQL is a must. Here you can find an easy way to make it work in PhpStorm without any service instalation on your poor windows machine.

1. Download the latest mysql zip version (`mysql-8.0.12-winx64.zip`) from here https://dev.mysql.com/downloads/mysql/.
2. Unzip it in `c:\mysql` or whatever.
3. Create `c:\mysql\data` folder and run `mysqld --initialize-insecure`.
4. After data files creation, run `mysql -uroot` and then `SET PASSWORD FOR 'root'@'localhost' = PASSWORD('MyNewPass');` to change your root password to whatever you want.
5. Create a file in `c:\mysql\bin\mysqldstart.bat` with this content:
```
@ECHO OFF
start c:\mysql\bin\mysqld --console
```
6. Start PhpStorm and, in the topbar, click on Edit configurations to edit the PHP Built-in Web Server configuration we created before.
7. Add a new external tool with the green plus symbol and just put a name and `c:\mysql\bin\mysqldstart.bat` in the program field.
8. Save your changes and voila, every time you start the PHP Built-in Web Server the mysql service will also start. Remember to close it if you want to restart your server.
9. (Optiona) You can also add your local mysql database as Data Source in PhpStorm to administrate it, this way you dont need to install phpmyadmin/adminer/etc.

