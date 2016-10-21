# การใช้ระบบ Standard Input/Output

## ภาษา C

* _คำว่า string ในที่นี้หมายถึง `char []` (array) ทั้งหมด_
* ต้อง `#include <stdio.h>`

### printf

* ใช้ได้ในรูปแบบ `printf("ข้อความที่ต้องการ", arg1, arg2, ...);`
* สามารถนำ arg1, arg2, ... มาแทนในข้อความได้
  - `%d` ใช้กับ `int`
  - `%f` ใช้กับ `float` (หากต้องการปรินท์ n ตำแหน่ง ให้พิมพ์ `%.nf` เช่น `%.2f`)
  - `%c` ใช้กับ `char`
  - `%s` ใช้กับ string (`char []`)

ตัวอย่าง
```c
int a = 5;
int b = 10;
printf("a is %d.\n", a);
printf("b is %d.\n", b);
printf("a + b is %d.\n", a + b);
```

### scanf

* ใช้ได้ในรูปแบบ `scanf("%_", pointer);`
* %_ ใช้คล้ายๆ `printf`
* pointer คือตำแหน่งของตัวแปรที่ต้องการให้รับค่าจากผู้ใช้
  - สังเกตว่า `scanf` เป็นฟังก์ชันแบบ Pass by Reference คือ `scanf` รับข้อมูลจากผู้ใช้แล้วจึงแก้ไขตัวแปรที่เราส่งตำแหน่งไปให้
* ไม่จำเป็นต้องใช้เครื่องหมาย `&` กับ string (`char []`)
* string จะอ่านถึงช่องว่าง (space bar/tab/new line) เท่านั้น
 

ตัวอย่าง
```c
int a;
scanf("%d", &a);
char b;
scanf("%c", &b);
char name[51]; // ใช้ได้มากสุด 50 ตัว (ตัวสุดท้ายเป็น \n)
scanf("%s", name);
printf("%s picked character %c and number %d.", name, b, a);
```

* หากต้องการอ่าน string ทั้งบรรทัดให้ใช้ `gets` แทน (เช่น `gets(name);` ในตัวอย่างข้างบน)

## ภาษา C++

* _คำว่า string ในที่นี้ สามารถใช้ได้กับทั้ง `char []` ของ C และ `string` ของ C++ เว้นแต่ว่าจะระบุไว้เป็นกรณีพิเศษ_
* สามารถใช้ `printf` และ `scanf` ได้ ถ้า `#include <cstdio>` (`#include <stdio.h>`)
* `cin` และ `cout` ของภาษา C++ ต้อง `#include <iostream>` และ `using namespace std`
* ควรเลือกใช้แบบ C หรือ C++ แบบใดๆ แบบหนึ่งเท่านั้น

### cout

* ใช้ได้ในรูปแบบ `cout << arg1 << arg2 << arg3 << ... << argn;`
* ของที่ใส่ลงไปจะเป็นตัวแปรพื้นฐานใดๆก็ได้ เช่น string, int, float โดยไม่ต้องระบุชนิด
* สามารถใช้ `endl` แทน `\n` ได้

ตัวอย่าง
```c
int n = 5;
cout << "n is " << n << "." << endl;
```

### cin

* ใช้ได้ในรูปแบบ `cin >> arg1 >> arg2 >> arg3 >> ... >> argn;`
* ใช้กับตัวแปรพื้นฐานใดๆก็ได้ เช่น string, int, float โดยไม่ต้องระบุชนิด

ตัวอย่าง
```c
char name[51]; // ใช้ได้มากสุด 50 ตัว (ตัวสุดท้ายเป็น \n)
int n;
cin >> name >> n;
cout << name << " picked " n << "." << endl;
```

* หากต้องการอ่าน string (`char []`) ทั้งบรรทัด ใช้ `gets` แบบเดิม หรือ `cin.getline(name, 50)` ก็ได้ (แบบหลังต้องระบุขนาดที่รองรับมากสุด)
* สำหรับ `string` ของ C++ ให้ใช้ `getline(cin, name);`