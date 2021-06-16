## 3. Containers
Mỗi container mà khi đã chạy đều có thể lặp lại nhờ tiêu chuẩn hóa từ việc bao gồm các dependencies, có nghĩa là ta sẽ có được behavior giống nhau ở bất kỳ nơi nào chạy nó.

Container tách các ứng dụng khỏi cơ sở hạ tầng máy chủ lưu trữ bên dưới. Điều này làm cho việc triển khai dễ dàng hơn trong các môi trường đám mây hoặc hệ điều hành khác nhau.

### 3.1 Container images
Container images là một gói phần mềm có thể chạy ở mọi nơi, nó chứa mọi thứ cần thiết để chạy một ứng dụng: code và bất kỳ runtime nào mà ứng dụng cần, các thư viện ứng dụng và hệ thống cũng như các giá trị mặc định cho bất kỳ cài đặt thiết yếu nào.

Theo thiết kế, container là bất biến: ta không thể thay đổi mã của container đang chạy. Nếu ta có một ứng dụng được chứa trong container và muốn thực hiện thay đổi, khi đó ta cần tạo một Image mới bao gồm các thay đổi đó, sau đó tạo lại container để bắt đầu từ container image đã cập nhật.

### 3.2 Container runtimes
Container runtimes là môi trường chịu trách nhiệm chạy các Containers. Kubernetes hỗ trợ một số container runtime như: Docker, containerd, CRI-O và bất kỳ triển khai nào của Kubernetes CRI (Container Runtime Interface).