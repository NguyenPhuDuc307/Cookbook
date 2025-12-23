# Tạo API RESTful đơn giản với Express.js

## Vấn đề
Làm thế nào để tạo một REST API đơn giản với Node.js và Express.js để quản lý dữ liệu?

## Giải pháp
Sử dụng Express.js framework để xây dựng API với các endpoint CRUD (Create, Read, Update, Delete).

## Ví dụ

### Cài đặt
```bash
# Khởi tạo project
npm init -y

# Cài đặt dependencies
npm install express
npm install --save-dev nodemon
```

### Server cơ bản
```javascript
// server.js
const express = require('express');
const app = express();
const PORT = process.env.PORT || 3000;

// Middleware để parse JSON
app.use(express.json());

// Dữ liệu mẫu (thay bằng database trong thực tế)
let books = [
    { id: 1, title: 'Đắc Nhân Tâm', author: 'Dale Carnegie', year: 1936 },
    { id: 2, title: 'Nhà Giả Kim', author: 'Paulo Coelho', year: 1988 },
    { id: 3, title: 'Tuổi Trẻ Đáng Giá Bao Nhiêu', author: 'Rosie Nguyễn', year: 2015 }
];

// GET - Lấy tất cả sách
app.get('/api/books', (req, res) => {
    res.json({
        success: true,
        data: books
    });
});

// GET - Lấy một sách theo ID
app.get('/api/books/:id', (req, res) => {
    const id = parseInt(req.params.id);
    const book = books.find(b => b.id === id);
    
    if (!book) {
        return res.status(404).json({
            success: false,
            message: 'Không tìm thấy sách'
        });
    }
    
    res.json({
        success: true,
        data: book
    });
});

// POST - Thêm sách mới
app.post('/api/books', (req, res) => {
    const { title, author, year } = req.body;
    
    // Validate
    if (!title || !author || !year) {
        return res.status(400).json({
            success: false,
            message: 'Thiếu thông tin sách'
        });
    }
    
    const newBook = {
        id: books.length > 0 ? Math.max(...books.map(b => b.id)) + 1 : 1,
        title,
        author,
        year
    };
    
    books.push(newBook);
    
    res.status(201).json({
        success: true,
        data: newBook
    });
});

// PUT - Cập nhật sách
app.put('/api/books/:id', (req, res) => {
    const id = parseInt(req.params.id);
    const { title, author, year } = req.body;
    
    const bookIndex = books.findIndex(b => b.id === id);
    
    if (bookIndex === -1) {
        return res.status(404).json({
            success: false,
            message: 'Không tìm thấy sách'
        });
    }
    
    // Cập nhật
    books[bookIndex] = {
        ...books[bookIndex],
        title: title || books[bookIndex].title,
        author: author || books[bookIndex].author,
        year: year || books[bookIndex].year
    };
    
    res.json({
        success: true,
        data: books[bookIndex]
    });
});

// DELETE - Xóa sách
app.delete('/api/books/:id', (req, res) => {
    const id = parseInt(req.params.id);
    const bookIndex = books.findIndex(b => b.id === id);
    
    if (bookIndex === -1) {
        return res.status(404).json({
            success: false,
            message: 'Không tìm thấy sách'
        });
    }
    
    const deletedBook = books.splice(bookIndex, 1)[0];
    
    res.json({
        success: true,
        message: 'Đã xóa sách',
        data: deletedBook
    });
});

// 404 handler
app.use((req, res) => {
    res.status(404).json({
        success: false,
        message: 'Endpoint không tồn tại'
    });
});

// Error handler
app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).json({
        success: false,
        message: 'Lỗi server'
    });
});

// Start server
app.listen(PORT, () => {
    console.log(`Server đang chạy tại http://localhost:${PORT}`);
});
```

**Giải thích:**
- `express.json()`: Middleware để parse request body dạng JSON
- `app.get()`: Định nghĩa endpoint GET
- `app.post()`: Định nghĩa endpoint POST
- `app.put()`: Định nghĩa endpoint PUT
- `app.delete()`: Định nghĩa endpoint DELETE
- `req.params`: Lấy parameters từ URL
- `req.body`: Lấy dữ liệu từ request body
- `res.json()`: Trả về response dạng JSON

### Test API với curl
```bash
# Lấy tất cả sách
curl http://localhost:3000/api/books

# Lấy một sách
curl http://localhost:3000/api/books/1

# Thêm sách mới
curl -X POST http://localhost:3000/api/books \
  -H "Content-Type: application/json" \
  -d '{"title":"Sapiens","author":"Yuval Noah Harari","year":2011}'

# Cập nhật sách
curl -X PUT http://localhost:3000/api/books/1 \
  -H "Content-Type: application/json" \
  -d '{"title":"Đắc Nhân Tâm (Updated)"}'

# Xóa sách
curl -X DELETE http://localhost:3000/api/books/1
```

### Cấu trúc project tốt hơn
```
project/
├── controllers/
│   └── bookController.js    # Logic xử lý
├── routes/
│   └── bookRoutes.js        # Định nghĩa routes
├── models/
│   └── bookModel.js         # Data model
├── middleware/
│   └── errorHandler.js      # Error handling
├── server.js                # Entry point
└── package.json
```

## Lưu ý

**Best Practices:**
- Sử dụng status code chuẩn: 200 (OK), 201 (Created), 400 (Bad Request), 404 (Not Found), 500 (Server Error)
- Validate input data
- Xử lý lỗi đúng cách
- Sử dụng environment variables cho config
- Implement authentication/authorization cho production
- Thêm rate limiting để chống spam
- Logging requests/responses

**HTTP Methods:**
- **GET**: Lấy dữ liệu (không thay đổi)
- **POST**: Tạo mới
- **PUT**: Cập nhật toàn bộ
- **PATCH**: Cập nhật một phần
- **DELETE**: Xóa

**RESTful URL conventions:**
- `GET /api/books` - Lấy tất cả
- `GET /api/books/:id` - Lấy một
- `POST /api/books` - Tạo mới
- `PUT /api/books/:id` - Cập nhật
- `DELETE /api/books/:id` - Xóa

**Security:**
- Luôn validate và sanitize input
- Sử dụng HTTPS trong production
- Implement CORS đúng cách
- Sử dụng helmet.js cho security headers
- Rate limiting với express-rate-limit

## Tham khảo
- [Express.js Official Documentation](https://expressjs.com/)
- [REST API Best Practices](https://stackoverflow.blog/2020/03/02/best-practices-for-rest-api-design/)
- [MDN - HTTP Methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
