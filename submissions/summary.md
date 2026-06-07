# Test Summary

> **Hướng dẫn**: Đây là hoạt động **Quality Assurance** — bạn đánh giá chất lượng tổng thể của phần mềm, không chỉ liệt kê lỗi.

---

# 1. Group info

| Item                     | Details                    |
| ------------------------ | -------------------------- |
| **Group**                | Group 29                   |
| **Class**                | 252ICT2012.L1              |
| **Date of report**       | From 16/05 to 13/06/2026   |
| **System under testing** | https://stqa.rbc.vn — v1.0 |

---

# 2. Summary of results

| TC type                    | Amount             |
| :------------------------- | :----------------- |
| Total amount of test cases | 43                 |
| Pass                       | 34                 |
| Fail                       | 9                  |
| Blocked                    | 0                  |
| Not Run                    | 0                  |
| **Pass rate**              | **34/43 \| 79.1%** |
| **Số bug phát hiện**       | **9**              |

## Results by each REQ

| REQ        | Amount of TCs | Pass | Fail | Pass rate | Related Bugs       |
| :--------- | :------------ | :--- | :--- | :-------- | :----------------- |
| **REQ-01** | 6             | 6    | 0    | 100%      |                    |
| **REQ-02** | 4             | 4    | 0    | 100%      |                    |
| **REQ-03** | 6             | 5    | 1    | 83.3%     | **BUG-01**         |
| **REQ-04** | 8             | 6    | 2    | 75.0%     | **BUG-02, BUG-03** |
| **REQ-05** | 4             | 2    | 2    | 50.0%     | **BUG-04, BUG-05** |
| **REQ-06** | 4             | 3    | 1    | 75.0%     | **BUG-07**         |
| **REQ-07** | 6             | 4    | 2    | 66.7%     | **BUG-08, BUG-09** |
| **REQ-08** | 5             | 3    | 2    | 60.0%     | **BUG-04, BUG-06** |

## Bugs by severity

| Severity | Amount | Bug ID                                                 |
| -------- | ------ | ------------------------------------------------------ |
| Critical | 1      | BUG-04                                                 |
| High     | 1      | BUG-02                                                 |
| Medium   | 7      | BUG-01, BUG-03, BUG-05, BUG-06, BUG-07, BUG-08, BUG-09 |
| Low      | 0      |                                                        |

---

# 3. Testing techniques applied

| Technique      | Applied for which REQ? | Amount of test cases | Explain how the technique was used                                                                                             |
| -------------- | ---------------------- | -------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| EP             | All                    | 41                   | For each value group that would cause the system to behave the same, 1 single value is chosen as the representative for the TC |
| BVA            | REQ-04                 | 2                    | Checking for off-by-one and wrong sign errors                                                                                  |
| Decision Table | REQ-04                 | 7                    | Isolating attributes to prevent errors from masking each other                                                                 |

---

# 4. Analysis of the software's quality

### 4.1. Strengths
- Proper checking for email and password on login
- Details of books
- General borrowing and returning of books
- Management system for librarians
### 4.2. Weaknesses
- Access control
- Creation of new member account
- Lack of overdue warning and indication

---

# 5. Suggestions on bug fixing priority

> 💡 Đây là phần **Quality Assurance**: bạn không chỉ tìm lỗi mà còn **đề xuất thứ tự ưu tiên** sửa chữa và đánh giá tác động.
> Nêu rõ tiêu chí ưu tiên: dựa vào **severity** (mức độ nghiêm trọng kỹ thuật) và/hoặc **priority** (mức độ ưu tiên kinh doanh).

| Bug    | Severity | Priority | Reason of priority                                                                               |
| ------ | -------- | -------- | ------------------------------------------------------------------------------------------------ |
| BUG-01 | Medium   | P3       | Books can still be found if the letter cases are correct                                         |
| BUG-02 | High     | P2       | Member is still prevented from borrowing more than 4 books                                       |
| BUG-03 | Medium   | P3       | Incorrect message, but contacting help desk should clear that up                                 |
| BUG-04 | Critical | P1       | Serious privacy and security breach                                                              |
| BUG-05 | Medium   | P3       | No overdue message doesn't change the fact that the book is overdue                              |
| BUG-06 | Medium   | P2       | Should improve book and member management for librarians to avoid missing overdue fees           |
| BUG-07 | Medium   | P1       | May cause people to be unfairly charged for overdue borrows                                      |
| BUG-08 | Medium   | P1       | Prevents people from signing up                                                                  |
| BUG-09 | Medium   | P2       | The account simply won't work, and user can simply create another account with the correct email |

---

# 6. Conclusion

The system is not yet ready to be deployed, as there are still too many bugs affecting essential parts of the system.

---

# 7. Lessons learned (optional)

- When a member of the group pushes a commit, other members must check out the commit and pull before continuing their work
- Doing things in order (TC -> execution -> bug report) is always better

---

# 8.AI Usage Declaration (Optional)
	
> Nếu nhóm có sử dụng công cụ AI (ChatGPT, Copilot, Gemini...), hãy ghi rõ bên dưới. Khai báo trung thực **không ảnh hưởng điểm** — đây là kỹ năng minh bạch trong nghề.

| AI Tool | Purpose / Section | Review & Verification Process                                                                                                                                                                        |
| ------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Gemini  | Test Execution    | Cross-check the test execution results against the SRS document. Verified that all test cases align with the functional requirements and manually corrected any discrepancies in the execution logs. |
