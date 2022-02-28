# dos:devopssec
## tools
### nginx
####  Nginx Performance

##### HTTP load-balancing
- upstream backend {
least_conn;
    server 10.10.10.1:80;
    server 10.10.10.2:80;
}
server {
    server_name site.ltd;
    location / {
        proxy_pass http://backend;
        proxy_redirect      off;
        proxy_set_header    Host            $host;
        proxy_set_header    X-Real-IP       $remote_addr;
        proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

##### WordPress Fastcgi cache 
###### put inside a configuration file in /etc/nginx/conf.d/
- -# do not cache xmlhttp requests
map $http_x_requested_with $http_request_no_cache {
    default 0;
    XMLHttpRequest 1;
}
- -# do not cache requests for the following cookies
map $http_cookie $cookie_no_cache {
    default 0;
    "~*wordpress_[a-f0-9]+" 1;
    "~*wp-postpass" 1;
    "~*wordpress_logged_in" 1;
    "~*wordpress_no_cache" 1;
    "~*comment_author" 1;
    "~*woocommerce_items_in_cart" 1;
    "~*woocommerce_cart_hash" 1;
    "~*wptouch_switch_toogle" 1;
    "~*comment_author_email_" 1;
}
- -# do not cache requests for the following uri
map $request_uri $uri_no_cache {
    default 0;
    "~*/wp-admin/" 1;
    "~*/wp-[a-zA-Z0-9-]+.php" 1;
    "~*/feed/" 1;
    "~*/index.php" 1;
    "~*/[a-z0-9_-]+-sitemap([0-9]+)?.xml" 1;
    "~*/sitemap(_index)?.xml" 1;
    "~*/wp-comments-popup.php" 1;
    "~*/wp-links-opml.php" 1;
    "~*/wp-.*.php" 1;
    "~*/xmlrpc.php" 1;
}
- -# do not cache request with args (like site.tld/index.php?id=1)
map $query_string $query_no_cache {
    default 1;
    "" 0;
}
-# map previous conditions with the variable $skip_cache
map $http_request_no_cache$cookie_no_cache$uri_no_cache$query_no_cache $skip_cache {
    default 1;
    0000 0;
} 

###### To put inside another configuration file in /etc/nginx/conf.d
- -# FastCGI cache settings
fastcgi_cache_path /var/run/nginx-cache levels=1:2 keys_zone=WORDPRESS:360m inactive=24h max_size=256M;
fastcgi_cache_key "$scheme$request_method$host$request_uri$cookie_pll_language";
fastcgi_cache_use_stale error timeout invalid_header updating http_500 http_503;
fastcgi_cache_methods GET HEAD;
fastcgi_buffers 256 32k;
fastcgi_buffer_size 256k;
fastcgi_connect_timeout 4s;
fastcgi_send_timeout 120s;
fastcgi_busy_buffers_size 512k;
fastcgi_temp_file_write_size 512K;
fastcgi_param SERVER_NAME $http_host;
fastcgi_ignore_headers Cache-Control Expires Set-Cookie;
fastcgi_keep_conn on;
fastcgi_cache_lock on;
fastcgi_cache_lock_age 1s;
fastcgi_cache_lock_timeout 3s;

###### fastcgi_cache vhost example
- 
    ```
        # pass requests to fastcgi with fastcgi_cache enabled
    location ~ \.php$ {
        try_files $uri =404;
        include fastcgi_params;
        fastcgi_pass php;
        fastcgi_cache_bypass $skip_cache;
        fastcgi_no_cache $skip_cache;
        fastcgi_cache WORDPRESS;
        fastcgi_cache_valid 200 30m;
    }
    # block to purge nginx cache with nginx was built with ngx_cache_purge module
    location ~ /purge(/.*) {
        fastcgi_cache_purge WORDPRESS "$scheme$request_method$host$1";
        access_log off;
    }
    ```


#### Nginx as a Proxy

##### Simple Proxy
- location / {
  proxy_pass http://127.0.0.1:3000;
  proxy_redirect      off;
  proxy_set_header    Host            $host;
  proxy_set_header    X-Real-IP       $remote_addr;
  proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
  }

##### Proxy in a subfolder
- location /folder/ { # The / is important!
  proxy_pass http://127.0.0.1:3000/;# The / is important!
  proxy_redirect      off;
  proxy_set_header    Host            $host;
  proxy_set_header    X-Real-IP       $remote_addr;
  proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
  }

##### Proxy keepalive for websocket
###### e.g. Proxy keepalive for websocket
- 
    ```
    # Upstreams
    upstream backend {
    server 127.0.0.1:3000;
    keepalive 5;
    }
    # HTTP Server
    server {
    server_name your_hostname.com;
    error_log /var/log/nginx/rocketchat.access.log;
    location / {
        proxy_pass http://backend;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forward-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forward-Proto http;
        proxy_set_header X-Nginx-Proxy true;
        proxy_redirect off;
    }
    }
    ```
##### Reverse-Proxy For Apache
- 
    ```
    server {

    server_name domain.tld;

    access_log /var/log/nginx/domain.tld.access.log;
    error_log /var/log/nginx/domain.tld.error.log;

    root /var/www/domain.tld/htdocs;

    # pass requests to Apache backend
    location / {
        proxy_pass http://backend;
    }
    # handle static files with a fallback
    location ~* \.(ogg|ogv|svg|svgz|eot|otf|woff|woff2|ttf|m4a|mp4|ttf|rss|atom|jpe?g|gif|cur|heic|png|tiff|ico|zip|webm|mp3|aac|tgz|gz|rar|bz2|doc|xls|exe|ppt|tar|mid|midi|wav|bmp|rtf|swf|webp)$ {
        add_header "Access-Control-Allow-Origin" "*";
        access_log off;
        log_not_found off;
        expires max;
        try_files $uri @fallback;
    }
    # fallback to pass requests to Apache if files are not found
    location @fallback {
        proxy_pass http://backend;
    }
    }
    ```

#### Nginx Security

##### Denying access
###### common backup and archives files
- location ~* "\.(old|orig|original|php#|php~|php_bak|save|swo|aspx?|tpl|sh|bash|bak?|cfg|cgi|dll|exe|git|hg|ini|jsp|log|mdb|out|sql|svn|swp|tar|rdf)$" {
    deny all;
}
###### Deny access to hidden files & directory
- location ~ /\.(?!well-known\/) {
    deny all;
}

##### Blocking common attacks

###### base64 encoded url
- location ~* "(base64_encode)(.*)(\()" {
    deny all;
}
###### javascript eval() url
- location ~* "(eval\()" {
    deny all;
}


#### Nginx SEO

##### Make a website not indexable
- add_header X-Robots-Tag "noindex";
location = /robots.txt {
  return 200 "User-agent: *\nDisallow: /\n";
}

##### robots.txt location
###### robots.txt
- location = /robots.txt {
    -# Some WordPress plugin gererate robots.txt file
    -# Refer #340 issue
    try_files $uri $uri/ /index.php?$args @robots;
    access_log off;
    log_not_found off;
    }
    location @robots {
    return 200 "User-agent: *\nDisallow: /wp-admin/\nAllow: /wp-admin/admin-ajax.php\n";
    }



#### Nginx Configurations

##### Listen To Port
- 
    ```
    server {
  # Standard HTTP Protocol
  listen 80;

  # Standard HTTPS Protocol
  listen 443 ssl;

  # For http2
  listen 443 ssl http2;

  # Listen on 80 using IPv6
  listen [::]:80;

  # Listen only on using IPv6
  listen [::]:80 ipv6only=on;
}
    ```

##### Access Logging
- 
    ```
    server {
  # Relative or full path to log file
  access_log /path/to/file.log;

  # Turn 'on' or 'off'
  access_log on;
    }

    ```

#####  Domain Name
- 
    ```
    server {
  # Listen to yourdomain.com
  server_name yourdomain.com;

  # Listen to multiple domains
  server_name yourdomain.com www.yourdomain.com;

  # Listen to all domains
  server_name *.yourdomain.com;

  # Listen to all top-level domains
  server_name yourdomain.*;

  # Listen to unspecified Hostnames (Listens to IP address itself)
  server_name "";

    }
    ```
#####  Static Assets
- server {
  listen 80;
  server_name yourdomain.com;
  location / {
          root /path/to/website;
  } 
}

#####  Redirect
- server {
  listen 80;
  server_name www.yourdomain.com;
  return 301 http://yourdomain.com$request_uri;
}

- server {
  listen 80;
  server_name www.yourdomain.com;
  location /redirect-url {
     return 301 http://otherdomain.com;
  }
}

#####  Load Balancing
- 
    ```
    upstream node_js {
  server 0.0.0.0:3000;
  server 0.0.0.0:4000;
  server 123.131.121.122;
    }

    server {
  listen 80;
  server_name yourdomain.com;

  location / {
     proxy_pass http://node_js;
  }
    }

    ```

##### SSL
-  
    ```
        server {
  listen 443 ssl;
  server_name yourdomain.com;

  ssl on;

  ssl_certificate /path/to/cert.pem;
  ssl_certificate_key /path/to/privatekey.pem;

  ssl_stapling on;
  ssl_stapling_verify on;
  ssl_trusted_certificate /path/to/fullchain.pem;

  ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
  ssl_session_timeout 1h;
  ssl_session_cache shared:SSL:50m;
  add_header Strict-Transport-Security max-age=15768000;
    }

    # Permanent Redirect for HTTP to HTTPS
    server {
  listen 80;
  server_name yourdomain.com;
  return 301 https://$host$request_uri;
    }
    ```
#####  [SSL Configuration Generator](https://ssl-config.mozilla.org/) <https://ssl-config.mozilla.org/>
###### nginx 1.17.7, intermediate config, OpenSSL 1.1.1k
- 
    ```
    # generated 2022-02-28, Mozilla Guideline v5.6, nginx 1.17.7, OpenSSL 1.1.1k, intermediate configuration
    # https://ssl-config.mozilla.org/#server=nginx&version=1.17.7&config=intermediate&openssl=1.1.1k&guideline=5.6
    server {
    listen 80 default_server;
    listen [::]:80 default_server;

    location / {
        return 301 https://$host$request_uri;
    }
    }

    server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;

    ssl_certificate /path/to/signed_cert_plus_intermediates;
    ssl_certificate_key /path/to/private_key;
    ssl_session_timeout 1d;
    ssl_session_cache shared:MozSSL:10m;  # about 40000 sessions
    ssl_session_tickets off;

    # curl https://ssl-config.mozilla.org/ffdhe2048.txt > /path/to/dhparam
    ssl_dhparam /path/to/dhparam;

    # intermediate configuration
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384;
    ssl_prefer_server_ciphers off;

    # HSTS (ngx_http_headers_module is required) (63072000 seconds)
    add_header Strict-Transport-Security "max-age=63072000" always;

    # OCSP stapling
    ssl_stapling on;
    ssl_stapling_verify on;

    # verify chain of trust of OCSP response using Root CA and Intermediate certs
    ssl_trusted_certificate /path/to/root_CA_cert_plus_intermediates;

    # replace with the IP address of your resolver
    resolver 127.0.0.1;
    }
    ```


#### Nginx configurations on Linux

##### Nginx config file path:

- /etc/nginx/nginx.conf

The below is the tree structure of /etc/nginx/ (these are the main files and folders we need to learn)

├── nginx.conf
├── sites-available
│ └── default
├── sites-enabled
│ └── default -> /etc/nginx/sites-available/default

open nginx.conf and you may see these two lines on the bottom of config file.

include /etc/nginx/conf.d/*.conf;
include /etc/nginx/sites-enabled/*;
The above 2 lines says include all the config files from the corresponding folders.

sites-available folder is for maintaining a copy of your nginx files, so usually we link sites-available with sites-enabled.


#####  proxying all the request to localhost:4060
- server {
        listen 80;
        server_name thatcoder.space;
        location / {
            proxy_pass http://localhost:4060;
            proxy_redirect     off;
            proxy_set_header   Host $host;
            proxy_set_header   X-Real-IP $remote_addr;
            proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header   X-Forwarded-Host $server_name;
        }
    }
##### To serve static pages or assets:
- location / {
                root /home/user/project-directory-path;
                try_files $uri;
        }
- location ~* \.(js|jpg|txt|ico|json|png|css|xml|html)$ {
                root /home/user/project-directory-path;
        }
- location ~* /_/(.*) {
                alias /home/user/project-directory-path;
                try_files $1.html $1 =404;
        }
- block direct IP serving:
    server {
        listen 80;
        server_name _;
        return 404;
    }                        
##### Cors and Header related
- 
    ```
    #to all domain
    add_header 'Access-Control-Allow-Origin' '*';
    # for specific domain
    #add_header 'Access-Control-Allow-Origin' '*.thatcoder.space';
    add_header 'Access-Control-Allow-Credentials' 'true';

    # to expose location header
    add_header 'Access-Control-Expose-Headers': 'Location';
    add_header 'Access-Control-Allow-Methods' 'GET, POST, PUT, DELETE, OPTIONS';
    add_header 'Access-Control-Allow-Headers' 'Location,Accept,Authorization,Cache-Control,Content-Type';
    ```
##### Gzip configurations
- gzip on;
gzip_disable "msie6";
gzip_vary on;
gzip_proxied any;
gzip_comp_level 6;
gzip_buffers 16 8k;
gzip_http_version 1.1;
gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;
##### For logging and formatting
- log_format timed_combined '$remote_addr - $remote_user [$time_local] '
'"$request" $status $body_bytes_sent '
'"$http_referer" "$http_user_agent" '
'$request_time $upstream_response_time $pipe';
access_log /var/log/nginx/access.log timed_combined;
error_log /var/log/nginx/error.log;
##### To redirect to another domain
- server {
        listen 80;
        server_name request-from.com;
        return 301 https://redirect-to.com/$request_uri;
}
-  location =  /blog/url {
            rewrite /blog/url https://blog.domain.com/url;
        }
- location = /tag/blog/page/2/ {
    return 301 /blog/;
} 
- rewrite /legal /privacy-policy permanent;        



#### references

- https://ssl-config.mozilla.org/
- https://virtubox.github.io/advanced-nginx-cheatsheet/
- https://gist.github.com/carlessanagustin/9509d0d31414804da03b
- https://vishnuch.tech/nginx-cheatsheet
- https://thatcoder.space/nginx-configurations-and-hacks/



