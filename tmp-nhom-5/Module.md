## 4 module

### Module 1: Cổng tương tác Người hiến & Quản lý Chiến dịch & Quản lý của ban quản trị (Portal & Campaign): Chính

Actor chính: Người hiến máu, Ban Quản trị.
Các use case:

1. Người hiến: Đăng ký tài khoản
2. Người hiến: Đăng nhập
3. Người hiến: Cập nhật thông tin cá nhân
4. Người hiến: Tra cứu chiến dịch
5. Người hiến: Đặt lịch hiến máu
6. Người hiến: Xem lịch sửa hiến máu
7. Ban quản trị: Quản lý các chiến dịch hiến máu
8. Ban quản trị: Quản lý tài khoản nội bộ

### Module 2: Tiếp nhận & Khám lâm sàng & Xét nghiệm (Reception & Clinical & Testing): Biên

Actor chính: Cán bộ y tế, kỹ thuật viên xét nghiệm
Các use case:

1. Cán bộ y tế: Tiếp nhận và nhập kết quả khám lâm sàng.
2. Cán bộ y tế: Xem danh sách người hiến đang chờ lấy máu.
3. Cán bộ y tế: Xác nhận lấy máu.
4. Kỹ thuật viên xét nghiệm: Nhập kết quả xét nghiệm nhanh
5. Hệ thống LIS: Tiếp nhận kết quả xét nghiệm chuyên sâu
6. Kỹ thuật viên xét nghiệm: Duyệt kết quả xét nghiệm chuyên sâu

### Module 3: Quản lý Kho: Tủ biệt trữ và Tủ thành phẩm (Inventory): Đăng

Actor chính: Kỹ thuật viên kho
Các use case:

1. Kỹ thuật viên kho: Nhập kho tủ biệt trữ
2. Kỹ thuật viên kho: Nhập kho tủ thành phẩm
3. Kỹ thuật viên kho: Xuất kho để tiêu hủy
4. Kỹ thuật viên kho: Xem báo cáo thống kê tồn kho

### Module 4: Phân phối (Distribution): Cường

Actor chính: Kỹ thuật viên kho, nhân viên bệnh viện tuyến dưới
Các use case:

1. Kỹ thuật viên kho: Duyệt yêu cầu cấp máu của bệnh viện tuyến dưới
2. Kỹ thuật viên kho: Xuất kho để cấp phát cho đơn yêu cầu
3. Kỹ thuật viên kho: Xuất kho để cấp phát cho nội bộ
4. Nhân viên bệnh viện tuyến dưới: Tạo đơn yêu cầu cấp máu
5. Nhân viên bệnh viện tuyến dưới: Theo dõi tiến độ của đơn yêu cầu cấp máu

## Yêu cầu

### 1. UC Spec

Với UC Spec đã có trong bảng: Kiểm tra lại nội dung, chỉnh sửa hợp lý, sắp xếp lại alter và exception flow lại theo quy tắc chung:

- Alternative: là luồng tương tác thay thế để UC thực hiện thành công (nói chung nó phải đi đến đích là post condition)
- Còn Exception: là luồng ngoại lệ, vẫn có thể xử lý để UC đi đến được đích nhưng đã là xử lý ngoại lệ thì nó là exception

Với UC Spec chưa có: Bổ sung

Một số lưu ý:

- ID của UC mn chưa cần quan tâm thứ tự, sau họp lại thì sẽ sắp xếp lại sau, chỉ cần chú ý nội dung
- Làm thật kỹ, bổ sung exception nếu thấy chưa đủ (Có thể tham khảo của module khác và về sửa của mình)
- Sửa trực tiếp trong overleaf
