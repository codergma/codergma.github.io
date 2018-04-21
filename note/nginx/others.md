1. 504 Gateway Timeout error on Nginx + FastCGI (php-fpm)   
```
vim     /etc/php5/fpm/php.ini
max_execution_time = 300

vim    /etc/php5/fpm/pool.d/www.conf
request_terminate_timeout = 300

add fastcgi_read_timeout variable inside our Nginx virtual host configuration:
location ~ .php$ {
root /var/www/sites/nginxtips.com;
try_files $uri =404;
fastcgi_pass unix:/tmp/php5-fpm.sock;
fastcgi_index index.php;
fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
include fastcgi_params;
fastcgi_read_timeout 300;
}

service nginx restart
```

2. 504 Gateway Timeout error using Nginx as Proxy
For Nginx as Proxy for Apache web server, this is what you have to try to fix the 504 Gateway Timeout error:
Add these variables to nginx.conf file:
 proxy_connect_timeout       600;
 proxy_send_timeout          600;
 proxy_read_timeout          600;
 send_timeout                600;
service nginx restart