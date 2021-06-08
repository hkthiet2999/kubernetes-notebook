Học cách khởi động Kubernetes Cluster bằng Kubeadm.

Kubeadm giải quyết vấn đề xử lý cấu hình mã hóa TLS (TLS encryption configuration), triển khai các thành phần Kubernetes cốt lõi và đảm bảo rằng các Nodes có thể dễ dàng tham gia vào Cluster. Một Cluster tạo bởi Kubedm được bảo mật thông qua các cơ chế như RBAC.

Thông tin chi tiết về Kubeadm tại https://github.com/kubernetes/kubeadm

## Step 1 - Initialise Master
Sau khi cài đặt Kubedm, ta có các Packages có sẵn như Ubuntu 16.04+, CentOS 7 hoặc HypriotOS v1.0.1 +.

Giai đoạn đầu tiên của quá trình khởi tạo Cluster là khởi chạy Node `Master`. Master chịu trách nhiệm chạy  control plane components, etcd và API Server. Clients sẽ giao tiếp với API để lên lịch khối lượng công việc và quản lý trạng thái của Cluster.

Lệnh dưới đây sẽ khởi tạo Cluster với một mã token cho trước để đơn giản hóa các bước thực hiện:

`kubeadm init --token=102952.1a7dd4cc8d1f4cc5 --kubernetes-version`

`kubeadm version -o short`

Trên máy host thông thường, để lấy mã token này ta phải....


Để quản lý cụm Kubernetes, cấu hình cho clients và certificates là bắt buộc. Cấu hình này được tạo khi kubeadm khởi chạy cluster. Lệnh sao chép cấu hình vào thư mục chính của người dùng và đặt biến môi trường để sử dụng với CLI như sau:

`sudo cp /etc/kubernetes/admin.conf $HOME/`

`sudo chown $(id -u):$(id -g) $HOME/admin.conf`

`export KUBECONFIG=$HOME/admin.conf `

## Step 2 - Deploy Container Networking Interface (CNI)