# Standard Template Library

* _ใช้ได้กับภาษา C++ เท่านั้น_
* Standard Template Library (C++) คือชุดฟังก์ชันและโครงสร้างข้อมูลที่ภาษา C++ เตรียมไว้ให้
* ในที่นี้ จะอธิบาย `vector`, `map` และ `multimap`
  - `vector` คือ array แต่มีการจัดการเรื่องขนาดของ array ให้อัตโนมัติ
  - `map` ใช้สำหรับเก็บค่า โดยอ้างอิงจากค่าชนิดหนึ่ง (key) ไปยังอีกค่าชนิดนึง (value) แทนที่จะใช้ตัวเลข index แบบ array
  - `multimap` เหมือน map แต่ key นึง อาจมีได้หลาย value

## vector

* ต้อง `#include <vector>` และ `using namespace std;`
* `vector` เป็นคลาสในภาษา C++ ทีควบคุมการสร้าง array การปรับขนาด และการเข้าถึงข้อมูลให้โดยอัตโนมัติ
* สามารถสร้าง `vector` ได้ในรูปแบบ `vector<Type> variableName;` เช่น `vector<int> studentID;`
* หรือสร้างแบบ `vector<Type> variableName(anotherVector)` เพื่อเลียนแบบ `vector` ที่ใส่เข้ามา
* หรือสร้างแบบ `vector<Type> variableName(first, last)` เพื่อสร้างจาก vector, map, array, etc. ในช่วง first ถึง last
  - last จะต้องอยู่เกินตำแหน่งสุดท้ายไป 1 ตำแหน่ง
  - หากเป็น array โดยทั่วไปจะใส่ pointer ตัวแรก (ตัว array) เอง และ pointer ที่บวกด้วยขนาด array (จะอยู่เกินไป 1 ตำแหน่งพอดี)

ตัวอย่าง
```c++
// สร้าง vector ว่าง
vector<int> students;

// สร้าง vector จาก array
int studentArray = { 4, 8, 15, 16, 23, 42 };
vector<int> newStudents(studentArray, studentArray + 6);

// สร้าง vector จาก vector อื่น
vector<int> oldStudents(newStudents);
```

### ฟังก์ชันของ vector

* การเรียกใช้ฟังก์ชัน เขียนในรูป `variableName.functionName(arg1, arg2, ...)`

#### Iterators
* ฟังก์ชัน `begin`, `end`, `rbegin`, `rend` เป็นฟังก์ชันที่ให้ iterator สำหรับ loop สมาชิกทุกตัว
  - iterator คือตัวช่วยในการเข้าถึงสมาชิกแต่ละตัว ดูในหัวข้อถัดไป
  - `begin` ให้ตำแหน่งตัวแรก ส่วน `end` ให้ตำแหน่งหลังตัวสุดท้าย 1 ตัว
  - `rbegin` ให้ตำแนห่งตัวสุดท้าย ส่วน `rend` ให้ตำแนห่งตัวก่อนตัวแรก 1 ตัว
  - ดูตัวอย่างได้ที่หัวข้อถัดไป

#### Capacity

* ฟังก์ชัน `size` ไว้สำหรับดูขนาดของ `vector`
  - เช่น `cout << "There are " << studentID.size() << " students.";`

* ฟังก์ชัน `empty` ไว้สำหรับดูว่า `vector` ว่างหรือไม่
  - เช่น `if (studentID.empty()) { cout << "There are no students."; }`

#### Element access

* สามารถเข้าถึงสมาชิกของ vector ได้แบบเดียวกันกับ array
  - แต่เข้าถึงได้มากสุด เท่าที่มีอยู่ใน vector เท่านั้น หากต้องการเพิ่มต่อท้ายต้องใช้ `push_back`
  - เช่น `studentID[0] = 0;` (เปลี่ยน studentID ที่ตำแหน่งแรกให้เป็น 0)

* ฟังก์ชัน `front` และ `back` มีไว้สำหรับเข้าถึงสมาชิกตัวแรกและตัวสุดท้าย
  - เช่น `cout << studentID.front();` (0)

* ฟังก์ชัน `at` ใช้เหมือนกันวงเล็บเหลี่ยมของ array
  - `studentID.at(0) = 0;`

#### Modifiers

* ฟังก์ชัน `push_back` มีไว้สำหรับเพิ่มสมาชิกต่อท้าย `vector`
  - เช่น `studentID.push_back(44677);`

* ฟังก์ชัน `pop_back` มีไว้สำหรับลบสมาชิกตัวสุดท้าของ `vector`
  - เช่น `studentID.pop_back();`

* ฟังก์ชัน `insert` มีไว้สำหรับแทรกสมาชิกเข้าไปก่อนหน้าตำแหน่งที่เราต้องการ

  - แบบแรก `insert(position, value)` position คือ iterator ตำแหน่งที่ต้องการ และ value คือค่าที่ต้องการแทรก
  - แบบที่สอง `insert(position, n, value)` คล้ายกับแบบข้างบน แต่จะแทรก value ทั้งหมด n ตัว
  - แบบที่สาม `insert(position, first, last)` เมื่อ first และ last คือ iterator ของอีก vector, map, array, etc. (last จะอยู่ตำแหน่งเกินตัวสุดท้าย 1 ตัว) มีไว้เพื่อแทรกช่วง first ถึง last ก่อนหน้าตำแหน่ง position
  
  - เช่น `studentID.insert(studentID.begin() + 3, 42);` จะเพิ่มเลข 42 ไปที่ตำแหน่ง index 3
  - `studentID.insert(studentID.begin(), 5, 555);` เพิ่มเลข 555 เข้าไป 5 ตัวที่ตำแหน่งแรก
  - `studentID.insert(studentID.begin() + 2, studentArray, studentArray + 6);` แทรกทั้ง array จากตัวอย่างหัวข้อที่แล้ว เริ่มที่ตำแหน่ง index 2

### การ loop ใน vector

* สามารถเข้าถึงสมาชิกทุกตัวใน `vector` ได้สองวิธี
* วิธีแรกคือการเข้าถึงแบบ array

```c++
for (int i = 0; i < studentID.size(); i++)
    cout << studentID[i] << endl;
```

* อีกวิธีหนึ่งคือการใช้ iterator โดย iterator จะมีลักษณะคล้ายๆ กับ pointer
* _เฉพาะมาตรฐาน C++11 ขึ้นไป_ ไม่จำเป็นต้องระบุชนิด iterator สามารถพิมพ์ `auto` ได้เลย

```c++
// it เป็นตัวแปรชนิด vector<int>::iterator ซึ่งมีลักษณะคล้ายๆ pointer
// สามารถเข้าถึงสมาชิกได้โดยพิมพ์ asterisk * ข้างหน้า
// เมื่อต้องการเคลื่อนไปตัวถัดไปสามารถใช้ it++ ได้เหมือน pointer

// loop จะหยุดทำงานเมื่อ loop ถึงตำแหน่งที่เกินตัวสุดท้าย (`studentID.end()`)
for (auto it = studentID.begin(); it != studentID.end(); ++it)
    cout << *it << endl;

// loop ย้อนหลัง
for (Auto it = studentID.rbegin(); it != studentID.rend(); ++it)
    cout << *it << endl;
```

* _เฉพาะมาตรฐาน C++11 ขึ้นไป_ สามารถ loop สมาชิกทุกตัวได้โดยใช้ range-based loop

```c++
for (auto std : studentID)
    cout << std << endl;
```
