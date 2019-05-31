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
#(GIT)
        git status
        git add %file_path%
        git commit -m "%commit_message%"
        git push origin master
        

sudo chown -R www-data:www-data *<p>
sudo ln -s /etc/nginx/sites-available/server001.ru /etc/nginx/sites-enabled/server001.ru<p>
CREATE DATABASE newdb_name CHARACTER SET utf8 COLLATE utf8_general_ci;<p>
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

Nginx{
        user www-data;
        worker_processes auto;
        pid /run/nginx.pid;

        events {
        worker_connections 768;
        # multi_accept on;
        }

        http {

                ##
                # Basic Settings
                ##

                sendfile on;
                tcp_nopush on;
                tcp_nodelay on;
                keepalive_timeout 650;
                types_hash_max_size 2048;
                # server_tokens off;

                # server_names_hash_bucket_size 64;
                # server_name_in_redirect off;

                include /etc/nginx/mime.types;
                default_type application/octet-stream;

                ##
                # SSL Settings
                ##

                ssl_protocols TLSv1 TLSv1.1 TLSv1.2; # Dropping SSLv3, ref: POODLE
                ssl_prefer_server_ciphers on;
                ##
                # Logging Settings
                ##

                access_log /var/log/nginx/access.log;
                error_log /var/log/nginx/error.log;

                ##
                # Gzip Settings
                ##

                gzip on;
                gzip_disable "msie6";

                # gzip_vary on;
                # gzip_proxied any;
                # gzip_comp_level 6;
                # gzip_buffers 16 8k;
                # gzip_http_version 1.1;
                # gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;
               ##
                # Virtual Host Configs
                ##

                include /etc/nginx/conf.d/*.conf;
                include /etc/nginx/sites-enabled/*;
        }
        #mail {
        #       # See sample authentication script at:
        ## http://wiki.nginx.org/ImapAuthenticateWithApachePhpScript
        #
        #       # auth_http localhost/auth.php;
                #       # pop3_capabilities "TOP" "USER";
        #       # imap_capabilities "IMAP4rev1" "UIDPLUS";
        #
        #       server {
        #               listen     localhost:110;
        #               protocol   pop3;
        #               proxy      on;
        #       }
        #
        #       server {
        #               listen     localhost:143;
        #               protocol   imap;
        #               proxy      on;
        #       }
        #}




}
