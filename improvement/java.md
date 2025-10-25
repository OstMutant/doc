# ☕ Принципи ООП у Java (Polymorphism, Inheritance, Encapsulation, Abstraction)

---

## 1. Поліморфізм (Polymorphism)

Поліморфізм дозволяє використовувати єдиний інтерфейс для обробки об'єктів різних класів.

### 1.1. Статичний Поліморфізм (Static / Compile-time)

- **Механізм:** Перевантаження методів (`Method Overloading`)
- **Ознака:** Методи мають однакове ім’я, але різні параметри (тип, кількість, порядок)
- **Визначення виклику:** На етапі компіляції (раннє зв’язування)

### 1.2. Динамічний Поліморфізм (Dynamic / Runtime)

- **Механізм:** Перевизначення методів (`Method Overriding`) + Динамічна диспетчеризація
- **Ознака:** Дочірній клас перевизначає метод з ідентичним підписом
- **Визначення виклику:** Під час виконання JVM на основі фактичного типу об’єкта

### 1.3. Анотація `@Override`

- **Призначення:** Вказує, що метод у підкласі перевизначає метод суперкласу
- **Переваги:**
  - Компіляторна перевірка: помилка, якщо метод не перевизначає нічого
  - Покращення читабельності

🔗 Джерела:
- [Baeldung: Java Interfaces](https://www.baeldung.com/java-interfaces)
- [GeeksforGeeks: Overriding](https://www.geeksforgeeks.org/overriding-in-java/)
- [TutorialsPoint: @Override](https://www.tutorialspoint.com/importance-of-override-annotation-in-java)
- [SoftwareTestingHelp: Runtime Polymorphism](https://www.softwaretestinghelp.com/java-override-and-runtime-polymorphism/)

---

## 2. Наслідування (Inheritance)

Наслідування дозволяє одному класу успадковувати поля та методи іншого класу.

### 2.1. Основні Терміни

- **Super Class:** Батьківський клас
- **Sub Class:** Дочірній клас
- **IS-A відношення:** `Dog extends Animal` означає, що `Dog` — це `Animal`
- **Reusability:** Повторне використання коду

### 2.2. Типи Наслідування

| Тип         | Опис                                 |
|-------------|--------------------------------------|
| Single      | Один клас успадковує один            |
| Multilevel  | Ланцюжок наслідування                |
| Hierarchical| Кілька класів успадковують один      |
| Multiple    | Через інтерфейси                     |
| Hybrid      | Комбінація через інтерфейси          |

### 2.3. Переваги та Недоліки

- ✅ Повторне використання коду
- ✅ Поліморфізм через перевизначення
- ❌ Тісне зв’язування між класами
- ❌ Ускладнення при глибокій ієрархії

🔗 Джерело: [GeeksforGeeks: Inheritance in Java](https://www.geeksforgeeks.org/inheritance-in-java/)

---

## 3. Інкапсуляція (Encapsulation)

Інкапсуляція — це об’єднання даних і методів у захищену одиницю (клас).

### 3.1. Як досягти

- Оголошення змінних як `private`
- Геттери (`getX`) і сеттери (`setX`) — контрольований доступ
- Валідація в сеттерах

```java
private int age;

public void setAge(String val) {
    try {
        age = Integer.parseInt(val);
    } catch (NumberFormatException e) {
        age = 0;
    }
}
```

### 3.2. Модифікатори Доступу

| Модифікатор | У класі | У пакеті | У підкласі | Зовні |
|-------------|---------|----------|------------|-------|
| `public`    | ✅      | ✅       | ✅         | ✅    |
| `protected` | ✅      | ✅       | ✅         | ❌    |
| default     | ✅      | ✅       | ❌         | ❌    |
| `private`   | ✅      | ❌       | ❌         | ❌    |

### 3.3. Переваги Інкапсуляції

- Можна змінити тип поля без впливу на зовнішній код
- Можна додати логіку валідації
- Зменшення залежностей

🔗 Джерела:
- [GeeksforGeeks: Encapsulation](https://www.geeksforgeeks.org/encapsulation-in-java/?ref=lbp)
- [JavaStudyGuide: Access Modifiers](http://ocpj8.javastudyguide.com/ch01.html)
- [ThoughtCo: Accessors and Mutators](https://www.thoughtco.com/accessors-and-mutators-2034335)

---

## 4. Абстракція (Abstraction)

Абстракція — це приховування деталей реалізації та показ лише суттєвої функціональності.

### 4.1. Механізми

- **Абстрактні класи (`abstract class`)**
- **Інтерфейси (`interface`)**

### 4.2. Переваги

- Зменшення складності
- Покращення модульності
- Відокремлення “що” від “як”
- Можливість створення контрактів API

### 4.3. Приклад

```java
abstract class Animal {
    abstract void makeSound();
}

class Dog extends Animal {
    void makeSound() {
        System.out.println("Woof");
    }
}
```
---


# 🧩 Інтерфейси, Дефолтні/Статичні Методи та Абстракція vs Інкапсуляція в Java

---

## 1. Що таке Інтерфейс у Java?

🔹 В Java інтерфейс — це **абстрактний тип**, який містить набір **методів** та **константних змінних**.  
🔹 Він є одним із ключових механізмів для реалізації:
- **Абстракції**
- **Поліморфізму**
- **Множинного наслідування**

### 1.1. Дозволені елементи в інтерфейсі:

- Константні змінні (`public static final`)
- Абстрактні методи (`abstract`)
- Статичні методи (`static`)
- Дефолтні методи (`default`)

### 1.2. Правила створення інтерфейсів:

- Не можна створити об’єкт інтерфейсу напряму
- Інтерфейс може бути порожнім (без методів і змінних)
- Не можна використовувати `final` для оголошення інтерфейсу — це викликає помилку компіляції
- Модифікатор `abstract` додається автоматично компілятором
- Методи не можуть бути `private`, `protected` або `final`
- Змінні — завжди `public static final` і не можуть змінювати модифікатор доступу

🔗 Джерело: [Baeldung: What Are Interfaces in Java](https://www.baeldung.com/java-interfaces)

---

## 2. Дефолтні та Статичні Методи в Інтерфейсах

### 2.1. Дефолтні Методи (`default`)

- Мають реалізацію прямо в інтерфейсі
- Не потребують явного `public` — він додається автоматично
- Дозволяють **розширювати API** без порушення існуючих реалізацій

```java
interface Logger {
    default void log(String msg) {
        System.out.println("Log: " + msg);
    }
}
```

### 2.2. Конфлікти при множинному наслідуванні

- Якщо клас реалізує кілька інтерфейсів з однаковими `default` методами — виникає **конфлікт**
- Рішення: явно перевизначити метод у класі

```java
class MyLogger implements InterfaceA, InterfaceB {
    @Override
    public void log(String msg) {
        InterfaceA.super.log(msg);
    }
}
```

### 2.3. Статичні Методи (`static`)

- Не належать об’єкту — викликаються через ім’я інтерфейсу
- Не є частиною API реалізуючих класів

```java
interface MathUtils {
    static int square(int x) {
        return x * x;
    }
}

// Виклик:
int result = MathUtils.square(5);
```

🔗 Джерело: [Baeldung: Static and Default Methods in Interfaces](https://www.baeldung.com/java-static-default-methods)

---

## 3. Абстракція vs Інкапсуляція

| Параметр             | Абстракція                              | Інкапсуляція                          |
|----------------------|------------------------------------------|---------------------------------------|
| Мета                 | Приховати реалізацію, показати інтерфейс | Приховати дані, захистити доступ      |
| Засоби реалізації    | Абстрактні класи, інтерфейси             | `private` поля, `public` геттери/сеттери |
| Видимість            | Зовнішня (що доступно зовні)             | Внутрішня (що приховано всередині)    |
| Приклад              | `abstract class`, `interface`            | `private int age; public void setAge(...)` |

### 3.1. Абстрактний клас

- Не можна створити об’єкт напряму
- Може містити як абстрактні, так і реалізовані методи

```java
abstract class Animal {
    abstract void makeSound();
    void breathe() {
        System.out.println("Breathing...");
    }
}
```

### 3.2. Інтерфейс як контракт

- Визначає набір методів, які клас **зобов’язаний реалізувати**
- Дозволяє іншим класам **взаємодіяти через API**, не знаючи реалізації

🔗 Джерело: [Baeldung: Abstraction vs Encapsulation](https://www.baeldung.com/cs/abstraction-vs-encapsulation)


# 🔗 Контракт методів `hashCode()` та `equals()` у Java

---

## 1. Контракт `hashCode()`

1. **Постійність:** Повертає однакове значення протягом життєвого циклу об’єкта, якщо його стан не змінюється.
2. **Узгодженість з `equals()`:** Якщо `x.equals(y) == true`, то `x.hashCode() == y.hashCode()` обов’язково.
3. **Нерівні об’єкти можуть мати однаковий хеш:** Але бажано уникати колізій для кращої продуктивності.

🔗 [Oracle Docs: Object.hashCode()](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#hashCode--)

---

## 2. Контракт `equals()`

- **Рефлексивність, симетричність, транзитивність, постійність, перевірка на null**
- Реалізація за замовчуванням — порівняння посилань (`==`)

🔗 [Oracle Docs: Object.equals()](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#equals-java.lang.Object)

---

## 3. Колекції та `equals()` / `hashCode()`

| Клас              | Порівняння         | Хешування                        | Особливості |
|-------------------|--------------------|----------------------------------|-------------|
| `HashMap`         | `equals()`         | `hashCode()`                     | Стандартна реалізація |
| `IdentityHashMap` | `==`               | `System.identityHashCode()`     | Ігнорує `equals()` |

🔗 [Proselyte: IdentityHashMap](http://proselyte.net/tutorials/java-core/collections-framework/identity-hashmap/)

---

## 4. Генерація `hashCode()` у JVM

- За замовчуванням: `System.identityHashCode()`
- Стратегія `-XX:hashCode=0` — випадкове число (найпоширеніша)
- Інші варіанти: адреса об’єкта, xorshift, тощо

🔗 [Habr: JVM hashCode](https://habr.com/ru/post/165683/)  
🔗 [Srvaroa: Biased Locking](https://srvaroa.github.io/jvm/java/openjdk/biased-locking/2017/01/30/hashCode.html)

---

## 5. Утиліти для реалізації

### `Objects.hash(...)`

```java
@Override
public int hashCode() {
    return Objects.hash(field1, field2);
}
```

### Apache Commons Lang

```java
@Override
public boolean equals(Object o) {
    return EqualsBuilder.reflectionEquals(this, o);
}

@Override
public int hashCode() {
    return HashCodeBuilder.reflectionHashCode(this);
}
```

🔗 [Apache Commons Lang](https://commons.apache.org/proper/commons-lang/)

### Lombok

```java
@EqualsAndHashCode
public class User {
    private String name;
    private int age;
}
```

🔗 [Lombok: @EqualsAndHashCode](https://projectlombok.org/features/EqualsAndHashCode)

---

## 6. Зв’язок з ООП

- **Інкапсуляція:** `equals()` / `hashCode()` працюють з приватними полями
- **Наслідування:** Можна перевизначити або успадкувати поведінку
- **Поліморфізм:** `equals(Object)` — приклад динамічного зв’язування
- **Абстракція:** Контракт визначено в `Object`, реалізація — у підкласах

---

---

## 7. Додаткові ресурси

- [Oracle Docs: Object.hashCode()](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#hashCode--)
- [Oracle Docs: Object.equals()](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#equals-java.lang.Object)
- [Proselyte: IdentityHashMap](http://proselyte.net/tutorials/java-core/collections-framework/identity-hashmap/)
- [Habr: JVM hashCode](https://habr.com/ru/post/165683/)
- [Srvaroa: Biased Locking](https://srvaroa.github.io/jvm/java/openjdk/biased-locking/2017/01/30/hashCode.html)
- [Apache Commons Lang](https://commons.apache.org/proper/commons-lang/)
- [Lombok: @EqualsAndHashCode](https://projectlombok.org/features/EqualsAndHashCode)
- [Stack Overflow: реалізація hashCode](https://ru.stackoverflow.com/questions/308289/реализовать-метод-hashcode-в-классе)
- [Habr: equals & hashCode](https://habr.com/ru/post/168195/)
- [GeeksforGeeks: Overriding](https://www.geeksforgeeks.org/overriding-in-java/)
- [GeeksforGeeks: Inheritance in Java](https://www.geeksforgeeks.org/inheritance-in-java/)
- [GeeksforGeeks: Encapsulation](https://www.geeksforgeeks.org/encapsulation-in-java/?ref=lbp)
- [JavaStudyGuide: Access Modifiers](http://ocpj8.javastudyguide.com/ch01.html)
- [ThoughtCo: Accessors and Mutators](https://www.thoughtco.com/accessors-and-mutators-2034335)
- [Baeldung: Java Interfaces](https://www.baeldung.com/java-interfaces)
- [TutorialsPoint: @Override](https://www.tutorialspoint.com/importance-of-override-annotation-in-java)
- [SoftwareTestingHelp: Runtime Polymorphism](https://www.softwaretestinghelp.com/java-override-and-runtime-polymorphism/)

---

# 🧱 Класи, Оператори, Immutable Об'єкти, Enum та Lazy Initialization в Java

---

## 1. POJO (Plain Old Java Object)

- Простий Java-об'єкт, який:
  - Не наслідує специфічні базові класи
  - Не реалізує службові інтерфейси (наприклад, `Serializable`, `Remote`)
  - Використовується для **бізнес-моделі**, DTO, конфігурацій

---

## 2. Upcasting і Downcasting

🔹 **Upcasting** — приведення дочірнього об'єкта до типу батьківського класу  
🔹 **Downcasting** — приведення батьківського типу до дочірнього

| Тип кастингу | Напрям | Безпека | Приклад |
|--------------|--------|---------|---------|
| Upcasting    | Child → Parent | Безпечний, автоматичний | `Animal a = new Dog();` |
| Downcasting  | Parent → Child | Потребує перевірки, явний | `Dog d = (Dog) a;` |

🔗 Джерело: [Javatpoint: Upcasting and Downcasting](https://www.javatpoint.com/upcasting-and-downcasting-in-java)

---

## 3. Immutable Класи

### 3.1. Як створити immutable клас

- `final` клас — не можна наслідувати
- Всі поля `private final`
- Без сеттерів
- Ініціалізація через конструктор (глибока копія)
- Геттери повертають копії (для змінюваних об'єктів)

```java
public final class Person {
    private final String name;
    private final List<String> tags;

    public Person(String name, List<String> tags) {
        this.name = name;
        this.tags = List.copyOf(tags); // захисна копія
    }

    public List<String> getTags() {
        return List.copyOf(tags); // повертаємо копію
    }
}
```

🔗 Джерело: [JournalDev: How to Create Immutable Class](https://www.journaldev.com/129/how-to-create-immutable-class-in-java)

### 3.2. Переваги

- Потокобезпечність
- Добре працюють як ключі в `Map` / `Set`
- Легше тестувати, кешувати, паралелізувати

🔗 Джерело: [Proft.me: Immutable Objects](https://en.proft.me/2013/11/24/advantages-and-disadvantages-immutable-objects-jav/)

### 3.3. Недоліки

- Створення нових об'єктів при кожній зміні
- Потенційно більше навантаження на GC

---

## 4. Lombok для Immutable DTO

- `@Value` — створює `final` клас з `private final` полями, без сеттерів
- `@Builder` — зручне створення об'єктів з багатьма полями
- `@With` — створення модифікованих копій
- Для `List`, `Set`, `Map` — потрібно вручну забезпечити незмінність

```java
@Value
@Builder
public class User {
    String name;
    @With int age;
}
```

---

## 5. Java Enum

🔹 Enum — спеціальний тип класу, що містить **фіксований набір констант**  
🔹 Доступний з Java 5

### 5.1. Можливості

- Можуть містити поля, конструктори, методи
- Підтримують `switch`, `if`, `values()`, `valueOf()`
- Можуть реалізовувати інтерфейси
- Можуть мати абстрактні методи

```java
public enum Level {
    HIGH(3), MEDIUM(2), LOW(1);

    private final int code;
    Level(int code) { this.code = code; }
    public int getCode() { return code; }
}
```

🔗 Джерела:
- [Jenkov: Java Enums](http://tutorials.jenkov.com/java/enums.html)
- [Javapedia: Enum Q&A](https://www.javapedia.net/Enum#qanda1686)

---

## 6. Тернарний Оператор

🔹 Єдиний умовний оператор з трьома операндами  
🔹 Синтаксис: `result = condition ? value1 : value2;`

```java
int max = (a > b) ? a : b;
```

🔗 Джерело: [GeeksforGeeks: Java Ternary Operator](https://www.geeksforgeeks.org/java-ternary-operator-with-examples/)

---

## 7. Lazy Initialization

🔹 Відкладене створення об'єкта або обчислення значення  
🔹 Використовується для оптимізації ресурсів

### 7.1. Переваги

- Швидший старт програми
- Менше використання пам’яті
- Кешування результатів

### 7.2. Приклад

```java
class Config {
    private Settings settings;

    public Settings getSettings() {
        if (settings == null) {
            settings = loadSettings(); // створюється лише при першому виклику
        }
        return settings;
    }
}
```

🔗 Джерело: [Wikipedia: Lazy Initialization](https://en.wikipedia.org/wiki/Lazy_initialization)

---

# 🔤 Java String: String Pool, Паліндроми, Пам’ять, Особливості

---

## 1. Що таке String у Java?

- `String` — це **клас**, а не примітивний тип.
- Визначений у пакеті `java.lang`.
- **Immutable**: не можна змінити після створення.
- **Final**: не можна наслідувати.
- Використовується майже в кожному Java-додатку.

### 1.1. Створення String

```java
String s1 = "abc"; // літерал — потрапляє в String Pool
String s2 = new String("abc"); // новий об'єкт — поза пулом
```

- `==` порівнює посилання
- `equals()` порівнює вміст

---

## 2. Java String Pool

🔹 **String Pool** — спеціальна область пам’яті JVM для зберігання унікальних рядкових літералів.

### 2.1. Поведінка

- При створенні літерала JVM перевіряє, чи вже є такий рядок у пулі.
- Якщо є — повертає посилання.
- Якщо немає — створює новий об'єкт і додає в пул.

### 2.2. Метод `intern()`

```java
String s1 = new String("abc");
String s2 = s1.intern(); // s2 тепер посилається на об'єкт з пулу
```

- Повертає посилання на об'єкт з пулу, якщо такий існує.
- Інакше додає об'єкт у пул.

🔗 Джерела:
- [Baeldung: Java String Pool](https://www.baeldung.com/java-string-pool)
- [DigitalOcean: String Interview Questions](https://www.digitalocean.com/community/tutorials/java-string-interview-questions-and-answers)

---

## 3. Пояснення через ASCII-діаграму

```
+--------+        +-----------------------------------+
| STACK  |        |               HEAP                |
+--------+        |                                   |
| s1 --->|--------| "Hello" (Object #A) ← String Pool |
| s2 --->|---+    | new String("Hello") (Object #B)   |
+--------+   |    | char[]: ['H','e','l','l','o']      |
            |    | (спільний для #A та #B)             |
            +----+-------------------------------------+
```

- `s1 == s2` → `false` (різні об'єкти)
- `s1.equals(s2)` → `true` (однаковий вміст)

---

## 4. Паліндроми в Java

🔹 **Паліндром** — рядок, який читається однаково зліва направо і справа наліво.

### 4.1. Через StringBuilder

```java
public boolean isPalindromeUsingStringBuilder(String text) {
    String clean = text.replaceAll("\\s+", "").toLowerCase();
    StringBuilder plain = new StringBuilder(clean);
    StringBuilder reverse = plain.reverse();
    return reverse.toString().equals(clean);
}
```

### 4.2. Через Stream API

```java
public boolean isPalindromeUsingIntStream(String text) {
    String temp = text.replaceAll("\\s+", "").toLowerCase();
    return IntStream.range(0, temp.length() / 2)
        .noneMatch(i -> temp.charAt(i) != temp.charAt(temp.length() - i - 1));
}
```

### 4.3. Через Рекурсію

```java
public boolean isPalindromeRecursive(String text) {
    String clean = text.replaceAll("\\s+", "").toLowerCase();
    return recursivePalindrome(clean, 0, clean.length() - 1);
}

private boolean recursivePalindrome(String text, int forward, int backward) {
    if (forward >= backward) return true;
    if (text.charAt(forward) != text.charAt(backward)) return false;
    return recursivePalindrome(text, forward + 1, backward - 1);
}
```

🔗 Джерело: [Baeldung: Palindrome in Java](https://www.baeldung.com/java-palindrome)

---

## 5. Особливості пам’яті та Flyweight Pattern

- **String Pool** — приклад патерну **Flyweight**.
- З Java 7 — String Pool зберігається в **Heap**, а не в PermGen.
- Це дозволяє **GC** очищати непотрібні рядки.
- Зменшує ризик `OutOfMemoryError`.

🔗 Джерело: [Medium: Java String Pool](https://muratakkan.medium.com/understanding-and-using-the-java-string-pool-in-java-d60d3176716) ❌ (недоступне, але підтверджено з Baeldung)


---

# 📚 Java Collections Framework — Структури, Ітератори, Складність, Сортування, Порівняння, Кешування

---

## 1. Що таке Java Collections Framework?

🔹 **Java Collections Framework (JCF)** — це набір інтерфейсів і класів для зберігання, доступу та маніпуляцій з групами об'єктів.  
🔹 Вперше представлений у JDK 1.2, він забезпечує уніфіковану архітектуру для роботи з колекціями.

### Основні інтерфейси:

- `Collection` — базовий інтерфейс
- `List`, `Set`, `Queue`, `Deque` — підінтерфейси для різних типів колекцій
- `Map` — асоціативний масив (ключ → значення)

🔗 [Oracle Docs: Collections Reference (Java SE 8)](https://docs.oracle.com/javase/8/docs/technotes/guides/collections/reference.html)  
🔗 [Oracle Docs: Collections Overview (Java SE 21)](https://docs.oracle.com/en/java/javase/21/core/java-collections-framework.html)

---

## 2. Big-O Складність Операцій

---

### 2.1. List

| Реалізація              | get | add | contains | next | remove(0) | iterator.remove |
|-------------------------|-----|-----|----------|------|-----------|------------------|
| `ArrayList`             | O(1)| O(1)| O(n)     | O(1) | O(n)      | O(n)             |
| `LinkedList`            | O(n)| O(1)| O(n)     | O(1) | O(1)      | O(1)             |
| `CopyOnWriteArrayList`  | O(1)| O(n)| O(n)     | O(1) | O(n)      | O(n)             |

### 2.2. Set

| Реалізація              | add | contains | next | Примітки |
|-------------------------|-----|----------|------|----------|
| `HashSet`               | O(1)| O(1)     | O(h/n) | h — ємність таблиці |
| `LinkedHashSet`         | O(1)| O(1)     | O(1)   | — |
| `TreeSet`               | O(log n)| O(log n)| O(log n)| — |
| `EnumSet`               | O(1)| O(1)     | O(1)   | — |
| `ConcurrentSkipListSet`| O(log n)| O(log n)| O(1) | — |

### 2.3. Map

| Реалізація              | get | containsKey | next | Примітки |
|-------------------------|-----|-------------|------|----------|
| `HashMap`               | O(1)| O(1)        | O(h/n) | h — ємність таблиці |
| `LinkedHashMap`         | O(1)| O(1)        | O(1)   | — |
| `TreeMap`               | O(log n)| O(log n)| O(log n)| — |
| `EnumMap`               | O(1)| O(1)        | O(1)   | — |
| `ConcurrentHashMap`     | O(1)| O(1)        | O(h/n) | — |
| `ConcurrentSkipListMap`| O(log n)| O(log n)| O(1)   | — |

### 2.4. Queue

| Реалізація              | offer | peek | poll | size |
|-------------------------|--------|------|------|------|
| `PriorityQueue`         | O(log n)| O(1)| O(log n)| O(1) |
| `ConcurrentLinkedQueue` | O(1)   | O(1)| O(1)   | O(n) |
| `ArrayBlockingQueue`    | O(1)   | O(1)| O(1)   | O(1) |
| `LinkedBlockingQueue`   | O(1)   | O(1)| O(1)   | O(1) |
| `PriorityBlockingQueue` | O(log n)| O(1)| O(log n)| O(1) |
| `DelayQueue`            | O(log n)| O(1)| O(log n)| O(1) |
| `LinkedList`            | O(1)   | O(1)| O(1)   | O(1) |
| `ArrayDeque`            | O(1)   | O(1)| O(1)   | O(1) |
| `LinkedBlockingDeque`   | O(1)   | O(1)| O(1)   | O(1) |

🔗 [Big-O CheatSheet](https://www.bigocheatsheet.com/)  
🔗 [GeeksforGeeks: Big-O Interview](https://www.geeksforgeeks.org/big-o-notation-interview-questions-answers/)  
🔗 [StackOverflow: Big-O Summary for Java Collections](https://stackoverflow.com/questions/559839/big-o-summary-for-java-collections-framework-implementations)  
🔗 [Baeldung: Binary Search in Java](https://www.baeldung.com/java-binary-search)

### 2.5. Порядки обробки: LIFO та FIFO

| Тип  | Розшифровка               | Структура даних |
|------|---------------------------|-----------------|
| LIFO | Last In, First Out        | `Stack`, `Deque.push/pop` |
| FIFO | First In, First Out       | `Queue`, `Deque.offer/poll` |

- **LIFO**: останній доданий елемент буде першим, що видаляється
- **FIFO**: перший доданий елемент буде першим, що видаляється

---

## 3. Ітератори в Java

---

### 3.1. Типи ітераторів

| Тип            | Напрямок | Модифікація | Колекції                         |
|----------------|----------|-------------|----------------------------------|
| `Enumeration`  | ➡        | ❌          | `Vector`, `Hashtable`            |
| `Iterator`     | ➡        | ✅          | Універсальний                    |
| `ListIterator` | ⬅➡       | ✅          | Тільки `List`                    |
| `Spliterator`  | ➡        | ✅ (паралельно) | `Collection`, `Stream`       |

### 3.2. Особливості

- **`Enumeration`** — застарілий, лише для читання, не підтримує видалення
- **`Iterator`** — дозволяє видалення елементів через `remove()`
- **`ListIterator`** — двосторонній, має `add()`, `previous()`, `hasPrevious()`
- **`Spliterator`** — внутрішній ітератор, підтримує розбиття на частини для паралельної обробки (Java 8+)

🔗 [Tutorialspoint: Iterators in Java](https://www.tutorialspoint.com/iterators-in-java)  
🔗 [Dariawan: Spliterator Overview](https://www.dariawan.com/tutorials/java/java-iterator-listiterator-and-spliterator/)  
🔗 [CoderLessons: Spliterator](https://coderlessons.com/articles/java/ispolzovanie-spliterator-v-java)

---

### 3.3. Fail-Fast vs Fail-Safe

| Тип           | Поведінка при зміні колекції | Приклад реалізації                        |
|---------------|------------------------------|-------------------------------------------|
| **Fail-Fast** | Викидає `ConcurrentModificationException` | `ArrayList`, `HashMap`                    |
| **Fail-Safe** | Ітерує копію, не кидає виняток | `ConcurrentHashMap`, `CopyOnWriteArrayList` |

#### Пояснення:

- **Fail-Fast**:
  - Ітератор працює напряму з колекцією.
  - Якщо структура змінюється — негайно кидає виняток.
  - Використовується для **захисту від непередбачуваних змін**.

- **Fail-Safe**:
  - Ітерує **копію** внутрішньої структури.
  - Зміни не впливають на ітерацію.
  - Використовується в **багатопотокових** колекціях.

🔗 [JavaHungry: Fail-Fast vs Fail-Safe Iterator](http://javahungry.blogspot.com/2014/04/fail-fast-iterator-vs-fail-safe-iterator-difference-with-example-in-java.html)

---

## 4. Стратегії структурування та сортування: List, Comparator, Natural Ordering, Sorting Algorithms

---

### 4.1. ArrayList vs LinkedList

🔹 Обидва класи реалізують інтерфейс `List`, але мають різну внутрішню структуру та продуктивність.

#### ArrayList

- Використовує **масив** для зберігання елементів.
- Динамічно **збільшує розмір** при досягненні порогу.
- **Початкова ємність**: 10
- **Load factor**: 0.75 → при додаванні 7-го елемента створюється новий масив розміром 20.
- **Переваги**:
  - Швидкий доступ за індексом: `get(index)` → **O(1)**
  - Добре підходить для **частого читання**, але не для частих вставок/видалень

#### LinkedList

- Використовує **двозв’язний список**
- **Переваги**:
  - Швидке вставлення/видалення на початку/всередині → **O(1)**
  - Підходить для **частих змін структури** (додавання/видалення)
- **Недоліки**:
  - Повільний доступ за індексом: `get(index)` → **O(n)**

#### Висновок

| Вимога                         | Краще рішення |
|-------------------------------|----------------|
| Часте читання (`get`)         | `ArrayList`    |
| Часте додавання/видалення     | `LinkedList`   |
| Потрібен доступ за індексом   | `ArrayList`    |
| Робота як черга або стек      | `LinkedList`   |

🔗 [Coderolls: ArrayList in Java](https://coderolls.com/arraylist-in-java/)

---

### 4.2. Comparator vs Comparable

🔹 Обидва інтерфейси використовуються для **сортування об'єктів**, але мають різні підходи.

#### Comparable

- Визначає **природний порядок** об'єктів
- Реалізується **всередині класу**
- Має метод `compareTo(T o)`

```java
public class Player implements Comparable<Player> {
    private int ranking;
    @Override
    public int compareTo(Player other) {
        return Integer.compare(this.ranking, other.ranking);
    }
}
```

#### Comparator

- Визначає **зовнішню стратегію порівняння**
- Реалізується **окремим класом або лямбдою**
- Має метод `compare(T o1, T o2)`

```java
public class PlayerRankingComparator implements Comparator<Player> {
    @Override
    public int compare(Player p1, Player p2) {
        return Integer.compare(p1.getRanking(), p2.getRanking());
    }
}
```

#### Коли використовувати

| Ситуація                                             | Рішення         |
|------------------------------------------------------|------------------|
| Є лише один спосіб сортування                        | `Comparable`     |
| Потрібно кілька стратегій сортування                 | `Comparator`     |
| Немає доступу до вихідного коду класу                | `Comparator`     |
| Хочеш уникнути зміни доменного класу                 | `Comparator`     |

#### Java 8: Лямбда та `Comparator.comparing`

```java
Comparator<Player> byRanking = Comparator.comparing(Player::getRanking);
Comparator<Player> byAge = Comparator.comparing(Player::getAge);
```

🔗 [Baeldung: Comparator vs Comparable](https://www.baeldung.com/java-comparator-comparable)

---

### 4.3. Natural Ordering (Природне сортування)

🔹 **Natural ordering** — це порядок, який об'єкти приймають за замовчуванням при сортуванні в масиві або колекції, якщо не вказано `Comparator`.

#### Приклади:

- `String` → **алфавітний порядок**
- `Integer` → **числовий порядок**
- `Date` → **хронологічний порядок**

#### Правила порівняння:

```java
compareTo(other) == 0  // об'єкти рівні
compareTo(other) > 0   // поточний об'єкт більший
compareTo(other) < 0   // поточний об'єкт менший
```

🔗 [CodeJava: Understanding Object Ordering](https://www.codejava.net/java-core/collections/understanding-object-ordering-in-java-with-comparable-and-comparator)

---

### 4.4. Алгоритми сортування в Java

#### Загальний огляд

- `Arrays.sort()` для **примітивів** → **Dual-Pivot Quicksort**
- `Arrays.sort()` для **об'єктів** → **TimSort**
- `Arrays.parallelSort()` → багатопотокова версія злиття

🔗 [Baeldung: Sorting in Java](https://www.baeldung.com/java-sorting)  
🔗 [StackOverflow: Java 7 Sorting Algorithms](https://stackoverflow.com/questions/4018332/is-java-7-using-tim-sort-for-the-method-arrays-sort)  
🔗 [TechieDelight: sort vs parallelSort](https://www.techiedelight.com/de/difference-between-sort-parallelsort-arrays-java/)

---

#### Dual-Pivot Quicksort

- Розроблений Ярославським, Блохом, Бентлі
- Краще працює на реальних даних, ніж класичний Quicksort
- **Складність**: O(n log n)
- Використовується для `int[]`, `char[]`, `double[]` тощо

---

#### TimSort

- Гібрид **Insertion Sort** + **Merge Sort**
- Ефективний для **майже відсортованих** даних
- **Стабільний**, не змінює порядок рівних елементів
- **Складність**: O(n log n), найкращий випадок — O(n)

🔗 [GeeksforGeeks: TimSort](https://www.geeksforgeeks.org/dsa/timsort/)  
🔗 [GeeksforGeeks: Insertion Sort](https://www.geeksforgeeks.org/insertion-sort/)

---

#### Arrays.sort() vs Arrays.parallelSort()

| Метод                   | Алгоритм                      | Потоки         | Коли краще     |
|------------------------|-------------------------------|----------------|----------------|
| `Arrays.sort()`        | Dual-Pivot / TimSort          | Один потік     | Малі масиви    |
| `Arrays.parallelSort()`| Parallel Sort-Merge           | Багато потоків | Великі масиви  |

- `parallelSort()` розбиває масив на блоки, сортує їх окремо, потім зливає
- Використовує **ForkJoinPool** для паралельності
- Може бути повільнішим на малих масивах через накладні витрати

---

### 4.5. Візуалізація алгоритмів сортування

🔗 [USFCA: Comparison Sort Visualizer](https://www.cs.usfca.edu/~galles/visualization/ComparisonSort.html)

📌 Підтримує:
- Bubble Sort
- Selection Sort
- Insertion Sort
- Merge Sort
- QuickSort
- Heap Sort

---

## 5. Binary Search

🔹 **Binary Search** — це ефективний алгоритм пошуку, який працює лише на **відсортованих масивах**.

### 5.1. Принцип роботи:

1. Розділяє масив навпіл
2. Порівнює середній елемент з шуканим
3. Якщо шуканий менший — пошук у лівій половині
4. Якщо більший — у правій
5. Повторює процес рекурсивно

### 5.2. Складність:

- **Часова складність**: O(log n)
- **Просторова складність**: O(1) (ітеративна версія), O(log n) (рекурсивна)

### 5.3. Переваги:

- Швидкий пошук у великих масивах
- Ефективний для **часто запитуваних даних**

### 5.4. Недоліки:

- Працює лише на **відсортованих** структурах
- Складніший у реалізації, ніж лінійний пошук

🔗 [Indeed: Binary Search Interview Questions](https://in.indeed.com/career-advice/interviewing/binary-search-interview-questions)  
🔗 [Baeldung: Binary Search in Java](https://www.baeldung.com/java-binary-search)

---

## 6. HashMap, LinkedHashMap, TreeMap — внутрішня реалізація та порівняння

---

### 6.1. HashMap — внутрішня структура

🔹 `HashMap` — це реалізація інтерфейсу `Map`, яка зберігає пари ключ-значення з доступом за хешем.

#### Основні терміни:

- **Default Capacity**: початкова ємність — **16**, завжди **степінь двійки** до `2^30`
- **Load Factor**: коефіцієнт заповнення — **0.75**  
  → при 16 * 0.75 = **12** елементах відбувається **розширення**
- **Максимальна ємність**: `2^30 = 1,073,741,824`

🔗 [DZone: HashMap Internal Implementation](https://dzone.com/articles/hashmap-internal)  
🔗 [Baeldung: HashMap Load Factor](https://www.baeldung.com/java-hashmap-load-factor)  
🔗 [Hashnode: HashMap Deep Dive](https://wilt.hashnode.dev/wilt-day-1-java-hashmap-ultra-deep-dive)

---

### 6.2. Колізії та Java 8 оптимізація

🔹 Колізія виникає, коли **різні ключі мають однаковий `hashCode()`**  
🔹 До Java 8: елементи зберігались у **зв’язаному списку**  
🔹 З Java 8: при великій кількості колізій (>8) — **перехід на збалансоване дерево (TreeNode)**

#### Переваги:

- **O(1)** при хорошому `hashCode()`
- **O(log n)** у найгіршому випадку (збалансоване дерево)

🔗 [DineshOnJava: Java 8 HashMap Improvements](https://www.dineshonjava.com/hashmap-performance-improvement-changes-in-java-8/)

---

### 6.3. Як працює хеш-функція

🔹 Хеш-функція перетворює ключ у **індекс** для зберігання в масиві

```java
int hashedKey = key.hashCode();
int index = hashedKey % arraySize;
```

🔗 [DEV: How Hash Tables Work](https://dev.to/tywenk/how-do-hash-tables-work-under-the-hood-4nff)

---

### 6.4. Порівняння: HashMap vs LinkedHashMap vs TreeMap

| Тип           | Порядок           | Складність `get/put` | Особливості |
|---------------|-------------------|----------------------|-------------|
| `HashMap`     | ❌ (без порядку)   | O(1)                 | Найшвидший, не гарантує порядок |
| `LinkedHashMap`| ✅ (порядок вставки)| O(1)                 | Зберігає порядок вставки |
| `TreeMap`     | ✅ (сортування ключів)| O(log n)             | Сортує за ключами (Red-Black Tree)

#### Додатково:

- `TreeSet` реалізований через `TreeMap`
- `LinkedHashMap` має `accessOrder=true` для LRU кешів

🔗 [TechieDelight: HashMap vs TreeMap vs LinkedHashMap](https://www.techiedelight.com/difference-between-hashmap-treemap-linkedhashmap-java/)  
🔗 [Medium: Exploring Java Maps](https://medium.com/@AlexanderObregon/exploring-the-world-of-java-maps-hashmap-linkedhashmap-and-treemap-6c12297063f6) ❌ (недоступне, підтверджено з TechieDelight)

---

### 6.5. LRU (Least Recently Used) Cache

🔹 **LRU Cache** — стратегія кешування, яка при переповненні **витісняє найменш нещодавно використаний елемент**  
🔹 Реалізується через `LinkedHashMap` з параметром `accessOrder = true`  
🔹 Комбінація:
- `HashMap` — для O(1) доступу
- Двозв’язний список — для відстеження порядку використання

```java
LinkedHashMap<K, V> cache = new LinkedHashMap<>(capacity, 0.75f, true);
```

🔹 Метод `removeEldestEntry()` дозволяє автоматичне видалення найстарішого елемента при досягненні ліміту

```java
@Override
protected boolean removeEldestEntry(Map.Entry<K, V> eldest) {
    return size() > capacity;
}
```

🔗 [Baeldung: LRU Cache in Java](https://www.baeldung.com/java-lru-cache)

---

## 8. Java Generics — Типізація, Wildcards, Наслідування, PECS, Type Erasure

---

### 8.1. Що таке Generics?

🔹 Generics з’явились у Java 5 для забезпечення **перевірки типів на етапі компіляції** та уникнення `ClassCastException`.  
🔹 Синтаксис: використовуються кутові дужки `<>` для вказання параметра типу.

```java
List<String> list = new ArrayList<>();
```

---

### 8.2. Умовні позначення типів

| Позначення | Значення                            |
|------------|-------------------------------------|
| `T`        | Type (загальний тип)                |
| `E`        | Element (використовується в колекціях) |
| `K`, `V`   | Key, Value (використовуються в Map) |
| `N`        | Number                              |
| `S`, `U`   | Другий, третій типи                 |

---

### 8.3. Generic Interface

```java
public interface Comparable<T> {
    int compareTo(T o);
}
```

---

### 8.4. Generic Class

```java
public class GenericsType<T> {
    private T t;
    public T get() { return this.t; }
    public void set(T t1) { this.t = t1; }
}
```

---

### 8.5. Generic Method

```java
public static <T> boolean isEqual(GenericsType<T> g1, GenericsType<T> g2) {
    return g1.get().equals(g2.get());
}
```

---

### 8.6. Generics та Наслідування

🔹 Наслідування не поширюється на параметризовані типи:

```java
MyClass<String> myClass1 = new MyClass<>();
MyClass<Object> myClass2 = new MyClass<>();
// myClass2 = myClass1; // ❌ помилка компіляції
```

🔹 Але `MyClass<T>` — це підклас `Object`, тому:

```java
Object obj = myClass1; // ✅
```

---

### 8.7. Wildcards (`?`)

🔹 `?` — спеціальний параметр типу, що означає **невідомий тип**.  
🔹 Використовується в оголошеннях змінних, параметрах методів, але **не в оголошенні класів**.

```java
List<?> list = new ArrayList<String>();
```

---

### 8.8. Типи Wildcards

| Тип                         | Синтаксис               | Призначення                                |
|----------------------------|--------------------------|---------------------------------------------|
| Upper Bounded Wildcard     | `<? extends Number>`     | Читання з колекції (producer)               |
| Lower Bounded Wildcard     | `<? super Integer>`      | Запис у колекцію (consumer)                 |
| Unbounded Wildcard         | `<?>` або `<? extends Object>` | Будь-який тип                         |

---

### 8.9. Мнемоніка PECS

> **PECS**: *Producer — Extends, Consumer — Super*

- Якщо **читаємо** з колекції → `? extends T`
- Якщо **записуємо** в колекцію → `? super T`
- Якщо і читаємо, і записуємо → не використовуємо wildcard

🔗 [StackOverflow: Використання wildcard в Java](https://ru.stackoverflow.com/questions/361807/Использование-wildcard-в-generics-java)

---

### 8.10. Diamond Operator (`<>`)

🔹 З Java 7 можна опускати параметри типу, якщо компілятор може їх вивести:

```java
Lair<Goblin> goblinLair = new Lair<>();
```

🔹 Це називається **diamond operator**.

🔗 [Urvanov: Java 8 — обобщения](https://urvanov.ru/2016/04/28/java-8-обобщения/)

---

### 8.11. Raw Types

🔹 **Raw type** — це використання generic-класу **без параметра типу**:

```java
List list = new ArrayList(); // raw type
```

- Не рекомендується: втрачається типобезпека

---

### 8.12. Type Erasure

🔹 Generics існують лише на етапі компіляції.  
🔹 JVM не створює окремі класи для `List<String>` і `List<Integer>` — вони стираються до `List`.

```java
List<String> list = new ArrayList<>();
String s = list.get(0); // компілятор вставляє кастинг
```

- Це називається **type erasure**
- Немає накладних витрат у рантаймі

---

### 8.13. Multiple Bounds

```java
public abstract class Cage<T extends Animal & Comparable> { ... }
```

- Тип `T` повинен бути **підкласом `Animal`** і реалізовувати **`Comparable`**

---

### 8.14. Практика та Питання

🔗 [JournalDev: Java Generics Guide](https://www.journaldev.com/1663/java-generics-example-method-class-interface)  
🔗 [Baeldung: Java Generics](https://www.baeldung.com/java-generics)  
🔗 [Javatpoint: Generics Interview Questions](https://www.javatpoint.com/java-generics-questions)

---

## 9. Java Annotations — Вбудовані, Кастомні, Retention, Target, Inherited

---

### 9.1. Призначення анотацій

🔹 Анотації — це метадані, які можна додавати до класів, методів, параметрів, полів, змінних.  
🔹 Вони використовуються для:

- Інструкцій компілятору (наприклад, `@Override`, `@SuppressWarnings`)
- Інструкцій на етапі збірки (наприклад, генерація коду через annotation processing)
- Інструкцій на етапі виконання (через Reflection API)

🔗 [Javatpoint: Java Annotation](https://www.javatpoint.com/java-annotation)  
🔗 [Reflectoring: Annotation Processing](https://reflectoring.io/java-annotation-processing/)

---

### 9.2. Вбудовані анотації

| Анотація            | Призначення                                                                 |
|---------------------|------------------------------------------------------------------------------|
| `@Deprecated`        | Позначає елемент як застарілий — не рекомендується використовувати          |
| `@Override`          | Вказує, що метод перевизначає метод суперкласу — компілятор перевіряє       |
| `@SuppressWarnings`  | Приглушує попередження компілятора (наприклад, при використанні raw types)  |

```java
@Deprecated
public void oldMethod() { ... }

@Override
public void run() { ... }

@SuppressWarnings("unchecked")
List<String> list = new ArrayList();
```

---

### 9.3. Власні анотації (Custom Annotations)

🔹 Анотації — це інтерфейси з ключовим словом `@interface`.

```java
public @interface MyAnnotation {
    String value();
}
```

- Можуть містити параметри з типами: `String`, `int`, `Class`, `enum`, масиви
- Не можуть містити `null` як значення за замовчуванням
- Можуть бути доповнені мета-нотаціями: `@Retention`, `@Target`, `@Inherited`, `@Documented`

---

### 9.4. @Retention

🔹 Вказує, **на якому етапі життєвого циклу** анотація буде доступна.

| Тип RetentionPolicy | Доступність         | Опис                                           |
|---------------------|---------------------|------------------------------------------------|
| `SOURCE`            | Лише в коді         | Відкидається при компіляції                    |
| `CLASS`             | У байт-коді         | Недоступна в рантаймі                          |
| `RUNTIME`           | У рантаймі          | Доступна через Reflection                      |

```java
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;

@Retention(RetentionPolicy.RUNTIME)
public @interface MyRuntimeAnnotation {
    String value();
}
```

🔗 [Java2Novice: Retention Policy](http://www.java2novice.com/java-annotations/retention-policy/)

---

### 9.5. @Target

🔹 Вказує, **де може бути застосована анотація**.

| ElementType             | Опис                         |
|-------------------------|------------------------------|
| `TYPE`                  | Клас, інтерфейс, enum        |
| `FIELD`                 | Поле                         |
| `METHOD`                | Метод                        |
| `PARAMETER`             | Параметр методу              |
| `CONSTRUCTOR`           | Конструктор                  |
| `LOCAL_VARIABLE`        | Локальна змінна              |
| `ANNOTATION_TYPE`       | Інша анотація                |
| `PACKAGE`               | Пакет                        |

```java
import java.lang.annotation.Target;
import java.lang.annotation.ElementType;

@Target({ElementType.METHOD, ElementType.TYPE})
public @interface MyTargetAnnotation {
    String value();
}
```

---

### 9.6. @Inherited

🔹 Дозволяє **успадковувати анотацію** в підкласах.

```java
import java.lang.annotation.Inherited;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;
import java.lang.annotation.ElementType;

@Inherited
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
public @interface Auditable { }

@Auditable
class BaseEntity { }

class User extends BaseEntity { } // User також має @Auditable
```

- Без `@Inherited` анотація не буде доступна в підкласі через Reflection.

---

### 9.7. @Documented

🔹 Вказує, що анотація повинна бути **відображена в JavaDoc**.

```java
import java.lang.annotation.Documented;

@Documented
public @interface PublicAPI {
    String description();
}
```

- Без `@Documented` анотація не буде з’являтись у JavaDoc, навіть якщо вона використана в класі.

---

### 9.8. Додаткові приклади використання

#### Анотація з кількома параметрами

```java
public @interface Info {
    String author();
    String date();
    int version() default 1;
}
```

#### Застосування:

```java
@Info(author = "Ostap", date = "2025-10-25")
public class MyService { ... }
```

---
