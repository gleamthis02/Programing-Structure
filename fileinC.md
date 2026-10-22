# การสร้างไฟล์ 

- Pointer
ตอนประกาศตัวแปร → บอกว่าตัวแปรนี้เป็น Pointer เช่น int $\color{red}{\text{*ptr}}$ ($\color{red}{\text{*ptr}}$ เป็น Pointer สำหรับชี้ตัวแปร int)
ตอนใช้งาน → ใช้ดึง ค่า ที่อยู่ในตำแหน่งที่ Pointer ชี้อยู่ เช่น *ptr

- Adress-of
ใช้หา ตำแหน่ง (Address) ของตัวแปร เช่น &x แปลว่า "ตำแหน่งที่อยู่ของตัวแปร x"
ex. 0x7ffc...

ใน Pseudocode 
```
PROCEDURE AppedFile()
    DECLARE fileName, newLine : STRING
    fileName <- "log.txt"
    INPUT newLine
    OPENFILE fileNaem FOR APPEND
    WRITEFILE fileName, newLine
    CLOSEFILE fileName
ENDPROCEDURE
```
ใน C

```c
#include <stdio.h>

void CreateFile() // ฟังก์ชันสร้างไฟล์
{
    char fileName[] = "notes.txt"; // กำหนดชื่อไฟล์
    FILE *file; // FILE คือชนิดตัวแปร // ประกาศตัวแปร *file  
    file = fopen(fileName, "w");

    if (file == NULL) {
        printf("Cannot create file!\n");
        return;
    }
    fprintf(file, "IGCSE File Handling\n");
    fprintf(file, "Coddy Tech\n");
    fprintf(file, "Line 3 Success\n");
    fclose(file);
}

void ReadFile()
{
    char fileName[] = "notes.txt";
    char line[1000];
    FILE *file;

    file = fopen(fileName, "r");

    if (file == NULL)
    {
        printf("File not found!\n");
        return;
    }

    while (fgets(line, sizeof(line), file) != NULL)
    {
        printf("%s", line);
    }

    fclose(file);
}

int main()
{
    CreateFile();
    ReadFile();
    return 0;
}
```

function จากโค้ดใช้เกี่ยวกับในไฟล์
```
1. ตัวแปร FILE *file
FILE * คือ pointer ที่ใช้ "ชี้" ไปยังไฟล์ที่เปิดอยู่ ทุกครั้งที่จะทำงานกับไฟล์ต้องมีตัวแปรชนิดนี้เสมอ
```
```c
fopen() — เปิดไฟล์หรือสร้างไฟล์ใหม่
ใช้เปิดไฟล์ตามโหมดที่กำหนด และคืนค่าเป็น FILE* Pointer
ex. FILE *file = fopen("filename.txt", "mode"); // mode คือ char
        ความหมาย:       ถ้าไม่มีไฟล์:           ถ้าไฟล์มีอยู่แล้ว:
"r"	    อ่านอย่างเดียว	    error (NULL)	       อ่านได้
"w"	    เขียนทับ	         สร้างใหม่	      ลบอันเก่าทิ้ง แล้วเขียนใหม่
"a"	    เขียนต่อท้าย	     สร้างใหม่           เขียนต่อท้ายของเดิม

fclose(file);
file (ชนิด FILE *): ตัวแปร Pointer ของไฟล์ที่เราเปิดไว้ และต้องการสั่งปิด
เปิดแล้วต้องปิด เพื่อบันทึกข้อมูลลงดิสก์ให้สมบูรณ์เพราะหากไม่ปิดข้อมูลยังคงอยู่ในหน่อยความจำชั่วคราว (Ram)
และเป็นการคืนทรัพยากรให้ระบบ เพราะไม่ใช้ Ram แล้ว ให้ไฟล์อื่นๆได้ถูกเปิดต่อไปได้มีประสิทธิภาพ
```
```c
fprintf() เขียนข้อความลงไฟล์
ex. fprintf(file, "Age: %d\n", age);
```
```c
fputs()
fputs("Text", file);
ข้อความล้วนธรรมดาที่ไม่ต้องแปลงค่าตัวแปร
```
```c
fputc()
fputc(ch, file);
ตัวอักษรเดียว (char)
```
```c
fwrite()
fwrite(&data, size, count, file);
โครงสร้างข้อมูล struct หรือไฟล์ Binary
```
