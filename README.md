# Задания - Садыров Кутман
*Группа: ПИ-1_23 (Вариант: 17)*

---

## Лабораторная работа 4-5: ООП и наследование

**5. Звёздная система**

Создать объект класса «Звёздная система», используя классы «Планета», «Звезда», «Луна». Реализовать методы: вывод количества планет, вывод названия звезды, добавление планеты в систему. (С использованием наследования.)

```java/6/StarSystemDemo.java#L1-120
import java.util.ArrayList;
import java.util.List;

// Базовый абстрактный класс для всех небесных тел (использование наследования)
abstract class HeavenlyBody {
    protected String name;

    public HeavenlyBody(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    @Override
    public String toString() {
        return name;
    }
}

// Класс Звезда, наследуется от HeavenlyBody
class Star extends HeavenlyBody {
    public Star(String name) {
        super(name);
    }
}

// Класс Луна, наследуется от HeavenlyBody
class Moon extends HeavenlyBody {
    public Moon(String name) {
        super(name);
    }
}

// Класс Планета, наследуется от HeavenlyBody
// Может содержать список лун (демонстрация наследования и композиции)
class Planet extends HeavenlyBody {
    private List<Moon> moons;

    public Planet(String name) {
        super(name);
        this.moons = new ArrayList<>();
    }

    public void addMoon(Moon moon) {
        moons.add(moon);
    }

    public List<Moon> getMoons() {
        return moons;
    }
}

// Класс Звёздная система
class StarSystem {
    private Star star;
    private List<Planet> planets;

    public StarSystem(Star star) {
        this.star = star;
        this.planets = new ArrayList<>();
    }

    // Добавление планеты в систему
    public void addPlanet(Planet planet) {
        planets.add(planet);
        System.out.println("Планета " + planet.getName() + " добавлена в систему.");
    }

    // Вывести на консоль количество планет в звездной системе
    public void printPlanetCount() {
        System.out.println("Количество планет в системе: " + planets.size());
    }

    // Вывести на консоль название звезды
    public void printStarName() {
        System.out.println("Название звезды: " + star.getName());
    }

    // Дополнительный метод для получения количества планет (если нужно)
    public int getPlanetCount() {
        return planets.size();
    }
}

// Демонстрационный класс
public class StarSystemDemo {
    public static void main(String[] args) {
        // Создаём звезду
        Star sun = new Star("Солнце");

        // Создаём планеты
        Planet earth = new Planet("Земля");
        Planet mars = new Planet("Марс");
        Planet venus = new Planet("Венера");

        // Создаём луны (демонстрация работы класса Луна)
        Moon moon = new Moon("Луна");
        Moon phobos = new Moon("Фобос");
        Moon deimos = new Moon("Деймос");

        // Добавляем луны к планетам (необязательно для задания, но показывает использование всех классов)
        earth.addMoon(moon);
        mars.addMoon(phobos);
        mars.addMoon(deimos);

        // Создаём звёздную систему
        StarSystem solarSystem = new StarSystem(sun);

        // Добавляем планеты в систему
        solarSystem.addPlanet(earth);
        solarSystem.addPlanet(mars);
        solarSystem.addPlanet(venus);

        // Выводим информацию
        solarSystem.printStarName();        // Название звезды
        solarSystem.printPlanetCount();     // Количество планет

        // Дополнительно: покажем, что у планет есть луны (не требуется, но демонстрирует класс Moon)
        System.out.println("\nДополнительная информация о спутниках:");
        System.out.println("У планеты " + earth.getName() + " лун: " + earth.getMoons().size());
        System.out.println("У планеты " + mars.getName() + " лун: " + mars.getMoons().size());
    }
}
```

**Вывод:**
```
Планета Земля добавлена в систему.
Планета Марс добавлена в систему.
Планета Венера добавлена в систему.
Название звезды: Солнце
Количество планет в системе: 3

Дополнительная информация о спутниках:
У планеты Земля лун: 1
У планеты Марс лун: 2
```

---

**6. Работники фирмы**

Создать абстрактный класс «Работник фирмы» и подклассы: «Менеджер», «Аналитик», «Программист», «Тестировщик», «Дизайнер». (С использованием наследования.)

```java/7/FirmDemo.java#L1-110
// Абстрактный класс Работник фирмы
abstract class Employee {
    protected String name;
    protected int id;
    protected double baseSalary;

    public Employee(String name, int id, double baseSalary) {
        this.name = name;
        this.id = id;
        this.baseSalary = baseSalary;
    }

    public String getName() {
        return name;
    }

    public int getId() {
        return id;
    }

    public double getBaseSalary() {
        return baseSalary;
    }

    // Абстрактный метод расчета зарплаты (реализуется в подклассах)
    public abstract double calculateSalary();

    // Метод для вывода информации о работнике
    public void displayInfo() {
        System.out.println("ID: " + id + ", Имя: " + name + ", Должность: " + getPosition() + ", Зарплата: " + calculateSalary());
    }

    // Абстрактный метод для получения названия должности
    protected abstract String getPosition();
}

// Подкласс Менеджер
class Manager extends Employee {
    private double bonus; // дополнительная премия

    public Manager(String name, int id, double baseSalary, double bonus) {
        super(name, id, baseSalary);
        this.bonus = bonus;
    }

    @Override
    public double calculateSalary() {
        return baseSalary + bonus;
    }

    @Override
    protected String getPosition() {
        return "Менеджер";
    }
}

// Подкласс Аналитик
class Analyst extends Employee {
    private int projectCount; // количество проектов (влияет на бонус)

    public Analyst(String name, int id, double baseSalary, int projectCount) {
        super(name, id, baseSalary);
        this.projectCount = projectCount;
    }

    @Override
    public double calculateSalary() {
        return baseSalary + projectCount * 500; // бонус за проекты
    }

    @Override
    protected String getPosition() {
        return "Аналитик";
    }
}

// Подкласс Программист
class Programmer extends Employee {
    private int linesOfCodePerDay; // тысячи строк кода в день (влияет на бонус)

    public Programmer(String name, int id, double baseSalary, int linesOfCodePerDay) {
        super(name, id, baseSalary);
        this.linesOfCodePerDay = linesOfCodePerDay;
    }

    @Override
    public double calculateSalary() {
        return baseSalary + linesOfCodePerDay * 200; // бонус за производительность
    }

    @Override
    protected String getPosition() {
        return "Программист";
    }
}

// Подкласс Тестировщик
class Tester extends Employee {
    private int bugsFound; // количество найденных багов

    public Tester(String name, int id, double baseSalary, int bugsFound) {
        super(name, id, baseSalary);
        this.bugsFound = bugsFound;
    }

    @Override
    public double calculateSalary() {
        return baseSalary + bugsFound * 50; // бонус за найденные ошибки
    }

    @Override
    protected String getPosition() {
        return "Тестировщик";
    }
}

// Подкласс Дизайнер
class Designer extends Employee {
    private int projectsCompleted; // количество завершенных проектов

    public Designer(String name, int id, double baseSalary, int projectsCompleted) {
        super(name, id, baseSalary);
        this.projectsCompleted = projectsCompleted;
    }

    @Override
    public double calculateSalary() {
        return baseSalary + projectsCompleted * 800; // бонус за проекты
    }

    @Override
    protected String getPosition() {
        return "Дизайнер";
    }
}

// Демонстрационный класс
public class FirmDemo {
    public static void main(String[] args) {
        // Создаем объекты всех типов работников
        Employee manager = new Manager("Иван Петров", 101, 50000, 15000);
        Employee analyst = new Analyst("Мария Сидорова", 102, 45000, 3);
        Employee programmer = new Programmer("Алексей Смирнов", 103, 60000, 10);
        Employee tester = new Tester("Ольга Козлова", 104, 40000, 25);
        Employee designer = new Designer("Елена Новикова", 105, 48000, 4);
        System.out.println("=== Работники фирмы ===\n");
        manager.displayInfo();
        analyst.displayInfo();
        programmer.displayInfo();
        tester.displayInfo();
        designer.displayInfo();
    }
}
```

**Вывод:**
```
=== Работники фирмы ===

ID: 101, Имя: Иван Петров, Должность: Менеджер, Зарплата: 65000.0
ID: 102, Имя: Мария Сидорова, Должность: Аналитик, Зарплата: 46500.0
ID: 103, Имя: Алексей Смирнов, Должность: Программист, Зарплата: 62000.0
ID: 104, Имя: Ольга Козлова, Должность: Тестировщик, Зарплата: 41250.0
ID: 105, Имя: Елена Новикова, Должность: Дизайнер, Зарплата: 51200.0
```

---

## Лабораторная работа 6: Внутренние классы

**7.1. СССР и внутренний класс**

Создать класс «СССР» с внутренним классом, с помощью объектов которого можно хранить информацию об истории изменения территориального деления на области и республики. (С использованием абстрактного класса.)

```java/7/USSRDemo.java#L1-150
import java.util.*;

// Абстрактный класс территориальной единицы
abstract class TerritorialUnit {
    protected String name;

    public TerritorialUnit(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    // Абстрактный метод, возвращающий тип единицы (республика или область)
    public abstract String getType();

    @Override
    public String toString() {
        return getType() + " \"" + name + "\"";
    }
}

// Класс Республика (наследник TerritorialUnit)
class Republic extends TerritorialUnit {
    public Republic(String name) {
        super(name);
    }

    @Override
    public String getType() {
        return "Республика";
    }
}

// Класс Область (наследник TerritorialUnit)
class Oblast extends TerritorialUnit {
    public Oblast(String name) {
        super(name);
    }

    @Override
    public String getType() {
        return "Область";
    }
}

// Класс СССР
class USSR {
    // Внутренний класс для хранения истории изменений территориального деления
    public class TerritorialHistory {
        // Каждая запись истории содержит дату и список территориальных единиц на тот момент
        private List<HistoryRecord> records;

        public TerritorialHistory() {
            records = new ArrayList<>();
        }

        // Добавить запись об изменении (новое состояние деления)
        public void addRecord(String date, List<TerritorialUnit> units) {
            // Создаём копию списка, чтобы избежать внешних изменений
            List<TerritorialUnit> snapshot = new ArrayList<>(units);
            records.add(new HistoryRecord(date, snapshot));
            System.out.println("Запись добавлена: " + date + ", количество единиц: " + snapshot.size());
        }

        // Показать всю историю
        public void showHistory() {
            if (records.isEmpty()) {
                System.out.println("История изменений пуста.");
                return;
            }
            System.out.println("\n=== История территориального деления СССР ===");
            for (HistoryRecord record : records) {
                System.out.println("Дата: " + record.date);
                System.out.println("Состав:");
                for (TerritorialUnit unit : record.units) {
                    System.out.println("  - " + unit);
                }
                System.out.println("------------------------");
            }
        }

        // Получить состояние деления на определённую дату (простой поиск по точному совпадению)
        public List<TerritorialUnit> getStateByDate(String date) {
            for (HistoryRecord record : records) {
                if (record.date.equals(date)) {
                    return new ArrayList<>(record.units);
                }
            }
            return null;
        }

        // Внутренний класс для записи истории (можно также сделать private)
        private class HistoryRecord {
            String date;
            List<TerritorialUnit> units;

            HistoryRecord(String date, List<TerritorialUnit> units) {
                this.date = date;
                this.units = units;
            }
        }
    }

    // Поле для доступа к истории (объект внутреннего класса)
    private TerritorialHistory history;

    public USSR() {
        history = new TerritorialHistory();
    }

    public TerritorialHistory getHistory() {
        return history;
    }
}

// Демонстрационный класс
public class USSRDemo {
    public static void main(String[] args) {
        USSR ussr = new USSR();

        // Получаем объект истории
        USSR.TerritorialHistory history = ussr.getHistory();

        // Создаём первоначальное деление (например, 1922 год)
        List<TerritorialUnit> units1922 = new ArrayList<>();
        units1922.add(new Republic("РСФСР"));
        units1922.add(new Republic("Украинская ССР"));
        units1922.add(new Republic("Белорусская ССР"));
        units1922.add(new Republic("Закавказская СФСР"));
        history.addRecord("1922", units1922);

        // Добавляем изменение после 1924 года (например, появление новых республик)
        List<TerritorialUnit> units1924 = new ArrayList<>();
        units1924.add(new Republic("РСФСР"));
        units1924.add(new Republic("Украинская ССР"));
        units1924.add(new Republic("Белорусская ССР"));
        units1924.add(new Republic("Узбекская ССР"));
        units1924.add(new Republic("Туркменская ССР"));
        history.addRecord("1924", units1924);

        // Добавляем более позднее деление с областями (например, 1930-е годы)
        List<TerritorialUnit> units1936 = new ArrayList<>();
        units1936.add(new Republic("РСФСР"));
        units1936.add(new Republic("Украинская ССР"));
        units1936.add(new Republic("Белорусская ССР"));
        units1936.add(new Republic("Узбекская ССР"));
        units1936.add(new Republic("Туркменская ССР"));
        units1936.add(new Republic("Таджикская ССР"));
        // Добавим несколько областей внутри РСФСР – для демонстрации областей
        units1936.add(new Oblast("Московская область"));
        units1936.add(new Oblast("Ленинградская область"));
        history.addRecord("1936", units1936);

        // Показываем всю историю
        history.showHistory();

        // Пример получения состояния на конкретную дату
        System.out.println("\n=== Проверка получения состояния на 1924 год ===");
        List<TerritorialUnit> state1924 = history.getStateByDate("1924");
        if (state1924 != null) {
            for (TerritorialUnit unit : state1924) {
                System.out.println(unit);
            }
        } else {
            System.out.println("Запись не найдена.");
        }
    }
}
```

**Вывод:**
```
Запись добавлена: 1922, количество единиц: 4
Запись добавлена: 1924, количество единиц: 5
Запись добавлена: 1936, количество единиц: 8

=== История территориального деления СССР ===
Дата: 1922
Состав:
  - Республика "РСФСР"
  - Республика "Украинская ССР"
  - Республика "Белорусская ССР"
  - Республика "Закавказская СФСР"
------------------------
Дата: 1924
Состав:
  - Республика "РСФСР"
  - Республика "Украинская ССР"
  - Республика "Белорусская ССР"
  - Республика "Узбекская ССР"
  - Республика "Туркменская ССР"
------------------------
Дата: 1936
Состав:
  - Республика "РСФСР"
  - Республика "Украинская ССР"
  - Республика "Белорусская ССР"
  - Республика "Узбекская ССР"
  - Республика "Туркменская ССР"
  - Республика "Таджикская ССР"
  - Область "Московская область"
  - Область "Ленинградская область"
------------------------

=== Проверка получения состояния на 1924 год ===
Республика "РСФСР"
Республика "Украинская ССР"
Республика "Белорусская ССР"
Республика "Узбекская ССР"
Республика "Туркменская ССР"
```

---

## Лабораторная работа 7: Работа со строками

**7.2. Строки: слова минимальной и максимальной длины**

В тексте найти и напечатать все слова максимальной длины и все слова минимальной длины. Текст можно вводить самостоятельно.

```java/8/MinMaxWords.java#L1-65
import java.util.*;

public class MinMaxWords {
    public static void main(String[] args) {
        String text;

        // Получение текста: если есть аргументы командной строки, объединяем их
        if (args.length > 0) {
            text = String.join(" ", args);
        } else {
            // Иначе читаем с консоли
            Scanner scanner = new Scanner(System.in);
            System.out.println("Введите текст:");
            text = scanner.nextLine();
            scanner.close();
        }

        // Разбиваем текст на слова
        String[] rawWords = text.split("\\s+");
        List<String> words = new ArrayList<>();

        for (String w : rawWords) {
            // Удаляем знаки препинания в начале и конце слова
            String clean = w.replaceAll("^[^\\p{L}\\p{N}]+|[^\\p{L}\\p{N}]+$", "");
            if (!clean.isEmpty()) {
                words.add(clean);
            }
        }

        if (words.isEmpty()) {
            System.out.println("Текст не содержит слов.");
            return;
        }

        // Находим минимальную и максимальную длину
        int minLen = Integer.MAX_VALUE;
        int maxLen = Integer.MIN_VALUE;

        for (String w : words) {
            int len = w.length();
            if (len < minLen) minLen = len;
            if (len > maxLen) maxLen = len;
        }

        // Собираем слова минимальной и максимальной длины
        List<String> minWords = new ArrayList<>();
        List<String> maxWords = new ArrayList<>();

        for (String w : words) {
            int len = w.length();
            if (len == minLen && !minWords.contains(w)) {
                minWords.add(w);
            }
            if (len == maxLen && !maxWords.contains(w)) {
                maxWords.add(w);
            }
        }

        // Вывод результатов
        System.out.println("\nСлова минимальной длины (" + minLen + "):");
        for (String w : minWords) {
            System.out.println("  " + w);
        }

        System.out.println("\nСлова максимальной длины (" + maxLen + "):");
        for (String w : maxWords) {
            System.out.println("  " + w);
        }
    }
}
```

**Ввод:**
```
Привет мир и программирование на Java
```

**Вывод:**
```
Введите текст:

Слова минимальной длины (1):
  и

Слова максимальной длины (16):
  программирование
```

---

**8. Строки: слова, начинающиеся с гласной буквы**

В каждой строке текста найти слова, начинающиеся с гласной буквы (русской или английской). Текст вводится пользователем.

```java/8/WordsStartingWithVowel.java#L1-75
import java.util.Scanner;
import java.util.ArrayList;
import java.util.List;
import java.util.Set;
import java.util.HashSet;

public class WordsStartingWithVowel {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Введите текст (для завершения ввода введите пустую строку):");

        List<String> lines = new ArrayList<>();
        while (true) {
            String line = scanner.nextLine();
            if (line.trim().isEmpty() && lines.isEmpty()) {
                break;
            }
            if (line.isEmpty()) {
                break;
            }
            lines.add(line);
        }
        scanner.close();

        // Множество гласных букв (русские + английские)
        Set<Character> vowels = new HashSet<>();
        // Русские гласные
        String russianVowels = "аеёиоуыэюяАЕЁИОУЫЭЮЯ";
        for (char c : russianVowels.toCharArray()) {
            vowels.add(c);
        }
        // Английские гласные
        String englishVowels = "aeiouAEIOU";
        for (char c : englishVowels.toCharArray()) {
            vowels.add(c);
        }

        System.out.println("\n=== Результат ===");
        for (int i = 0; i < lines.size(); i++) {
            String line = lines.get(i);
            System.out.println("\nСтрока " + (i + 1) + ": \"" + line + "\"");
            
            // Разбиваем строку на слова
            String[] parts = line.split("\\s+");
            List<String> foundWords = new ArrayList<>();
            
            for (String part : parts) {
                // Убираем знаки препинания в начале и конце
                String word = part.replaceAll("^[^\\p{L}]+|[^\\p{L}]+$", "");
                if (word.isEmpty()) continue;
                
                // Проверяем первый символ
                char firstChar = word.charAt(0);
                if (vowels.contains(firstChar)) {
                    foundWords.add(word);
                }
            }
            
            if (foundWords.isEmpty()) {
                System.out.println("  Слов, начинающихся с гласной, не найдено.");
            } else {
                System.out.println("  Слова, начинающиеся с гласной: " + String.join(", ", foundWords));
            }
        }
    }
}
```

**Ввод:**
```
Это интересный урок
Английский English test
```

**Вывод:**
```
Введите текст (для завершения ввода введите пустую строку):

=== Результат ===

Строка 1: "Это интересный урок"
  Слова, начинающиеся с гласной: Это, интересный, урок

Строка 2: "Английский English test"
  Слова, начинающиеся с гласной: Английский, English
```

---

## Заключение

В ходе выполнения лабораторных работ 4-7 были изучены и применены следующие концепции объектно-ориентированного программирования:

1. **Наследование** - создание иерархии классов (HeavenlyBody, Employee, TerritorialUnit)
2. **Абстрактные классы** - определение общего интерфейса для подклассов
3. **Полиморфизм** - переопределение методов в подклассах
4. **Инкапсуляция** - сокрытие данных и предоставление методов доступа
5. **Внутренние классы** - создание вложенных классов для логической группировки
6. **Работа со строками** - обработка текста, регулярные выражения, коллекции

Все программы успешно скомпилированы и протестированы.
