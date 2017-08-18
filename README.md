# Webserver with Apache and PHP on Ubuntu

There are 3 versions of PHP:
- PHP 5.3
- PHP 5.5.9
- PHP 7

All 3 Dockerfiles are for development, below you can see the default params:
- display_errors **on**
- error_reporting **22527**
  - You can get the number of error_reporting on [PHP Error Reporting Wizard](http://www.bx.com.au/tools/ultimate-php-error-reporting-wizard)
- date.timezone **America/Sao_Paulo**
- max_execution_time **60**
- max_input_time **120**
- memory_limit **512**
- post_max_size **30M**
- upload_max_filesize **30M**

The port 80 is expose on all Dockerfiles.

# How to use
###### For php 5.3
```
docker run -d -v [host_path]:/var/www -p [host_port]:80 edersondev/php5.3
```

###### For php 5.5 and higher
```
docker run -d -v [host_path]:/var/www/html -p [host_port]:80 edersondev/php[5.5.9 OR 7]
```