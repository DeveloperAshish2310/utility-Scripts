Here's a **README** for configuring and troubleshooting the virtual host setup for `ashish.test` on Ubuntu with Apache2:

---

# README: Configure Virtual Host for `ashish.test` on Apache (Ubuntu)

This README explains how to set up a local virtual host for `ashish.test` on your Ubuntu machine using Apache2. Follow these steps to ensure that your virtual host works as expected, accessible both by `localhost` and `ashish.test`.

## 1. Create a Virtual Host Configuration File

Create a virtual host configuration file in `/etc/apache2/sites-available/`.

```bash
sudo nano /etc/apache2/sites-available/ashish.test.conf
```

Add the following content:

```apache
<VirtualHost *:80>
    ServerAdmin admin@ashish.test
    ServerName ashish.test
    DocumentRoot /var/www/ashish.test
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

- Replace `/var/www/ashish.test` with the actual directory path where your site files are stored.

## 2. Enable the Site

After creating the configuration file, enable the new virtual host with the `a2ensite` command:

```bash
sudo a2ensite ashish.test.conf
```

This will create a symbolic link in `/etc/apache2/sites-enabled/` to activate the virtual host.

## 3. Add to `/etc/hosts` File

To ensure that `ashish.test` resolves to your local machine, update your `/etc/hosts` file:

```bash
sudo nano /etc/hosts
```

Add the following line:

```bash
127.0.0.1 ashish.test
```

This step is essential to map `ashish.test` to `localhost` (your local machine).

## 4. Restart Apache

Once the virtual host is set up and the domain is mapped in the hosts file, restart Apache to apply changes:

```bash
sudo systemctl restart apache2
```

## 5. Ensure Document Root Exists

Make sure the document root (`/var/www/ashish.test`) exists and has the right permissions. Create it if it doesn’t exist:

```bash
sudo mkdir -p /var/www/ashish.test
sudo chown -R $USER:$USER /var/www/ashish.test
```

## 6. Access the Site

After completing the setup:
- You can access the site via `http://localhost` (if that's your default Apache root).
- You can also access it via `http://ashish.test` thanks to the `/etc/hosts` configuration.

Both URLs will serve the same local content.

---

## Troubleshooting

- **Error: "Site ashish.test does not exist"**: Ensure the virtual host file is created in `/etc/apache2/sites-available/` and that you enabled the site using `sudo a2ensite ashish.test.conf`.
- **Apache Not Restarting**: If you face issues restarting Apache, check the error logs at `/var/log/apache2/error.log`.
- **File Permission Errors**: Ensure that the document root directory (`/var/www/ashish.test`) has the correct ownership and permissions to allow Apache to serve files.

---

This guide helps set up and troubleshoot a virtual host for `ashish.test` on your local Apache server. For further assistance, consult the Apache documentation or explore specific error logs if needed.


# Add SSL to That Domain

To configure SSL for your local domain ashish.test in Ubuntu using Apache2, follow these steps:

## 1 Install Apache2 and SSL Module

Make sure Apache2 and the SSL module are installed:

```bash
sudo apt update
sudo apt install apache2
sudo a2enmod ssl
```

## 2. Create a Self-Signed SSL Certificate

Since you're using a local domain, you can create a self-signed SSL certificate:

```bash
sudo mkdir /etc/apache2/ssl
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/ashish.test.key -out /etc/apache2/ssl/ashish.test.crt
```

During the openssl command, you'll be asked to enter details for the certificate. For Common Name (CN), make sure to enter ```ashish.test.```

## 3. Configure Apache for SSL

Next, configure Apache to serve your local domain using SSL.

### 3.1 Create a new configuration file or modify your existing virtual host file for ```ashish.test```:


```bash
sudo nano /etc/apache2/sites-available/ashish.test.conf
```

Add the following configuration:

```bash
<VirtualHost *:443>
    ServerName ashish.test
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html/pyapp

    SSLEngine on
    SSLCertificateFile /etc/apache2/ssl/ashish.test.crt
    SSLCertificateKeyFile /etc/apache2/ssl/ashish.test.key

    WSGIDaemonProcess flaskapp_ssl threads=5
    WSGIScriptAlias / /var/www/html/pyapp/app.wsgi
    WSGIApplicationGroup %{GLOBAL}
    
    <Directory /var/www/html/pyapp>
         WSGIProcessGroup flaskapp_ssl
         WSGIApplicationGroup %{GLOBAL}
         Require all granted
    </Directory>

    ErrorLog /var/www/html/pyapp/log/error-ssl.log
    CustomLog /var/www/html/pyapp/log/access-ssl.log combined
</VirtualHost>
```

### 3.2. If you don’t already have a port 80 configuration for ashish.test, you can also add:

```bash
<VirtualHost *:80>
    ServerName ashish.test
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html/pyapp

    Redirect permanent / https://ashish.test/
    
    WSGIDaemonProcess flaskapp threads=5
    WSGIScriptAlias / /var/www/html/pyapp/app.wsgi
    WSGIApplicationGroup %{GLOBAL}
    
    <Directory /var/www/html/pyapp>
         WSGIProcessGroup flaskapp
         WSGIApplicationGroup %{GLOBAL}
         Require all granted
    </Directory>

    ErrorLog /var/www/html/pyapp/log/error.log
    CustomLog /var/www/html/pyapp/log/access.log combined
</VirtualHost>

```

## 4. Enable the New Virtual Host and SSL

Now, enable the new virtual host configuration and the SSL site:

```
sudo a2ensite ashish.test.conf
sudo systemctl restart apache2
```


## Remove Certificate

### 1. Delete the Existing SSL Certificate and Key
Remove the previously created certificate and key files:

```bash
sudo rm /etc/apache2/ssl/ashish.test.crt /etc/apache2/ssl/ashish.test.key
sudo systemctl restart apache2
```