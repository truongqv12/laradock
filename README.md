
## HƯỚNG DẪN CÀI ĐẶT

<p>Link tham khảo<p>

<a href="https://kipalog.com/posts/Trien-khai-du-an-laravel-voi-laradock--p-1 "> https://kipalog.com/posts/Trien-khai-du-an-laravel-voi-laradock--p-1 </a>


<p>Clone<p>

```bash
git clone https://github.com/truongqv12/laradock.git
```
<p>config host<p>

```bash
127.0.0.1    hostname
```
<p>tạo file env<p>

```bash
cp env-example .env
```

```bash
Để dự án laravel vào thư mục web cùng cấp với laradock
```

<p>Cấu hình nginx<p>

laravel1 là tên project

```bash
server {

    listen 80 laravel1;
    listen [::]:80 laravel1 ipv6only=on;

    # For https
    # listen 443 ssl default_server;
    # listen [::]:443 ssl default_server ipv6only=on;
    # ssl_certificate /etc/nginx/ssl/default.crt;
    # ssl_certificate_key /etc/nginx/ssl/default.key;

    server_name laravel1.local;
    root /var/www/laravel1/public;
    index index.php index.html index.htm;

    location / {
         try_files $uri $uri/ /index.php$is_args$args;
    }

    location ~ \.php$ {
        try_files $uri /index.php =404;
        fastcgi_pass php-upstream;
        fastcgi_index index.php;
        fastcgi_buffers 16 16k;
        fastcgi_buffer_size 32k;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        #fixes timeouts
        fastcgi_read_timeout 600;
        include fastcgi_params;
    }

    location ~ /\.ht {
        deny all;
    }

    location /.well-known/acme-challenge/ {
        root /var/www/letsencrypt/;
        log_not_found off;
    }

    error_log /var/log/nginx/lararvel1_error.log debug;
    access_log /var/log/nginx/laravel1_access.log;
}
```
<p>Chạy docker compose<p>

```bash
docker-compose up -d nginx mariadb adminer workspace
```

<p>Vào workspace<p>

```bash
docker-compose exec --user=laradock workspace bash
```

## License

[MIT](https://github.com/laradock/laradock/blob/master/LICENSE) © Mahmoud Zalt
