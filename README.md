# modx

#
m90833zx
pk6UahD6


sudo apt-get update<p>
sudo apt-get install nginx<p>
sudo apt-get install mysql-server<p>
sudo apt-get install php-fpm php-mysql<p>

sudo chown -R www-data:www-data *<p>
sudo ln -s /etc/nginx/sites-available/server001.ru /etc/nginx/sites-enabled/server001.ru<p>
  
  
location ~ \.php$ {
  fastcgi_pass unix:/tmp/php5-fpm.sock;
  fastcgi_index index.php;
  fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
  include fastcgi_params;
  fastcgi_read_timeout 300;
}
