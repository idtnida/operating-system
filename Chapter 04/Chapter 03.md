# Chapter 03

## Topic
*

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

## Credit
Operatin System (6th Edition)
