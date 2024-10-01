# NGINX

## Definition

NGINX (phát âm là "engine-x") là một phần mềm máy chủ web mã nguồn mở, được biết đến với hiệu suất cao và khả năng xử lý đồng thời nhiều kết nối tốt. Ban đầu, NGINX được phát triển để giải quyết vấn đề C10k, tức là xử lý 10.000 kết nối đồng thời. Hiện nay, NGINX không chỉ được sử dụng như một máy chủ web mà còn được sử dụng rộng rãi như một reverse proxy, load balancer, và HTTP cache. Dưới đây là một số tính năng nổi bật của NGINX:

**Hiệu suất cao**: NGINX được thiết kế để xử lý một lượng lớn kết nối đồng thời với tài nguyên phần cứng ít hơn so với các máy chủ web truyền thống như Apache.

**Reverse Proxy**: NGINX có thể hoạt động như một reverse proxy, giúp phân phối tải đến nhiều máy chủ backend khác nhau, cung cấp bảo mật và cân bằng tải.

**Load Balancing**: NGINX hỗ trợ nhiều phương pháp cân bằng tải khác nhau như round-robin, least connections, và IP hash để phân phối yêu cầu đến các máy chủ backend.

**HTTP Cache**: NGINX có thể lưu trữ các tài nguyên tĩnh (như hình ảnh, file CSS/JS) để giảm tải cho máy chủ backend và cải thiện hiệu suất.

**Khả năng mở rộng và tin cậy**: NGINX được biết đến với khả năng mở rộng tốt, dễ cấu hình và vận hành ổn định trong các môi trường yêu cầu hiệu suất cao.

**Hỗ trợ nhiều giao thức**: NGINX hỗ trợ các giao thức HTTP, HTTPS, HTTP/2, và cả giao thức gRPC, giúp nó phù hợp với nhiều loại ứng dụng web khác nhau.

**Cộng đồng và tài liệu**: NGINX có một cộng đồng lớn và nhiều tài liệu hỗ trợ, giúp người dùng dễ dàng học hỏi và triển khai.

Với những tính năng này, NGINX đã trở thành một lựa chọn phổ biến cho nhiều doanh nghiệp và tổ chức trong việc triển khai các ứng dụng web hiệu suất cao và đáng tin cậy.

## Các lệnh cơ bản
#### Start & Stop Nginx trên linux
```sh
sudo systemctl start nginx

sudo systemctl stop nginx
```

#### Kiểm tra trạng thái NGINX
```sh
sudo systemctl status nginx
```

#### Restart lại Nginx Server
```sh
sudo systemctl restart nginx
```

#### Reload lại cái file đã config mà vẫn giữ server hoạt động và nó an toàn hơn restart
```sh
sudo service nginx reload
```

#### Kiểm tra cấu hình trước khi restart or reload
```sh
sudo nginx -t
```
