---
layout: blog
book: true
title:  "leetcode c++纯虚函数 by DylanChou 刷leetcode心得"
background-image: http://ot1cc1u9t.bkt.clouddn.com/17-7-15/82431810.jpg
date:   2021-8-11 14:12:54
tags:
- C++基础
- 纯虚函数
---






在[C++](http://c.biancheng.net/cplus/)中，可以将虚函数声明为纯虚函数，语法格式为：

```
virtual 返回值类型 函数名 (函数参数) = 0;
```

纯虚函数没有函数体，只有函数声明，在虚函数声明的结尾加上`=0`，表明此函数为纯虚函数。

> 最后的`=0`并不表示函数返回值为0，它只起形式上的作用，告诉编译系统“这是纯虚函数”。

包含纯虚函数的类称为抽象类（Abstract Class）。之所以说它抽象，是因为它无法实例化，也就是无法创建对象。原因很明显，纯虚函数没有函数体，不是完整的函数，无法调用，也无法为其分配内存空间。

抽象类通常是作为基类，让派生类去实现纯虚函数。派生类必须实现纯虚函数才能被实例化。

```c++
#include <iostream>
using namespace std;

//线
class Line {
public:
    Line(float len);
    virtual float area() = 0;
    virtual float volume() = 0;
protected:
    float m_len;
};
Line::Line(float len) : m_len(len) { }

//矩形
class Rec : public Line {
public:
    Rec(float len, float width);
    float area();
protected:
    float m_width;
};
Rec::Rec(float len, float width) : Line(len), m_width(width) { }
float Rec::area() { return m_len * m_width; }

//长方体
class Cuboid : public Rec {
public:
    Cuboid(float len, float width, float height);
    float area();
    float volume();
protected:
    float m_height;
};
Cuboid::Cuboid(float len, float width, float height) : Rec(len, width), m_height(height) { }
float Cuboid::area() { return 2 * (m_len * m_width + m_len * m_height + m_width * m_height); }
float Cuboid::volume() { return m_len * m_width * m_height; }

//正方体
class Cube : public Cuboid {
public:
    Cube(float len);
    float area();
    float volume();
};
Cube::Cube(float len) : Cuboid(len, len, len) { }
float Cube::area() { return 6 * m_len * m_len; }
float Cube::volume() { return m_len * m_len * m_len; }

int main() {
    Line* p = new Cuboid(10, 20, 30);
    cout << "The area of Cuboid is " << p->area() << endl;
    cout << "The volume of Cuboid is " << p->volume() << endl;

    p = new Cube(15);
    cout << "The area of Cube is " << p->area() << endl;
    cout << "The volume of Cube is " << p->volume() << endl;

    return 0;
}
```

