

# Khởi chạy script giám sát log và thiết bị
python3 monitor_system.py --config config.yaml

```

## Thiết bị kiểm tra danh sách kiểm tra

-   [x] Kiểm tra nguồn điện và UPS cho trạm cảm biến-03
    
-   [ ] Kiểm tra độ ổn định của mạng ăng-ten tín hiệu định nghĩa 4G
    
-   [ ] Xác thực quyền truy cập nhật ký cơ sở dữ liệu trên máy chủ chính
    

## Phần cứng thông tin của bảng

**Tên bị**

**Đơn giá (V)**

**Kho lưu trữ**

Ổ cứng SSD Kingston NV2 500GB PCIe 4.0

1.250.000

SSD NVMe

Ổ cứng HDD Seagate Barracuda 1TB

1.150.000

Ổ cứng SATA

Ổ cứng SSD Samsung 980 Pro 1TB

2.450.000

SSD NVMe

## Phân tích hệ thống

### 1. Xác định Đầu vào – Quá trình – Đầu ra của nhật ký lọc chức năng

-   **Đầu vào (Đầu vào):** RAW tập tin nhật ký (tệp nhật ký) chứa hàng loạt sự kiện ghi, lỗi,cảnh báo từ các trạm cảm biến kèm theo các bộ lọc (tiêu chí lọc) như khoảng thời gian,lỗi độ (`ERROR`,  `WARNING`),hoặc mã (ví dụ:  `sensor-03`).
    
-   **Quy trình (Xử lý):**
    
    -   Cú pháp quét và phân tích (phân tích) từng dòng nhật ký theo chuẩn định dạng.
        
    -   Áp dụng các bộ lọc điều kiện (ví dụ:tìm các dòng chứa `sensor-03`và từ khóa `TIMEOUT`).
        
    -   Sắp xếp và thống kê tần suất xuất hiện của các sự cố theo thời gian hoặc theo trạm.
        
-   **Đầu ra (đầu ra):**Danh sách các dòng nhật ký đã được chặn điều kiện mãn tính,hoặc báo cáo tổng hợp các sự cố theo yêu cầu kỹ thuật trợ giúp của thành viên dễ dàng truy tìm lỗi.
    

### 2. Phân loại phát biểu theo mô hình DIKW (Data – Information – Knowledge – Wisdom)

-   **(b) Dữ liệu:**  _“2026-10-12 08:15:01 [ERROR] sensor-03 Kết nối hết thời gian chờ sau 30 giây”_
    

        
-   **(c) Thông tin (không tin):**  _“Hôm nay hệ thống ghi nhận 8 sự cố, trong đó có 4 sự cố đến từ trạm cảm biến-03.”_
    

        
-   **(d) Kiến thức (Tri thức):**  _“Trạm cảm biến-03 hay mất kết nối vào buổi chiều làm sóng yếu, nên cần gắn thêm anten.”_
    
 
        
-   **(a) Trí tuệ (Sự khôn ngoan/Hành động tối ưu):** _“Quyết định thay modem trạm cảm biến-03 trước thứ Sáu.”_
    
 
