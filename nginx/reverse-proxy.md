# Reverse proxy

**Reverse proxy** là một máy chủ hoặc ứng dụng hoạt động như một trung gian giữa các máy khách (client) và một hoặc nhiều máy chủ. Reverse proxy nhận các yêu cầu từ các máy khách và chuyển tiếp các yêu cầu đó tới máy chủ thích hợp, sau đó chuyển lại phản hồi từ máy chủ tới các máy khách. Đây là một số lợi ích và ứng dụng của reverse proxy:


```sh
server {
    listen 80;
    listen [::]:80;

    server_name your-server-name;

    location / {
        proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header   Host $host;
        proxy_pass         http://127.0.0.1:8080;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}
```

```
nano  /etc/nginx/sites-available/jenkins
```
```
server {
    listen 80;
    server_name jenkins;

    location / {
        proxy_pass http://localhost:8181;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Forwarded-Port $server_port;

        proxy_redirect off;

        # 👇 Thêm các dòng này để tránh timeout
        proxy_connect_timeout 300;
        proxy_send_timeout 300;
        proxy_read_timeout 300;
        send_timeout 300;

        # (tùy chọn) giữ kết nối ổn định hơn khi Jenkins stream log
        proxy_buffering off;
    }
}
```
```
sudo ln -s /etc/nginx/sites-available/jenkins /etc/nginx/sites-enabled/jenkins
```
```
sudo systemctl reload nginx
```
```
sudo nginx -t
```


