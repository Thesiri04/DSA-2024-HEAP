# ใบงานการทดลอง: โครงสร้างข้อมูล Heap

## วัตถุประสงค์การเรียนรู้
1. อธิบายหลักการทำงานของโครงสร้างข้อมูลแบบ Heap ได้
2. เขียนโปรแกรมเพื่อสร้างและจัดการ Heap ได้
3. ประยุกต์ใช้ Heap ในการแก้ปัญหาได้

## ทฤษฎีที่เกี่ยวข้อง
Heap เป็นโครงสร้างข้อมูลแบบต้นไม้แบบทวิภาค (Binary Tree) ที่มีคุณสมบัติพิเศษดังนี้:
- เป็นต้นไม้ที่สมบูรณ์ (Complete Binary Tree)
- ทุกโหนดพ่อแม่ต้องมีค่ามากกว่าหรือเท่ากับโหนดลูกทั้งสอง (กรณี Max Heap)
- หรือทุกโหนดพ่อแม่ต้องมีค่าน้อยกว่าหรือเท่ากับโหนดลูกทั้งสอง (กรณี Min Heap)

## ตัวอย่างการเขียนโปรแกรม

### การสร้าง Max Heap
```python
class MaxHeap:
    def __init__(self):
        self.heap = []
        
    def parent(self, i):
        return (i - 1) // 2
        
    def left_child(self, i):
        return 2 * i + 1
        
    def right_child(self, i):
        return 2 * i + 2
        
    def swap(self, i, j):
        self.heap[i], self.heap[j] = self.heap[j], self.heap[i]
        
    def insert(self, key):
        self.heap.append(key)
        self._sift_up(len(self.heap) - 1)
        
    def _sift_up(self, i):
        parent = self.parent(i)
        if i > 0 and self.heap[i] > self.heap[parent]:
            self.swap(i, parent)
            self._sift_up(parent)
```

### การลบค่าสูงสุด
```python
def extract_max(self):
    if len(self.heap) == 0:
        return None
    
    max_val = self.heap[0]
    self.heap[0] = self.heap[-1]
    self.heap.pop()
    
    if len(self.heap) > 0:
        self._sift_down(0)
    
    return max_val

def _sift_down(self, i):
    max_index = i
    left = self.left_child(i)
    right = self.right_child(i)
    
    if left < len(self.heap) and self.heap[left] > self.heap[max_index]:
        max_index = left
    
    if right < len(self.heap) and self.heap[right] > self.heap[max_index]:
        max_index = right
        
    if i != max_index:
        self.swap(i, max_index)
        self._sift_down(max_index)
```

## แบบฝึกหัด

### แบบฝึกหัดที่ 1: การแทรกค่า
จงเขียนโปรแกรมเพื่อแทรกค่าต่อไปนี้ลงใน Max Heap ที่ว่างเปล่า: 5, 3, 8, 1, 2, 7, 6, 4
พร้อมแสดงค่า Max Heap ที่ได้หลังจากเพิ่มข้อมูลครบแล้ว
```python
class MaxHeap:
    def __init__(self):
        self.heap = []

    def insert(self, val):
        """แทรกค่าเข้าไปใน heap และปรับให้อยู่ในรูปแบบ Max Heap"""
        self.heap.append(val)
        self._sift_up(len(self.heap) - 1)

    def _sift_up(self, i):
        """ดึงค่าที่เพิ่มเข้าไปขึ้นไปหาตำแหน่งที่เหมาะสม"""
        while i > 0:
            parent = (i - 1) // 2
            if self.heap[i] > self.heap[parent]:
                self._swap(i, parent)
                i = parent
            else:
                break

    def _swap(self, i, j):
        """สลับค่าระหว่างตำแหน่ง i และ j"""
        self.heap[i], self.heap[j] = self.heap[j], self.heap[i]

    def __str__(self):
        return str(self.heap)

# สร้าง MaxHeap และแทรกข้อมูล
max_heap = MaxHeap()
values = [5, 3, 8, 1, 2, 7, 6, 4]

for val in values:
    max_heap.insert(val)

print("Max Heap:", max_heap)
```
![image](https://github.com/user-attachments/assets/30d6c39f-55ca-4620-ac94-9db143f9c5b5)


### แบบฝึกหัดที่ 2: การลบค่า
จากข้อ 1 จงเขียนลำดับการลบค่าสูงสุดออกจาก Heap จำนวน 3 ครั้ง แสดงข้อมูล Heap หลังจากลบแต่ละครั้ง

```python
class MaxHeap:
    def __init__(self):
        self.heap = []

    def insert(self, val):
        """แทรกค่าเข้าไปใน heap และปรับให้อยู่ในรูปแบบ Max Heap"""
        self.heap.append(val)
        self._sift_up(len(self.heap) - 1)

    def extract_max(self):
        """ลบค่ามากที่สุดออกจาก heap และปรับโครงสร้าง heap"""
        if len(self.heap) == 0:
            return None

        max_val = self.heap[0]
        self.heap[0] = self.heap[-1]  # นำค่าตัวสุดท้ายมาแทนที่ Root
        self.heap.pop()  # ลบค่าตัวสุดท้ายออก
        self._sift_down(0)  # ปรับโครงสร้าง heap

        return max_val

    def _sift_up(self, i):
        """ดึงค่าที่เพิ่มเข้าไปขึ้นไปหาตำแหน่งที่เหมาะสม"""
        while i > 0:
            parent = (i - 1) // 2
            if self.heap[i] > self.heap[parent]:
                self._swap(i, parent)
                i = parent
            else:
                break

    def _sift_down(self, i):
        """ปรับโครงสร้าง heap หลังจากลบค่ามากที่สุด"""
        max_index = i
        left = 2 * i + 1
        right = 2 * i + 2

        if left < len(self.heap) and self.heap[left] > self.heap[max_index]:
            max_index = left
        if right < len(self.heap) and self.heap[right] > self.heap[max_index]:
            max_index = right

        if i != max_index:
            self._swap(i, max_index)
            self._sift_down(max_index)

    def _swap(self, i, j):
        """สลับค่าระหว่างตำแหน่ง i และ j"""
        self.heap[i], self.heap[j] = self.heap[j], self.heap[i]

    def __str__(self):
        return str(self.heap)


# สร้าง MaxHeap และแทรกข้อมูล
max_heap = MaxHeap()
values = [5, 3, 8, 1, 2, 7, 6, 4]

for val in values:
    max_heap.insert(val)

print("เริ่มต้น Max Heap:", max_heap)

# ลบค่ามากที่สุด 3 ครั้ง และแสดงผลลัพธ์แต่ละครั้ง
for i in range(3):
    removed = max_heap.extract_max()
    print(f"ลบค่า {removed} ออกจาก Heap → {max_heap}")

```
![image](https://github.com/user-attachments/assets/fc7053b6-2880-4d23-9129-73bbb445d42f)


### แบบฝึกหัดที่ 3: การเขียนโปรแกรม
จงเขียนฟังก์ชัน `is_max_heap(arr)` ที่รับ array เข้ามาและตรวจสอบว่าป็น Max Heap หรือไม่ 

```python
def is_max_heap(arr):
    n = len(arr)
    
    for i in range(n // 2):  # ตรวจสอบเฉพาะโหนดที่เป็นพ่อ (ไม่ต้องตรวจลูก)
        left = 2 * i + 1
        right = 2 * i + 2

        if left < n and arr[i] < arr[left]:  # ถ้าพ่อ < ลูกซ้าย ไม่ใช่ Max Heap
            return False
        if right < n and arr[i] < arr[right]:  # ถ้าพ่อ < ลูกขวา ไม่ใช่ Max Heap
            return False

    return True  # ถ้าตรวจหมดแล้วไม่มีปัญหา แสดงว่าเป็น Max Heap
# ตัวอย่างที่เป็น Max Heap
arr1 = [9, 7, 6, 5, 3, 2, 4]
print(arr1,' is ',is_max_heap(arr1))  #True

# ตัวอย่างที่ไม่เป็น Max Heap (เพราะ 5 < 7)
arr2 = [5, 7, 6, 3, 2, 4, 1]
print(arr2,' is ',is_max_heap(arr2))  #False

```
![image](https://github.com/user-attachments/assets/2f0821fa-7429-443c-b832-91a1250f52d7)



## การประยุกต์ใช้งานจริง

### 1. ระบบจัดการคิวผู้ป่วยฉุกเฉิน (Emergency Room Triage)
```python
class Patient:
    def __init__(self, name, priority):
        self.name = name
        self.priority = priority  # ระดับความรุนแรง 1-5 (1 = ฉุกเฉินมาก)
    
    def __lt__(self, other):
        return self.priority < other.priority

class ERQueue:
    def __init__(self):
        self.queue = []  # Min Heap เพื่อให้ผู้ป่วยที่มี priority ต่ำ (อาการหนัก) ได้รับการรักษาก่อน
    
    def add_patient(self, patient):
        heapq.heappush(self.queue, patient)
    
    def treat_next_patient(self):
        if self.queue:
            return heapq.heappop(self.queue)
        return None

# ตัวอย่างการใช้งาน
er = ERQueue()
er.add_patient(Patient("คนไข้ A", 1))  # หัวใจวาย
er.add_patient(Patient("คนไข้ B", 3))  # ปวดท้อง
er.add_patient(Patient("คนไข้ C", 2))  # กระดูกหัก
```

![image](https://github.com/user-attachments/assets/e6ea4388-684f-4ae9-bd00-199873e47151)


### 2. ระบบแนะนำสินค้าขายดี (Top K Items)
```python
class ProductRanking:
    def __init__(self, k):
        self.k = k
        self.products = []  # Min Heap เก็บ k สินค้าขายดีที่สุด
    
    def update_sales(self, product_id, sales):
        if len(self.products) < self.k:
            heapq.heappush(self.products, (sales, product_id))
        else:
            if sales > self.products[0][0]:
                heapq.heapreplace(self.products, (sales, product_id))
    
    def get_top_k(self):
        return sorted(self.products, reverse=True)

# ตัวอย่างการใช้งาน
ranking = ProductRanking(3)  # เก็บ 3 อันดับสินค้าขายดี
ranking.update_sales("สินค้า A", 100)
ranking.update_sales("สินค้า B", 150)
ranking.update_sales("สินค้า C", 80)
ranking.update_sales("สินค้า D", 200)
```
![image](https://github.com/user-attachments/assets/1f9fb4be-d29c-449d-872d-3a9fa920631c)


### 3. ตัวอย่างระบบคิวธนาคาร แบบมีระดับความสำคัญ โดยใช้ heapq
```python 
import heapq
from datetime import datetime
import time

class BankCustomer:
    def __init__(self, name, service_type, is_premium=False):
        self.name = name
        self.service_type = service_type
        self.is_premium = is_premium
        self.arrival_time = datetime.now()
        
        # กำหนดลำดับความสำคัญตาม service_type และสถานะลูกค้า
        self.priority = self._calculate_priority()
        
    def _calculate_priority(self):
        # ลำดับความสำคัญ (ยิ่งน้อยยิ่งสำคัญ)
        priority = {
            'ฝาก-ถอน': 3,
            'ชำระค่าบริการ': 2,
            'เปิดบัญชี': 1,
            'สินเชื่อ': 0
        }
        
        # ลูกค้า Premium จะได้ priority สูงกว่าปกติ 1 ระดับ
        base_priority = priority.get(self.service_type, 4)
        if self.is_premium:
            base_priority -= 0.5
            
        return base_priority
        
    def __lt__(self, other):
        # เปรียบเทียบลำดับความสำคัญ
        if self.priority == other.priority:
            # ถ้าความสำคัญเท่ากัน ใช้เวลามาก่อน-หลัง
            return self.arrival_time < other.arrival_time
        return self.priority < other.priority
        
class BankQueue:
    def __init__(self):
        self.queue = []  # heap queue
        self.waiting_count = 0
        
    def add_customer(self, customer):
        heapq.heappush(self.queue, customer)
        self.waiting_count += 1
        print(f"ลูกค้า: {customer.name}")
        print(f"บริการ: {customer.service_type}")
        print(f"สถานะ: {'Premium' if customer.is_premium else 'ทั่วไป'}")
        print(f"จำนวนคิวรอ: {self.waiting_count}")
        print("-" * 30)
        
    def serve_next_customer(self):
        if not self.queue:
            print("ไม่มีลูกค้าในคิว")
            return None
            
        customer = heapq.heappop(self.queue)
        self.waiting_count -= 1
        
        wait_time = datetime.now() - customer.arrival_time
        print(f"\nเรียกลูกค้า: {customer.name}")
        print(f"บริการ: {customer.service_type}")
        print(f"เวลารอ: {wait_time.seconds} วินาที")
        print(f"จำนวนคิวรอ: {self.waiting_count}")
        print("-" * 30)
        
        return customer
        
    def display_queue(self):
        if not self.queue:
            print("ไม่มีลูกค้าในคิว")
            return
            
        print("\nรายการคิวที่รอ:")
        # สร้าง copy ของคิวเพื่อไม่ให้กระทบคิวจริง
        temp_queue = self.queue.copy()
        position = 1
        
        while temp_queue:
            customer = heapq.heappop(temp_queue)
            print(f"{position}. {customer.name} - {customer.service_type}")
            position += 1
        print("-" * 30)

# ตัวอย่างการใช้งาน
def demo_bank_queue():
    bank = BankQueue()
    
    # เพิ่มลูกค้าเข้าคิว
    customers = [
        BankCustomer("คุณแดง", "ฝาก-ถอน"),
        BankCustomer("คุณขาว", "สินเชื่อ", is_premium=True),
        BankCustomer("คุณเขียว", "ชำระค่าบริการ"),
        BankCustomer("คุณม่วง", "เปิดบัญชี"),
        BankCustomer("คุณฟ้า", "สินเชื่อ")
    ]
    
    for customer in customers:
        bank.add_customer(customer)
        time.sleep(1)  # จำลองการมาถึงต่างเวลากัน
        
    print("\nแสดงลำดับคิว:")
    bank.display_queue()
    
    # จำลองการเรียกลูกค้าเข้ารับบริการ
    print("\nเริ่มเรียกลูกค้า:")
    for _ in range(len(customers)):
        bank.serve_next_customer()
        time.sleep(1)

if __name__ == "__main__":
    demo_bank_queue()
```
### ทำการปรับปรุงโปรแกรม โดยให้ทำการกดเลือกธุรกรรม แล้วจะมีเลขคิวในแต่ละช่วงของการทำธุรกรรม แทนชื่อของลูกค้า และมีการเรียกคิวตามระดับความสำคัญและเวลาที่มาก่อนหลังของลูกค้า

```python
import heapq
from datetime import datetime
import time

class BankCustomer:
    queue_counter = 1  # ตัวนับหมายเลขคิว
    
    def __init__(self, service_type, is_premium=False):
        self.queue_number = BankCustomer.queue_counter
        BankCustomer.queue_counter += 1
        self.service_type = service_type
        self.is_premium = is_premium
        self.arrival_time = datetime.now()
        self.priority = self._calculate_priority()
    
    def _calculate_priority(self):
        priority = {
            'ฝาก-ถอน': 3,
            'ชำระค่าบริการ': 2,
            'เปิดบัญชี': 1,
            'สินเชื่อ': 0
        }
        base_priority = priority.get(self.service_type, 4)
        if self.is_premium:
            base_priority -= 0.5
        return base_priority
    
    def __lt__(self, other):
        if self.priority == other.priority:
            return self.arrival_time < other.arrival_time
        return self.priority < other.priority

class BankQueue:
    def __init__(self):
        self.queue = []
        self.waiting_count = 0
    
    def add_customer(self, customer):
        heapq.heappush(self.queue, customer)
        self.waiting_count += 1
        print(f"หมายเลขคิว: {customer.queue_number}")
        print(f"บริการ: {customer.service_type}")
        print(f"สถานะ: {'Premium' if customer.is_premium else 'ทั่วไป'}")
        print(f"จำนวนคิวรอ: {self.waiting_count}")
        print("-" * 30)
    
    def serve_next_customer(self):
        if not self.queue:
            print("ไม่มีลูกค้าในคิว")
            return None
        
        customer = heapq.heappop(self.queue)
        self.waiting_count -= 1
        wait_time = datetime.now() - customer.arrival_time
        print(f"\nเรียกหมายเลขคิว: {customer.queue_number}")
        print(f"บริการ: {customer.service_type}")
        print(f"เวลารอ: {wait_time.seconds} วินาที")
        print(f"จำนวนคิวรอ: {self.waiting_count}")
        print("-" * 30)
        return customer
    
    def display_queue(self):
        if not self.queue:
            print("ไม่มีลูกค้าในคิว")
            return
        print("\nรายการคิวที่รอ:")
        temp_queue = self.queue.copy()
        position = 1
        while temp_queue:
            customer = heapq.heappop(temp_queue)
            print(f"{position}. หมายเลขคิว {customer.queue_number} - {customer.service_type}")
            position += 1
        print("-" * 30)

# ระบบการเพิ่มคิวแบบโต้ตอบ
def interactive_bank_queue():
    bank = BankQueue()
    services = ['ฝาก-ถอน', 'ชำระค่าบริการ', 'เปิดบัญชี', 'สินเชื่อ']
    while True:
        print("\nเลือกธุรกรรม:")
        for i, service in enumerate(services, start=1):
            print(f"{i}. {service}")
        print("5. ออกจากระบบ")
        choice = input("เลือกหมายเลขบริการ: ")
        
        if choice == '5':
            break
        
        if choice in map(str, range(1, 5)):
            service_type = services[int(choice) - 1]
            is_premium = input("เป็นลูกค้า Premium หรือไม่? (y/n): ").lower() == 'y'
            customer = BankCustomer(service_type, is_premium)
            bank.add_customer(customer)
        else:
            print("ตัวเลือกไม่ถูกต้อง กรุณาเลือกใหม่")
        
        print("\nแสดงลำดับคิว:")
        bank.display_queue()
        
        input("กด Enter เพื่อเรียกลูกค้ารายถัดไป...")
        bank.serve_next_customer()

if __name__ == "__main__":
    interactive_bank_queue()
```
![image](https://github.com/user-attachments/assets/594daca2-fec2-4e96-bb59-df25569fedb6)

