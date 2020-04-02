## 面试问题
### c++部分

#### 如何使一个类不能派生成其他子类
    将构造函数声明为私有，派生类将无法编译。同样的，该类也不能通过构造函数进行实例化，应提供一个接口完成实例化操作。

#### 如何使一个类只能生成一个实例
```c++
class A {
  private :
    A() = default;
  public:
    static A &instance() {
      static A instance{};
      return instance;
    }
};
int main() {
 A a = A::instance();
}
```
    参考如上，限定了该类不能通过构造函数生成实例化对象，限定该类只能通过A::instance 生成实例化对象，且实例仅有一个。对应设计模式应该是单例设计模式（这句话不确定）

#### 如何使一个类只能在堆上创建对象
    将析构函数设为私有。且提供接口完成delete操作

```c++
class A {
  private :
    ~A() {
      printf("delete\n");
    };
  public:
    void free() {
      delete this;
    }
};
int main() {
  A * a = new A;
  a->free();
}
```
