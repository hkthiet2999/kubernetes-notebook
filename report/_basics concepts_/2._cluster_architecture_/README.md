## 2. Kiến trúc của Cluster
### 2.1 Nodes

Kubernetes chạy workload bằng cách đặt các containers vào Pod để chạy trên Nodes. Một Node có thể là một máy ảo hoặc máy vật lý, tùy thuộc vào cluster. Mỗi node được quản lý bởi control plane và chứa các service cần thiết để chạy Pod

Các thành phần trên một Node bao gồm kubelet, container runtime và kube-proxy.

### 2.2 Control Plane-Node Communication

### 2.3 Controllers

### 2.4 Cloud Controller Manager
