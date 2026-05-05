- **SystemUser (Người dùng hệ thống):**
  - **`citizenID`**: Số CCCD, khóa chính
  - `password`: Mật khẩu
  - `fullName`: Họ và tên
  - `dateOfBirth`: Ngày sinh
  - `gender`: Giới tính
  - `phoneNumber`: Số điện thoại
  - `email`: Email
  - `citizenIdFrontPath`: Đường dẫn ảnh CCCD mặt trước
  - `citizenIdBackPath`: Đường dẫn ảnh CCCD mặt sau
  - `deferredUntil`: Khóa hiến máu đến ngày... (Nếu bị khóa vĩnh viễn thì sẽ chọn ngày 01/01/3000).
  - `failedLoginAttempts` (Mặc định: 0): Đếm số lần đăng nhập sai liên tiếp. Nếu đăng nhập đúng, reset về 0. Nếu sai, cộng thêm 1.
  - `lastFailedLoginTime`: Lưu thời điểm của lần đăng nhập sai gần nhất. Khi đăng nhập (bất kể mật khẩu sai hay đúng) nếu số lần thời điểm sai gần nhất đến thời điểm hiện tại quá 30 phút thì reset `failedLoginAttempts` về 0.
  - `lockedUntil` (Mặc định: null): Lưu thời điểm tài khoản được mở khóa. Khi `failedLoginAttempts` đạt mốc 5, hệ thống sẽ lấy thời gian hiện tại cộng thêm 30 phút và gán vào thuộc tính này.

- **RevokedToken (Danh sách đen - Blacklist, Lưu trữ các Access Token đã bị vô hiệu hóa trước thời hạn):**
  - **`id`**: Khóa chính.
  - `token`: Chuỗi Access Token bị thu hồi.
  - `revokedAt`: Thời điểm token bị đưa vào danh sách đen.
  - `expiryDate`: Thời điểm token này vốn dĩ sẽ hết hạn. Lưu ý: Thuộc tính này cực kỳ quan trọng. Cần nó để hệ thống tự động xóa bản ghi này khỏi DB sau khi nó thực sự hết hạn, giúp bảng RevokedToken không bị phình to vô hạn theo thời gian.

- **BloodDonor (Người hiến máu):**
  - `aboGroup`: Nhóm máu hệ ABO (`A`, `B`, `O`, `AB`).
  - `rhFactor`: Yếu tố Rh (`+` hoặc `-`).

- **InternalUser (Người dùng nội bộ: Cán bộ y tế, KTV xét nghiệm, KTV kho, KTV kho tuyến dưới, Ban quản trị):**
  - `role`: Vai trò (`MedicalStaff` - Cán bộ y tế, `LAB_TECHNICIAN` - KTV xét nghiệm, `CENTER_INVENTORY_TECHNICIAN` - KTV kho trung tâm, `LOWER_INVENTORY_TECHNICIAN` - KTV kho tuyến dưới, `Admin` - Ban quản trị).
  - `isActive`: true/false. Dùng khi tài khoản bị Admin Khóa/Mở khóa.

<!--
- **MedicalStaff (Cán bộ y tế):**

- **LabTechnician (Kỹ thuật viên xét nghiệm):**

- **InventoryTechnician (Kỹ thuật viên kho):**

- **LowerInventoryStaff (Kỹ thuật viên/Nhân viên kho tuyến dưới):**
-->

---

- **BloodDrive (Chiến dịch hiến máu):**
  - **`id`**: Khóa chính.
  - `name`: Tên chiến dịch
  - `location`: Địa điểm
  - `startTime`: Thời gian bắt đầu
  - `endTime`: Thời gian kết thúc
  - `isActive`: Trạng thái chiến dịch (true/false)

- **TimeSlot (Khung giờ của Chiến dịch hiến máu):**
  - **`id`**: Khóa chính.
  - `startTime`: Thời gian bắt đầu của 1 khung giờ
  - `endTime`: Thời gian kết thúc của 1 khung giờ

- **HealthSurveyQuestion (Câu hỏi khảo sát sức khỏe):**
  - **`id`**: Khóa chính.
  - `questionText`: Nội dung câu hỏi (VD: "Bạn có đang bị sốt không?").
- **HealthSurveyResponse (Câu trả lời khảo sát sức khỏe, chỉ có class, db thì không cần):**
  - **`id`**: Khóa chính.
  - `answerValue`: Giá trị người dùng chọn (true/false).

- **DonationAppointment (Lịch hẹn hiến máu hay có thể hiểu là lịch hiến đã được người dùng đặt):**
  - **`qrCodePayload`**: Khóa chính. Là một mã UUID và dùng thư viện `qrcode.react` của ReactJS để hiển thị hình ảnh QR.
  - `status`: Trạng thái lịch hẹn (`BOOKED`, `NO_SHOW`, `CHECKED_IN`, `CANCELED`)
  - `createdAt`: Thời gian tạo
    - Lưu ý bảng này còn nối với bảng TimeSlot để biết người dùng đã đặt ca nào

- **BloodDonation (Thông tin Lần hiến máu):**
  - **`id`**: Khóa chính.
  - `rapidTestCode`: Mã của ống máu xét nghiệm nhanh. Unique. Tuân thủ chuẩn Code 128.
  - `checkInTime`: Thời gian check in
  - `weight`: Cân nặng
  - `heartRate`: Nhịp tim
  - `systolicBloodPressure`: Huyết áp tâm thu
  - `diastolicBloodPressure`: Huyết áp tâm trương
  - `bloodVolume`: Lượng máu hiến đơn vị ml
  - `screeningStatus`: Trạng thái khám lâm sàng (`PENDING`, `PASSED`, `FAILED`) - cửa ải 1
  - `rapidTestStatus`: Trạng thái xét nghiệm nhanh (`PENDING`, `PASSED`, `FAILED`) - cửa ải 2, chỉ được thực hiện nếu cửa 1 = PASSED
  - `labTestStatus`: Trạng thái xét nghiệm chuyên sâu trong phòng lab (`NOT_STARTED`, `PENDING`, `PASSED`, `FAILED`) - cửa ải 3, chỉ bắt đầu chuyển sang PENDING nếu Cán bộ y tế "Xác nhận lấy máu"

---

- **BloodBag (Thông tin túi máu):**
  - **`bagCode`**: Khóa chính. Và cũng là mã vạch dán trên túi máu và 2 ống xét nghiệm sâu. Tuẩn thủ chuẩn Code 128.
  - `collectionDate`: Ngày lấy máu. Còn dùng để tính hạn sử dụng (+ 35 ngày).
  - `expirationDate`: Ngày hết hạn
  - `aboGroup`: Nhóm máu hệ ABO (`A`, `B`, `O`, `AB`).
  - `rhFactor`: Yếu tố Rh (`+` hoặc `-`).
  - `bloodVolume`: Lượng máu trong túi.
  - `status`: Trạng thái của túi máu (`COLLECTED` - Đã thu thập, `QUARANTINED` - Biệt trữ, `QUALIFIED` - Đạt chuẩn, `REACTIVE` - Nhiễm bệnh, `AVAILABLE` - Sẵn sàng cấp phát, `ISSUED_EXTERNAL` - Đã cấp phát tuyến dưới, `ISSUED_INTERNAL` - Đã cấp phát nội bộ, `EXPIRED` - Đã hết hạn, `DISCARDED` - Đã tiêu hủy)
    - Liên kết về thực thể BloodDonation (Để biết cái túi vật lý này được lấy từ lần hiến máu nào của ai).

- **LabTestResult (Kết quả xét nghiệm chuyên sâu):**
  - **`sampleCode`**: Khóa chính, là mã của mã vạch ống máu và giống với `bagCode` của túi máu tương ứng
  - `aboGroup`: Nhóm máu hệ ABO (`A`, `B`, `O`, `AB`). Ở database thì không cần do đã lưu ở `BloodBag`.
  - `rhFactor`: Yếu tố Rh (`+`, `-`). Ở database thì không cần do đã lưu ở `BloodBag`.
  - `hivResult`: Kết quả xét nghiệm HIV (`NEGATIVE` - Âm tính, `POSITIVE` - Dương tính).
  - `hbvResult`: Kết quả Viêm gan B (`NEGATIVE`, `POSITIVE`).
  - `hcvResult`: Kết quả Viêm gan C (`NEGATIVE`, `POSITIVE`).
  - `syphilisResult`: Kết quả Giang mai (`NEGATIVE`, `POSITIVE`).
  - `malariaResult`: Kết quả Sốt rét (`NEGATIVE`, `POSITIVE`).
  - `receivedAt`: Thời điểm hệ thống tiếp nhận dữ liệu từ API.
  - `status`: Trạng thái phê duyệt xét nghiệm (`PENDING` - Chờ duyệt, `APPROVED` - Đã duyệt, `REJECTED` - Từ chối kết quả).
    - Liên kết đến thực thể BloodBag (Túi máu tương ứng với ống mẫu này).

---

- **DiscardRecord (Biên bản tiêu hủy / Nhật ký tiêu hủy):**
  - **`id`**: Định danh duy nhất của bản ghi lưu vết.
  - `discardedAt`: Thời điểm bấm nút "Xác nhận tiêu hủy" (Bước 11 & 12).
  - `reason`: Lý do tiêu hủy. Theo Bước 7a2: Lưu chuỗi văn bản do KTV nhập tay (ví dụ: "Túi máu bị rách vỏ ngoài"). Theo Bước 8: Hệ thống tự điền là "Hết hạn sử dụng".
    - Liên kết đến thực thể BloodBag (Để biết chính xác túi máu vật lý nào đã bị hủy).
    - Liên kết đến thực thể KTV kho (Đại diện cho KTV kho thực hiện hành động quét mã - giải quyết bài toán truy vết ai là người hủy).

- **BloodIssueRecord (Phiếu xuất kho / Phiếu cấp phát):**
  - **`id`**: Định danh duy nhất (Sẽ được in làm Barcode/QR trên tờ phiếu giấy).
  - `issueType`: Loại xuất kho (EXTERNAL - Dùng cho xuất kho tuyến dưới, INTERNAL - Dùng cho xuất kho nội bộ).
  - `issuedAt`: Thời điểm bấm "Xác nhận xuất kho".
    - Liên kết đến KTV Kho để lưu vết KTV nào đã thực hiện hành động này.
    - Liên kết đến BloodRequest (Chỉ bắt buộc với UC18. Nếu là UC19 thì trường này mang giá trị null).
    - Liên kết danh sách (One-to-Many) tới các BloodBag đã được quét vào phiếu này.

---

- **Hospital (Bệnh viện / Cơ sở y tế)**:
  - **`id`**: Định danh duy nhất (Mã bệnh viện).
  - `name`: Tên bệnh viện (Ví dụ: "Bệnh viện Đa khoa Tỉnh A").
  - `address`: Địa chỉ chi tiết.
  - `hotline`: Số điện thoại trực ban/cấp cứu.
  - `isActive`: Trạng thái hợp tác (Đang hoạt động hay đã ngừng liên kết).
    - Liên kết đến danh sách MedicalStaff (Bệnh viện này có những nhân viên nào).
    - Liên kết đến danh sách BloodRequest (Bệnh viện này đã tạo những phiếu yêu cầu nào).

- **BloodRequest (Phiếu yêu cầu cấp máu)**:
  - **`id`**: Định danh duy nhất của phiếu yêu cầu (Mã phiếu).
  - `priorityLevel`: Mức ưu tiên của phiếu (`NORMAL` - Bình thường, `URGENT` - Khẩn cấp).
  - `status`: Trạng thái phê duyệt (`PENDING` - Chờ duyệt, `APPROVED` - Đã duyệt, `PARTIALLY_APPROVED` - Duyệt một phần, `IN_TRANSIT` - Đang vận chuyển, `REJECTED` - Đã từ chối, `CANCELLED` - Đã hủy, `COMPLETED` - Đã hoàn thành).
  - `createdAt`: Thời điểm tạo phiếu.
  - `rejectionReason`: Lý do bị từ chối duyệt
    - Liên kết đến thực thể Nhân viên BV tuyến dưới tạo phiếu.
    - Liên kết đến thực thể đại diện cho Bệnh viện tuyến dưới nhận máu. (Đảm bảo tính lịch sử)
    - Liên kết đến danh sách các thực thể BloodRequestItem (Các nhóm máu nằm trong phiếu này).

- **BloodRequestItem (Chi tiết yêu cầu máu)**:
  - **`id`**: Định danh dòng chi tiết.
  - `aboGroup`: Nhóm máu hệ ABO (`A`, `B`, `O`, `AB`).
  - `rhFactor`: Yếu tố Rh (`+`, `-`).
  - `volume`: Dung tích yêu cầu (Ví dụ: 250, 350, 450 ml).
  - `quantity`: Số lượng túi máu cần cấp.
  - `approvedQuantity`: Số lượng đã được duyệt.
    - Liên kết ngược lại thực thể cha BloodRequest.
