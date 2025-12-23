# 🤝 Hướng dẫn đóng góp

Cảm ơn bạn đã quan tâm đến việc đóng góp cho Cookbook! Dự án này tồn tại nhờ sự đóng góp của cộng đồng.

## 🎯 Các cách đóng góp

### 1. Thêm công thức mới
- Viết một bài hướng dẫn về một chủ đề cụ thể
- Sử dụng [TEMPLATE.md](./TEMPLATE.md) làm mẫu

### 2. Cải thiện công thức hiện có
- Sửa lỗi chính tả, văn phạm
- Thêm ví dụ code mới
- Cải thiện giải thích
- Cập nhật thông tin lỗi thời

### 3. Đề xuất chủ đề mới
- Mở một Issue với tag "suggestion"
- Mô tả chủ đề bạn muốn thấy

### 4. Báo lỗi
- Mở một Issue với tag "bug"
- Mô tả chi tiết vấn đề

## 📝 Quy trình đóng góp

### Bước 1: Fork và Clone
```bash
# Fork repo trên GitHub, sau đó clone về máy
git clone https://github.com/YOUR-USERNAME/Cookbook.git
cd Cookbook
```

### Bước 2: Tạo Branch mới
```bash
# Tạo branch cho công việc của bạn
git checkout -b feature/ten-cong-thuc

# Hoặc cho bug fix
git checkout -b fix/ten-loi
```

### Bước 3: Viết nội dung
1. Sao chép [TEMPLATE.md](./TEMPLATE.md) vào thư mục phù hợp
2. Đổi tên file theo định dạng kebab-case (vd: `bubble-sort.md`)
3. Điền nội dung theo cấu trúc template

### Bước 4: Kiểm tra
- Code ví dụ phải chạy được
- Kiểm tra chính tả và ngữ pháp
- Đảm bảo format markdown đúng
- Link tham khảo phải hoạt động

### Bước 5: Commit
```bash
# Add files
git add .

# Commit với message rõ ràng
git commit -m "Add: Thêm công thức về [chủ đề]"
# hoặc
git commit -m "Fix: Sửa lỗi trong [file]"
# hoặc
git commit -m "Update: Cập nhật [nội dung]"
```

### Bước 6: Push
```bash
git push origin feature/ten-cong-thuc
```

### Bước 7: Tạo Pull Request
1. Vào GitHub repository của bạn
2. Click "New Pull Request"
3. Chọn branch vừa push
4. Điền tiêu đề và mô tả chi tiết
5. Submit Pull Request

## ✅ Checklist trước khi submit PR

- [ ] Code ví dụ đã test và chạy được
- [ ] Tuân theo cấu trúc trong TEMPLATE.md
- [ ] Viết bằng tiếng Việt, rõ ràng dễ hiểu
- [ ] Có giải thích chi tiết cho code
- [ ] Nêu rõ ưu/nhược điểm
- [ ] Có phần "Khi nào nên/không nên dùng"
- [ ] Include links tham khảo
- [ ] Đã thêm link vào README.md của thư mục tương ứng
- [ ] Đã thêm link vào README.md chính (nếu cần)

## 📏 Quy tắc viết

### Ngôn ngữ
- Sử dụng tiếng Việt
- Rõ ràng, dễ hiểu
- Tránh thuật ngữ quá phức tạp (hoặc giải thích nếu cần dùng)

### Code
- Chạy được và đã test
- Có comment giải thích
- Follow best practices của ngôn ngữ đó
- Format code đúng chuẩn

### Cấu trúc
```markdown
# Tiêu đề công thức

## Vấn đề
[Mô tả vấn đề ngắn gọn]

## Giải pháp
[Giải thích cách giải quyết]

## Ví dụ
[Code với giải thích chi tiết]

## Lưu ý
- Ưu điểm
- Nhược điểm
- Khi nào nên dùng
- Khi nào KHÔNG nên dùng

## Tham khảo
- [Links hữu ích]
```

### Tên file
- Sử dụng kebab-case: `bubble-sort.md`, `python-data-types.md`
- Tên ngắn gọn, mô tả đúng nội dung
- Extension `.md`

### Commit messages
```
<type>: <subject>

Types:
- Add: Thêm nội dung mới
- Fix: Sửa lỗi
- Update: Cập nhật nội dung
- Remove: Xóa nội dung
- Docs: Cập nhật documentation

Ví dụ:
Add: Thêm công thức về Binary Search
Fix: Sửa lỗi code trong bubble-sort.md
Update: Cập nhật ví dụ trong linked-list.md
```

## 🎨 Style Guide

### Code blocks
```markdown
### Python
\```python
def example():
    print("Hello World")
\```

### JavaScript
\```javascript
function example() {
    console.log("Hello World");
}
\```
```

### Inline code
Sử dụng `backticks` cho inline code: `variable`, `function()`, `class`

### Links
```markdown
[Text hiển thị](URL)
[Python Documentation](https://docs.python.org/)
```

### Lists
```markdown
- Item 1
- Item 2
  - Sub-item 2.1
  - Sub-item 2.2
```

## ❓ Câu hỏi thường gặp

### Tôi chưa biết Git, có thể đóng góp không?
Có! Bạn có thể:
- Tạo Issue để đề xuất nội dung
- Gửi nội dung qua email
- Học Git qua công thức [Git Basics](./git/git-basics.md) của chúng tôi

### Tôi nên viết về chủ đề gì?
- Xem phần "Chủ đề đề xuất" trong README.md
- Xem Issues với tag "help wanted"
- Viết về điều bạn vừa học được
- Viết về vấn đề bạn hay gặp

### Code ví dụ có cần phải hoàn hảo không?
Không nhất thiết, nhưng phải:
- Chạy được
- Giải quyết được vấn đề
- Follow best practices cơ bản
- Có giải thích rõ ràng

### Tôi có thể dịch nội dung từ nguồn khác không?
Có, nhưng:
- Phải ghi rõ nguồn
- Không vi phạm bản quyền
- Thêm góc nhìn/ví dụ của riêng bạn
- Đảm bảo phù hợp với phong cách Cookbook

## 📞 Liên hệ

Nếu có thắc mắc:
- Tạo Issue với tag "question"
- Email: [your-email]
- Discussions tab trên GitHub

## 🙏 Cảm ơn

Mọi đóng góp, dù lớn hay nhỏ, đều được trân trọng!

Happy coding! 🚀
