# Setup pi with Ubuntu

To set up your Raspberry Pi with Ubuntu Server for hosting brochureware websites (static websites without a database), you can follow these steps to install and configure the necessary software components. Since your websites are predominantly static, you don't need complex setups like databases or backend frameworks. Here's what you'll need:

### 1. **Web Server Software**
You need a web server to serve your static HTML, CSS, and JavaScript files. The two most popular web servers are:

- **Apache HTTP Server** (`apache2`)
- **Nginx** (`nginx`)

Both are excellent choices, but Nginx is often preferred for its lightweight nature and better performance under high loads. However, Apache is more feature-rich out of the box.

#### To Install Nginx:
```bash
sudo apt update
sudo apt install nginx
```

#### To Install Apache:
```bash
sudo apt update
sudo apt install apache2
```

After installation, you can check if the web server is running by visiting `http://<your-raspberry-pi-ip>` in your browser. You should see the default welcome page.

### 2. **Firewall Configuration**
Ensure that your firewall allows HTTP (port 80) and HTTPS (port 443) traffic.

#### For UFW (Uncomplicated Firewall):
```bash
sudo ufw allow 'Nginx Full'   # If using Nginx
# OR
sudo ufw allow 'Apache Full'  # If using Apache
sudo ufw enable
```

### 3. **SSL/TLS Encryption (Optional but Recommended)**
Even though your sites are brochureware, it’s good practice to secure them with HTTPS. You can use **Let's Encrypt** to obtain free SSL certificates.

#### Install Certbot for Nginx:
```bash
sudo apt install certbot python3-certbot-nginx
```

#### Install Certbot for Apache:
```bash
sudo apt install certbot python3-certbot-apache
```

#### Obtain SSL Certificate:
For Nginx:
```bash
sudo certbot --nginx
```

For Apache:
```bash
sudo certbot --apache
```

Certbot will guide you through the process of obtaining and installing the SSL certificate.

### 4. **Hosting Multiple Websites (Virtual Hosts)**
If you want to host multiple websites on the same server, you’ll need to set up virtual hosts.

#### For Nginx:
1. Create a new configuration file for each site in `/etc/nginx/sites-available/`.
   ```bash
   sudo nano /etc/nginx/sites-available/example.com
   ```
2. Add the following configuration (adjust paths as needed):
   ```nginx
   server {
       listen 80;
       server_name example.com www.example.com;

       root /var/www/example.com;
       index index.html;

       location / {
           try_files $uri $uri/ =404;
       }
   }
   ```
3. Enable the site by creating a symbolic link:
   ```bash
   sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/
   ```
4. Test the configuration and restart Nginx:
   ```bash
   sudo nginx -t
   sudo systemctl restart nginx
   ```

#### For Apache:
1. Create a new configuration file for each site in `/etc/apache2/sites-available/`.
   ```bash
   sudo nano /etc/apache2/sites-available/example.com.conf
   ```
2. Add the following configuration:
   ```apache
   <VirtualHost *:80>
       ServerName example.com
       ServerAlias www.example.com
       DocumentRoot /var/www/example.com

       <Directory /var/www/example.com>
           Options Indexes FollowSymLinks
           AllowOverride All
           Require all granted
       </Directory>

       ErrorLog ${APACHE_LOG_DIR}/error.log
       CustomLog ${APACHE_LOG_DIR}/access.log combined
   </VirtualHost>
   ```
3. Enable the site and reload Apache:
   ```bash
   sudo a2ensite example.com.conf
   sudo systemctl reload apache2
   ```

### 5. **File Storage for Websites**
Create directories for each website under `/var/www/`.

For example:
```bash
sudo mkdir -p /var/www/example.com
sudo chown -R $USER:$USER /var/www/example.com
```

Place your website files (HTML, CSS, JS) in the respective directories.

### 6. **Domain Name and DNS Configuration**
If you have domain names for your websites, you’ll need to point them to your Raspberry Pi's IP address. This is done via your domain registrar's DNS settings.

- Set an **A record** pointing to your Raspberry Pi's public IP.
- If you're behind a router, ensure port forwarding is set up for ports 80 (HTTP) and 443 (HTTPS).

### 7. **Optional: Monitoring and Logging**
You may want to monitor your server's performance and log access to your websites.

- **Log Files**: Both Nginx and Apache store logs in `/var/log/`. Check these regularly for errors or unusual activity.
- **Monitoring Tools**: You can install tools like `htop` for system monitoring or `GoAccess` for real-time web log analysis.

#### Install GoAccess:
```bash
sudo apt install goaccess
```

Run GoAccess on your log files:
```bash
sudo goaccess /var/log/nginx/access.log -o /var/www/html/report.html --log-format=COMBINED --real-time-html
```

You can then view the report at `http://<your-raspberry-pi-ip>/report.html`.

---

### Summary of Components Installed:
1. **Web Server**: Nginx or Apache
2. **Firewall**: UFW (optional)
3. **SSL/TLS**: Certbot for Let's Encrypt certificates
4. **Virtual Hosts**: Configured for multiple websites
5. **Static File Hosting**: Directories under `/var/www/`
6. **DNS**: Point your domain to your Raspberry Pi's IP
7. **Optional Monitoring**: GoAccess or other tools

This setup should be sufficient for hosting static brochureware websites on your Raspberry Pi running Ubuntu Server.
