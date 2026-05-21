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

## IDM — Login (REQ-01)

| Characteristic            | Block     | Value                 | Expected result                                     |
| ------------------------- | --------- | --------------------- | --------------------------------------------------- |
| Email exists in database? | Yes       | librarian@library.com | Successful login                                    |
|                           | No        | noone@email.com       | Display message: email not found                    |
| Correct password?         | Yes       | admin123              | Successful login                                    |
|                           | No        | wrongpass             | Display message: wrong password                     |
| Blank input field?        | Not blank | a@b.c, abc            | Processes inputs according to above characteristics |
|                           | Blank     | `""`                  | Display message: "Please enter"                     |

## IDM — Search for book (REQ-03)

| Characteristic           | Block                  | Value        | Expected result                                 |
| ------------------------ | ---------------------- | ------------ | ----------------------------------------------- |
| Book exists in database? | Yes (book name)        | "Lập trình"  | Display books containing "Lập trình"            |
|                          | Yes (author name)      | "Vũ Thị Mai" | Display books of author "Vũ Thị Mai"            |
|                          | Yes (category)         | "Công nghệ"  | Display books belonging to category "Công nghệ" |
|                          | No                     | "XYZ123"     | Display message "No books found"                |
| Case insensitive?        | Yes (book/author name) | "lập trình"  | Same result as "Lập trình"                      |
|                          | Yes (category)         | "vũ thị mai" | Same result as "Vũ Thị Mai"                     |

## IDM — Borrowing a book (REQ-04, REQ-05)

| Characteristic                      | Block                | Value                        | Expected result                          |
| ----------------------------------- | -------------------- | ---------------------------- | ---------------------------------------- |
| State of book?                      | Available            | BOOK001                      | Borrow allowed                           |
|                                     | Borrowed             | BOOK003                      | Borrow rejected                          |
|                                     | Lost                 | BOOK007                      | Borrow rejected                          |
| State of member?                    | Active               | MEM002                       | Borrow allowed                           |
|                                     | Suspended            | MEM004                       | Borrow rejected, display error           |
|                                     | Expired              | MEM005                       | Borrow rejected                          |
| Amount of books currently borrowed? | < 3 (BVA: 0, 1, 2)   | MEM006 (0 books)             | Borrow rejected                          |
|                                     | = 3 (BVA: max limit) | Member with 3 books borrowed | Borrow rejected, announce exceeded limit |

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

| Test Case ID | Test Objective                                          | Preconditions                                        | Test Steps                                                                                         | Input Data                                               | Expected Result                                                                                                                | REQ    | Testing Technique |
| ------------ | ------------------------------------------------------- | ---------------------------------------------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ | ------ | ----------------- |
| TC-01-01     | Login with correct email and password                   | Website is opened                                    | Enter librarian@library.com  and `admin123` into the Email and Password fields respectively        | - Email: librarian@library.com <br>-Password: admin123   | Display the library homepage with the corresponding username "Nguyễn Thủ Thư"                                                  | REQ-01 | EP                |
| TC-01-02     | Login with incorrect email                              | Website is opened                                    | Enter noone@email.com and `password123` respectively                                               | - Email: noone@email.com<br>- Password: admin123         | Login fails, display error message: "Member not found"                                                                         | REQ-01 | EP                |
| TC-01-03     | Login with incorrect password                           | Website is opened, member's email already exists     | Enter librarian@library.com and `wrongpass` respectively                                           | - Email: librarian@library.com <br>- Password: wrongpass | Login fails, display error message: "Incorrect password"                                                                       | REQ-01 | EP                |
| TC-01-04     | Leave email, password, or both blank                    | Website is opened                                    | Leave blank, or only enter a@b.c into the email field, or only enter `abc` into the password field | Blank, or only email: a@b.c, or only password: abc       | Login fails, display error message: "Please enter email and password"                                                          | REQ-01 | EP                |
| TC-02-01     | View book list as a Librarian                           | Logged in as librarian                               | Count and view details of books displayed on the homepage                                          | x                                                        | Display all 20 book titles with full information: title, author, genre, publication year, status (Available / Borrowed / Lost) | REQ-02 | EP                |
| TC-02-02     | View book list as a Member                              | Logged in as member                                  | (same as above)                                                                                    | x                                                        | (same as above)                                                                                                                | REQ-02 | EP                |
| TC-02-03     | Instant update upon borrowing/returning books           | Logged in as member; member eligible to borrow books | Click the borrow button for book BOOK001 "Lập trình Flutter cơ bản"                                | x                                                        | The book's status changes from "Available" to "Borrowed"                                                                       | REQ-02 | EP                |
| TC-03-01     | Search for book by title without proper capitalization  | Logged in                                            | Enter the keyword `lập trình` into the search box (by book title or author).                       | Keyword: "lập trình"                                     | Display book titles: "Lập trình Flutter cơ bản" and "Nhập môn lập trình Python"                                                | REQ-03 | EP                |
| TC-03-02     | Search for book by author without proper capitalization | (same as above)                                      | Enter `vũ thị mai` into the search box (by book title or author).                                  | Keyword: "vũ thị mai"                                    | Display the book title: "Nguyên lý kế toán" with the author "Vũ Thị Mai".                                                      | REQ-03 | EP                |
| TC-03-03     | Filter books by category without proper capitalization  | (same as above)                                      | Enter the keyword `công nghệ` into the category filter box                                         | Keyword: "công nghệ"                                     | Display book titles belonging to the "Công nghệ" category.                                                                     | REQ-03 | EP                |
|              |                                                         |                                                      |                                                                                                    |                                                          |                                                                                                                                |        |                   |


---
# Summary
*Do chia các trường hợp kiểm thử theo REQ nên cột "REQ phủ" sẽ được lược bỏ.*

| REQ       | Amount of TCs     | IDM technique used |
| --------- | ----------------- | ------------------ |
| REQ-01    | 4                 | EP                 |
| REQ-02    | 3                 | EP                 |
| REQ-03    | 3                 | EP                 |
| REQ-04    |                   |                    |
| REQ-05    |                   |                    |
| REQ-06    |                   |                    |
| REQ-07    |                   |                    |
| REQ-08    |                   |                    |
| **Total** | **<!-- ≥ 20 -->** |                    |
