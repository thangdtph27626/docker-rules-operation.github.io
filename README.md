<p align="center">
 <h1 align="center">Quy tắc hoạt động của docker và một số khái niệm cơ bản cần biết trong docker</h1>
</p> 

## Docker container là gì ? 

Docker container có thể được coi là đóng gói phần mềm nhẹ, độc lập và có thể thực thi, bao gồm mọi thứ cần thiết để chạy một phần mềm, bao gồm mã, thời gian chạy, thư viện, biến môi trường và tệp cấu hình. Bộ chứa cách ly phần mềm với môi trường xung quanh, đảm bảo rằng nó hoạt động thống nhất trên các môi trường khác nhau.

Một số lệnh phổ biến bao gồm:

- docker run: Được sử dụng để tạo và bắt đầu một vùng chứa mới.
- docker container ls: Liệt kê các container đang chạy.
- docker container stop: Dừng một container đang chạy.
- docker container rm: Xóa một container đã dừHình ảnh Docker được xây dựng và quản lý bằng Dockerfiles. Dockerfile là một tập lệnh bao gồm các hướng dẫn để tạo hình ảnh Docker, cung cấp hướng dẫn từng bước để thiết lập môi trường ứng dụng.ng.
- docker exec: Thực thi lệnh bên trong vùng chứa đang chạy.

## Docker image là gì?

- Docker image là một file bất biến - không thay đổi, chứa các source code, libraries, dependencies, tools và các files khác cần thiết cho một ứng dụng để chạy
- Docker image được xây dựng và quản lý bằng Dockerfiles. Dockerfile là một tập lệnh bao gồm các hướng dẫn để tạo Docker image, cung cấp hướng dẫn từng bước để thiết lập môi trường ứng dụng.

docker image ls: Liệt kê tất cả các image có sẵn trên hệ thống cục bộ của bạn.
docker build: Xây dựng image từ Dockerfile.
docker image rm: Xóa một hoặc nhiều image.
docker pull: Kéo một image từ sổ đăng ký (ví dụ: Docker Hub) vào hệ thống cục bộ của bạn.
docker push: Đẩy một image vào một kho lưu trữ.

## Registry là gì ?

- Docker Registry: là nơi lưu trữ riêng của Docker Images. Images được push vào registry và client sẽ pull images từ registry.
- Các câu lệnh với Registry có thể được sử dụng để tìm kiếm và quản lý các Images. Bạn có thể sử dụng các câu lệnh như docker search, docker pull, docker push, docker login, và docker logout. \

## Dockerfile là gì ?

Dockerfile là một  document  chứa danh sách các hướng dẫn được sử dụng bởi công cụ Docker để xây dựng một image. Mỗi hướng dẫn trong Dockerfile thêm một layer  mới vào image. Docker sẽ xây dựng image dựa trên các hướng dẫn này và sau đó bạn có thể chạy các vùng chứa từ image. Dockerfiles là một trong những yếu tố chính của cơ sở hạ tầng dưới dạng mã.

Dưới đây là danh sách một số hướng dẫn Dockerfile phổ biến và mục đích của chúng:

- FROM: Đặt hình ảnh cơ sở để bắt đầu. Bắt buộc phải có FROM làm hướng dẫn đầu tiên trong Dockerfile.
- WORKDIR: Đặt thư mục làm việc cho bất kỳ hướng dẫn RUN, CMD, ENTRYPOINT, COPY hoặc ADD nào. Nếu thư mục không tồn tại, nó sẽ được tạo tự động.
- COPY : Sao chép tệp hoặc thư mục từ máy chủ lưu trữ vào hệ thống tệp của bộ chứa.
- ADD: Tương tự như COPY, nhưng cũng có thể xử lý các URL từ xa và tự động giải nén các tệp lưu trữ.
- RUN: Thực thi một lệnh trong hình ảnh dưới dạng một lớp mới.
- CMD: Xác định lệnh mặc định để thực thi khi chạy vùng chứa từ hình ảnh.
- ENTRYPOINT: Tương tự như CMD, nhưng nó được thiết kế để cho phép vùng chứa dưới dạng tệp thực thi với các tham số riêng của nó.
- EXPOSE: Thông báo cho Docker rằng bộ chứa sẽ lắng nghe trên các cổng mạng được chỉ định khi chạy.
- ENV: Đặt biến môi trường cho vùng chứa.

ví dụ 

```
# Sử dụng thời gian chạy Python chính thức làm image gốc
FROM python:3.7-slim

# Đặt thư mục làm việc thành /app
WORKDIR /app

# Sao chép nội dung thư mục hiện tại vào vùng chứa tại /app
COPY . /app

# Cài đặt bất kỳ gói cần thiết nào được chỉ định trong requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Cung cấp cổng 80 cho thế giới bên ngoài vùng chứa này
EXPOSE 80

# Xác định biến môi trường
ENV NAME World

# Chạy app.py khi vùng chứa khởi chạy
CMD ["python", "app.py"]
```

Chạy docker: docker build -t my-image:tag .

#  Docker hoạt động như thế nào ?

Docker image là nền tảng của container, có thể hiểu Docker image như khung xương giúp định hình cho container, nó sẽ tạo ra container khi thực hiện câu lệnh chạy image đó. Nếu nói với phong cách lập trình hướng đối tượng, Docker image là class, còn container là thực thể (instance, thể hiện) của class đó.
Docker có hai khái niệm chính cần hiểu, đó là image và container:

Container: Tương tự như một máy ảo, xuất hiện khi mình khởi chạy image.

Tốc độ khởi chạy container nhanh hơn tốc độ khởi chạy máy ảo rất nhiều và bạn có thể thoải mái chạy 4,5 container mà không sợ treo máy.

Các files và settings được sử dụng trong container được lưu, sử dụng lại, gọi chung là images của docker.

Image: Tương tự như file .gho để ghost win mà mấy ông cài win dạo hay dùng.

Image này không phải là một file vật lý mà nó chỉ được chứa trong Docker.

Một image bao gồm hệ điều hành (Windows, CentOS, Ubuntu, …) và các môi trường lập trình được cài sẵn (httpd, mysqld, nginx, python, git, …).

Docker hub là nơi lưu giữ và chia sẻ các file images này (hiện có khoảng 300.000 images)

Bạn có thể tìm tải các image mọi người chia sẻ sẵn trên mạng hoặc có thể tự tạo cho mình một cái image như ý.
