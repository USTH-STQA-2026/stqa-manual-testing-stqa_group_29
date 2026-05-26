# Test Execution — Test Execution Results

| Information       |                           |
| ----------------- | ------------------------- |
| **Group** | Group 29                  |
| **Execution Date**| From 16/05 to 13/06/2026  |
| **Browser** | Chrome 148.0.xxxx.xx      |
| **OS** | Windows 11                |

---

# Detailed results

| TC ID     | REQ    | Expected result (short summary)                                            | Observed result                                                      | Conclusion | Evidence                                               | Bug        |
| :-------- | :----- | :------------------------------------------------------------------------- | :------------------------------------------------------------------- | :--------- | :----------------------------------------------------- | :--------- |
| **TC-01** | REQ-01 | Redirect to homepage, AppBar shows "Nguyễn Thủ Thư" + "Librarian"          | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-02** | REQ-01 | Redirect to homepage, AppBar shows "Nguyễn Học Bá" + "Member"              | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-03** | REQ-01 | Login fails, displays error "Member not found"                             | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-04** | REQ-01 | Login fails, displays error "Incorrect password"                           | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-05** | REQ-01 | Login fails, displays error "Please enter email and password"              | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-06** | REQ-01 | Login fails, displays error "Please enter email and password"              | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-07** | REQ-02 | Displays 20 books with details; BOOK001-"Available", BOOK003-"Borrowed"    | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-08** | REQ-02 | Member views all 20 books with exactly identical details as Librarian      | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-09** | REQ-02 | Status of BOOK001 changes from "Available" to "Borrowed" instantly         | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-10** | REQ-02 | Status of BOOK003 changes from "Borrowed" to "Available" instantly         | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-11** | REQ-03 | Displays list containing "Lập trình Flutter cơ bản"                        | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-12** | REQ-03 | Displays 2 books authored by "Nguyễn Minh Đức"                             | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-13** | REQ-03 | Case-insensitive search returns the same result for uppercase inputs       | Displays message: "Không tìm thấy sách"                              | **Fail**   | ![[Screenshot bug01-1.png]]![[Screenshot bug01-2.png]] | **BUG-01** |
| **TC-14** | REQ-03 | Non-existing keyword returns empty list and "No books found" msg           | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-15** | REQ-03 | Category filter dropdown displays exactly 8 books under "Technology"       | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-16** | REQ-03 | Intersection filter returns BOOK001 and BOOK009                            | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-17** | REQ-04 | Borrow success, new slip status is "Borrowing" with dueDate +14 days       | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-18** | REQ-04 | "Borrow" button is disabled or triggers "Book not available for borrowing" | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-19** | REQ-04 | Cannot borrow a lost book, displays status "Lost"                          | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-20** | REQ-04 | Reject request, displays "Member is currently suspended. Cannot borrow."   | Displays error message: "Thành viên đã hết hạn, không thể mượn sách" | **Fail**   | ![[Screenshot bug03.png]]                              | **BUG-03** |
| **TC-21** | REQ-04 | Reject request, displays "Member has expired. Cannot borrow."              | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-22** | REQ-04 | Successfully borrows the 3rd book (total borrow count becomes 3)           | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-23** | REQ-04 | Reject request, displays "Maximum borrow limit reached (3 books)"          | Member successfully borrows the 4th book                             | **Fail**   | ![[Screenshot bug02-1.png]]                            | **BUG-02** |
| **TC-24** | REQ-04 | Due date matches exactly 14 days after the current borrow date             | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-25** | REQ-05 | Slip status updates to "Returned", book returns to "Available", no warning | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-26** | REQ-05 | Book status reverts to "Available", slip is "Returned" + overdue warning   | Book returned successfully but no overdue warning is displayed       | **Fail**   | ![[Screenshot bug05.png]]                              | **BUG-05** |
| **TC-27** | REQ-05 | "Return" button does not exist or is disabled for a "Returned" slip        | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-28** | REQ-05 | Slip BR001 does not appear in "My borrow slips", actions are blocked       | Member can view and successfully return another member's book        | **Fail**   | ![[Screenshot bug04-1.png]]![[Screenshot bug04-2.png]] | **BUG-04** |
| **TC-29** | REQ-06 | Overdue slip BR001 changes status from "Borrowing" to "Overdue"            | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-30** | REQ-06 | "Check Overdue" button is completely hidden on Member's UI                 | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-31** | REQ-06 | Member sees slip BR001 status changed to "Overdue" in their list           | Overdue status update is invisible in Member's borrow records        | **Fail**   | ![[Screenshot bug07-1.png]]![[Screenshot bug07-2.png]] | **BUG-07** |
| **TC-32** | REQ-06 | Slips within the 14-day duration retain "Borrowing" status safely          | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-33** | REQ-07 | Member created successfully, member count increases from 6 to 7            | Form validation fails, displays: "Email không hợp lệ"                | **Fail**   | ![[Screenshot bug09-1.png]]                            | **BUG-08** |
| **TC-34** | REQ-07 | Block creation, form remains open, displays invalid email format error     | System displays success message and adds member with invalid email   | **Fail**   | ![[Screenshot bug09-1.png]]![[Screenshot bug09-2.png]] | **BUG-09** |
| **TC-35** | REQ-07 | Block creation, triggers standard format error message for email           | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-36** | REQ-07 | Block creation, triggers error message "Email already exists"              | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-37** | REQ-07 | Block creation, triggers input error message requiring Full Name           | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-38** | REQ-07 | "Members" management tab is completely omitted from Member UI              | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-39** | REQ-08 | Displays complete historical slip list belonging specifically to MEM002    | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-40** | REQ-08 | Displays empty record list or triggers "No slips found" notification       | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-41** | REQ-08 | Member only accesses slips where borrower ID matches their own account     | **as expected**                                                      | **Pass**   |                                                        |            |
| **TC-42** | REQ-08 | Block search access / Lookup filter elements are hidden from Member role   | Member can freely look up and query other members' borrow slips      | **Fail**   | ![[Screenshot bug04-1.png]]![[Screenshot bug04-2.png]] | **BUG-04** |
| **TC-43** | REQ-08 | Slips display correct explicit labels ("Borrowing", "Returned", "Overdue") | No overdue indication or late labels appear in returned history      | **Fail**   | ![[Screenshot bug06.png]]                              | **BUG-06** |

---

# Summary

| TC type | Amount |
| :--- | :--- |
| Total amount of test cases | **43** |
| Pass | **34** |
| Fail | **9** |
| Blocked | **0** |
| Not Run | **0** |
| **Pass rate** | **34/43 \| 79.1%** |

## Results by each REQ

| REQ | Amount of TCs | Pass | Fail | Pass rate | Related Bugs |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **REQ-01** | 6 | 6 | 0 | 100% | |
| **REQ-02** | 4 | 4 | 0 | 100% | |
| **REQ-03** | 6 | 5 | 1 | 83.3% | **BUG-01** |
| **REQ-04** | 8 | 6 | 2 | 75.0% | **BUG-02, BUG-03** |
| **REQ-05** | 4 | 2 | 2 | 50.0% | **BUG-04, BUG-05** |
| **REQ-06** | 4 | 3 | 1 | 75.0% | **BUG-07** |
| **REQ-07** | 6 | 4 | 2 | 66.7% | **BUG-08, BUG-09** |
| **REQ-08** | 5 | 3 | 2 | 60.0% | **BUG-04, BUG-06** |
