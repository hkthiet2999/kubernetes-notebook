# Ghi lại các kết quả đạt được trong ngày
### 1. Cài đặt kubenetes cluster trên Docker Desktop
### 2. Tìm hiểu về Kubenetes Dashboard và K9S để quản lý K8S

`kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-beta6/aio/deploy/recommended.yaml`

`kubectl proxy`

### 3. Lệnh kubectl và ghi chú một số lệnh cơ bản 

Lệnh kubectl tương tác với Cluster, cú pháp chính

kubectl [command] [TYPE] [NAME] [flags]
`Trong đó:

[command] là lệnh, hành động như apply, get, delete, describe ...
[TYPE] kiểu tài nguyên như ns, no, po, svc ...
[NAME] tên đối tượng lệnh tác động
[flags] các thiết lập, tùy thuộc loại lệnh`

`kubectl version --short`: Xem version kubenetes

`kubectl cluster-info`: Xem thông tin cluster



### 4. Node

Trong Kubernetes Node là đơn vị nhỏ nhất xét về phần cứng. Nó là một máy vật lý hay máy ảo (VPS) trong cụm máy (cluster). 

- Xem các node trong cluster: ``kubectl get nodes`
- Xem info chi tiết 1 node: `kubectl describe node/docker-desktop` ( node mặc định) 

### 5. POD

Kubernetes không chạy các container một cách trực tiếp, thay vào đó nó bọc một hoặc vài container vào với nhau trong một cấu trúc gọi là POD. Các container cùng một pod thì chia sẻ với nhau tài nguyên và mạng cục bộ của pod.

Pod là thành phần đơn vị (nhỏ nhất) để Kubernetes thực hiện việc nhân bản (replication), có nghĩa là khi cần thiết thì Kubernetes có thể cấu hình để triển khai nhân bản ra nhiều pod có chức năng giống nhau để tránh quá tải, thậm chí nó vẫn tạo ra nhiều bản copy của pod khi không quá tải nhằm phòng lỗi (ví dụ node bị die).

Pod có thể có nhiều container mà pod là đơn vị để scale (có nghĩa là tất cả các container trong pod cũng scale theo) nên nếu có thể thì cấu hình ứng dụng sao cho một Pod có ít container nhất càng tốt.

Cách sử dụng hiệu quả và thông dụng là dùng loại Pod trong nó chỉ chạy một container.
Pod loại chạy nhiều container trong đó thường là đóng gọi một ứng dụng xây dựng với sự phối hợp chặt chẽ từ nhiều container trong một khu vực cách ly, chúng chia sẻ tài nguyên ổ đĩa, mạng cho nhau.

### 6. ReplicaSet - HPA - Deployment

ReplicaSet là một điều khiển Controller - nó đảm bảo ổn định các nhân bản (số lượng và tình trạng của POD, replica) khi đang chạy.
Chạy ReplicaSet deployment được định nghĩa trong file deployment.yaml và xem các thông tin cơ bản của Node:


Horizontal Pod Autoscaler là chế độ tự động scale (nhân bản POD) dựa vào mức độ hoạt động của CPU đối với POD, nếu một POD quá tải - nó có thể nhân bản thêm POD khác và ngược lại - số nhân bản dao động trong khoảng min, max cấu hình
Để linh loạt và quy chuẩn, nên tạo ra HPA (HorizontalPodAutoscaler) từ cấu hình file yaml như file [hpa](hpa.yaml) hoặc [hpabeta](hpabeta.yaml) ở trên.

 - `kubectl explain hpa`
 - `kubectl apply -f hpa.yaml`
 - `kubectl get hpa`


Deployment quản lý một nhóm các Pod - các Pod được nhân bản, nó tự động thay thế các Pod bị lỗi, không phản hồi bằng pod mới nó tạo ra. Như vậy, deployment đảm bảo ứng dụng của bạn có một (hay nhiều) Pod để phục vụ các yêu cầu.

Deployment sử dụng mẫu Pod (Pod template - chứa định nghĩa / thiết lập về Pod) để tạo các Pod (các nhân bản replica), khi template này thay đổi, các Pod mới sẽ được tạo để thay thế Pod cũ ngay lập tức.

Tạo file cấu hình [deployment](deployment.yaml):

 - `kubectl apply -f deployment.yaml`
 - `kubectl get deployments`
 - `kubectl get pods`
 - `kubectl get svc`
