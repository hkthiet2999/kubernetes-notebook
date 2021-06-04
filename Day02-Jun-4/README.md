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

# Tạo / chạy container và Một số tham số thêm vào khi tạo container
## Các thao tác cơ bản với Container
Dừng hoạt động một container
`docker stop containerid` 

Chạy một container
`docker start -i containerid`

Khởi động lại container
`docker restart containerid`

Xóa container
`docker rm containerid`

Thoát -it terminal nhưng container vẫn chạy
`CTRL +P, CTRL + Q`


## Docker Image, chạy Container
Tạo, chạy một container từ image với id (name) là image_id
`docker run -it --name nameyourcontainer -h "nameyourhost" image_id`

Thiết lập để Docker tự khởi động container
`docker run -it --restart=always`

Vào terminal container đang chạy
`docker container attach containerid`

## Lệnh Docker exec, lưu container thành image với commit, xuất image ra file .tar
`docker exec -it containerid command`
chạy một lệnh command trên container đang hoạt động


`docker commit containerid imagename:imageversion`
Lưu một container đang dừng thành Image

Lưu Image ra thành đĩa (file .tar)
`docker save --output myimage.tar myimage_id`

Nạp Image trên đĩa (file .tar) vào Docker
`docker load -i myimage.tar`

Đổi tên Image ? 2018 - clone Image
`docker tag image_id imagename:version`

## Chia sẻ dữ liệu trong Docker, tạo và quản lý disk ( Volume) trong Docker
Ánh xạ thư mục máy host vào container ( path sử dụng dấu /)
`docker run -it -v path-in-host:path-in-container`

Chia sẻ thư mục đã ánh xạ từ 1 container đến 1 container khác 
`docker run -it --name nameyourcontainer --volumes-from other-container-name imagename`

Container có cổng ngoài public-port ánh xạ vào cổng trong target-port
`docker run -it -p public-port:target-port`

Thiết lập để Docker tự khởi động container
`docker run -it --restart=always`

Gắn ổ đĩa Volume vào container
`docker run --it --mount source=DISK,target=pathContainer imageID`

Xem thông tin ổ đĩa
`docker volume inspect diskName`

Tạo ổ đĩa ánh xạ đến thư mục của máy host
`docker create --opt device=pathHOST --opt type=none --opt o=bind DISKNAME`

Ánh xạ ỗ đĩa đến thư mục Container của Image
`docker run -it -v DISKNAME:pathContainer ImageID`

## Network trong Docker, tạo và quản lý Network trong Docker
Liệt kê các network
`docker network ls`

Tạo mạng kiểu bridge đặt tên là name-network
`docker network create --driver bridge name-network`


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
