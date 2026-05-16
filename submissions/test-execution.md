# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

| Thông tin         |                           |
| ----------------- | ------------------------- |
| **Nhóm**          | Nhóm 29                   |
| **Ngày thực thi** | từ 16/05 đến 13/06/2026   |
| **Trình duyệt**   | Chrome `<!-- version -->` |
| **Hệ điều hành**  | Windows 11                |

---

## Kết quả chi tiết

| Mã TC    | Nhóm chức năng | Kết quả mong đợi (tóm tắt)                                      | Kết quả thực tế | Kết luận | Minh chứng                                                           | Bug |
| -------- | -------------- | --------------------------------------------------------------- | --------------- | -------- | -------------------------------------------------------------------- | --- |
| TC-01-01 | REQ-01         | Hiện trang chủ, tên người dùng "Nguyễn Thủ Thư"                 | như mong đợi    | **Pass** | [[TC-01-01.png]]                                                     |     |
| TC-01-02 | REQ-01         | Không đăng nhập được, báo lỗi "Không tìm thấy thành viên"       | như mong đợi    | **Pass** | [[TC-01-02.png]]                                                     |     |
| TC-01-03 | REQ-01         | Không đăng nhập được, báo lỗi "Mật khẩu không đúng"             | như mong đợi    | **Pass** | [[TC-01-03.png]]                                                     |     |
| TC-01-04 | REQ-01         | Không đăng nhập được, báo lỗi "Vui lòng nhập email và mật khẩu" | như mong đợi    | **Pass** | [[TC-01-04 (1).png]]<br>[[TC-01-04 (2).png]]<br>[[TC-01-04 (3).png]] |     |
|          |                |                                                                 |                 |          |                                                                      |     |

---

## Tổng hợp kết quả

| Chỉ số            | Giá trị |
| ----------------- | ------- |
| Tổng số test case | 4       |
| Pass              | 4       |
| Fail              | 0       |
| Blocked           | 0       |
| Not Run           | 0       |
| **Tỷ lệ Pass**    | 100%    |

### Kết quả theo nhóm chức năng

| Nhóm   | Tổng TC | Pass | Fail | Tỷ lệ Pass |
| ------ | ------- | ---- | ---- | ---------- |
| REQ-01 | 4       | 4    | 0    | 100%       |
| REQ-02 |         |      |      |            |
| REQ-03 |         |      |      |            |
| REQ-04 |         |      |      |            |
| REQ-05 |         |      |      |            |
| REQ-06 |         |      |      |            |
| REQ-07 |         |      |      |            |
| REQ-08 |         |      |      |            |
