# Service Boundary của nhóm

## 1. Thông tin nhóm

- Tên nhóm: Nhóm 6
- Lớp: CNTT17-13
- Thành viên: 4
- Service nhóm phụ trách: Analytics Service
- Sản phẩm tổng thể của lớp: Smart Campus Operations Platform

## 2. Actor

Thiết bị IoT (ESP32, cảm biến): Cung cấp dữ liệu nhiệt độ, độ ẩm, chuyển động.
Camera IP: Cung cấp luồng hình ảnh/video để phân tích.
Đầu đọc RFID: Ghi nhận sự kiện quẹt thẻ ra/vào.
Người dùng (Sinh viên/Nhân viên): Thực hiện hành động quẹt thẻ hoặc di chuyển trong khu vực giám sát.

## 3. System Boundary

Nhóm em xây phần nào?

Phần nhóm kiểm soát:

Logic tổng hợp dữ liệu từ nhiều nguồn khác nhau (IoT, Camera, Access Gate, Core).
Hệ thống tính toán các chỉ số (metric) như trung bình, tổng hợp theo thời gian.
Cơ sở dữ liệu lưu trữ các báo cáo và thống kê (PostgreSQL, TimescaleDB, hoặc MongoDB).
Các endpoint trả về báo cáo JSON cho Dashboard.

Phần nhóm chỉ tích hợp:

Dữ liệu thô từ các cảm biến thông qua IoT Ingestion Service.
Dữ liệu sự kiện hình ảnh từ Camera Stream / AI Vision Service.
Dữ liệu lượt ra/vào từ Access Gate Service.
Dữ liệu về các quyết định nghiệp vụ và cảnh báo từ Core Business Service.

## 4. Service Boundary

Service của nhóm có trách nhiệm gì?

Tổng hợp dữ liệu từ nhiều service khác để tạo metric, thống kê và báo cáo.
Cung cấp các chỉ số vận hành như: số lượt ra/vào theo giờ, nhiệt độ trung bình, số lượng cảnh báo trong ngày.
Service KHÔNG làm gì?

KHÔNG trực tiếp nhận dữ liệu từ phần cứng (việc này của IoT Ingestion, Access Gate).
KHÔNG thực hiện phân tích hình ảnh (việc này của AI Vision).
KHÔNG ra quyết định xử lý nghiệp vụ hay tạo cảnh báo (việc này của Core Business).
KHÔNG trực tiếp gửi tin nhắn/email cho người dùng (việc này của Notification).

## 5. Input / Output

### Input

- Dữ liệu từ IoT Ingestion Service (Temperature, Humidity, Motion, CO2).
- Dữ liệu từ Access Gate Service (FaceID, RFID Scan Log).
- Dữ liệu từ AI Vision Service (Detection Event).
- Dữ liệu từ Core Business Service (Occupancy Alert, Zone Info).

### Output

- ...

## 6. API dự kiến

| Method | Endpoint | Mục đích |
|---|---|---|
| GET | /health | Kiểm tra service |
| POST | ... | ... |

## 7. Phụ thuộc service khác

Service này gọi đến service nào?

Service nào gọi đến service này?

## 8. Sơ đồ minh họa

Có thể vẽ bằng Mermaid, draw.io, Ludichart hoặc ảnh chụp sơ đồ.

```mermaid
flowchart LR
    User[Actor] --> Service[Service của nhóm]
    Service --> DB[(Database)]
    Service --> Other[Service khác]
