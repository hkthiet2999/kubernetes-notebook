# HPA
Horizontal Pod Autoscaler là chế độ tự động scale (nhân bản POD) dựa vào mức độ hoạt động của CPU đối với POD, nếu một POD quá tải - nó có thể nhân bản thêm POD khác và ngược lại - số nhân bản dao động trong khoảng min, max cấu hình
Để linh loạt và quy chuẩn, nên tạo ra HPA (HorizontalPodAutoscaler) từ cấu hình file yaml như file [hpa](hpa.yaml) hoặc [hpabeta](hpabeta.yaml) ở trên.

 - `kubectl explain hpa`
 - `kubectl apply -f hpa.yaml`
 - `kubectl get hpa`


_Thực hành dựa trên hướng dẫn của [thetip4you](https://www.youtube.com/watch?v=M2NroN1DYqM&list=PLVx1qovxj-akr_3XqQQgpqRyQw4GYuS4h&index=1&t=508s):_

**Khởi động Kubernetes Cluster và list các file YAML**

![](images/1.png)

`kubectl apply -f deployment.yaml`

![](images/2.png)

`kubectl apply -f hpa.yaml`

![](images/3.png)
