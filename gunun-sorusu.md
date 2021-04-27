# Günün Sorusu
- [Günün Sorusu](#günün-sorusu)
    - [Günün Sorusu 001](#günün-sorusu-001)
    - [Günün Sorusu 002](#günün-sorusu-002)
    - [Günün Sorusu 003](#günün-sorusu-003)
    - [Günün Sorusu 004](#günün-sorusu-004)
    - [Günün Sorusu 005](#günün-sorusu-005)
    - [Günün Sorusu 006](#günün-sorusu-006)
    - [Günün Sorusu 007](#günün-sorusu-007)
    - [Günün Sorusu 008](#günün-sorusu-008)
    - [Günün Sorusu 009](#günün-sorusu-009)
    - [Günün Sorusu 010](#günün-sorusu-010)
    - [Günün Sorusu 011](#günün-sorusu-011)
    - [Günün Sorusu 012](#günün-sorusu-012)
    - [Günün Sorusu 013](#günün-sorusu-013)
    - [Günün Sorusu 014](#günün-sorusu-014)
    - [Günün Sorusu 015](#günün-sorusu-015)
    - [Günün Sorusu 016](#günün-sorusu-016)
    - [Günün Sorusu 017](#günün-sorusu-017)
    - [Günün Sorusu 018](#günün-sorusu-018)
    - [Günün Sorusu 019](#günün-sorusu-019)
    - [Günün Sorusu 020](#günün-sorusu-020)
    - [Günün Sorusu 021](#günün-sorusu-021)
    - [Günün Sorusu 022](#günün-sorusu-022)
    - [Günün Sorusu 023](#günün-sorusu-023)
    - [Günün Sorusu 024](#günün-sorusu-024)
    - [Günün Sorusu 025](#günün-sorusu-025)
    - [Günün Sorusu 026](#günün-sorusu-026)
    - [Günün Sorusu 027](#günün-sorusu-027)
    - [Günün Sorusu 028](#günün-sorusu-028)
    - [Günün Sorusu 029](#günün-sorusu-029)
    - [Günün Sorusu 030](#günün-sorusu-030)
    - [Günün Sorusu 031](#günün-sorusu-031)
    - [Günün Sorusu 032](#günün-sorusu-032)


### [Günün Sorusu 001](https://t.me/trcpp/8766)

- Aşağıdaki kodda\
a) tanımsız davranış söz konusudur.\
b) Kodda bir sorun yoktur. Çıkış akımına şunu yazar:

```cpp
#include <iostream>

void g(int &&r) {
    r += 3;
    std::cout << r;
}

void g(int &r) {
    std::cout << r++;
}

template <typename T>
void f(T &&x) {
    x *= 5;
    g(x);
    g(std::forward<T>(x));
}

int main() {
    f(1);
}
```

### [Günün Sorusu 002](https://t.me/trcpp/8774)

- Aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:

```cpp
#include <iostream>

struct A {
    A() { std::cout << "1"; }
};

struct B {
    B() { std::cout << "2"; }
    B(A) { std::cout << "3"; }
    void b() { std::cout << "4"; }
};

A a() {
    std::cout << "5";
    return A{};
}

B b(A (*)()) {
    std::cout << "6";
    return B{};
}

int main() {
    B b(A());
    b(a).b();
}
```

### [Günün Sorusu 003](https://t.me/trcpp/8798)
- Aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpp
#include <iostream>

auto& g() { return std::cout << 1; }
auto f() {
    std::cout << 2;
    return g;
}

int main() {
    std::cout << (f()() << 3 ? 4 : 5);
}

```

### [Günün Sorusu 004](https://t.me/trcpp/8862)
- Aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpp
#include <iostream>

int main() {
    int a[]{1, 4, 7, 2};
    int* x{a};

    decltype(++x) y(x);
    decltype(++y) z(y);

    std::cout << *x + *y + *z;
}

```

### [Günün Sorusu 005](https://t.me/trcpp/8874)
- Aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpp
#include <iostream>

int main() {
    int a[2];
    decltype(a) b[2];
    decltype(b) c[3]{0, 1, 2, 3, 4};

    std::cout << c[0][1][2] << "\n";
}
```

### [Günün Sorusu 006](https://t.me/trcpp/8891)
- Aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpp
#include <algorithm>
#include <iostream>

int main() {
    auto x{1}, y{2};
    auto a{&x}, b{&y}, c{a++};
    std::copy(c, a, b);
    std::cout << x << y;
}
```

### [Günün Sorusu 007](https://t.me/trcpp/8909)
- Aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpp
#include <iostream>

template <auto n>
struct A : A<n + 1> {
    A() { std::cout << n; }
    ~A() { std::cout << n; }
};

template <>
struct A<5> {};
template <>
struct A<0> {};

int main() {
    A<1> x;
}
```

### [Günün Sorusu 008](https://t.me/trcpp/8974)
[Cevap](https://t.me/trcpp/9021)
- Aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpp
#include <iostream>

int main() {
    auto x = 2;
    auto y = x > 0 ? 5 : 1.4;
    std::cout << y / x;
}
```

### [Günün Sorusu 009](https://t.me/trcpp/9022)
- Aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpp
#include <iostream>
#include <type_traits>

int main() {
    auto c = 'c';
    std::cout << std::is_same_v<decltype(c), decltype(+c)>;
}
```

### [Günün Sorusu 010](https://t.me/trcpp/9061)
- Aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpp
#include <iostream>
#include <type_traits>

int main() {
    auto a{[] {}};
    auto b{[] {}};
    auto c(+a);
    auto d(+b);

    std::cout << std::is_same_v<decltype(a), decltype(b)>;
    std::cout << std::is_same_v<decltype(a), decltype(c)>;
    std::cout << std::is_same_v<decltype(c), decltype(d)>;
}
```

### [Günün Sorusu 011](https://t.me/trcpp/9112)
- Aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpp
#include <iostream>

struct A {
    static int x;
    static int foo() { return 1; }
};

int foo() { return 2; }

int A::x = foo();

int main() {
    std::cout << A::x;
    A::x = foo();
    std::cout << A::x;
}
```

### [Günün Sorusu 012](https://t.me/trcpp/9129)
- Aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpp
#include <iostream>

void f(long double) { std::cout << 1; }
void f(char) { std::cout << 2; }

int main() {
    f(2.5);
}
```

### [Günün Sorusu 013](https://t.me/trcpp/9158)
- Aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpp
#include <iostream>

int main() {
    std::cout << "hello";
    std::cout.operator<<("world");
}
```

### [Günün Sorusu 014](https://t.me/trcpp/9165)
- Aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpp
#include <iostream>

int main() {
    int typedef* ip;
    auto i{0};
    ip const p{&i};
    ++*p;
    std::cout << i;
}
```

### [Günün Sorusu 015](https://t.me/trcpp/9180)
- Aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpp
#include <iostream>

template <typename T, size_t n>
using ptr = T (*)[n];

int main() {
    int a[3][2]{0, 1, 3, 5, 7, 9};

    ptr<int, 2> b{a};
    ++b;
    ++**b;
    for (const auto& x : a)
        for (auto y : x)
            std::cout << y;
}
```

### [Günün Sorusu 016](https://t.me/trcpp/9205)
[Cevap](https://t.me/trcpp/9223)
- Aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpP
#include <iostream>

struct A {
    A() { std::cout << "A"; }
    ~A() { std::cout << "a"; }
};

struct B {
    B() { std::cout << "B"; }
    ~B() { std::cout << "b"; }
    B(A) { std::cout << "C"; }
};

A a;
int main() {
    B(a);
}
```

### [Günün Sorusu 017](https://t.me/trcpp/9255)
- Aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpp
#include <iostream>
#include <vector>

struct A {
    A() { std::cout << "1"; }
    ~A() { std::cout << "2"; }
    A(int) { std::cout << "3"; }
    A(const A&) { std::cout << "4"; }
    A(A&&) { std::cout << "5"; }
};

int main() {
    std::vector<A> v;
    v.emplace_back(1);
    v.push_back(v[0]);
}
```

### [Günün Sorusu 018](https://t.me/trcpp/9315)
- Aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpp
#include <iostream>

template <typename T>

void f(T) { std::cout << "1"; }

template <>
void f(int*) { std::cout << "2"; }

void f(int&) { std::cout << "3"; }

void f(int&&) { std::cout << "4"; }

int main() {
    int x{};
    int* p{&x};
    f(&x);
    f(p);
}
```

### [Günün Sorusu 019](https://t.me/trcpp/9333)
- Aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpp
#include <iostream>

template <int x, int y, int z>
using N = char[x][y][z];

template <int e = 2, int c = 3, int o = 4>
constexpr int n = sizeof(N<e, c, o>);

int main() {
    std::cout << n<> + n<1> + n<1, 2> + n<1, 2, 3>;
}
```

### [Günün Sorusu 020](https://t.me/trcpp/9404)
- Aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpp
#include <iostream>

struct A {
    operator void*() {
        return static_cast<A*>(this);
    }
};

int main() {
    A a, b;
    std::cout << (a == a) << (a == b) << (a == &a) << (a == &b);
}
```

### [Günün Sorusu 021](https://t.me/trcpp/9439)
- Aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpp
#include <iostream>

struct A {
    A() { std::cout << 'A'; }
    ~A() { std::cout << 'D'; }
    A(const A&) { std::cout << 'C'; }
    A(A&&) { std::cout << 'M'; }
};

void f(A) {}
A g() { return A{}; }

int main() {
    f(g());
}
```

### [Günün Sorusu 022](https://t.me/trcpp/9468)
- C++17 standartlarına göre aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpp
#include <iostream>

void foo(int x) {
    try {
        throw std::runtime_error{"R.T.E"};
    } catch (const std::exception& ex) {
        if (x)
            throw ex;
        else
            throw;
    }
}

void func(int x) {
    try {
        foo(x);
    } catch (const std::runtime_error&) {
        std::cout << 1;
    } catch (const std::exception&) {
        std::cout << 2;
    }
}

int main() {
    int a{1};
    func(a--);
    func(a);
}
```

### [Günün Sorusu 023](https://t.me/trcpp/9574)
- C++17 standartlarına göre aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpp
#include <iostream>

struct A {
    explicit A(double) {
        std::cout << "D";
    }
    A(long long) {
        std::cout << "L";
    }
};

A func(A) {
    return 128e9;
}

int main() {
    auto x = func(128e9);
}
```

### [Günün Sorusu 024]()
- C++17 standartlarına göre aşağıdaki kodda\
a) Sentaks hatası var.\
b) Sentaks hatası yok.
```cpp
class A {
   private:
    struct N {};

   public:
    static N foo();
};

int main() {
    auto x = A::foo();
}
```

### [Günün Sorusu 025](https://t.me/trcpp/9643)
- C++17 standartlarına göre aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpp
#include <iostream>

int x;

int main() {
    int x{x};
    std::cout << x;
}

```

### [Günün Sorusu 026](https://t.me/trcpp/9705)
- C++17 standartlarına göre aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpp
#include <iostream>

class base {
   public:
    virtual void override() {
        std::cout << 1;
    }
};

class final final : public base {
   public:
    virtual void override() final override {
        std::cout << 2;
    }
};

void f(base* p) {
    p->base::override();
}

int main() {
    final final;
    f(&final);
}
```

### [Günün Sorusu 027](https://t.me/trcpp/9762)
[Cevap](https://t.me/trcpp/9765)
- C++17 standartlarına göre aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:
```cpp
#include <iostream>

class Base {
   public:
    virtual void f(int a = 1) {
        std::cout << "B" << a;
    }
};

class Der : public Base {
   private:
    void f(int a = 2) override {
        std::cout << "D" << a;
    }
};

void g(Base* baseptr) {
    baseptr->f();
}

int main() {
    auto p{new Der};
    g(p);
    delete p;
}

```

### [Günün Sorusu 028](https://t.me/trcpp/9925)
- C++17 standartlarına göre aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:

```cpp
#include <iostream>

template <typename T>
size_t f1(T x[]) { return sizeof x; }

template <typename T>
size_t f2(T &x) { return sizeof(x); }

template <typename T>
size_t f3(T *x) { return sizeof(*x); }

template <typename T>
size_t f4(T x) { return sizeof(x); }

template <typename T, size_t n>
size_t f5(T (&x)[n]) { return sizeof x; }

int main() {
    int a[20]{};

    std::cout << (sizeof(a) == f1(a));
    std::cout << (sizeof(a) == f2(a));
    std::cout << (sizeof(a) == f3(a));
    std::cout << (sizeof(a) == f4(a));
    std::cout << (sizeof(a) == f5(a));
}
```

### [Günün Sorusu 029](https://t.me/trcpp/9958)
- C++17 standartlarına göre aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:

```cpp
#include <array>
#include <iostream>

struct Nec {
    Nec() { std::cout << 1; }
    ~Nec() { std::cout << 2; }
    Nec(const Nec &) { std::cout << 3; }
    void f() {
        std::cout << "4";
    }
};

int main() {
    std::array<Nec, 2> ar;

    for (auto n : ar)
        n.f();
}
```


### [Günün Sorusu 030](https://t.me/trcpp/9977)
- C++17 standartlarına göre aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:

```cpp
#include <iostream>

struct Base {
    virtual int foo() = 0;
};

struct Der : Base {
    int foo() override { return 2; }
};

int Base::foo() { return 1; }

int main() {
    Der der;
    std::cout << der.foo();
    std::cout << ((Base&)der).foo();
    std::cout << ((Base*)&der)->foo();
    std::cout << der.Base::foo();
}
```

### [Günün Sorusu 031](https://t.me/trcpp/10011)
[Cevap](https://t.me/trcpp/10022)
- C++17 standartlarına göre aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector vx(0, 0);
    std::vector vy{0, 0};

    std::cout << (vy > vx);
}
```

### [Günün Sorusu 032](https://t.me/trcpp/10067)
- C++17 standartlarına göre aşağıdaki kodda\
a) Sentaks hatası var.\
b) Tanımsız davranış (undefined behavior) var.\
c) Belirlenmemiş davranış (unspecified behavior) var.\
d) Derlenip çalıştırıldığında ekran çıktısı şu olur:

```cpp
#include <iostream>

int main() {
    int x = 0, y = 1, z = 2;

    std::cout << (++x || --y && --z);
    std::cout << x << y << z;
}
```