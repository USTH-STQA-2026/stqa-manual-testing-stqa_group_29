# Bug Reports

> **Hướng dẫn**: Tạo 1 mục bug cho mỗi TC có kết quả **Fail**.
> Xem [examples/sample-bug-report.md](../examples/sample-bug-report.md) để hiểu cách viết bug report tốt.
> Mỗi bug cần: tiêu đề mô tả hành vi lỗi, bước tái hiện, expected vs actual, severity + giải thích.

| Information     |                          |
| --------------- | ------------------------ |
| **Group**       | Group 29                 |
| **Report Date** | From 16/05 to 13/06/2026 |

## Environment 
- Browser: Chrome 148
- Operating System: Windows 11
- Application:  Library System 
- URL: [https://stqa.rbc.vn](https://stqa.rbc.vn/)
> **Note:** some bugs are related to multiple test cases or even multiple REQs, but the test cases themselves have been determined to be related significantly to only 1 REQ.
---
# BUG-01: Book search/filter function is case-sensitive for book category input

| Atrribute             | Details    |
| --------------------- | ---------- |
| **Bug ID**            | BUG-01     |
| **Relevant TC**       | TC-13      |
| **Relevant REQ**      | REQ-03     |
| **Severity**          | Medium     |
| **Tester**            | Group 29   |
| **Date of discovery** | 22/05/2026 |
| **State**             | Open       |

## Preconditions
- User has successfully logged into the system.
- User is currently on the “Books” tab.
## Steps to Reproduce
1. Open the “Books” tab.
2. In the search/filter input field, enter the keyword: `CÔNG NGHỆ`.
3. Observe the displayed book list.
## Expected Result
The system should display books belonging to the “Công nghệ” category because REQ-03 specifies that the search function must be case-insensitive.
Expected books include:
- BOOK001 — Lập trình Flutter cơ bản
- BOOK002 — Cấu trúc dữ liệu và giải thuật
- BOOK003 — Kiểm thử phần mềm nhập môn
## Actual Result
The system displays the message:  
`Không tìm thấy sách`
No books are displayed when the input is `CÔNG NGHỆ`.
## Impact
Users may fail to find books when entering uppercase or differently formatted category names, reducing usability and violating REQ-03 of the SRS.
## Severity
**Medium**
## Evidence
- Screenshot 1:  ![[Screenshot bug01-1.png]]
	- Input `CÔNG NGHỆ` → no books found.
- Screenshot 2:  ![[Screenshot bug01-2.png]]
	- Input `Công nghệ` → books are displayed correctly.

## Suggested Fix

Normalize both user input and stored category values into the same format (e.g., convert all strings to lowercase before comparison) to ensure case-insensitive search behavior as required by the SRS. 

-----
# BUG-02: System allows member to borrow a 4th book even though the maximum limit is 3 books

| Atrribute             | Details    |
| --------------------- | ---------- |
| **Bug ID**            | BUG-02     |
| **Relevant TC**       | TC-23      |
| **Relevant REQ**      | REQ-04     |
| **Severity**          | High       |
| **Tester**            | Group 29   |
| **Date of discovery** | 22/05/2026 |
| **State**             | Open       |

## Preconditions
- User logged in with an active member account.
- Member already borrowed 3 books.
- Another book is currently available.
## Steps to Reproduce
1. Login using an active member account.
2. Borrow books until the member currently has 3 borrowed books.
3. Attempt to borrow a 4th available book.
4. Observe the system response.
## Expected Result
The system must reject the borrow request because REQ-04 specifies that a member may borrow a maximum of 3 books at the same time.
The system should display an error message indicating that the borrowing limit has been reached.
## Actual Result
The system allows the member to successfully borrow the 4th book.
The error message:  
`"Đã đạt giới hạn mượn tối đa 3 sách"`  
only appears when attempting to borrow the 5th book.
## Impact
This issue violates the business rule defined in REQ-04 and allows members to exceed the maximum borrowing limit, causing incorrect borrow records and inconsistent system data.
## Severity
**High**
## Evidence
- Screenshot 1: ![[Screenshot bug02-1.png]]
- Screenshot 2: ![[Screenshot bug02-2.png]]

## Suggested Fix
Review and correct the borrowing limit validation logic.  
The validation condition may currently be implemented as:
```java
borrowCount > 3
```
It should instead be:
```java
borrowCount >= 3
```

----
# BUG-03: Suspended member receives incorrect “expired member” error message when borrowing books

| Atrribute          | Details              |
| ------------------- | --------------------- |
| **Bug ID**          | BUG-03                |
| **Relevant TC**    | TC-20       |
| **Relevant REQ**   | REQ-04     |
| **Severity**          | Medium     |
| **Tester** | Group 29   |
| **Date of discovery**  | 22/05/2026 |
| **State**      | Open       |

## Preconditions
- Login using suspended member account:  
    `cu.le@email.com`
- At least one book is currently available.
## Steps to Reproduce
1. Login using the suspended member account.
2. Open the “Books” tab.
3. Attempt to borrow an available book.
4. Observe the displayed error message.
## Expected Result
The system should reject the borrow request and display an error message indicating that the member account is suspended.
Example:
```text
Member is suspended and cannot borrow books.
```
## Actual Result
The system displays the message:
```text
Thành viên đã hết hạn, không thể mượn sách
```
The error message incorrectly indicates that the member account is expired instead of suspended.
## Impact
The system provides incorrect rejection information to users, potentially causing confusion for both members and librarians. This behavior violates REQ-04, which requires the system to display the correct rejection reason.
## Severity
**Medium**
## Evidence

- Screenshot: ![[Screenshot bug03.png]]
    

## Suggested Fix
Review the validation and error-handling logic for member status checking to ensure suspended and expired states are handled separately with correct corresponding messages.

---
# BUG-04: Member can view and return books borrowed by another member

| Atrribute             | Details        |
| --------------------- | -------------- |
| **Bug ID**            | BUG-04         |
| **Relevant TC**       | TC-28, TC-42   |
| **Relevant REQ**      | REQ-05, REQ-08 |
| **Severity**          | Critical       |
| **Tester**            | Group 29       |
| **Date of discovery** | 22/05/2026     |
| **State**             | Open           |

## Preconditions
- Login using member account:  
    `ba.nguyen@email.com` (MEM002)
- Member MEM006 currently has an active borrow record for BOOK013.
## Steps to Reproduce
1. Login using account `ba.nguyen@email.com`.
2. Open the “Borrow / Return” tab.
3. Search for borrow records belonging to member `MEM006`.
4. Observe the displayed borrow records.
5. Attempt to return BOOK013 borrowed by MEM006.
## Expected Result
According to REQ-05 and REQ-08:
- Members must only view their own borrow records.
- Members must only return books they personally borrowed.
The system should prevent MEM002 from viewing or returning books borrowed by MEM006.
## Actual Result
- MEM002 can view borrow records belonging to MEM006.
- MEM002 can successfully return BOOK013 borrowed by MEM006.
## Impact
This issue violates access control and authorization rules defined in REQ-05 and REQ-08. Members can manipulate other users’ borrow records, potentially causing data integrity and security problems
## Severity
**Critical**
## Evidence
- Screenshot 1: ![[Screenshot bug04-1.png]]
- Screenshot 2: ![[Screenshot bug04-2.png]]
## Suggested Fix
Implement proper authorization checks before displaying borrow records and processing return actions. The system should verify that the logged-in member is the actual borrower of the selected book before allowing access or return operations.

----
# BUG-05: System does not display overdue warning when returning overdue books

| Atrribute          | Details   |
| ------------------- | ---------- |
| **Bug ID**          | BUG-05     |
| **Relevant TC**    | TC-26      |
| **Relevant REQ**   | REQ-05     |
| **Severity**          | Medium     |
| **Tester** | Group 29   |
| **Date of discovery**  | 22/05/2026 |
| **State**      | Open       |

## Preconditions
- BOOK013 is borrowed by MEM006.
- Borrow information:
    - Borrow Date: 01/10/2024
    - Due Date: 15/10/2024
    - Return Date: 22/05/2026
- The borrow record is overdue.
## Steps to Reproduce
1. Login to the system.
2. Navigate to the “Borrow / Return” tab.
3. Return BOOK013 after the due date has passed.
4. Observe the system response after returning the book.
## Expected Result
According to REQ-05:  
If a book is returned after the due date, the system must display an overdue warning message.
## Actual Result
The book is returned successfully, but the system does not display any overdue warning or notification.
## Impact
Users and librarians may not realize that a returned book was overdue. This may affect overdue tracking, penalties, and borrow record accuracy.
## Severity
**Medium**
## Evidence

- Screenshot: ![[Screenshot bug05.png]]

## Suggested Fix
Add overdue validation during the return process.  
If:  
returnDate > dueDate
the system should automatically display an overdue warning message before or after completing the return operation.

----
# BUG-06: System does not display overdue indication for books returned after the due date

| Atrribute          | Details        |
| ------------------- | --------------- |
| **Bug ID**          | BUG-06          |
| **Relevant TC**    | TC-43           |
| **Relevant REQ**   | REQ-06          |
| **Severity**          | Medium          |
| **Tester** | Group 29        |
| **Date of discovery**  | 22/05/2026 |
| **State**      | Open            |

## Preconditions
- Borrow record BR005 exists with:
    - Borrow Date: 01/06/2024
    - Due Date: 15/06/2024
    - Return Date: 20/06/2024
## Steps to Reproduce
1. Login to the system.
2. Navigate to the “Borrow / Return” section.
3. Locate borrow record BR005.
4. Observe the displayed borrow status and return information.
## Expected Result
According to REQ-05, if a book is returned after the due date, the system should display an overdue warning or indication that the return was late.
## Actual Result
The system only displays the status:
```text
Đã trả
```
No overdue warning, overdue label, or late-return indication is displayed even though the book was returned after the due date.
## Impact
Users and librarians cannot identify whether a returned book was overdue, reducing the accuracy and usefulness of borrow history tracking.
## Severity
**Medium**
## Evidence
- Screenshot: ![[Screenshot bug06.png]]
## Suggested Fix
Add overdue validation for returned borrow records.  
If:  
returnDate > dueDate
the system should display a visible overdue or late-return indicator in the borrow history.

----
# BUG-07: Overdue borrow records are not displayed to the corresponding member after overdue checking

| Atrribute             | Details      |
| --------------------- | ------------ |
| **Bug ID**            | BUG-07       |
| **Relevant TC**       | TC-31, TC-43 |
| **Relevant REQ**      | REQ-06       |
| **Severity**          | Medium       |
| **Tester**            | Group 29     |
| **Date of discovery** | 22/05/2026   |
| **State**             | Open         |

## Preconditions
- Librarian account is available.
- Member MEM006 has an overdue borrow record:
    - Borrow Date: 01/10/2024
    - Due Date: 15/10/2024
- Current date is later than the due date.
## Steps to Reproduce
1. Login as Librarian.
2. Click the “Kiểm tra quá hạn” button.
3. Verify that MEM006 borrow record is marked as “Quá hạn”.
4. Logout from Librarian account.
5. Login using MEM006 account.
6. Navigate to the “Borrow / Return” tab.
7. Observe the borrow record status.
## Expected Result
According to REQ-06:  
Members should be able to view their own overdue borrow records after overdue processing.
The borrow record of MEM006 should display status:
```text
Quá hạn
```
## Actual Result
The overdue borrow record is visible as “Quá hạn” to the Librarian, but MEM006 does not see the overdue status in their own borrow records.
## Impact
Members may not be aware that their borrowed books are overdue, causing inconsistent overdue tracking and incorrect user information display between roles.
## Severity
**Medium**
## Evidence

- Screenshot 1: ![[Screenshot bug07-1.png]]
- Screenshot 2: ![[Screenshot bug07-2.png]]
## Suggested Fix
Synchronize overdue status visibility across user roles.  
After overdue processing, the system should consistently update and display overdue status for both Librarians and the corresponding Members.

-----

# BUG-08: System rejects valid email format when adding a new member

| Atrribute             | Details    |
| --------------------- | ---------- |
| **Bug ID**            | BUG-08     |
| **Relevant TC**       | TC-33      |
| **Relevant REQ**      | REQ-07     |
| **Severity**          | Medium     |
| **Tester**            | Group 29   |
| **Date of discovery** | 22/05/2026 |
| **State**             | Open       |

## Preconditions
- Login as Librarian.
- Open the “Member Management” section.
## Steps to Reproduce
1. Click “Add Member”.
2. Enter the following information:
    - Full Name: `noname`
    - Email: `noname@domain.com`
    - Phone Number: `0123456789`
3. Submit the form.
## Expected Result
The system should accept the email because:
```text
noname@domain.com
```
matches the valid email format defined in REQ-07.
The member should be created successfully.
## Actual Result
The system displays:
```text
Email không hợp lệ
```
The valid email address is incorrectly rejected.
## Impact
Valid users cannot be added into the system, causing incorrect validation behavior and reducing usability of the member management feature.
## Severity
**Medium**
## Evidence
- Screenshot: ![[Screenshot bug08.png]]

## Suggested Fix
Review the email validation logic to ensure valid email formats containing both:
- `@`
- `.` in the domain section
are accepted correctly.

----
# BUG-09: System accepts invalid email formats when adding new member

| Atrribute             | Details    |
| --------------------- | ---------- |
| **Bug ID**            | BUG-09     |
| **Relevant TC**       | TC-34      |
| **Relevant REQ**      | REQ-07     |
| **Severity**          | Medium     |
| **Tester**            | Group 29   |
| **Date of discovery** | 22/05/2026 |
| **State**             | Open       |

## Preconditions
- Login as Librarian.
- Open the “Member Management” section.
## Steps to Reproduce
1. Click “Add Member”.
2. Enter invalid email:
    ```
    noname@domain
    ```
3. Submit the form.
4. Repeat using:
    ```text
    noname.com@domain
    ```
## Expected Result
The system should reject both email formats because the domain section does not contain a dot (`.`), violating REQ-07 email validation rules.
## Actual Result
The system displays:
```text
Thêm thành viên thành công
```
The invalid email addresses are accepted and new members are created successfully.
## Impact
Invalid member data can be stored in the system, reducing data quality and potentially causing future communication or account management issues.
## Severity
**Medium**
## Evidence
- Screenshot 1: ![[Screenshot bug09-1.png]]
- Screenshot 2: ![[Screenshot bug09-2.png]]
## Suggested Fix
Improve email format validation to ensure:
- email contains `@`
- domain section contains at least one `.`
before allowing member creation.

----
