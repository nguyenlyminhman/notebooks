# Label

Trong Kubernetes (K8s), Label là một cơ chế quan trọng để gán các metadata (dữ liệu mô tả) cho các object (đối tượng) trong hệ thống. Các Label có thể được sử dụng để:

**Tổ chức và nhóm các object:** Bạn có thể gán các Label cho các object như Pods, Services, Deployments, etc. để nhóm chúng lại với nhau. Ví dụ: app=frontend, environment=production, team=devops.

**Chọn và lọc object:** Bạn có thể sử dụng các Label để tìm và chọn các object phù hợp. Ví dụ: Tìm tất cả các Pod có Label app=frontend.

**Áp dụng các policy và cấu hình:** Bạn có thể sử dụng các Label để áp dụng các policy, cấu hình hoặc tự động hóa các quá trình. Ví dụ: Tự động triển khai các Pod có Label app=frontend trên các node có Label zone=us-east-1.

**Theo dõi và giám sát:** Bạn có thể sử dụng các Label để nhóm và theo dõi các metrics (số liệu) ở cấp độ object.
Các Label có định dạng "**key=value**" và được gán vào các object thông qua các field như metadata.labels. 

## Ví dụ:

### pod-label.yaml
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: static-web-server
  labels:
    app: frontend
    env: production
    team: devops
spec:
  containers:
    - name: web
      image: nginx
      ports:
        - name: web
          containerPort: 80
          protocol: TCP
```

Trong ví dụ trên, Pod có 3 Label: **app=frontend, env=production và team=devops**.

Chúng ta có thể sử dụng các Label để tìm, lọc và áp dụng các chính sách cho các object trong Kubernetes. Việc sử dụng Label một cách có ý nghĩa và phù hợp là rất quan trọng để quản lý và tổ chức các ứng dụng trong một môi trường Kubernetes phức tạp.

```sh
kubectl get pods -l app=frontend
```
