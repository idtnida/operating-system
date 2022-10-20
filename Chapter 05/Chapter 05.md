# Chapter 05 : Memory Management

## Topic
*

## Address Binding
OS Code กับ Data เวลาโหลดขึ้น Memory จริง ๆ จะ Share กัน Share Address Space
1. OS จะรู้ได้ไงใครใช้ process ไหนอยู่ ใครใช้ Memory ที่ Address ไหน

* Compile Time
* Load Time
* Execution Time
> ```
>
>   +--------------+
>   |     Code     |
>   +--------------+
>   |     Data     |
>   +--------------+
>   |     Heap     |
>   +--------------+
>   |     Stack    |
>   +--------------+
>
> ```



## Logical Address vs Physical Address


## Memory Management
* Contiguous Allocation
* Simple Paging
* Simple Segmentation




## Resource Abstraction Address Space
การที่ OS สร้างภาพ Memory ให้เรามองเห็น มันไม่ใช่ของจริง เช่น เรามีไฟล์เป็น Resource Abstraction แทน Harddisk, IO
นอกจากนี้มี Process Address Space แทน Memory

Virtual Memory
เราเอาบางส่วน Copy ลง HDD ก่อน ตรง Swap Area

## Pros.
ข้อดีของการที่ OS สร้างภาพ Memory ให้เรามองเห็น มันไม่ใช่ของจริง เพราะฉะนั้นมันคือ Resource Abstraction Address Space
เวลาเขียนโปรแกรม
* ไม่ต้องกังวลว่าจะมี Space พอหรือไม่พอ
* ไม่ต้องกังวลว่าจะมีใครใช้ Memory อยู่รึป่าว
* ไม่ต้องกังวลว่า Process อื่นจะมาแตะ Memory ของเรา เพราะ Process สองตัวไม่มีทางไปแตะ Memory ของกันและกันได้

## Page Table Entries
> ```
>
>                      Process Address Space
>           0  +---------------------------------+  --+
>              |                                 |    |
>              |             Page #0             |    | 4KB = 4 * K = 2^2 * 2^10 = 2^12 byte
>              |                                 |    |
>              |---------------------------------|  --+
>              |                                 |
>              |             Page #1             |
>              |                                 |
>              |---------------------------------|
>              |                 .               |
>              |                 .               |
>              |                 .               |
>              |                 .               |
>              |                 .               |
>              |                 .               |
>              |                 .               |
>              |                 .               |
>              |                 .               |
>              |---------------------------------|
>              |                                 |
>              |             Page #n             |
>    2^32 - 1  |                                 |
>              +---------------------------------+
>   
> ```
1. 1 Page มีขนาด 4KB แปลงให้อยู่ในรูป byte ที่ Address บน Memory ใช้ จะได้ 2^12 byte
2. Address ทั้งหมดมีขนาด 2^32 byte จะมีทั้งหมดกี่ Page ให้ทำการหารปกติ
3. แทนค่าลงในสูตร (2^32) / (2^12) = 2^20 Page

#### Homework
```bash
- Address Bus : 32 bit
- Page Size : 1 KB
- Page Table Entry : 4 byte
```


#### Exam
1. มี Page Table Entries ทั้งหมดเท่าไหร่ [2^80 entries]()
```bash
- มี page ทั้งหมด 2^20 page
```

2. Page Table มีขนาดเท่าไหร่ [4 MB]()
```bash
- กำหนดให้แต่ละ Page Table Entries มีขนาด 4 byte
- 2^20 entries * 4 byte = 4 MB
- เราอยากใช้ Virtual Memory กับ Page Table ด้วย
```

3. 1 Page สามารถมี Page Table Entries ได้ทั้งหมดกี่ entries 

## Credit
Operatin System (6th Edition)
