# modx

m90833zx
pk6UahD6
<dn>
# (nginx)
sudo apt-get update<p>
sudo apt-get install nginx<p>
sudo apt-get install mysql-server<p>
sudo apt-get install php-fpm php-mysql<p>
sudo apt-get install php-curl<p>
sudo phpenmod curl<p>

sudo chown -R www-data:www-data *<p>
sudo ln -s /etc/nginx/sites-available/server001.ru /etc/nginx/sites-enabled/server001.ru<p>
<dn>
# (503)
location ~ \.php$ {<p>
  fastcgi_pass unix:/tmp/php5-fpm.sock;<p>
  fastcgi_index index.php;<p>
  fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;<p>
  include fastcgi_params;<p>
  fastcgi_read_timeout 300;<p>
}<p>
<dn>
