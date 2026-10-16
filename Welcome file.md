1. input 
**Định nghĩa:** Đầu vào là dạng dữ liệu đầu vào thuần túy, bao gồm các ký tự chuỗi, ghi chú nhanh, ý tưởng rời rạc hoặc tài liệu chưa qua định dạng xử lý. Nó tập trung hoàn toàn vào **nội dung cốt lõi** mà không bận tâm đến cách trình bày hoặc thẩm định mỹ phẩm.
2.output 

**Định nghĩa:** Đầu ra là sản phẩm đầu ra sau khi văn bản thô đã được phân tích, cấu trúc lại và phủ lên một "lớp áo" hiển thị trực quan, hiện đại. Nó là tập trung vào **trải nghiệm người dùng (UX)** , giúp người đọc nắm bắt thông tin nhanh chóng và chính xác nhất.
**Source code:**
```( đây là code python ) 
## 3. Mã Nguồn Python Điều Khiển Máy Bơm

Dưới đây là đoạn mã nguồn Python hoàn chỉnh dùng để đọc dữ liệu cảm biến và bật/tắt rơ-le máy bơm tự động:

Python

```
import time
import RPi.GPIO as GPIO
import Adafruit_DHT

# Khai báo cấu hình chân phần cứng và loại cảm biến
SENSOR_TYPE = Adafruit_DHT.DHT22
PIN_SENSOR = 4
PIN_RELAY = 17
HUMIDITY_THRESHOLD = 65.0  # Ngưỡng kích hoạt tưới tiêu tối thiểu (%)

GPIO.setmode(GPIO.BCM)
GPIO.setup(PIN_RELAY, GPIO.OUT)

def control_irrigation():
    try:
        while True:
            humidity, temperature = Adafruit_DHT.read_retry(SENSOR_TYPE, PIN_SENSOR)
            if humidity is not None:
                print(f"Độ ẩm: {humidity:.1f}% | Nhiệt độ: {temperature:.1f}C")
                if humidity < HUMIDITY_THRESHOLD:
                    print("Cảnh báo: Độ ẩm thấp! Đang bật máy bơm nước...")
                    GPIO.output(PIN_RELAY, GPIO.HIGH)
                else:
                    print("Độ ẩm ổn định. Đang tắt máy bơm.")
                    GPIO.output(PIN_RELAY, GPIO.LOW)
            else:
                print("Lỗi: Không thể kết nối với cảm biến độ ẩm!")
            time.sleep(10)
    except KeyboardInterrupt:
        print("Đã dừng chương trình thủ công.")
    finally:
        GPIO.cleanup()

if __name__ == "__main__":
    control_irrigation()

```

## 4. Task List Kiểm Tra Thiết Bị

-   [x] Kiểm tra nguồn điện ổn định cấp cho mạch điều khiển trung tâm
    
-   [x] Lắp đặt cảm biến điện dung mới vào luống lan thử nghiệm số 1
    
-   [ ] Cấu hình chính xác chân tín hiệu `PIN_SENSOR` và `PIN_RELAY` trong file cấu hình
    
-   [ ] Chạy kiểm tra hệ thống bằng lệnh `python control_irrigation.py`
    
-   [ ] Giám sát log hoạt động và độ ổn định của hệ thống trong 24 giờ đầu tiên
