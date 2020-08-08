#         M2-Installation
####    prerequisite:
     - apache (web server)
     - php (7.2)
     - mysql (phpMyadmin)

### Step-1 Download Magento from the webiste [ LINK in the Description ]
#### https://magento.com/tech-resources/download

## step-2 Make a magento directory and extract the content there
```
sudo mkdir /var/www/html/codex/
```
```
sudo tar -zxvf ~/Downloads/Magento-CE*.tar.gz -C /var/www/html/codex/
```
## Step-3 Creata a database named Codex (As you want)
## Step-4 Configure the apache2 Virtual host -
```
sudo gedit /etc/apache2/sites-available/codex.conf
 ```
 ### Copy and paste bellow lines in the Conf file
 ```
  <VirtualHost *:80>
   ServerAdmin admin@codex.com
   DocumentRoot /var/www/html/codex/
   ServerName codex.com
   ServerAlias www.codex.com
     <Directory /var/www/html/codex/>
      Options Indexes FollowSymLinks MultiViews
      AllowOverride All
      Order allow,deny
      allow from all
     </Directory>
   ErrorLog ${APACHE_LOG_DIR}/error.log
   CustomLog ${APACHE_LOG_DIR}/access.log combined
 </VirtualHost>
 ```
 ## Step-5 Enable the codex site and Rewrite Module
 ``` 
 sudo a2ensite codex.conf | sudo a2enmod rewrite
 ```
 ## Step-6 Restart the server
 ```
     sudo systemctl restart apache2.service
 ```
 ## Step-7 Run the following commands -

 ```
cd /var/www/html

	ls -al
	groups www-data
	groups $USER
	sudo usermod -G $USER www-data
	sudo chown -R $USER:www-data *
	ls -al
  ```
  ## Step-8 Run the following commands for magento (codex) folder properties

  ```
sudo find . -type d -exec chmod 0770 {} \; -print && sudo find . -type f -exec chmod 0660 {} \; -print
	
sudo find var generated vendor pub/static pub/media app/etc -type f -exec chmod g+w {} \; -print

sudo find var generated vendor pub/static pub/media app/etc -type d -exec chmod g+ws {} \; -print

sudo chown -R :www-data .

sudo chmod u+x bin/magento
```
## Step-9 Restart the server
```
sudo systemctl restart apache2.service
```

        
