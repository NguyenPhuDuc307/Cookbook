# Sắp xếp nổi bọt (Bubble Sort)

## Vấn đề
Làm thế nào để sắp xếp một mảng/danh sách theo thứ tự tăng dần hoặc giảm dần?

## Giải pháp
Bubble Sort là thuật toán sắp xếp đơn giản, so sánh từng cặp phần tử liền kề và hoán đổi chúng nếu chúng không đúng thứ tự. Quá trình này lặp lại cho đến khi mảng được sắp xếp.

## Ví dụ

### Python
```python
def bubble_sort(arr):
    """
    Sắp xếp mảng theo thứ tự tăng dần bằng Bubble Sort
    
    Args:
        arr: Danh sách cần sắp xếp
    
    Returns:
        Danh sách đã được sắp xếp
    """
    n = len(arr)
    
    # Duyệt qua tất cả phần tử
    for i in range(n):
        # Cờ để kiểm tra xem có hoán đổi nào không
        swapped = False
        
        # Phần tử cuối cùng đã ở đúng vị trí
        for j in range(0, n - i - 1):
            # So sánh phần tử liền kề
            if arr[j] > arr[j + 1]:
                # Hoán đổi nếu không đúng thứ tự
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        
        # Nếu không có hoán đổi, mảng đã sắp xếp
        if not swapped:
            break
    
    return arr

# Sử dụng
numbers = [64, 34, 25, 12, 22, 11, 90]
print(f"Mảng ban đầu: {numbers}")
sorted_numbers = bubble_sort(numbers.copy())
print(f"Mảng đã sắp xếp: {sorted_numbers}")
```

**Giải thích:**
- Vòng lặp ngoài chạy n lần (n là số phần tử)
- Vòng lặp trong so sánh các cặp phần tử liền kề
- Sau mỗi lần lặp, phần tử lớn nhất "nổi" lên cuối mảng
- Sử dụng cờ `swapped` để tối ưu: dừng sớm nếu mảng đã sắp xếp

### JavaScript
```javascript
function bubbleSort(arr) {
    const n = arr.length;
    
    for (let i = 0; i < n; i++) {
        let swapped = false;
        
        for (let j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                // Hoán đổi
                [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
                swapped = true;
            }
        }
        
        if (!swapped) break;
    }
    
    return arr;
}

// Sử dụng
const numbers = [64, 34, 25, 12, 22, 11, 90];
console.log("Mảng ban đầu:", numbers);
const sortedNumbers = bubbleSort([...numbers]);
console.log("Mảng đã sắp xếp:", sortedNumbers);
```

### Java
```java
public class BubbleSort {
    public static void bubbleSort(int[] arr) {
        int n = arr.length;
        
        for (int i = 0; i < n; i++) {
            boolean swapped = false;
            
            for (int j = 0; j < n - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    // Hoán đổi
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                    swapped = true;
                }
            }
            
            if (!swapped) break;
        }
    }
    
    public static void main(String[] args) {
        int[] numbers = {64, 34, 25, 12, 22, 11, 90};
        System.out.println("Mảng ban đầu: " + Arrays.toString(numbers));
        bubbleSort(numbers);
        System.out.println("Mảng đã sắp xếp: " + Arrays.toString(numbers));
    }
}
```

## Độ phức tạp

| Trường hợp | Độ phức tạp thời gian |
|------------|----------------------|
| Tốt nhất   | O(n) - mảng đã sắp xếp |
| Trung bình | O(n²) |
| Tệ nhất    | O(n²) |
| Không gian | O(1) - sắp xếp tại chỗ |

## Lưu ý
**Ưu điểm:**
- Đơn giản, dễ hiểu và dễ implement
- Sắp xếp ổn định (stable sort)
- Không cần thêm bộ nhớ (in-place)
- Phát hiện được khi mảng đã sắp xếp

**Nhược điểm:**
- Hiệu suất kém với mảng lớn (O(n²))
- Không phù hợp cho ứng dụng thực tế với dữ liệu lớn

**Khi nào nên dùng:**
- Mảng nhỏ (< 50 phần tử)
- Mục đích học tập
- Mảng gần như đã được sắp xếp

**Khi nào KHÔNG nên dùng:**
- Dữ liệu lớn (hãy dùng Quick Sort, Merge Sort, hoặc Heap Sort)
- Yêu cầu hiệu suất cao

## Tham khảo
- [Wikipedia - Bubble Sort](https://en.wikipedia.org/wiki/Bubble_sort)
- [GeeksforGeeks - Bubble Sort](https://www.geeksforgeeks.org/bubble-sort/)
- [Visualgo - Sorting Visualization](https://visualgo.net/en/sorting)
