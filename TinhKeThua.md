# **[Buổi 3] Tính kế thừa**

## **1. Khái niệm**

<p align="center">
  <img src="https://blog.luyencode.net/wp-content/uploads/2020/02/inheritance2-768x333.png" width="400" height="220">
</p>

> Là khả năng lấy một thuộc tính, đặc tính của một lớp cha để áp dụng lên lớp con

- *Parent / base class* : Lớp có các thuộc tính được kế thừa bởi lớp con (lớp cơ sở)

- *Child / derived class* : Lớp kế thừa các thuộc tính từ một lớp khác (lớp dẫn xuất)

```
class sub_class : access_mode base_class{
    // code
};
```
- subclass_name là tên lớp con sẽ áp dụng kế thừa
- base_class_name là tên lớp cha
- access_mode có thể là public, private hoặc protected
- không chỉ rõ access_mode thì mặc định sẽ là private

### **Phạm vi kế thừa**

- `public` : Sau khi kế thừa, tất cả các thành viên dạng `public` lớp cha sẽ `public` ở lớp con, dạng `protected` ở lớp cha vẫn sẽ là `protected` ở lớp con.
- `protected` : Sau khi kế thừa, tất cả các thành viên dạng `public` lớp cha sẽ trở thành `protected` tại lớp con.
- `private` : Sau khi kế thừa, tất cả các thành viên dạng `public` và `protected` ở lớp cha sẽ thành `private` tại lớp con.

## **2. Các loại kế thừa**

### **Đơn kế thừa (Single Inheritance)**

<p align="center">
  <img src="https://blog.luyencode.net/wp-content/uploads/2020/02/single-inheritance.png" >
</p>

>Một lớp chỉ được kế thừa từ đúng một lớp khác (lớp con chỉ có duy nhất một lớp cha)

```
class Employee {
protected:
    string name;
    int age;
public:
    Employee();
    Employee(string name, int age) {
        this->name = name;
        this->age = age;
    }
    void introduceYourself() {
        cout << "Hello my name is " << name << " I'm " << age << " years old\n";
    }
};
class Teacher : public Employee {
public:
    string subject;
    void prepareLesson() {
        cout << name << " is preparing " << subject << " lesson\n";
    }
    Teacher(string name, int age, string subject)
        : Employee(name, age) {
        this->subject = subject;
    }
    void Work() {
        cout << name << " is teaching " << subject << "\n";
    }
};
```
### **Đa kế thừa (Multiple Inheritance)**

<p align="center">
  <img src="https://blog.luyencode.net/wp-content/uploads/2020/02/multiple-inheritance-768x186.png" width="400" height="220">
</p>

>Một lớp có thể kế thừa từ nhiều hơn một lớp khác (lớp con được kế thừa từ nhiều hơn một lớp cha)

```
class subclass_name : access_mode base_class1, access_mode base_class2, ....
{
  //body of subclass
};
```
## **3. Nạp chồng hàm (Function Overloading)**

>Một khai báo `nạp chồng` là một khai báo mà đã được khai báo với **cùng tên** như một khai báo được khai báo trước đó trong **cùng phạm vi**, ngoại trừ rằng: cả hai khai báo có các tham số khác nhau và định nghĩa khác nhau.

```
int int_max(int a, int b)
{
    if (a > b)
        return a;
    else
        return b;
}
 
int float_max(float a, float b)
{
    if (a > b)
        return a;
    else
        return b;
}
```

```
int_max(4, 5)
float_max(4.4, 5.5)
```
## **4. Nạp chồng toán tử (Operator Overloading)**

>Dùng để định nghĩa toán tử có sẵn trong C++\

Nạp chồng toán tử trong lớp `phanso`

```
phanso operator +(phanso b)
{
    phanso c;
    c.tu = this->tu * b.mau + this->mau * b.tu;
    c.mau = this->mau * b.mau;
    return c;
}  
```
```  
phanso a, b, c;
c = a + b; 
```
## **5. Function overriding (ghi đè)**
> Function overloading : nhiều cách định nghĩa cho 1 tên hàm (có thể thay đổi input, output của hàm)

> Function overriding : Định nghĩa lại 1 hàm của lớp cha trong lớp con (giữ nguyên mẫu hàm)

```
#include <bits/stdc++.h>
using namespace std;
class Employee {
protected:
    string name;
    int age;
public:
    Employee();
    Employee(string name, int age) {
        this->name = name;
        this->age = age;
    }
    virtual void introduceYourself() {
        cout << "Hello my name is " << name << " I'm " << age << " years old\n";
    }
};
class Teacher : public Employee {
public:
    string subject;
    void prepareLesson() {
        cout << name << " is preparing " << subject << " lesson\n";
    }
    Teacher();
    Teacher(string name, int age, string subject)
        : Employee(name, age) {
        this->subject = subject;
    }
    void introduceYourself() { // overriding
        cout << "Hello my name is " << name << " I'm " << age << " years old and";
        cout << " I teach " << subject << "\n";
    }
    void Work() {
        cout << name << " is teaching " << subject << "\n";
    }
};
int main() {
    Employee e = Employee("Linh", 20);
    e.introduceYourself();
    Teacher t = Teacher("Lan", 30, "Physics");
    t.introduceYourself();
}
```
## **6. Hàm friend**

- Hàm bạn trong c++ là hàm tự do, không thuộc lớp. Tuy nhiên hàm bạn trong c++ có quyền truy cập các thành viên `private` của lớp.
- Một lớp trong c++ có thể có nhiều hàm bạn, và chúng phải nằm bên ngoài class
- Không thể áp đặt hàm bạn cho một lớp, nếu như chưa khai báo hàm bạn trong lớp

```
class Tester {
    string name;
public:
    friend void hangout(Tester t);
};

void hangout(Tester t) {
    cout << " and " << t.name << " is going shopping\n";
}
```
