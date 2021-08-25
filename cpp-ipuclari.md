- [C++20 ipuçları 001](#c20-ipuçları-001)
- [C++20 ipuçları 002](#c20-ipuçları-002)
- [C++20 ipuçları 003](#c20-ipuçları-003)
- [C++20 ipuçları 004](#c20-ipuçları-004)
- [C++20 ipuçları 005](#c20-ipuçları-005)
- [C++20 ipuçları 006](#c20-ipuçları-006)
- [C++20 ipuçları 007](#c20-ipuçları-007)
- [C++20 ipuçları 008](#c20-ipuçları-008)
- [C++20 ipuçları 009](#c20-ipuçları-009)


### [C++20 ipuçları 001](https://t.me/trcpp/9585)

C++20 öncesinde aşağıdaki üye fonksiyonların geri dönüş değerleri yoktu. 

list::remove
list::remove_if
forward_list::remove
forward_list::remove_if

Oysa doğal ve kullanışlı olan bu fonksiyonların, kaptan silinen öğe sayısını döndürmeleri. C++20 ile bu yanlıştan dönüldü. Artık bu işlevlerin geri dönüş değerleri container::size_type türünden ve silinen öğe sayısını döndürüyorlar.

```cpp
#include <iostream>
#include <list>

int main() {
    std::list<int> ilist{2, 4, 7, 9, 2, 4, 2, 3, 7, 2, 1, 4};
    auto n = ilist.remove(2);
    std::cout << "n = " << n << "\n";
    n = ilist.remove_if([](int a) { return a % 2 != 0; });
    std::cout << "n = " << n << "\n";
}
```

### [C++20 ipuçları 002](https://t.me/trcpp/9592)

global erase ve erase_if işlevleri

Bir kaptan belirli değere sahip öğeleri silmek için artık global erase fonksiyonlarımız var. Yine bir kaptan belirli koşulları sağlayan öğeleri silmek için global erase_if fonksiyonlarımız var.
Örneğin std::vector, std::deque ve std::string sınıfları için uzun (verbose) remove_erase idiyomunu yazmamız gerekmiyor. Bu fonksiyonların geri dönüş değerleri de yine kapların size_type türünden.

```cpp
#include <deque>
#include <iostream>
#include <string>
#include <vector>

int main() {
    std::vector<int> ivec{1, 2, 3, 1, 4, 1};

    auto erased = erase(ivec, 1);
    std::cout << "erased = " << erased << "\n";

    std::deque<int> id{7, 2, 3, 5, 4, 1};
    erased = erase_if(id, [](int a) { return a > 3; });
    std::cout << "erased = " << erased << "\n";

    std::string s{"Aegroto dum anuma est, spes est"};
    erased = erase(s, ' ');
    std::cout << "erased = " << erased << "\n";
}
```

### [C++20 ipuçları 003](https://t.me/trcpp/9607)
C++20 standartlarından önce "associative" ve "unordered associative" kaplarda arama için sadece count ve find üye işlevleri vardı. C++20 standartları ile  bu kaplara contains işlevleri de eklendi. contains işlevi anahtar (key) değerini alarak bool döndürüyor.

```cpp
#include <iostream>
#include <set>

int main() {
    std::set<int> s{2, 3, 5, 7, 11, 13, 17, 19};
    for (auto i : {1, 2, 3, 4, 5, 6, 7, 8})
        if (s.contains(i))
            std::cout << "var\n";
        else
            std::cout << "yok\n";
}

```


### [C++20 ipuçları 004](https://t.me/trcpp/9645)
C++20 standartlarına göre artık *"stateless"* lambda'lardan oluşturulan kapanış sınıflarının *(closure types)* varsayılan kurucu işlevleri *(default constructors)* delete edilmiyor.

```cpp
#include <set>

int main() {
    auto fx = [](int a, int b) { return a > b; };
    // decltype(fx) fy; // C++17'de gecersiz C++20'de gecerli

    std::set<int, decltype(fx)> s;  // C++17'de gecersiz C++20'de gecerli
    int i{};
    auto g = [i](int x) { return i + x; };
    decltype(g) fy;  // C++17/20'de gecersiz
}

```

### [C++20 ipuçları 005](https://t.me/trcpp/9766)
`<bit>` başlık dosyasında yer alan *endian* isimli *enum class* ile derleme zamanında *"endianness"* sorgulaması yapılabiliyor:

Sistem (platform) *"little endian"* ise *"native"* numaralandırma sabiti ile *little* sabiti eşit olmak zorunda.
Sistem *"big endian"* ise *"native"* numaralandırma sabiti ile *big* sabiti eşit olmak zorunda.
Eğer sistem hem *"little endian"* hem de *"big endian"* düzenini destekliyor ise *"native"* numaralandırma sabiti hem *little* hem de *big* sabitinden farklı olmak zorunda.

```cpp
#include <bit>
#include <iostream>

int main() {
    using namespace std;

    if constexpr (endian::native == endian::little) {
        cout << "little end in";
    } else if constexpr (endian::native == endian::big) {
        cout << "big end in";
    } else {
        cout << "mixed\n";
    }
}
```

### [C++20 ipuçları 006](https://t.me/trcpp/10073)
C++20 standartlarından önce, sınıfların bit alanı (bitfields) elemanları için "varsayılan ilk değer verici" (default member initializer) kullanılamıyordu. C++20 standartları ile bu mümkün kılındı.

```cpp
#include <iostream>

struct Nec {
    unsigned x : 3 {2};  // C++17'de gecersiz C++20'de gecerli
    unsigned y : 3 = 1;  // C++17'de gecersiz C++20'de gecerli
};

int main() {
    Nec mynec;
    std::cout << mynec.x << mynec.y;
}
```

### [C++20 ipuçları 007](https://t.me/trcpp/10295)
Kapsamlı numaralandırma türleri *(scoped enums) C++11* standartları ile dile eklenmişti. Kapsamlı numaralandırma türlerinin kullanımı ile daha güvenli kodlar oluşturabiliyoruz.  Ancak kapsamlı numaralandırma sabitlerinin *(enumaration constants)* özellikle yerel *(local)* kod alanlarında yoğun kullanımı kod kalabalığı *(verbose code)* oluşturabiliyor.  *C++20* standartları ile artık numaralandırma türleri ya da numaralandırma sabitleri için *using* bildirimi yapabiliyoruz. Böylece *using* bildiriminin yapıldığı kapsamda *(scope)* numaralandırma sabitlerini çözünürlük operatörü *(scope resolution operator)* olmadan kullanabiliyoruz.

```cpp
enum class suit { club, diamond, heart, spade };

enum class face { two, three, four, five, six, seven, eight, nine, ten, jack, queen, king, ace };

void f(suit s, face f) {
    using enum suit;              // enum class icin using bildirimi
    using face::ace, face::king;  // enumarator'ler icin using bildirimi

    if (s == suit::heart) s = suit::spade;  // C++20 oncesinde
    if (s == heart) s = spade;              // C++20

    if (f == face::king) f = face::ace;  // C++20 oncesinde
    if (f == king) f = ace;              // C++20
    // if (f == four) f = five; // C++20'de de gecersiz
}
```


### [C++20 ipuçları 008](https://t.me/trcpp/10719)
C99 standartları ile C diline eklenmiş olan *"designated initializer"*  C++20 standartları ile C++ diline de eklendi. Ancak C dilinden farklı olarak,  C++ dilinde ilk değerlerin bildirimdeki sırayla belirtilmesi gerekiyor.

```cpp
#include <iostream>

struct A {
    int x;
    double d{2.4};
    char str[20];
};

int main() {
    A x = {.x = 45, .str = "necati"};    // 45, 2.4, "necati"
    A y = {.d = 1.5, .str = "mustafa"};  // 0, 1.5, "mustafa"
    A z = {.d = 4.4, .x = 5};            // gecersiz. x'e d'den once ilk deger verilmeli
}
```

### [C++20 ipuçları 009](https://t.me/trcpp/11337)
C++17'de yapısal bağlama *(structured binding)* ile tanımlanmış değişkenler *lambda* ifadelerinde doğrudan yakalanamıyordu *(capture)*. Böyle değişkenleri yakalamak için "generalized lambda capture" ("lambda init capture" da deniliyor) kullanmak zorundaydık. C++20'de bu kısıtlama ortadan kalktı.

```cpp
#include <utility>

std::pair<int, int> foo();

int main() {
    auto [x, y] = foo();
    auto f = [x]() { return x + 5; };      // C++17'de gecersiz C++20'de gecerli
    auto g = [x = x]() { return x + 5; };  // C++17'de gecerli
}
```