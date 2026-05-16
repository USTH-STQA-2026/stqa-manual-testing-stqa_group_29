# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Viết tối thiểu **20 TC** phủ đủ các chức năng chính (REQ-01 → REQ-08).
> Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.
> Tự tổ chức và phân nhóm test case theo cách hợp lý nhất.

| Thông tin      |                     |
| -------------- | ------------------- |
| **Nhóm**       | Nhóm 29             |
| **Ngày tạo**   | 16/05/2026`         |
| **Hệ thống**   | https://stqa.rbc.vn |
| **Tham chiếu** | SRS v1.0            |

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

> 📖 **Textbook:** Chương 6 — *Input Domain Modeling*, Paul Ammann & Jeff Offutt.
> **Trước khi viết Test Case**, nhóm **phải** phân tích miền đầu vào bằng bảng IDM bên dưới.
> Mỗi chức năng cần xác định: **Đặc tính (Characteristic)**, **Phân vùng (Block/Partition)**, và **Giá trị đại diện (Value)**.

### IDM — Đăng nhập (REQ-01)

| Đặc tính (Characteristic)  | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi             |
| -------------------------- | ----------------- | ------------------------ | ---------------------------- |
| Email có tồn tại trong DB? | Có                | `librarian@library.com`  | Đăng nhập thành công         |
|                            | Không             | `noone@email.com`        | Thông báo lỗi                |
| Mật khẩu có đúng?          | Đúng              | `admin123`               | Đăng nhập thành công         |
|                            | Sai               | `wrongpass`              | Thông báo lỗi                |
| Ô nhập có rỗng?            | Không rỗng        | (giá trị bất kỳ)         | Xử lý bình thường            |
|                            | Rỗng              | `""`                     | Thông báo "Vui lòng nhập..." |

### IDM — Tìm kiếm sách (REQ-03)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Từ khóa có tồn tại trong DB? | Có (tên sách) | `"Flutter"` | Hiển thị sách chứa "Flutter" |
| | Có (tên tác giả) | `"Nguyễn"` | Hiển thị sách của tác giả Nguyễn |
| | Không | `"XYZ123"` | Danh sách rỗng |
| Phân biệt HOA/thường? | Chữ thường | `"flutter"` | Kết quả giống "Flutter" |
| | Chữ HOA | `"FLUTTER"` | Kết quả giống "Flutter" |

### IDM — Mượn sách (REQ-04, REQ-05)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Trạng thái sách? | Có sẵn | BOOK001 | Cho phép mượn |
| | Đang mượn | BOOK003 | Không cho phép |
| | Thất lạc | BOOK007 | Không cho phép |
| Trạng thái thành viên? | Hoạt động | MEM002 | Cho phép mượn |
| | Tạm ngưng | MEM004 | Từ chối, thông báo lỗi |
| | Hết hạn | MEM005 | Từ chối, thông báo lỗi |
| Số sách đang mượn? | < 3 (BVA: 0, 1, 2) | MEM006 (0 sách) | Cho phép mượn |
| | = 3 (BVA: giới hạn) | MEM đã mượn 3 sách | Từ chối, thông báo vượt giới hạn |

### IDM — `<!-- Nhóm tự bổ sung cho REQ-05 đến REQ-08 -->`

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| `<!-- Nhóm tự điền -->` | | | |

> 💡 **Gợi ý kỹ thuật**: Sử dụng **Phân lớp tương đương (EP)** cho các phân vùng rời rạc, **Phân tích giá trị biên (BVA)** cho các phân vùng số (ví dụ: giới hạn 3 sách). Xem textbook §6.1–6.3.

---

## Bước 2: Test Cases
*Chúng ta sẽ phân nhóm các trường hợp kiểm thử theo REQ 01-08.*

<!-- Tự tổ chức bảng test case: có thể chia nhóm theo chức năng, theo REQ, hoặc theo luồng nghiệp vụ — tùy nhóm quyết định. -->
<!-- Mỗi TC phải ánh xạ ngược về *ít nhất* 1 dòng trong bảng IDM ở Bước 1. -->

| Mã TC    | Mục tiêu kiểm thử                     | Tiền điều kiện                                   | Bước thực hiện                                                                   | Dữ liệu đầu vào                                          | Kết quả mong đợi                                                           | REQ    | Kỹ thuật |
| -------- | ------------------------------------- | ------------------------------------------------ | -------------------------------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------------------------- | ------ | -------- |
| TC-01-01 | Đăng nhập bằng email và mật khẩu đúng | Trang web đã mở                                  | Nhập vào lần lượt librarian@library.com và admin123 vào các ô Email và Mật khẩu  | - Email: librarian@library.com <br>- Mật khẩu: admin123  | Hiện trang chủ của thư viện, với tên người dùng tương ứng "Nguyễn Thủ Thư" | REQ-01 | EP       |
| TC-01-02 | Đăng nhập bằng email sai              | Trang web đã mở                                  | Nhập vào lần lượt noone@email.com và password123                                 | - Email: noone@email.com<br>- Mật khẩu: admin123         | Không đăng nhập được, báo lỗi "Không tìm thấy thành viên"                  | REQ-01 | EP       |
| TC-01-03 | Đăng nhập bằng mật khẩu sai           | Trang web đã mở, email của thành viên đã tồn tại | Nhập vào lần lượt librarian@library.com và wrongpass                             | - Email: librarian@library.com <br>- Mật khẩu: wrongpass | Không đăng nhập được, báo lỗi "Mật khẩu không đúng"                        | REQ-01 | EP       |
| TC-01-04 | Bỏ trống email, mật khẩu hoặc cả hai  | Trang web đã mở                                  | Không nhập gì, hoặc chỉ nhập a@b.c vào ô email, hoặc chỉ nhập abc vào ô mật khẩu | Rỗng, hoặc chỉ email: a@b.c, hoặc chỉ mật khẩu: abc      | Không đăng nhập được, báo lỗi "Vui lòng nhập email và mật khẩu"            | REQ-01 | EP       |
|          |                                       |                                                  |                                                                                  |                                                          |                                                                            |        |          |

---

## Tổng hợp
*Do chia các trường hợp kiểm thử theo REQ nên cột "REQ phủ" sẽ được lược bỏ.*

| Nhóm chức năng | Số TC             | Kỹ thuật IDM áp dụng |
| -------------- | ----------------- | -------------------- |
| REQ-01         | 4                 | EP                   |
| **Tổng**       | **<!-- ≥ 20 -->** |                      |
