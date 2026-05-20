# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Viết tối thiểu **20 TC** phủ đủ các chức năng chính (REQ-01 → REQ-08).
> Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.
> Tự tổ chức và phân nhóm test case theo cách hợp lý nhất.

| Thông tin      |                     |
| -------------- | ------------------- |
| **Nhóm**       | Nhóm 29             |
| **Ngày tạo**   | 16/05/2026          |
| **Hệ thống**   | https://stqa.rbc.vn |
| **Tham chiếu** | SRS v1.0            |

---

# Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

> 📖 **Textbook:** Chương 6 — *Input Domain Modeling*, Paul Ammann & Jeff Offutt.
> **Trước khi viết Test Case**, nhóm **phải** phân tích miền đầu vào bằng bảng IDM bên dưới.
> Mỗi chức năng cần xác định: **Đặc tính (Characteristic)**, **Phân vùng (Block/Partition)**, và **Giá trị đại diện (Value)**.

## IDM — Đăng nhập (REQ-01)

| Đặc tính (Characteristic)  | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi             |
| -------------------------- | ----------------- | ------------------------ | ---------------------------- |
| Email có tồn tại trong DB? | Có                | `librarian@library.com`  | Đăng nhập thành công         |
|                            | Không             | `noone@email.com`        | Thông báo lỗi                |
| Mật khẩu có đúng?          | Đúng              | `admin123`               | Đăng nhập thành công         |
|                            | Sai               | `wrongpass`              | Thông báo lỗi                |
| Ô nhập có rỗng?            | Không rỗng        | (giá trị bất kỳ)         | Xử lý bình thường            |
|                            | Rỗng              | `""`                     | Thông báo "Vui lòng nhập..." |
## IDM - Xem danh sách sách (REQ-02) | chưa làm
## IDM — Tìm kiếm sách (REQ-03)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Từ khóa có tồn tại trong DB? | Có (tên sách) | `"Flutter"` | Hiển thị sách chứa "Flutter" |
| | Có (tên tác giả) | `"Nguyễn"` | Hiển thị sách của tác giả Nguyễn |
| | Không | `"XYZ123"` | Danh sách rỗng |
| Phân biệt HOA/thường? | Chữ thường | `"flutter"` | Kết quả giống "Flutter" |
| | Chữ HOA | `"FLUTTER"` | Kết quả giống "Flutter" |

## IDM — Mượn sách (REQ-04, REQ-05)

| Đặc tính (Characteristic) | Phân vùng (Block)   | Giá trị đại diện (Value) | Kết quả mong đợi                 |
| ------------------------- | ------------------- | ------------------------ | -------------------------------- |
| Trạng thái sách?          | Có sẵn              | BOOK001                  | Cho phép mượn                    |
|                           | Đang mượn           | BOOK003                  | Không cho phép                   |
|                           | Thất lạc            | BOOK007                  | Không cho phép                   |
| Trạng thái thành viên?    | Hoạt động           | MEM002                   | Cho phép mượn                    |
|                           | Tạm ngưng           | MEM004                   | Từ chối, thông báo lỗi           |
|                           | Hết hạn             | MEM005                   | Từ chối, thông báo lỗi           |
| Số sách đang mượn?        | < 3 (BVA: 0, 1, 2)  | MEM006 (0 sách)          | Cho phép mượn                    |
|                           | = 3 (BVA: giới hạn) | MEM đã mượn 3 sách       | Từ chối, thông báo vượt giới hạn |

## IDM — `<!-- Nhóm tự bổ sung cho REQ-05 đến REQ-08 -->`

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| `<!-- Nhóm tự điền -->` | | | |

> 💡 **Gợi ý kỹ thuật**: Sử dụng **Phân lớp tương đương (EP)** cho các phân vùng rời rạc, **Phân tích giá trị biên (BVA)** cho các phân vùng số (ví dụ: giới hạn 3 sách). Xem textbook §6.1–6.3.

---

# Bước 2: Test Cases
*Chúng ta sẽ phân nhóm các trường hợp kiểm thử theo REQ 01-08.*
*Tên các test cases đặt theo định dạng: TC-(số REQ)-(01, 02, 03, ...)*

<!-- Tự tổ chức bảng test case: có thể chia nhóm theo chức năng, theo REQ, hoặc theo luồng nghiệp vụ — tùy nhóm quyết định. -->
<!-- Mỗi TC phải ánh xạ ngược về *ít nhất* 1 dòng trong bảng IDM ở Bước 1. -->

| Test Case ID | Test Objective                                | Preconditions                                                    | Test Steps                                                                                         | Input Data                                               | Expected Result                                                                                                          | REQ    | Testing Technique |
| ------------ | --------------------------------------------- | ---------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ | ------ | ----------------- |
| TC-01-01     | Login with correct email and password         | Website is opened                                                | Enter librarian@library.com  and `admin123` into the Email and Password fields respectively        | - Email: librarian@library.com <br>-Password: admin123   | Displays the library homepage with the corresponding username "Nguyen Thu Thu"                                           | REQ-01 | EP                |
| TC-01-02     | Login with incorrect email                    | Website is opened                                                | Enter noone@email.com and `password123` respectively                                               | - Email: noone@email.com<br>- Password: admin123         | Login fails, displays error message: "Member not found"                                                                  | REQ-01 | EP                |
| TC-01-03     | Login with incorrect password                 | Website is opened, member's email already exists                 | Enter librarian@library.com and `wrongpass` respectively                                           | - Email: librarian@library.com <br>- Password: wrongpass | Login fails, displays error message: "Incorrect password"                                                                | REQ-01 | EP                |
| TC-01-04     | Leave email, password, or both blank          | Website is opened                                                | Leave blank, or only enter a@b.c into the email field, or only enter `abc` into the password field | Blank, or only email: a@b.c, or only password: abc       | Login fails, displays error message: "Please enter email and password""                                                  | REQ-01 | EP                |
| TC-02-01     | View book list as an Administrator            | Logged into the website as an Administrator                      | Count and view details of books displayed on the homepage                                          | x                                                        | Displays all 20 book titles with full information: title, author, genre, publication year, status (Available / Borrowed) | REQ-02 | EP                |
| TC-02-02     | View book list as a Member                    | Logged into the website as a Member                              | (Same as above)                                                                                    | x                                                        | (Same as above)                                                                                                          | REQ-02 | EP                |
| TC-02-03     | Instant update upon borrowing/returning books | Logged in as a Member; member meets all criteria to borrow books | Click the borrow button for book BOOK001 "Lap trinh Flutter co ban"                                | x                                                        | The book's status changes from "Available" to "Borrowed"                                                                 | REQ-02 | EP                |
|              |                                               |                                                                  |                                                                                                    |                                                          |                                                                                                                          |        |                   |

---

# Tổng hợp
*Do chia các trường hợp kiểm thử theo REQ nên cột "REQ phủ" sẽ được lược bỏ.*

| Nhóm chức năng | Số TC             | Kỹ thuật IDM áp dụng |
| -------------- | ----------------- | -------------------- |
| REQ-01         | 4                 | EP                   |
| REQ-02         | 3                 | EP                   |
| REQ-03         |                   |                      |
| REQ-04         |                   |                      |
| REQ-05         |                   |                      |
| REQ-06         |                   |                      |
| REQ-07         |                   |                      |
| REQ-08         |                   |                      |
| **Tổng**       | **<!-- ≥ 20 -->** |                      |
