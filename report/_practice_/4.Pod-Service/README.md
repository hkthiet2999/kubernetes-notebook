# Kubernetes Pods
Khi bạn triển khai ứng dụng thông qua Module 2, Kubernetes tạo ra Pod để lưu trữ phiên bản chạy của ứng dụng của bạn. Một Pod là một khái niệm trừu tượng của Kubernetes, đại diện cho một nhóm gồm một hoặc nhiều ứng dụng containers (ví dụ như Docker hoặc rkt) và một số tài nguyên được chia sẻ cho các containers đó. Những tài nguyên đó bao gồm:

Lưu trữ được chia sẻ, dưới dạng Volumes
Kết nối mạng, như một cluster IP duy nhất
Thông tin về cách chạy từng container, chẳng hạn như phiên bản container image hoặc các ports cụ thể để sử dụng
Một Pod mô phỏng một "máy chủ logic" dành riêng cho ứng dụng và có thể chứa các ứng dụng containers khác nhau được liên kết tương đối chặt chẽ. Ví dụ, một Pod có thể bao gồm cả container với ứng dụng Node.js của bạn cũng như một container khác cung cấp dữ liệu hiển thị bởi webserver của Node.js. Các containers trong một Pod chia sẻ một địa chỉ IP và port space, chúng luôn được đặt cùng vị trí, cùng lên lịch trình, và chạy trong ngữ cảnh được chia sẻ trên cùng một Node.

Pods là các đơn vị nguyên tử trên nền tảng Kubernetes. Khi chúng tôi tạo một kịch bản triển khai (Deployment) trên Kubernetes, kịch bản triển khai đó tạo ra các Pods với các containers bên trong chúng (trái ngược với việc tạo các containers trực tiếp). Mỗi Pod được gắn với Node nơi nó được lên lịch trình, và tiếp tục ở đó cho đến khi chấm dứt (theo chính sách khởi động lại). Trong trường hợp có lỗi ở Node, các Pods giống nhau được lên lịch trình trên các Nodes có sẵn khác trong cluster.

# Service trong Kubernetes

Các POD được quản lý trong Kubernetes, trong vòng đời của nó chỉ diễn ra theo hướng - được tạo ra, chạy và khi nó kết thúc thì bị xóa và khởi tạo POD mới thay thế. ! Có nghĩa ta không thể có tạm dừng POD, chạy lại POD đang dừng ...

Mặc dù mỗi POD khi tạo ra nó có một IP để liên lạc, tuy nhiên vấn đề là mỗi khi POD thay thế thì là một IP khác, nên các dịch vụ truy cập không biết IP mới nếu ta cấu hình nó truy cập đến POD nào đó cố định. Để giải quết vấn đề này sẽ cần đến Service.

Service (micro-service) là một đối tượng trừu tượng nó xác định ra một nhóm các POD và chính sách để truy cập đến POD đó. Nhóm cá POD mà Service xác định thường dùng kỹ thuật Selector (chọn các POD thuộc về Service theo label của POD).

Cũng có thể hiểu Service là một dịch vụ mạng, tạo cơ chế cân bằng tải (load balancing) truy cập đến các điểm cuối (thường là các Pod) mà Service đó phục vụ.

# Thực hành

## Định nghĩa Service trong Kubernetes

- Tạo Nginx pod sử dụng manifest yaml file

- Tạo Service sử dụng Service manifest file và selector.

## 1. 
Khởi động kubernetes cluster, nội dung hai file manifest yaml :

![](images/1.png)


Ta định nghĩa 1 Pod chứa 1 Container `nginxwebport` chạy ở cổng `80` với giao thức `TCP`, Pod này có label app là nginx. Và một Service tương ứng có selector trùng với Pod là `nginx`. type của Service này là NodePort, sử dụng giao thức TCP chạy trên cổng 80 và nodePort là 31050, targetPort đến `nginxwebport` của Pod.

## Chạy các yml trên

`kubectl create -f pod.yml`

![](images/2.png)

` kubectl create -f service.yml`
Dùng lệnh `minikube `, ta sẽ có được url của Service, mở trình duyệt lên và truy cập đến Nginx Server từ url đó, kết quả như sau:

![](images/3.png)

Khi Nginx đang chạy, ta có thể ping tới địa chỉ đó bằng `curl` như sau:

![](images/4.png)
