# **Polymorphism - Tính đa hình**
## **1. Đặt vấn đề**
> **Đa hình (polymorphism)** nghĩa là có nhiều hình thái khác nhau

vd :  Con mèo sẽ kêu “meo meo” còn con chó lại “gâu gâu”. Hành động phát ra tiếng này tuy là một hành động nhưng khi được 2 đối tượng khác nhau là chó và mèo thực hiện thì lại khác nhau.

**Phân biệt kế thừa và đa hình :**

Đa hình là một khả năng của một đối tượng để hành xử theo nhiều cách trong từng trường hợp

Kế thừa là tạo ra một lớp mới bằng cách sử dụng các thuộc tính và phương thức của một lớp hiện có

<p align="center">
  <img src="https://techacademy.edu.vn/wp-content/uploads/2022/03/cac-loai-da-hinh-trong-c-1.png" width="500" height="300">
</p>

## **2. Phương thức ảo, từ khóa virtual**

**Đặt vấn đề** : 

Sự kế thừa trong C++ cho phép có sự tương ứng giữa lớp cơ sở và các lớp dẫn xuất:  

>Một con trỏ có kiểu lớp cơ sở luôn có thể trỏ đến địa chỉ của một đối tượng của lớp dẫn xuất. 

Tuy nhiên, khi thực hiện lời gọi một phương thức của lớp, trình biên dịch sẽ quan tâm đến kiểu của con trỏ chứ không phải đối tượng mà con trỏ đang trỏ tới: phương thức của lớp mà con trỏ có kiểu được gọi chứ không phải phương thức của đối tượng mà con trỏ đang trỏ tới được gọi. 

```c++
class Animal {
public:
    void makeSound() {
        cout << "Animal make sound...\n";
    }
};

class Cat : public Animal {
public:
    void makeSound() {
        cout << "meow meow\n";
    }
};

class Dog : public Animal {
public:
    void makeSound() {
        cout << "woof woof\n";
    }
};
int main() {
    Animal* cat = new Cat();
    cat->makeSound();
}
```
```
Animal make sound...
```
Để giải quyết vấn đề trên chúng ta có thể dùng từ khóa `virtual`

```c++
class Animal {
public:
    virtual void makeSound() {
        cout << "Animal make sound...\n";
    }
};
```
khi đó `makeSound` trở thành 1 phương thức ảo

- Phương thức ảo (virtual method) là một hàm hay phương thức có thể thừa kế và ghi đè

- Phương thức ảo được khai báo bằng cách thêm từ khóa virtual vào khai báo của hàm trong lớp cơ sở

## **3. Lớp ảo. Phương thức thuần ảo**
### **3.1 Hàm thuần ảo (pure virtual function)**

- Hàm thuần ảo không có thân hàm và bắt buộc phải kết thúc với “= 0”

- Cú pháp “= 0” không phải là gán hàm thuần ảo có giá trị bằng 0. Đó chỉ là cú pháp cho biết đó là hàm thuần ảo

- Không cần sử dụng hàm này trong lớp cơ sở, chỉ phục vụ cho lớp dẫn xuất

- Lớp dẫn xuất bắt buộc phải định nghĩa lại hàm thuần ảo

```c++
class Animal { // abstract class ; lop truu tuong, can't create Animal object
public:
    virtual void makeSound() = 0; // pure virtual function
};

class Cat : public Animal {
public:
    void makeSound() {
        cout << "meow meow\n";
    }
};

class Dog : public Animal {
public:
    void makeSound() {
        cout << "woof woof\n";
    }
};
int main() {
    Animal* cat = new Cat();
    Animal* dog = new Dog();
    Animal* animal[2] = { cat,dog };
    for (int i = 0; i < 2; i++) {
        animal[i]->makeSound();
    }
}
```

### **3.2 Lớp cơ sở ảo (virtual base class)**

<p align="center">
  <img src="https://gochocit.com/wp-content/uploads/2021/11/so-do-ke-thua-virtual-base-class-oop.png" >
</p>

Nếu đối tượng của lớp D gọi đến một hàm được kế thừa từ lớp A thì sẽ gây ra một sự mơ hồ. Không biết hàm đó được kế thừa gián tiếp từ lớp B hay lớp C.

Để giải quyết tính không rõ ràng này, C++ có một cơ chế mà nhờ đó chỉ có một bản sao của lớp A ở trong lớp D. Đó là sử dụng lớp cơ sở ảo (virtual base class).

```c++
//Cach 1:
class B : virtual public A{
};

//Cach 2:
class B : public virtual A{
};
```

Việc chỉ định A là lớp cơ sở ảo trong các lớp B và C, nghĩa là A sẽ chỉ xuất hiện một lần trong lớp D. Khai báo này không ảnh hưởng đến các lớp B và C.