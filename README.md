# modx

m90833zx
pk6UahD6
# (nginx)
sudo apt-get update<p>
sudo apt-get install nginx<p>
sudo apt-get install mysql-server<p>
sudo apt-get install php-fpm php-mysql<p>
sudo apt-get install php-curl<p>
sudo phpenmod curl<p>

sudo chown -R www-data:www-data *<p>
sudo ln -s /etc/nginx/sites-available/server001.ru /etc/nginx/sites-enabled/server001.ru<p>
server {
        
        listen 80;
        server_name server002.ru www.server002.ru;
        root /var/www/server002.ru/public_html;
        index index.php index.html;
        client_max_body_size 30M;
        
        location / {
                root /var/www/server002.ru/public_html;
                if (!-e $request_filename) {
                        rewrite ^/(.*)$ /index.php?q=$1 last;
                }
        }

        location ~ \.php$ {
                try_files $uri =404;
                fastcgi_split_path_info ^(.+\.php)(.*)$;
                #fastcgi_pass   127.0.0.1:9000;
                fastcgi_index  index.php;
                fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
                include fastcgi_params;
                fastcgi_ignore_client_abort on;
                fastcgi_param  SERVER_NAME $http_host;
                fastcgi_pass unix:/run/php/php7.0-fpm.sock;
                fastcgi_read_timeout 300;
        }

        location ~ /\.ht {
                deny  all;
        }
}
