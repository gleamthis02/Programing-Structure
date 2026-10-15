# Pointer และ Address
Address คือค่าตัวเลขตำแหน่ง
```c
int x = 10;
printf("%d\n", x);    // ค่าของ x → 10
printf("%p\n", &x);   // address ของ x → เช่น 0x7ffd1234
```
Pointer คือตัวแปรเก็บค่าตำแหน่งนั้น
```c
int x = 10;
int *p = &x;   // pointer เก็บ address ของ x 
```
```
 address      ชื่อ     ค่าที่เก็บ
┌─────────────────────────────
│ 0x1000   │  x   │    10     │ 
├─────────────────────────────   
│ 0x1004   │  p   │  0x1000   │
└─────────────────────────────
Address ของ x มีอยู่แล้ว (ก็ตัวมันเอง)
Pointer เก็บ Adress ของ x และยังมี Address เป็นของตัวเองของ Pointer เอง
```
```c
int x = 10;
int *p = &x;

printf("%d\n", x);    // 10
printf("%p\n", &x);   // 0x1000  (address ของ x)
printf("%p\n", p);    // 0x1000  (ค่าใน p = address ของ x)
printf("%d\n", *p);   // 10      (ค่าที่ p ชี้อยู่)
printf("%p\n", &p);   // 0x1004  (address ของตัว p เอง)

*p = 99;              // แก้ค่าที่ p ชี้อยู่ → x กลายเป็น 99
printf("%d\n", x);    // 99
```
