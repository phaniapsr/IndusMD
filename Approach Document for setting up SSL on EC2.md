#### Aim: 
      To setup SSL on EC2 environment
###### Step 1:
    Login to ssh/terminal on your server and enable SSL for WebServer(Apache2)
            command: sudo a2enmod ssl
###### Step 2:
     Create the server SSL Key
            command: sudo bash
**_Note 1:_**
  On Ubuntu this changes you to the root user as you cannot access the directory on the next step.
           
          command: cd /etc/ssl/private
          
          command: openssl genrsa -des3 -out indusmdemr.com.key 2048
          
**_Note 2:_**
 
  Make sure its 2048 and not 1024 bit as this would be required later on GoDaddy.
Enter keyphrase {in terminal you need to enter a keyphrase, it is a temporary passcode}

###### Step 3:
Create the CSR (Certificate Service Request) to be entered on GoDaddy
            command : openssl req -new -key indusmdemr.com.key -out indusmdemr.com.csr

###### Step 4:
View the generated CSR and copy. Paste it later to your GoDaddy SSL Certificate Management Tool 

###### Step 5:
Install your certificate gd_bundle.crt and indusmdemr.com.crt to your server. Upload them to the server and  execute the following 
            command : mv gd_bundle.crt /etc/ssl/gd_bundle.crt
            command : mv indusmdemr.com.crt /etc/ssl/certs/indusmdemr.com.crt

###### Step 6:
Edit the default Apache2 values at /etc/apache2/sites-available/default. Create a new virtualhost
NameVirtualHost *:443
DocumentRoot /var/www/
SSLEngine on
SSLOptions +FakeBasicAuth +ExportCertData +StrictRequire
SSLCertificateFile /etc/ssl/certs/indusdmemr.com.crt
SSLCertificateKeyFile /etc/ssl/private/indusmdemr.com.key
SSLCertificateChainFile /etc/ssl/gd_bundle.crt

###### Step 7:
  Make sure Apache2 to listen on port 443, edit the /etc/apache2/ports.conf  and restart Apache
              command : /etc/init.d/apache2 restart
**_Note 3:_**
    
    If all went well you should be able to access https. For EC2 make sure Port 443 is enabled as well on the AWS Console

###### Step 8:
Create an htaccess file and upload to your root www folder
RewriteEngine On
RewriteCond %{SERVER_PORT} 80
RewriteRule ^(.*)$ https://www.indusmdemr.com/$1 [R,L]
By following the above steps one can install the SSL certificate  on EC2 environment
