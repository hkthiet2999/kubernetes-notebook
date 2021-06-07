# Các kết quả đạt được trong ngày
1. Cài đặt kubenetes cluster trên Docker Desktop
2. Tìm hiểu về Kubenetes Dashboard và K9S để quản lý K8S
`kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-beta6/aio/deploy/recommended.yaml`

`kubectl proxy`


3. Ghi chú một số lệnh cơ bản

`kubectl version --short`: Xem version kubenetes

`kubectl cluster-info`: Xem thông tin cluster

`kubectl get nodes` : Lấy node

`kubectl describe node/docker-desktop` ( node mặc định) : xem info chi tiết

4. ReplicaSet - HPA - Deployment
ReplicaSet là một điều khiển Controller - nó đảm bảo ổn định các nhân bản (số lượng và tình trạng của POD, replica) khi đang chạy.
Chạy ReplicaSet deployment được định nghĩa trong file deployment.yaml và xem các thông tin cơ bản của Node:


Horizontal Pod Autoscaler là chế độ tự động scale (nhân bản POD) dựa vào mức độ hoạt động của CPU đối với POD, nếu một POD quá tải - nó có thể nhân bản thêm POD khác và ngược lại - số nhân bản dao động trong khoảng min, max cấu hình
Để linh loạt và quy chuẩn, nên tạo ra HPA (HorizontalPodAutoscaler) từ cấu hình file yaml như trên.

 - `kubectl explain hpa`
 - `kubectl apply -f hpa.yaml`
 - `kubectl get hpa`


Deployment quản lý một nhóm các Pod - các Pod được nhân bản, nó tự động thay thế các Pod bị lỗi, không phản hồi bằng pod mới nó tạo ra. Như vậy, deployment đảm bảo ứng dụng của bạn có một (hay nhiều) Pod để phục vụ các yêu cầu.

Deployment sử dụng mẫu Pod (Pod template - chứa định nghĩa / thiết lập về Pod) để tạo các Pod (các nhân bản replica), khi template này thay đổi, các Pod mới sẽ được tạo để thay thế Pod cũ ngay lập tức.

Tạo file cấu hình Deployment (yaml) tham khảo API - Deployment API


 - `kubectl apply -f deployment.yaml`
 - `kubectl get deployments`
 - `kubectl get pods`
 - `kubectl get svc`