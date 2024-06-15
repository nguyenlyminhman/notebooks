# Simple Pod

## Định nghĩa
Trong Kubernetes (K8s), một Pod (viết tắt của "Process-Oriented Domain") là đơn vị cơ bản nhất và là khối xây dựng cơ sở của ứng dụng. Một Pod đại diện cho một nhóm các container chạy cùng nhau trên cùng một host, được quản lý và triển khai cùng nhau.

Một Pod trong K8s có các đặc điểm sau:

**Shared Resources:** Các container trong cùng một Pod chia sẻ các tài nguyên như file system, mạng, và không gian bộ nhớ. Điều này cho phép các container trong cùng một Pod có thể giao tiếp với nhau một cách hiệu quả.

**Single IP Address:** Mỗi Pod có một địa chỉ IP duy nhất trong cụm K8s. Các container bên trong Pod có thể giao tiếp với nhau sử dụng localhost.
Scheduling và Deployment: Pods là đơn vị được Kubernetes sử dụng để lập kế hoạch, triển khai và quản lý các ứng dụng.

**Tính khả dụng và Fault Tolerance:** Khi một node trong cụm K8s gặp sự cố, Kubernetes sẽ tự động sắp xếp lại các Pod trên các node khác, đảm bảo tính khả dụng của ứng dụng.

**Container Lifecycle:** Kubernetes quản lý vòng đời của Pod, bao gồm cả việc khởi tạo, thay thế, scale up/down và xóa các Pod.

Mỗi Pod chứa một hoặc nhiều container, và Kubernetes sẽ đảm bảo các container trong cùng một Pod hoạt động như một thực thể duy nhất. Điều này làm cho việc triển khai, quản lý và mở rộng các ứng dụng trở nên dễ dàng hơn.

Tóm lại, Pod là khối xây dựng cơ bản nhất trong Kubernetes, đóng vai trò quan trọng trong việc quản lý và triển khai các ứng dụng phân tán.

## simple-pod.yaml
```yml
apiVersion: v1
# ở đây phiên bản cũ hơn của kubernetes có dạng extensions/v1beta1
kind: Pod
# kind có nhiều loại, Pod, Service, Deployment, ở đây khai báo là Pod,
metadata:
  name: static-web
  # Tên của pod
spec:
  containers:
    - name: web
      image: nginx
      # image của container docker
      ports:
        - name: web
          containerPort: 80
          # port bên trong container
          protocol: TCP
```
