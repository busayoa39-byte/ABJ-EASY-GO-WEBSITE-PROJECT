# ABJ EASY GO — Ubuntu deployment

This is a static front-end demo. It needs no Node.js runtime or database. Sign-in, shopping, airtime, and electricity screens are demo interactions; real accounts, orders, and payments need a secure backend and payment/provider integrations.

## Deploy to Ubuntu with Nginx

1. Copy `index.html` to your Ubuntu server. From this folder on your computer, for example:

   ```bash
   scp index.html YOUR_USER@YOUR_SERVER_IP:/tmp/abj-easy-go.html
   ```

2. SSH to the server and install Nginx, then publish the page:

   ```bash
   sudo apt update
   sudo apt install -y nginx
   sudo mkdir -p /var/www/abj-easy-go
   sudo cp /tmp/abj-easy-go.html /var/www/abj-easy-go/index.html
   sudo chown -R www-data:www-data /var/www/abj-easy-go
   ```

3. Copy `nginx-abj-easy-go.conf` to `/etc/nginx/sites-available/abj-easy-go`, then edit `server_name` to your domain (or use your server IP).

   ```bash
   sudo ln -s /etc/nginx/sites-available/abj-easy-go /etc/nginx/sites-enabled/abj-easy-go
   sudo nginx -t
   sudo systemctl reload nginx
   ```

4. Allow web traffic if UFW is enabled:

   ```bash
   sudo ufw allow 'Nginx Full'
   ```

5. For a domain, point its DNS A record to the server IP. To enable HTTPS after DNS is working:

   ```bash
   sudo apt install -y certbot python3-certbot-nginx
   sudo certbot --nginx -d your-domain.com -d www.your-domain.com
   ```

Replace `YOUR_USER`, `YOUR_SERVER_IP`, and `your-domain.com` with your own values. Do not expose SSH credentials or private keys when asking for help. This package does not configure DNS or change your server directly.
