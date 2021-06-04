# Một số lệnh Docker phổ biến
`docker --version` kiểm tra phiên bản docker

`docker info` Thông tin hệ thống docker

`docker images -a`
Liệt kê các image

`docker pull nameimage:tag`
Tải về một image từ hub.docker.com

`docker ps`
Liệt kê các container đang chạy

`docker ps -a`
Liệt kê các container

`docker container ls -a`
Liệt kê các container
Tạo / chạy container

`docker run -it --name nameyourcontainer -h "nameyourhost" image_id`
tạo, chạy một container từ image với id (name) là image_id

# Một số tham số thêm vào khi tạo container:

`-v path-in-host:path-in-container`
Ánh xạ thư mục máy host vào container

`--volumes-from other-container-name`
Nhận chia sẻ thư mục đã ánh xạ từ container khác

`-p public-port:target-port`
Container có cổng ngoài public-port ánh xạ vào cổng trong target-port

`--restart=always`
Thiết lập để Docker tự khởi động container

`docker container attach containerid`
Vào terminal container đang chạy

`docker exec -it containerid command`
chạy một lệnh command trên container đang hoạt động

`docker stop containerid` Dừng hoạt động một container

`docker start -i containerid`
Chạy một container

`docker restart containerid`
Khởi động lại container

`docker rm containerid`
Xóa container

`CTRL +P, CTRL + Q`
Thoát -it terminal nhưng container vẫn chạy

`docker commit containerid imagename:imageversion`
Lưu một container đang dừng thành Image

`docker save --output myimage.tar myimage_id`
Lưu image ra đĩa

`docker load -i myimage.tar`
Nạp Image trên đĩa vào Docker

`docker tag image_id imagename:version`
Đổi tên Image

`docker network ls`
Liệt kê các network

`docker network create --driver bridge name-network`
Tạo mạng kiểu bridge đặt tên là name-network

`docker network connect name-network name-container`
Nối container vào mạng name-network

`docker inspect name_or_id_of_image_container`
Lấy thông tin về image hoặc container

`docker history name_or_id_of_image`
Lấy thông lịch sử tạo thành iamge

`docker diff container-name-or-id`
Theo dõi thay đổi các file trên container

`docker logs -f container-name-or-id`
Đọc log container

`docker stats container-name-or-id`
Đo lường thông tin
