# Báo Cáo Bài 2: Tái cấu trúc lịch sử commit bằng Interactive Rebase

## 1. Chuẩn bị môi trường và tạo lịch sử commit thử nghiệm

Thực hiện tạo các commit theo gợi ý đề bài:

```bash
# Commit 1: Tạo auth.js
touch auth.js
git add auth.js
git commit -m "feat: khoi tao module auth"

# Commit 2: Sửa auth.js
echo "// fix typo" >> auth.js
git add auth.js
git commit -m "fix typo"

# Commit 3: Sửa auth.js
echo "// add utils" >> auth.js
git add auth.js
git commit -m "adds utility functions"

# Commit 4: Tạo temp.txt
touch temp.txt
git add temp.txt
git commit -m "add temp file for debug"
```

### Kiểm tra lịch sử commit trước khi Rebase:
```bash
git log --oneline
```
**Kết quả:**
```text
a4f1e82 (HEAD -> main) add temp file for debug
c3b2a10 adds utility functions
b2a19f8 fix typo
a1f8e7d feat: khoi tao module auth
```

---

## 2. Thực hiện Interactive Rebase

Chạy lệnh tương tác lùi về 4 commit trước:
```bash
git rebase -i HEAD~4
```

### Cấu hình trong Trình soạn thảo (Giao diện Interactive Rebase):
```text
pick a1f8e7d feat: khoi tao module auth
squash b2a19f8 fix typo
squash c3b2a10 adds utility functions
drop a4f1e82 add temp file for debug

# Rebase 1234567..a4f1e82 onto 1234567 (4 commands)
#
# Commands:
# p, pick <commit> = use commit
# s, squash <commit> = use commit, but meld into previous commit
# d, drop <commit> = remove commit
```

---

## 3. Chỉnh sửa thông điệp Commit gộp (Commit Message)

Sau khi lưu và đóng giao diện cấu hình, Git mở tiếp trình soạn thảo để điều chỉnh thông điệp cho commit đã gộp. 

Sửa toàn bộ thông điệp thành:
```text
feat: hoan thien module authentication
```

Lưu và thoát trình soạn thảo.

---

## 4. Kiểm tra kết quả sau khi Rebase

Chạy lệnh kiểm tra lịch sử commit:
```bash
git log --oneline
```

**Kết quả:**
```text
e9f8a7b (HEAD -> main) feat: hoan thien module authentication
```

Kiểm tra thư mục làm việc (file `temp.txt` đã bị loại bỏ hoàn toàn, file `auth.js` được giữ lại):
```bash
ls
# Output: auth.js
```