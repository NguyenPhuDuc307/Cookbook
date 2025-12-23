# Các câu lệnh Git cơ bản

## Vấn đề
Làm thế nào để sử dụng Git để quản lý mã nguồn, làm việc với repository, và cộng tác với team?

## Giải pháp
Sử dụng các câu lệnh Git cơ bản để khởi tạo repository, commit code, làm việc với branch, và đồng bộ với remote.

## Ví dụ

### Cài đặt và cấu hình ban đầu
```bash
# Cài đặt thông tin user
git config --global user.name "Nguyễn Văn A"
git config --global user.email "a@example.com"

# Xem cấu hình
git config --list

# Thiết lập editor mặc định
git config --global core.editor "code --wait"
```

### Khởi tạo repository
```bash
# Tạo repository mới
git init

# Clone repository có sẵn
git clone https://github.com/username/repo.git

# Clone vào thư mục cụ thể
git clone https://github.com/username/repo.git my-folder
```

### Làm việc với files
```bash
# Kiểm tra trạng thái
git status

# Thêm file vào staging area
git add file.txt              # Thêm một file
git add .                     # Thêm tất cả files
git add *.js                  # Thêm files theo pattern

# Xóa file khỏi staging area
git reset file.txt
git reset                     # Xóa tất cả

# Xem thay đổi
git diff                      # Thay đổi chưa staged
git diff --staged             # Thay đổi đã staged
git diff HEAD                 # So với commit cuối

# Bỏ qua thay đổi
git restore file.txt          # Hủy thay đổi file
git restore --staged file.txt # Unstage file
```

### Commit
```bash
# Commit với message
git commit -m "Add new feature"

# Commit tất cả thay đổi (bỏ qua staging)
git commit -am "Update files"

# Sửa commit cuối
git commit --amend -m "New message"

# Xem lịch sử commit
git log                       # Log đầy đủ
git log --oneline            # Log ngắn gọn
git log --graph --oneline    # Với đồ thị
git log -n 5                 # 5 commits gần nhất
git log --author="Nguyen"    # Theo author
git log --since="2 weeks ago" # Theo thời gian

# Xem chi tiết commit
git show <commit-hash>
```

### Làm việc với branches
```bash
# Xem danh sách branch
git branch                    # Local branches
git branch -r                 # Remote branches
git branch -a                 # Tất cả branches

# Tạo branch mới
git branch feature-login

# Chuyển branch
git checkout feature-login
git switch feature-login      # Cách mới hơn

# Tạo và chuyển branch
git checkout -b feature-signup
git switch -c feature-signup  # Cách mới hơn

# Đổi tên branch
git branch -m old-name new-name

# Xóa branch
git branch -d feature-login   # Xóa đã merge
git branch -D feature-login   # Xóa bắt buộc
```

### Merge và Rebase
```bash
# Merge branch vào branch hiện tại
git merge feature-login

# Rebase (áp dụng commits lên branch khác)
git rebase main

# Hủy rebase
git rebase --abort

# Tiếp tục rebase sau khi giải quyết conflict
git rebase --continue
```

### Làm việc với Remote
```bash
# Xem remote
git remote -v

# Thêm remote
git remote add origin https://github.com/username/repo.git

# Đổi URL remote
git remote set-url origin https://github.com/username/new-repo.git

# Lấy thay đổi từ remote
git fetch                     # Lấy về nhưng không merge
git fetch origin main         # Lấy branch cụ thể

# Pull (fetch + merge)
git pull                      # Pull branch hiện tại
git pull origin main          # Pull branch cụ thể

# Push
git push                      # Push branch hiện tại
git push origin main          # Push branch cụ thể
git push -u origin main       # Push và set upstream
git push --all                # Push tất cả branches
git push --tags               # Push tags

# Xóa remote branch
git push origin --delete feature-login
```

### Xử lý Conflicts
```bash
# Khi có conflict, Git sẽ đánh dấu trong file:
# <<<<<<< HEAD
# Code từ branch hiện tại
# =======
# Code từ branch đang merge
# >>>>>>> feature-branch

# Sau khi sửa conflict:
git add conflicted-file.txt
git commit -m "Resolve merge conflict"
```

### Stash - Lưu thay đổi tạm thời
```bash
# Lưu thay đổi
git stash
git stash save "Work in progress"

# Xem danh sách stash
git stash list

# Áp dụng stash
git stash apply              # Áp dụng stash cuối
git stash apply stash@{0}    # Áp dụng stash cụ thể

# Áp dụng và xóa stash
git stash pop

# Xóa stash
git stash drop stash@{0}
git stash clear              # Xóa tất cả
```

### Tags
```bash
# Tạo tag
git tag v1.0.0
git tag -a v1.0.0 -m "Version 1.0.0"

# Xem tags
git tag
git show v1.0.0

# Push tags
git push origin v1.0.0
git push --tags

# Xóa tag
git tag -d v1.0.0                    # Local
git push origin --delete v1.0.0     # Remote
```

### Các lệnh hữu ích khác
```bash
# Xem ai sửa file
git blame file.txt

# Tìm kiếm trong code
git grep "function"

# Dọn dẹp
git clean -n                 # Preview files sẽ xóa
git clean -f                 # Xóa untracked files
git clean -fd                # Xóa files và directories

# Xem lịch sử một file
git log --follow file.txt

# Cherry-pick (áp dụng một commit cụ thể)
git cherry-pick <commit-hash>
```

## Lưu ý

**Best Practices:**
- Commit thường xuyên với messages rõ ràng
- Sử dụng branch cho mỗi feature/bugfix
- Pull trước khi push để tránh conflicts
- Review code trước khi merge
- Sử dụng `.gitignore` để loại trừ files không cần thiết

**Commit Message Convention:**
```
<type>: <subject>

<body>

<footer>
```

Types phổ biến:
- `feat`: Feature mới
- `fix`: Bug fix
- `docs`: Cập nhật documentation
- `style`: Format code
- `refactor`: Refactor code
- `test`: Thêm tests
- `chore`: Maintenance tasks

**Ví dụ:**
```
feat: add user authentication

Implement JWT-based authentication system
- Add login endpoint
- Add register endpoint
- Add middleware for protected routes

Closes #123
```

**Git Workflow phổ biến:**
1. **GitHub Flow**: main + feature branches
2. **Git Flow**: main + develop + feature/release/hotfix branches
3. **Trunk Based**: main + short-lived feature branches

## Tham khảo
- [Git Official Documentation](https://git-scm.com/doc)
- [Pro Git Book](https://git-scm.com/book/en/v2)
- [GitHub Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
- [Conventional Commits](https://www.conventionalcommits.org/)
