# DNS Tip

Change the A record to the IP that you need to point to.

# OS - Ubuntu

1. Install: 
    ```$ apt-get install certbot```
2. Run this command: (If you need the notification remove the last line)
    ```
    $ certbot certonly \
        -d mydomain.com \
        --noninteractive \
        --standalone \
        --agree-tos \
        --register-unsafely-without-email 
    ```

3. Usually the cert is going to be /etc/letsencrypt/live/domain

4. Configure nginx (usually we can find the configuration file here: /etc/nginx/sites-available/default)
    ```
    server {
        listen 80 default_server;
        return 301 https://$host$request uri;
    }
    
    server {
        listen 443 ssl;
        
        ssl_certificate      /etc/letsencrypt/live/domain/fullchain.pem;
        ssl_certificate_key  /etc/letsencrypt/live/domain/privkey.pem;
        ssl_protocols        TLSv1 TLSv1.1 TLSv1.2;

        root /var/www/html

        index index.html index.htm index.nginx-debian.html;

        location / {
            try_files $uri $uri/ =404;
        }
    }
    ```

5. How to renew, just run this command:
    ```
    $ cert renew
    ```

# Manual Approach:

Follow this link: https://synkre.com/ssl-for-your-website/



    





