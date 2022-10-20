# Operating System

## Topic
* [I/O Controller](http://webneena.blogspot.com/2018/01/io-controller_23.html)
* [Static Library vs Dynamic Library](http://webneena.blogspot.com/2018/01/static-library-vs-dynamic-link-library.html)
* [32-bit vs 64-bit](http://www.tamemo.com/post/115/os-memory-paging/)

## Interrupt
การทำงานของ CPU โดยปกติจะต้องติดต่อกับอุปกรณ์ Hardware ต่าง ๆ เชน Disk, Keyboard, Clock, Printer ซึ่งอาจจะถูกขัดจังหวะการทำงานด้วยอุปกรณ์เหล่านี้ โดย Interrupt จะถูกแบ่งออกเป็น 4 ประเภท
* Interrupt ที่เกิดจากความผิดพลาดของโปรแกรม เช่น Overflow, Devide by Zero หรือเกิดจากการ Execute คำสั่งที่ไม่ถูกต้อง
* Interrupt ที่เกิดจากการตั้งเวลาของ CPU เอง เพื่อตรวจสอบการทำงาน
* Interrupt ที่เกิดจากตัวควบคุมอุปกรณ์ Device Controller ต่าง ๆ เพื่อบอกสถานะการทำงาน
* Interrupt ที่เกิดจากความผิดพลาดของ Hardware

## Interrupt Controller
>```
>
>              CPU                                Interrupt Controller
>     +-------------------+                  +----------------------------+
>   --|                   |--      Ack       |                            |
>     |                   |     -------->    |                            |
>   --|                   |--                |                            |    <---------   Disk
>     |                   |                  |                            |
>   --|                   |--                |                            |
>     |                   |     <--------    |                            |    <---------   Keyboard
>   --|                   |--   Controller   |                            |
>     +-------------------+       Issue      |                            |
>                               Interrupt    |                            |    <---------   Clock
>                                            |                            |
>                                            |                            |
>                                            |                            |    <---------   Printer
>                                            |                            |
>                                            |                            |
>                                            +----------------------------+
>                                  ถ้าเสร็จพร้อมกัน จะเลือก Priority สูงที่สุด ส่ง IRQ ไปยัง CPU
>
>               |                                           |                               |
>               +------------------------------------------------------------------------------------> Bus
>
>```
1. Hardware จะส่งสัญญาณ Interrupt ไปยัง Interrupt Controller
2. Interrupt Controller จะรับสัญญาณจากอุปกรณ์ Hardware ส่งต่อไปยัง CPU
3. หากมีสัญญาณ Interrupt เข้ามาพร้อมกัน Interrupt Controller จะเลือกอุปกรณ์ที่มี Priority สูงที่สุด
4. หลังจากที่ CPU ได้รับ ก็จะตอบ ACK กลับไปยัง Interrupt Controller

## Interrupt Handler
เป็นการจัดการกับ Interrupt ที่เข้ามาใน CPU ซึ่งจะทำหลังจากที่ CPU Excute Instruction คำสั่งปัจจุบันเสร็จ โดยคำสั่งในการจัดการ Interrupt จะถูก Set ตอนเริ่มระบบปฏิบัติการ Boot OS จะเริ่มจากการนำ Interrupt Vector ซึ่งใช้ในการเก็บ Address เข้าสู่ Physical Memory เพื่ออ้างอิงไปยัง Address ของ Interrupt Handler ที่ใช้เก็บคำสั่งในการจัดการ Interrupt
> ```
>
>   ไม่ใช่ Address จริง ๆ คล้าย ๆ Array                                                  Internal Register
>    ^                                                                                      ^
>    |                                                                                      |
>    |          Physical Memory                                                     CPU     |
>        +-------------------------+ --+                            +---------------------------------+
>   [0]  |                         |   |                            |            +--------------------|
>        |-------------------------|   |                            |   +----+   |        +-------+   |
>   [1]  |          1500           |   |     start boot os          |   | PC |   |  PC'   |       |   |
>        |-------------------------|   |-->  Intterrupt vector      |   +----+   |        +-------+   |
>   [2]  |          2000           |   |     keep Address           |            |                    |
>        |-------------------------|   |                            |   +-----+  |        +-------+   |
>        |                         |   |                            |   | PSW |  |  PSW'  |       |   |
>        |-------------------------| --+                            |   +-----+  |        +-------+   |
>        |            .            |                                |            |                    |
>        |            .            |                                |   +----+   |        +-------+   |
>        |            .            |                                |   | SP |   |  SP'   |       |   |
>        |-------------------------| --+                            |   +----+   |        +-------+   |
>   1500 |    Interrupt Handler    |   |                            |            +--------------------|
>        |-------------------------|   |--> os set boot             +---------------------------------+
>   2000 |    Interrupt Handler    |   |
>        |-------------------------| --+
>        |                         |
>        |-------------------------|
>        |          Code           |----------------+
>        |-------------------------|                |
>        |          Data           |----------+     |
>        |-------------------------|          |     |
>        |          Heap           |          |     |                      Excel Program
>        |-------------------------|          |     |               +-------------------------+
>        |       User Stack        |          |     +---------------|          Code           |
>        |-------------------------|          |                     |-------------------------|
>        |      Kernel Stack       |          +---------------------|          Data           |
>       +--------------------------+                                +-------------------------+
>   
> ```
1. Copy ค่าใส Internal Register
2. Edit ค่าใน SP เป็น Kernel Stack
3. Copy ค่าใน Internal Register ลงบน Memory ส่วนที่เป็น Kernel Stack
4. ค่า Address ใน PC จะเปลี่ยนไปทำ Interrupt Handler ที่ 2000 หลังจากนั้น Software ทำต่อ
Note : PC, PSW และ SP เป็นส่วนของ Hardware ทำ

## Credit
Operatin System (6th Edition)

## License
Webneena license.
