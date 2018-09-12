# php7-xdebug-phpstorm-guide
Short guide to setup php7's built in server + xdebug to work with PhpStorm on windows

(WIP)

1. Install PhpStorm
2. Install php7.x (https://windows.php.net/download#php-7.2) in c:\php (or whatever)
3. Go to c:\php\ and rename php.ini-development to php.ini
4. Add c:\php to PATH env var.
5. Exec php -i > info.txt and copy/paste it here (https://xdebug.org/wizard.php)
6. Download xdebug extension file from step 5 result and place it in c:\php\ext
7. Add this to your php.ini 
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
8. Open PhpStorm and open Settings -> Languages & Frameworks -> PHP
9. Add a new CLI interpreter and use your path (c:\php\php.exe). Click on validate and you´ll see your configuration path (c:\php\php.ini) and your current xdebug version (you dont need to add any more info here)
10. Create a new project with simple index.php with a few lines to test
11. In the topbar, click on Edit configurations and add a new PHP Built-in Web Server. You can use localhost as host and the /public folder as Document Root.
12. In the same topbar, click on the telephone icon to start listening xdebug stuff and run your newly created server.
13. Add a breakpoint somewhere in your index.php and try to access localhost in your browser.
14. Voila!

Optional PHP Code Sniffer configuration
