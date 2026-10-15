# CPPlabs
#include <iostream>

struct StepeniGrustnosti {
    int sadness; 
    int vospriimchivosti; //skoliko nado sek chotbi grustnosti ubrati
      
};
//naushniki gde nahodissya po vremeni, nado chtobi stavilasi pauza posle ischerpania grustonosti
struct DlitelnostiMusic {
    int second;     
    
};

struct Naushniki {        
    DlitelnostiMusic playhead; 
};

DlitelnostiMusic computeTimeToRemoveSad(StepeniGrustnosti stepeni){
    int second=stepeni.sadness*stepeni.vospriimchivosti;
    return { second };
}

struct GrustnyyCel
{
StepeniGrustnosti sad;
};

void slushati(Naushniki* naushniki,GrustnyyCel* cel)
{
    auto t = computeTimeToRemoveSad(cel->sad);
    naushniki.playhead = { naushniki.playhead->second + t.second };
    cel->sad.sadness = 0;
}


int main() {
    
    GrustnyyCel chel{{100,2}};
    Naushniki naushniki{{0,0}};
    slushati(&naushniki,&chel);
    std::cout<<"grustnosti: "<<chel.sad.sadness<<std::endl;
    std::cout<<"music stop cherez: "<<naushniki.playhead.min<<naushniki.playhead.second<<std::endl;

}
# 1. Стоимость заказа

Подсчёт итоговой стоимости заказа клиента на основе цен на напитки, первое и второе блюдо.

**Код (C++):**

```cpp
#include <iostream>

struct Prices {
    int drink;
    int first;
    int second;
};

struct Choices {
    int drink;
    int first;
    int second;
};

int customerTotal(Prices prices, Choices choices) {
    return choices.drink * prices.drink
         + choices.first * prices.first
         + choices.second * prices.second;
}

int main() {
    Prices prices{10, 20, 30};

    {
        Choices c1{100, 0, 250};
        std::cout << "Клиент 1: "
                  << customerTotal(prices, c1) << std::endl;
    }

    {
        Choices c2{0, 300, 0};
        std::cout << "Клиент 2: "
                  << customerTotal(prices, c2) << std::endl;
    }
}
```

**Вывод:**

```text
Клиент 1: 8500
Клиент 2: 6000
```

---

# 2. Делёж конфет

`N` конфет делятся между `M` детьми поровну, остаток отдаётся самому младшему.

**Код (C++):**

```cpp
#include <iostream>

struct Distribution {
    int perChild;       // Сколько конфет каждому ребёнку
    int youngestTotal;  // Сколько конфет младшему с остатком
};

Distribution distribute(int totalCandies, int childrenCount) {
    int perChild = totalCandies / childrenCount;
    int remainder = totalCandies % childrenCount;
    int youngestTotal = perChild + remainder;

    return Distribution{perChild, youngestTotal};
}

int main() {
    int totalCandies = 17;
    int childrenCount = 5;

    Distribution result = distribute(totalCandies, childrenCount);

    std::cout << "Каждому ребёнку: "
              << result.perChild << std::endl;

    std::cout << "Младшему: "
              << result.youngestTotal << std::endl;
}
```

**Вывод:**

```text
Каждому ребёнку: 3
Младшему: 5
```

---

# 3. Калорийность блюда

Расчёт калорийности по количеству белков, жиров и углеводов.

Коэффициенты:
- Белки — **4 ккал/г**.
- Жиры — **9 ккал/г**.
- Углеводы — **4 ккал/г**.

**Код (C++):**

```cpp
#include <iostream>

struct Dish {
    int protein;  // Граммы белков
    int fat;      // Граммы жиров
    int carbs;    // Граммы углеводов
};

struct CaloriesPerGram {
    int protein;  // Ккал на грамм белков
    int fat;      // Ккал на грамм жиров
    int carbs;    // Ккал на грамм углеводов
};

int calculateCalories(Dish dish, CaloriesPerGram coefficients) {
    return dish.protein * coefficients.protein
         + dish.fat * coefficients.fat
         + dish.carbs * coefficients.carbs;
}

int main() {
    Dish dish{10, 5, 20};
    CaloriesPerGram coefficients{4, 9, 4};

    int totalCalories = calculateCalories(dish, coefficients);

    std::cout << "Калорийность: "
              << totalCalories << " ккал" << std::endl;
}
```

**Вывод:**

```text
Калорийность: 165 ккал
```

---

# 4. Копилка

В копилке `X` рублей и `Y` копеек. В неё добавляют `A` рублей и `B` копеек. Количество копеек не может превышать 99 — лишние копейки переводятся в рубли.

**Код (C++):**

```cpp
#include <iostream>

struct PiggyBank {
    int rubles;
    int kopecks;
};

struct Money {
    int rubles;
    int kopecks;
};

void deposit(PiggyBank* piggyBank, Money amount) {
    int totalRubles = piggyBank->rubles + amount.rubles;
    int totalKopecks = piggyBank->kopecks + amount.kopecks;

    totalRubles += totalKopecks / 100;
    totalKopecks %= 100;

    piggyBank->rubles = totalRubles;
    piggyBank->kopecks = totalKopecks;
}

int main() {
    PiggyBank piggyBank{10, 50};
    Money amount{5, 75};

    deposit(&piggyBank, amount);

    std::cout << "В копилке: "
              << piggyBank.rubles << " руб. "
              << piggyBank.kopecks << " коп."
              << std::endl;
}
```

**Вывод:**

```text
В копилке: 16 руб. 25 коп.
```
