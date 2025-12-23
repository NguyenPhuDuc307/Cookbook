# Các kiểu dữ liệu cơ bản trong Python

## Vấn đề
Làm thế nào để làm việc với các kiểu dữ liệu cơ bản trong Python: số, chuỗi, boolean, list, tuple, dictionary, và set?

## Giải pháp
Python cung cấp nhiều kiểu dữ liệu built-in giúp lưu trữ và xử lý thông tin hiệu quả.

## Ví dụ

### Số (Numbers)
```python
# Integer (số nguyên)
age = 25
count = -10

# Float (số thực)
price = 99.99
temperature = -15.5

# Các phép toán cơ bản
sum_result = 10 + 5      # 15
difference = 10 - 5      # 5
product = 10 * 5         # 50
division = 10 / 3        # 3.333...
floor_division = 10 // 3 # 3
modulo = 10 % 3          # 1
power = 2 ** 3           # 8
```

### Chuỗi (Strings)
```python
# Khai báo chuỗi
name = "Nguyễn Văn A"
message = 'Hello World'
multiline = """Đây là
chuỗi nhiều dòng"""

# Các thao tác với chuỗi
uppercase = name.upper()           # "NGUYỄN VĂN A"
lowercase = name.lower()           # "nguyễn văn a"
length = len(name)                 # 11
substring = name[0:6]              # "Nguyễn"
contains = "Văn" in name           # True
replaced = name.replace("A", "B")  # "Nguyễn Văn B"

# String formatting
formatted = f"Tên: {name}, Tuổi: {age}"
```

### Boolean
```python
is_active = True
is_deleted = False

# Các phép toán logic
result1 = True and False  # False
result2 = True or False   # True
result3 = not True        # False

# So sánh
is_equal = (5 == 5)       # True
is_greater = (10 > 5)     # True
is_not_equal = (5 != 3)   # True
```

### List (Danh sách)
```python
# Khai báo list
fruits = ["táo", "chuối", "cam"]
numbers = [1, 2, 3, 4, 5]
mixed = [1, "hello", True, 3.14]

# Thao tác với list
fruits.append("xoài")           # Thêm phần tử
fruits.insert(0, "dưa hấu")     # Thêm vào vị trí
fruits.remove("táo")            # Xóa phần tử
last = fruits.pop()             # Lấy và xóa phần tử cuối
first = fruits[0]               # Truy cập phần tử
fruits[1] = "nho"               # Sửa phần tử
sublist = fruits[1:3]           # Cắt list
length = len(fruits)            # Độ dài list
```

### Tuple (Bộ - không thay đổi được)
```python
# Khai báo tuple
coordinates = (10, 20)
rgb = (255, 128, 0)
single_item = (42,)  # Lưu ý dấu phấy

# Truy cập phần tử
x = coordinates[0]   # 10
y = coordinates[1]   # 20

# Unpacking
r, g, b = rgb
```

### Dictionary (Từ điển)
```python
# Khai báo dictionary
person = {
    "name": "Nguyễn Văn A",
    "age": 25,
    "city": "Hà Nội"
}

# Thao tác với dictionary
name = person["name"]              # Truy cập giá trị
person["email"] = "a@example.com"  # Thêm key mới
person["age"] = 26                 # Cập nhật giá trị
del person["city"]                 # Xóa key
exists = "name" in person          # Kiểm tra key tồn tại

# Các phương thức hữu ích
keys = person.keys()               # Lấy tất cả keys
values = person.values()           # Lấy tất cả values
items = person.items()             # Lấy cặp key-value
age = person.get("age", 0)         # Lấy giá trị hoặc default
```

### Set (Tập hợp - không trùng lặp)
```python
# Khai báo set
unique_numbers = {1, 2, 3, 4, 5}
colors = {"đỏ", "xanh", "vàng"}

# Thao tác với set
colors.add("tím")              # Thêm phần tử
colors.remove("đỏ")            # Xóa phần tử
exists = "xanh" in colors      # Kiểm tra tồn tại

# Các phép toán tập hợp
set1 = {1, 2, 3}
set2 = {3, 4, 5}
union = set1 | set2            # {1, 2, 3, 4, 5}
intersection = set1 & set2     # {3}
difference = set1 - set2       # {1, 2}
```

## Lưu ý
- **List** dùng khi cần thứ tự và có thể thay đổi
- **Tuple** dùng khi cần thứ tự nhưng không thay đổi (hiệu năng tốt hơn list)
- **Dictionary** dùng khi cần ánh xạ key-value
- **Set** dùng khi cần loại bỏ trùng lặp và thực hiện phép toán tập hợp
- List và Dictionary có thể thay đổi (mutable)
- String, Tuple, và các kiểu số không thay đổi được (immutable)

## Tham khảo
- [Python Official Documentation - Built-in Types](https://docs.python.org/3/library/stdtypes.html)
- [Real Python - Basic Data Types](https://realpython.com/python-data-types/)
