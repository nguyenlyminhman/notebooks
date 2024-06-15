# Namespace

Namespace là một cách để chia tách và cô lập các resources trong một cụm K8s. Namespace cung cấp một cách để nhóm và cô lập các đối tượng (objects) như Pods, Services, Deployments, etc.

Một số đặc điểm chính của Namespace trong K8s:

**Phân chia và Cô lập Resources:** Namespace cho phép bạn chia tách các resources như Pods, Services, Deployments, v.v. vào các không gian riêng biệt. Điều này giúp tổ chức và quản lý các ứng dụng, môi trường (dev, staging, prod) hoặc teams trong cùng một cụm K8s

**Scope của Resources:** Các resources như Pods, Services, Deployments, v.v. chỉ tồn tại trong phạm vi của một Namespace cụ thể. Điều này giúp tránh xung đột tên và cô lập các tài nguyên.

**Truy cập và Visibility:** Bạn có thể control quyền truy cập vào các Namespace thông qua các policies như RBAC (Role-Based Access Control). Mỗi Namespace có thể có các users, roles và permissions riêng.

**Resource Quotas:** Bạn có thể thiết lập các resource quota (hạn ngạch tài nguyên) như CPU, RAM, số lượng Pods, v.v. cho từng Namespace để kiểm soát mức sử dụng tài nguyên.

**Networking và Service Discovery:** Kubernetes sẽ tự động cung cấp một private DNS domain trong mỗi Namespace để các resources có thể tìm và kết nối với nhau.

> Mặc định, Kubernetes có một Namespace mặc định là default. Tuy nhiên, bạn nên tạo các Namespace riêng biệt để tổ chức và quản lý các ứng dụng của mình. Ví dụ: dev, staging, prod.

Sử dụng Namespace giúp chúng ta có thể quản lý, cô lập và chia sẻ tài nguyên trong cụm K8s một cách hiệu quả.


apiVersion: v1
# ở đây phiên bản cũ hơn của kubernetes có dạng extensions/v1beta1
kind: Pod
# kind có nhiều loại, Pod, Service, Deployment, ở đây khai báo là Pod,
metadata:
  name: static-web
  # Tên của pod
  labels:
    role: myrole
spec:
  replicas: 2
  # replica ở đây sẽ tạo ra 2 pods luôn luôn chạy, khi một số pods bị down hay chết hay bất kì lý do nào đó.
  # Pod sẽ tự động tạo lại số lượng đã khai báo ở trên.
  containers:
    - name: web
      image: nginx
      # image của container docker
      ports:
        - name: web
          containerPort: 80
          # port bên trong container
          protocol: TCP