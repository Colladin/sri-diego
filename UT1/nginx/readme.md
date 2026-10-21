cat /etc/nginx/sites-available/www.diego.test
server {
    listen 80;
    server_name www.diego.test diego.test;

    root /var/www/www.diego.test;
    index index.html;

    location /admin/ {
        satisfy any;

        allow 127.0.0.1;
        allow 10.3.1.38;
        deny all;

        auth_basic "Zona de Administracion";
        auth_basic_user_file /etc/nginx/passwords/.htpasswd_admin;

        try_files $uri $uri/ /admin/index.html =404;
    }

    location / {
        try_files $uri $uri/ =404;
    }
}

 sudo nano /etc/nginx/sites-available/www.diego.test

server {
    listen 80;
    server_name www.diego.test diego.test;

    root /var/www/www.diego.test;
    index index.html;

    location /admin/ {
        satisfy any;

        allow 127.0.0.1;
        allow 10.3.1.38;
        deny all;

        auth_basic "Zona de Administracion";
        auth_basic_user_file /etc/nginx/passwords/.htpasswd_admin;

        try_files $uri $uri/ /admin/index.html =404;
    }

    location / {
        try_files $uri $uri/ =404;
    }
}




