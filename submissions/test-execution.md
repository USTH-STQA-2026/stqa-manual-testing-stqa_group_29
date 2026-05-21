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
# Detailed results

| TC       | REQ    | Expected result (short summary)                                       | Observed result    | Conclusion | Evidence                                                             | Bug |
| -------- | ------ | --------------------------------------------------------------------- | ------------------ | ---------- | -------------------------------------------------------------------- | --- |
| TC-01-01 | REQ-01 | Display the library homepage with the username "Nguyễn Thủ Thư"       | **as expected**    | **Pass**   | [[TC-01-01.png]]                                                     |     |
| TC-01-02 | REQ-01 | Login fails, display error message: "Member not found"                | **as expected**    | **Pass**   | [[TC-01-02.png]]                                                     |     |
| TC-01-03 | REQ-01 | Login fails, display error message: "Incorrect password"              | **as expected**    | **Pass**   | [[TC-01-03.png]]                                                     |     |
| TC-01-04 | REQ-01 | Login fails, display error message: "Please enter email and password" | **as expected**    | **Pass**   | [[TC-01-04 (1).png]]<br>[[TC-01-04 (2).png]]<br>[[TC-01-04 (3).png]] |     |
| TC-02-01 | REQ-02 | Display all 20 books with their relevant info                         | **as expected**    | **Pass**   | [[TC-02-01 (1).png]]<br>[[TC-02-01 (2).png]]                         |     |
| TC-02-02 | REQ-02 | (same as above)                                                       | **as expected**    | **Pass**   | [[TC-02-02 (1).png]]<br>[[TC-02-02 (2).png]]                         |     |
| TC-02-03 | REQ-02 | The book's status changes from "Available" to "Borrowed"              | **as expected**    | **Pass**   | [[TC-02-03.png]]                                                     |     |
| TC-03-01 | REQ-03 | Display books containing "Lập trình"                                  | **as expected**    | **Pass**   | [[TC-03-01.png]]                                                     |     |
| TC-03-02 | REQ-03 | Display books of author "Vũ Thị Mai"                                  | **as expected**    | **Pass**   | [[TC-03-02.png]]                                                     |     |
| TC-03-03 | REQ-03 | Display books of "Công nghệ" category                                 | Display empty list | **Fail**   | [[TC-03-03.png]]                                                     |     |
| TC-03-04 | REQ-03 | (same as above)                                                       | **as expected**    | **Pass**   | [[TC-03-04.png]]                                                     |     |
|          |        |                                                                       |                    |            |                                                                      |     |

---
# Summary

| TC type                    | Amount         |
| -------------------------- | -------------- |
| Total amount of test cases | 11             |
| Pass                       | 10             |
| Fail                       | 1              |
| Blocked                    | 0              |
| Not Run                    | 0              |
| **Pass rate**              | 10/11 \| 90.9% |

## Results by each REQ

| REQ    | Amount of TCs | Pass | Fail | Pass rate |
| ------ | ------------- | ---- | ---- | --------- |
| REQ-01 | 4             | 4    | 0    | 100%      |
| REQ-02 | 3             | 3    | 0    | 100%      |
| REQ-03 | 4             | 3    | 1    | 75%       |
| REQ-04 |               |      |      |           |
| REQ-05 |               |      |      |           |
| REQ-06 |               |      |      |           |
| REQ-07 |               |      |      |           |
| REQ-08 |               |      |      |           |
