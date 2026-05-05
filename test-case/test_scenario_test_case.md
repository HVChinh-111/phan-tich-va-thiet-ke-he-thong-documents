# Test Scenario & Test Case

## A. Khái niệm chung

### 1. Test Scenario là gì?

**Test Scenario** là một tình huống/chức năng cần được kiểm thử ở mức tổng quát. Test Scenario thường được rút ra từ **User Requirement** hoặc **Use Case Specification**, nhằm trả lời câu hỏi: “Cần kiểm tra những hành vi/chức năng nào của hệ thống?”

Ví dụ: Với use case “Đăng nhập”, có thể có các Test Scenario như:

* Kiểm tra đăng nhập thành công.
* Kiểm tra đăng nhập thất bại khi nhập sai mật khẩu.
* Kiểm tra khóa tài khoản sau nhiều lần đăng nhập sai.
* Kiểm tra điều hướng đúng giao diện theo vai trò người dùng.

### 2. Test Case là gì?

**Test Case** là bản mô tả chi tiết cách kiểm thử một Test Scenario cụ thể. Một Test Case cần chỉ rõ: điều kiện trước khi kiểm thử, dữ liệu kiểm thử, các bước thực hiện, kết quả mong đợi, kết quả thực tế và trạng thái Pass/Fail.

Nói ngắn gọn:

> **Test Scenario** cho biết “cần kiểm thử cái gì”.
> **Test Case** cho biết “kiểm thử như thế nào”.

Một Test Scenario có thể sinh ra nhiều Test Case. Ví dụ scenario “Kiểm tra đăng nhập” có thể gồm các test case: đăng nhập đúng, sai mật khẩu, sai tên đăng nhập, bỏ trống trường, tài khoản bị khóa, phiên đăng nhập hết hạn.

---

## B. Các bước thực hiện

Xuất phát từ **Use Case Specification** và **User Requirements**. Nên làm theo từng UC riêng, sau đó tổng hợp theo module.

### Bước 1: Đọc và xác định phạm vi kiểm thử

Với mỗi Use Case, cần đọc kỹ:

* Actor thực hiện use case.
* Trigger.
* Pre-condition và post-condition.
* Basic flow.
* Alternative flow.
* Exception flow.
* Business rules hoặc ràng buộc dữ liệu.

Không viết test case dựa trên suy đoán cá nhân. Nội dung kiểm thử phải bám vào đặc tả yêu cầu/use case. 

### Bước 2: Liệt kê Test Scenario

Với mỗi Use Case, xác định các tình huống cần kiểm thử theo các nhóm sau:

* **Luồng đúng:** người dùng thực hiện đúng và hệ thống xử lý thành công.
* **Luồng sai/ngoại lệ:** nhập sai, thiếu dữ liệu, dữ liệu không hợp lệ, thao tác không được phép.
* **Luồng thay thế:** người dùng chọn một hướng xử lý khác nhưng vẫn nằm trong nghiệp vụ.
* **Ràng buộc nghiệp vụ:** kiểm tra điều kiện tuổi, trạng thái tài khoản, trạng thái túi máu, nguyên tắc FEFO, giới hạn số lượng, quyền truy cập.
* **Phân quyền:** actor không đúng vai trò thì không được thực hiện chức năng.

Cách đặt tên Test Scenario nên ngắn gọn, bắt đầu bằng “Kiểm tra…” hoặc “Xác minh…”.

**Naming Convention:**

* **Test Scenario ID:** `TS_<UseCaseID>_<STT>`

  * Ví dụ: `TS_UC02_01`
* **Test Scenario Name:** Viết bằng tiếng Việt, nêu rõ hành vi cần kiểm thử.

  * Ví dụ: `Kiểm tra đăng nhập thành công`


### Bước 3: Viết Test Case cho từng Test Scenario

Với mỗi Test Scenario, viết một hoặc nhiều Test Case chi tiết.
Các trường nên có:

| Trường           | Ý nghĩa                              |
| ---------------- | ------------------------------------ |
| Test Case ID     | Mã định danh duy nhất của test case  |
| Test Scenario ID | Scenario mà test case thuộc về       |
| Use Case         | Use Case mà test case thuộc về       |
| Test Case Title  | Tên test case                  |
| Test Case Description          | Mô tả ngắn mục tiêu test               |
| Assumptions      | Giả định khi kiểm thử          |
| Pre-condition    | Điều kiện cần có trước khi chạy test |
| Test Data        | Dữ liệu đầu vào dùng để kiểm thử     |
| Steps            | Các bước thực hiện                   |
| Expected Outcome | Kết quả mong đợi                     |
| Post-condition   | Trạng thái hệ thống sau kiểm thử     |

**Phân biệt Assumptions và Pre-condition**

| Thành phần        | Ý nghĩa                                                                                                                                                                                                           | Ví dụ                                                                                               |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| **Assumptions**   | Các giả định về môi trường, dữ liệu hoặc công cụ kiểm thử. Đây là những điều được giả định là đúng để test case có thể chạy ổn định, nhưng không phải trạng thái nghiệp vụ trực tiếp của hệ thống trước khi test. | Trình duyệt được hỗ trợ; server hoạt động bình thường; dữ liệu test đã được seed sẵn.               |
| **Pre-condition** | Điều kiện bắt buộc phải tồn tại ngay trước khi thực hiện test. Nếu không thỏa điều kiện này thì test case không thể chạy đúng mục tiêu.                                                                           | Người dùng chưa đăng nhập; tài khoản `0912345678` đang hoạt động; tài khoản chưa bị khóa đăng nhập. |

Nói ngắn gọn:
**Assumptions = giả định nền để test chạy được.**
**Pre-condition = trạng thái bắt buộc của hệ thống/người dùng ngay trước khi chạy test.**

**Naming Convention:**

* **Test Case ID:** `TC_<UseCaseID>_<ScenarioSTT>_<CaseSTT>`

  * Ví dụ: `TC_UC02_01_01`
* **Test Case Title:** Mô tả ngắn gọn trường hợp kiểm thử.

  * Ví dụ: `Đăng nhập thành công bằng tài khoản hợp lệ`

---

## C. Lưu ý khi viết Test Scenario & Test Case

* Test case phải **đơn giản, rõ ràng, dễ hiểu**.
* Viết theo góc nhìn **người dùng cuối**, không viết theo góc nhìn code.
* Tránh lặp lại các test case giống nhau.
* Không tự giả định thêm nghiệp vụ ngoài đặc tả.
* Đảm bảo **100% coverage** đối với các requirement/use case được giao.
* Test case phải có ID rõ ràng để truy vết.
* Nên áp dụng các kỹ thuật kiểm thử như:

  * Positive testing.
  * Negative testing.
  * Boundary value testing.
  * Equivalence partitioning.
  * State transition testing.
  * Role/permission testing.
* Test case nên có khả năng **self-cleaning**, tức là sau khi chạy xong hệ thống trở về trạng thái phù hợp để có thể chạy lại.
* Test case phải **repeatable**, chạy nhiều lần với cùng điều kiện thì cho cùng kết quả.
---

## D. Ví dụ minh họa 

### Use Case UC02 - Đăng nhập

### 1. Danh sách Test Scenario mẫu

| Module                  | Use Case ID | Test Scenario ID | Test Scenario Name                                                       | # Test Cases |
| ----------------------- | ----------- | ---------------- | ------------------------------------------------------------------------ | -----------: |
| Portal & Authentication | UC02        | TS_UC02_01       | Kiểm tra đăng nhập thành công bằng tài khoản hợp lệ                      |            1 |
| Portal & Authentication | UC02        | TS_UC02_02       | Kiểm tra đăng nhập thất bại khi sai mật khẩu                             |            1 |
| Portal & Authentication | UC02        | TS_UC02_03       | Kiểm tra khóa tạm thời tài khoản sau 5 lần đăng nhập sai liên tiếp       |            1 |
| Portal & Authentication | UC02        | TS_UC02_04       | Kiểm tra từ chối đăng nhập với tài khoản nội bộ bị vô hiệu hóa bởi Admin |            0 |
| Portal & Authentication | UC02        | TS_UC02_05       | Kiểm tra điều hướng giao diện đúng theo vai trò sau khi đăng nhập        |            0 |


## 2. Test Case mẫu

### Test Case 1: Đăng nhập thành công bằng tài khoản hợp lệ

| Trường                    | Nội dung                                                                                                                                                                                                                                    |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Test Case ID**          | TC_UC02_01_01                                                                                                                                                                                                                               |
| **Test Scenario ID**      | TS_UC02_01                                                                                                                                                                                                                                  |
| **Use Case**              | UC02 - Đăng nhập                                                                                                                                                                                                                            |
| **Test Case Title**       | Đăng nhập thành công bằng tài khoản Người hiến máu hợp lệ                                                                                                                                                                                   |
| **Test Case Description** | Kiểm tra hệ thống cho phép người dùng đăng nhập khi nhập đúng thông tin định danh và mật khẩu, sau đó cấp Access Token và chuyển hướng đến giao diện phù hợp với vai trò.                                                                   |
| **Assumptions**           | Hệ thống đang hoạt động bình thường; cơ sở dữ liệu có sẵn tài khoản test; trình duyệt đang dùng được hệ thống hỗ trợ; kết nối mạng ổn định.                                                                                                 |
| **Pre-condition**         | Người dùng chưa đăng nhập vào hệ thống; tài khoản `0912345678` tồn tại; tài khoản đang hoạt động; tài khoản không bị khóa tạm thời do đăng nhập sai; bộ đếm đăng nhập sai hiện tại có thể bằng 0 hoặc lớn hơn 0 nhưng chưa đạt ngưỡng khóa. |
| **Test Data**             | Thông tin định danh: `0912345678` <br> Mật khẩu: `Valid@123` <br> Vai trò tài khoản: Người hiến máu                                                                                                                                         |
| **Steps**                 | 1. Truy cập trang đăng nhập của hệ thống. <br> 2. Nhập `0912345678` vào trường thông tin định danh. <br> 3. Nhập `Valid@123` vào trường mật khẩu. <br> 4. Nhấn nút **Đăng nhập**.                                                           |
| **Expected Outcome**      | Hệ thống xác thực tài khoản thành công; reset bộ đếm đăng nhập sai về 0; sinh và trả về Access Token JWT cho Client; chuyển hướng người dùng đến giao diện dành cho Người hiến máu; không hiển thị thông báo lỗi.                           |
| **Post-condition**        | Người dùng đang trong phiên đăng nhập hợp lệ; Client lưu Access Token; bộ đếm đăng nhập sai của tài khoản được đặt về 0.                                                                                                                    |

### Test Case 2: Đăng nhập thất bại khi nhập sai mật khẩu nhưng chưa đạt ngưỡng khóa

| Trường                    | Nội dung                                                                                                                                                                                                                                      |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Test Case ID**          | TC_UC02_02_01                                                                                                                                                                                                                                 |
| **Test Scenario ID**      | TS_UC02_02                                                                                                                                                                                                                                    |
| **Use Case**              | UC02 - Đăng nhập                                                                                                                                                                                                                              |
| **Test Case Title**       | Đăng nhập thất bại khi nhập sai mật khẩu lần thứ nhất                                                                                                                                                                                         |
| **Test Case Description** | Kiểm tra hệ thống từ chối đăng nhập khi người dùng nhập sai mật khẩu, đồng thời tăng bộ đếm đăng nhập sai và thông báo số lần thử còn lại.                                                                                                    |
| **Assumptions**           | Hệ thống đang hoạt động bình thường; cơ sở dữ liệu có sẵn tài khoản test; kết nối đến cơ sở dữ liệu ổn định; chưa có lỗi server trong quá trình xác thực.                                                                                     |
| **Pre-condition**         | Người dùng chưa đăng nhập vào hệ thống; tài khoản `0912345678` tồn tại; tài khoản đang hoạt động; tài khoản chưa bị khóa tạm thời; số lần đăng nhập sai liên tiếp trong vòng 30 phút hiện tại là 0.                                           |
| **Test Data**             | Thông tin định danh: `0912345678` <br> Mật khẩu sai: `Wrong@123`                                                                                                                                                                              |
| **Steps**                 | 1. Truy cập trang đăng nhập của hệ thống. <br> 2. Nhập `0912345678` vào trường thông tin định danh. <br> 3. Nhập `Wrong@123` vào trường mật khẩu. <br> 4. Nhấn nút **Đăng nhập**.                                                             |
| **Expected Outcome**      | Hệ thống không cấp Access Token; không chuyển hướng vào hệ thống; tăng bộ đếm đăng nhập sai của tài khoản từ 0 lên 1; lưu thời gian đăng nhập sai hiện tại; hiển thị thông báo: “Tài khoản hoặc mật khẩu không chính xác. Bạn còn 4 lần thử.” |
| **Post-condition**        | Người dùng vẫn ở trạng thái chưa đăng nhập; bộ đếm đăng nhập sai của tài khoản là 1; tài khoản chưa bị khóa.                                                                                                                                  |

### Test Case 3: Khóa tạm thời tài khoản sau 5 lần đăng nhập sai liên tiếp

| Trường                    | Nội dung                                                                                                                                                                                                                                                                                         |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Test Case ID**          | TC_UC02_03_01                                                                                                                                                                                                                                                                                    |
| **Test Scenario ID**      | TS_UC02_03                                                                                                                                                                                                                                                                                       |
| **Use Case**              | UC02 - Đăng nhập                                                                                                                                                                                                                                                                                 |
| **Test Case Title**       | Khóa tạm thời tài khoản sau lần nhập sai mật khẩu thứ 5 liên tiếp                                                                                                                                                                                                                                |
| **Test Case Description** | Kiểm tra cơ chế bảo vệ brute-force: nếu người dùng nhập sai mật khẩu 5 lần liên tiếp trong vòng 30 phút, hệ thống phải khóa quyền đăng nhập của tài khoản trong 30 phút.                                                                                                                         |
| **Assumptions**           | Hệ thống đang hoạt động bình thường; thời gian hệ thống được đồng bộ chính xác; tài khoản test có thể được reset trạng thái trước khi chạy test; kết nối mạng và cơ sở dữ liệu ổn định.                                                                                                          |
| **Pre-condition**         | Người dùng chưa đăng nhập vào hệ thống; tài khoản `0912345678` tồn tại; tài khoản đang hoạt động; tài khoản chưa bị khóa tạm thời; tài khoản đã có 4 lần đăng nhập sai liên tiếp trong vòng 30 phút gần nhất.                                                                                    |
| **Test Data**             | Thông tin định danh: `0912345678` <br> Mật khẩu sai lần thứ 5: `Wrong@123`                                                                                                                                                                                                                       |
| **Steps**                 | 1. Truy cập trang đăng nhập của hệ thống. <br> 2. Nhập `0912345678` vào trường thông tin định danh. <br> 3. Nhập `Wrong@123` vào trường mật khẩu. <br> 4. Nhấn nút **Đăng nhập**. <br> 5. Thử đăng nhập lại ngay bằng đúng mật khẩu `Valid@123`.                                                 |
| **Expected Outcome**      | Sau bước 4, hệ thống không cấp Access Token; tăng bộ đếm đăng nhập sai lên 5; khóa quyền đăng nhập của tài khoản trong 30 phút. Sau bước 5, dù nhập đúng mật khẩu, hệ thống vẫn từ chối đăng nhập và hiển thị thông báo: “Tài khoản của bạn đang bị khóa tạm thời. Vui lòng thử lại sau X phút.” |
| **Post-condition**        | Người dùng vẫn chưa đăng nhập; tài khoản ở trạng thái bị khóa tạm thời do đăng nhập sai 5 lần liên tiếp; thời điểm hết khóa được ghi nhận là sau 30 phút kể từ lúc bị khóa.                                                                                                                      |

---

## E. Kết quả cần bàn giao

1. **Danh sách Test Scenario** cho từng Use Case.
2. **Danh sách Test Case chi tiết** cho từng Test Scenario.