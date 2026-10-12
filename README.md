# Báo cáo Thực hành: Lưu trữ dữ liệu với Docker Volume

## 1. Mục tiêu
Kiểm chứng tính toàn vẹn và bền vững của dữ liệu lưu trong Docker Named Volume giữa các phiên chạy của Container độc lập.

## 2. Các bước thực hiện

### Bước 1: Khởi tạo Named Volume
```bash
docker volume create easy-volume

```

Kiểm tra danh sách volume:

```bash
docker volume ls

```

Output:

```text
DRIVER    VOLUME NAME
local     easy-volume

```

### Bước 2: Ghi dữ liệu vào Volume qua Container 1

Sử dụng container tạm thời (`--rm`) để mount volume và ghi dữ liệu:

```bash
docker run --rm -v easy-volume:/data alpine sh -c "echo 'Luu tru du lieu Docker' > /data/test.txt"

```

*(Container 1 tự động bị xóa sau khi hoàn tất lệnh ghi)*

### Bước 3: Đọc dữ liệu từ Volume qua Container 2

Khởi chạy một container mới hoàn toàn để kiểm tra dữ liệu:

```bash
docker run --rm -v easy-volume:/data alpine cat /data/test.txt

```

## 3. Kết quả kiểm tra

Nội dung in ra terminal:

```text
Luu tru du lieu Docker

```

## 4. Kết luận

* Dữ liệu trong `easy-volume` không bị mất đi dù container ghi dữ liệu đã bị xóa.
* Container thứ hai có thể truy cập và đọc chính xác dữ liệu từ volume được chia sẻ.

## 5. Dọn dẹp (nếu cần)

```bash
docker volume rm easy-volume

```
