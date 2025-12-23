# Linked List (Danh sách liên kết)

## Vấn đề
Làm thế nào để tạo và sử dụng cấu trúc dữ liệu Linked List - một cấu trúc cho phép chèn/xóa phần tử hiệu quả?

## Giải pháp
Linked List là cấu trúc dữ liệu tuyến tính trong đó các phần tử được lưu trữ không liền kề. Mỗi phần tử (node) chứa dữ liệu và con trỏ đến node tiếp theo.

## Ví dụ

### Python - Singly Linked List
```python
class Node:
    """Node trong linked list"""
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    """Linked List đơn"""
    def __init__(self):
        self.head = None
    
    def append(self, data):
        """Thêm node vào cuối list"""
        new_node = Node(data)
        
        if not self.head:
            self.head = new_node
            return
        
        current = self.head
        while current.next:
            current = current.next
        current.next = new_node
    
    def prepend(self, data):
        """Thêm node vào đầu list"""
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
    
    def insert_after(self, prev_node, data):
        """Chèn node sau một node cho trước"""
        if not prev_node:
            print("Node trước không tồn tại")
            return
        
        new_node = Node(data)
        new_node.next = prev_node.next
        prev_node.next = new_node
    
    def delete(self, key):
        """Xóa node đầu tiên có giá trị key"""
        current = self.head
        
        # Nếu head chứa key
        if current and current.data == key:
            self.head = current.next
            current = None
            return
        
        # Tìm node cần xóa
        prev = None
        while current and current.data != key:
            prev = current
            current = current.next
        
        # Nếu không tìm thấy
        if not current:
            return
        
        # Xóa node
        prev.next = current.next
        current = None
    
    def search(self, key):
        """Tìm kiếm node có giá trị key"""
        current = self.head
        while current:
            if current.data == key:
                return True
            current = current.next
        return False
    
    def print_list(self):
        """In ra toàn bộ list"""
        elements = []
        current = self.head
        while current:
            elements.append(str(current.data))
            current = current.next
        print(" -> ".join(elements))
    
    def length(self):
        """Đếm số lượng node"""
        count = 0
        current = self.head
        while current:
            count += 1
            current = current.next
        return count

# Sử dụng
llist = LinkedList()
llist.append(1)
llist.append(2)
llist.append(3)
llist.prepend(0)
print("Linked List:")
llist.print_list()  # 0 -> 1 -> 2 -> 3

llist.delete(2)
print("\nSau khi xóa 2:")
llist.print_list()  # 0 -> 1 -> 3

print(f"\nTìm 3: {llist.search(3)}")  # True
print(f"Độ dài: {llist.length()}")    # 3
```

**Giải thích:**
- `Node`: Lớp đại diện cho một node với data và con trỏ next
- `append()`: Thêm node vào cuối - O(n)
- `prepend()`: Thêm node vào đầu - O(1)
- `delete()`: Xóa node - O(n)
- `search()`: Tìm kiếm - O(n)

### JavaScript
```javascript
class Node {
    constructor(data) {
        this.data = data;
        this.next = null;
    }
}

class LinkedList {
    constructor() {
        this.head = null;
    }
    
    append(data) {
        const newNode = new Node(data);
        
        if (!this.head) {
            this.head = newNode;
            return;
        }
        
        let current = this.head;
        while (current.next) {
            current = current.next;
        }
        current.next = newNode;
    }
    
    prepend(data) {
        const newNode = new Node(data);
        newNode.next = this.head;
        this.head = newNode;
    }
    
    delete(key) {
        if (!this.head) return;
        
        if (this.head.data === key) {
            this.head = this.head.next;
            return;
        }
        
        let current = this.head;
        while (current.next) {
            if (current.next.data === key) {
                current.next = current.next.next;
                return;
            }
            current = current.next;
        }
    }
    
    printList() {
        const elements = [];
        let current = this.head;
        while (current) {
            elements.push(current.data);
            current = current.next;
        }
        console.log(elements.join(' -> '));
    }
}

// Sử dụng
const llist = new LinkedList();
llist.append(1);
llist.append(2);
llist.append(3);
llist.prepend(0);
llist.printList(); // 0 -> 1 -> 2 -> 3
```

## Độ phức tạp

| Thao tác | Độ phức tạp thời gian |
|----------|----------------------|
| Truy cập | O(n) |
| Tìm kiếm | O(n) |
| Chèn đầu | O(1) |
| Chèn cuối | O(n) hoặc O(1) với tail pointer |
| Xóa đầu | O(1) |
| Xóa cuối | O(n) |
| Không gian | O(n) |

## Lưu ý

**Ưu điểm:**
- Kích thước động (không cần khai báo trước)
- Chèn/xóa đầu list rất nhanh O(1)
- Không lãng phí bộ nhớ

**Nhược điểm:**
- Truy cập phần tử chậm O(n) (không như array là O(1))
- Tốn thêm bộ nhớ cho con trỏ
- Không thể truy cập ngẫu nhiên

**Các loại Linked List:**
- **Singly Linked List**: Node chỉ trỏ đến node tiếp theo
- **Doubly Linked List**: Node trỏ đến cả node trước và sau
- **Circular Linked List**: Node cuối trỏ lại node đầu

**Khi nào nên dùng:**
- Cần chèn/xóa phần tử thường xuyên
- Không biết trước kích thước dữ liệu
- Implement Stack, Queue, Graph

**Khi nào KHÔNG nên dùng:**
- Cần truy cập ngẫu nhiên nhanh (dùng Array)
- Bộ nhớ hạn chế (overhead của con trỏ)

## Tham khảo
- [GeeksforGeeks - Linked List](https://www.geeksforgeeks.org/data-structures/linked-list/)
- [Programiz - Linked List](https://www.programiz.com/dsa/linked-list)
- [Visualgo - Linked List Visualization](https://visualgo.net/en/list)
