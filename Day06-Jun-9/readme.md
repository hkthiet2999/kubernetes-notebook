Tổng hợp lý thuyết về các built-in workload resources từ [Documents của Kubernetes](https://kubernetes.io/docs/home/)

# Workloads trong Kubernetes
Workloads là một application chạy trên Kubernetes. Cho dù Workload là một thành phần đơn lẻ hay nhiều thành phần hoạt động cùng nhau thì trên Kubernetes đều sẽ chạy nó bên trong một tập hợp các Pods.

Các Pods trong Kubernetes có một vòng đời xác định. Khi một Pod đang chạy trong Cluster xảy ra lỗi trên Node nơi Pod đó đang chạy dẫn đến tất cả các Pod trên Node đó đều bị lỗi.
Khi đó ra sẽ cần tạo một Pod mới để khôi phục lại trạng thái ok ban đầu và vì vậy việc quản lý Pods là cực kỳ quan trọng.
Tuy nhiên ta không cần phải quản lý trực tiếp từng Pod. Thay vào đó có thể sử dụng Workload resources để quản lý một tập các Pods. 
Các Workload resources này định cấu hình controllers để đảm bảo một lượng phù hợp các Pods đang chạy và phù hợp với state được chỉ định từ trước.

<h3><i> Kubernetes cung cấp một số built-in workload resources như sau:</i></h3>

## 1. Deployment và ReplicaSet
Mục đích của [ReplicaSet](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/) là duy trì một tập hợp các bản sao của Pod có thể chạy ổn định tại bất kỳ thời điểm nào. 
  Do đó nó thường được sử dụng để đảm bảo tính khả dụng của một số lượng Pods giống hệt nhau.
  
Một ReplicaSet được định nghĩa bằng các fields, bao gồm một bộ selector chỉ định cách xác định các Pods mà ReplicaSet có thể gom lại được, một số replicas cho biết nó sẽ duy trì bao nhiêu Pod và một pod template chỉ định dữ liệu của các Pod mới mà nó sẽ tạo để đáp ứng số lượng của tiêu chí nhân bản. Sau đó, một ReplicaSet thực hiện mục đích của nó bằng cách tạo và xóa các Pod nếu cần để đạt được số lượng mong muốn. Khi một ReplicaSet cần tạo các Pod mới, nó sẽ sử dụng Pod teplate của nó để tạo.

Một ReplicaSet được liên kết với Pods của nó thông qua field `metadata.ownerRefferences` của Pods, field này chỉ định tài nguyên mà đối tượng hiện tại sở hữu. Tất cả các Pods được ReplicaSet gom lại đều có thông tin nhận dạng của ReplicaSet lữu trữ trong field chủ sở hữu của chúng. Thông qua liên kết này mà ReplicaSet biết về state của các Pod mà nó đang duy trì và lập kế hoạch cho phù hợp.

Một ReplicaSet xác định các Pods mới bằng cách sử dụng selector của nó. Nếu có một Pod không có OwnerReference hoặc OwnerReference không phải là Contoller và nó khớp với selector của ReplicaSet, nó sẽ ngay lập tức được ReplicaSet đó gom lại

Tham khảo thêm về ví dụ, cách viết manifest cho ReplicaSet và làm việc với nó tại [documents](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/#working-with-replicasets)

Một ReplicaSet đảm bảo rằng một số lượng bản sao các Pod được chỉ định đang chạy tại bất kỳ thời điểm nào. Tuy nhiên, Deployment là một khái niệm cấp cao hơn so với ReplicaSets và cung cấp các bản cập nhật khai báo cho Pods cùng với rất nhiều tính năng hữu ích khác. Do đó thông thường người ta sử dụng Deployments thay vì trực tiếp sử dụng ReplicaSets, trừ khi họ có nhu cầu tùy chỉnh và điều phối các cập nhật hoặc hoàn toàn không yêu cầu cập nhật.


[Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) cung cấp các bản cập nhật khai báo cho Pods và ReplicaSets. Ta mô tả một desired state trong Deployment và Deployment Controller thay đổi actual state thành desired state mà mình mong muốn với tốc độ kiểm soát được. Ta cũng có thể định nghĩa các Deployment để tạo các ReplicaSets mới hoặc để xóa các Deployment hiện có và sử dụng tất cả các tài nguyên của chúng cho Deployment mới.

Dưới đây là các trường hợp sử dụng điển hình cho Deployment:

  - [Tạo Deployment để rollout một ReplicaSet](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#creating-a-deployment): 
 ReplicaSet tạo các Pods trong background, ta có thể kiểm tra trạng thái rollout để xem liệu nó có thành công hay không.

  - [Khai báo new state của Pods bằng cách cập nhật PodTemplateSpec của Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#updating-a-deployment):
  Một ReplicaSet mới được tạo và Deployment quản lý việc di chuyển các Pod từ ReplicaSet cũ sang ReplicaSet mới với tốc độ kiểm soát được. Mỗi ReplicaSet mới sẽ cập nhật lại bản sửa đổi của Deployment.

  - [Quay lại phiên bản Deployment trước đó nếu trạng thái hiện tại của Deployment không ổn định](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-back-a-deployment): 

   - [Mở rộng quy mô Triển khai để tạo điều kiện tải nhiều hơn](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#scaling-a-deployment)
   
   - [Tạm dừng Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#pausing-and-resuming-a-deployment):
Để áp dụng nhiều bản sửa lỗi cho PodTemplateSpec của nó và sau đó tiếp tục triển khai để bắt đầu một đợt phát hành mới.

  - [Sử dụng status của Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#deployment-status) như một indicator cho quá trình rollout nếu bị lỗi
  - [Dọn dẹp các ReplicaSets](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#clean-up-policy) cũ không cần dùng đến nữa
  
