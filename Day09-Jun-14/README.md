# Thực hành trên máy  local

# Lab 1: Launch Single Node Kubernetes Cluster - minikube start
### Step 1, 2: Khởi động Minikube và Xem thông tin Kubernetes Cluster

Cài đặt dựa trên hướng dẫn của minikube.

Khởi động cluster bằng cách chạy lệnh minikube start với driver là Docker: `minikube start --driver=docker`

Ta có thể tương tác với Kubernetes Cluster bằng cách sử dụng kubectl CLI. Đây là cách tiếp cận chính được sử dụng để quản lý Kubernetes và các ứng dụng chạy trên cùng Kubernetes Cluster.

Để xem thông tin chi tiết của Kubernetes Cluster, ta chạy lệnh: `kubectl cluster-info`

Để xem thông tin tất cả các node trong cluster: `kubectl get nodes`

![](images/lab1_1.png)

### Step 3: Interact with your cluster
If you already have kubectl installed, you can now use it to access your shiny new cluster.

`kubectl get po -A`. Kết quả như sau:

![](images/lab1_2.png)

Ban đầu, một số dịch vụ chẳng hạn như trình cung cấp bộ nhớ, có thể chưa ở trạng thái Đang chạy. Đây là tình trạng bình thường trong quá trình khởi động cụm và sẽ tự giải quyết trong giây lát. Để có thêm thông tin chi tiết về trạng thái cụm của bạn, minikube đóng gói Bảng điều khiển Kubernetes, cho phép bạn dễ dàng làm quen với môi trường mới của mình:

![](images/lab1_3.png)

### Step 4 - Deploy Containers
![](images/lab1_4.png)

![](images/lab1_5.png)


