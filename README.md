# Задания - Садыров Кутман
*Группа: ПИ-1_23 (Вариант: 17)*


## Индивидеальная работа 1

**1,1   Найти по сторонам треугольника его площадь**
```java
import java.util.Scanner;

public class HeronArea {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.println("Введите стороны треугольника:");
        double a = sc.nextDouble();
        double b = sc.nextDouble();
        double c = sc.nextDouble();

        // Проверка существования треугольника
        if (a + b <= c || a + c <= b || b + c <= a) {
            System.out.println("Такого треугольника не существует");
            return;
        }

        double p = (a + b + c) / 2.0;
        double s = Math.sqrt(p * (p - a) * (p - b) * (p - c));

        System.out.printf("Площадь: %.2f\n", s);
        sc.close();
    }
}
```
ввод:
```
3 4 5
```
вывод:
```
Площадь: 6.00
```

---

**1,2  Решить математическую задачу**
```java
public class MathFormula {
    public static void main(String[] args) {
        double x = 2.45;
        double y = -0.423e-2;
        double z = 1.232e3;

        double numerator = Math.pow(x, 2 * y) + Math.exp(y - 1);
        double denominator = 1 + x * Math.abs(y - Math.tan(z));
        double otherPart = 10 * Math.cbrt(x) - Math.log(z);

        double h = (numerator / denominator) + otherPart;

        System.out.println("x = " + x);
        System.out.println("y = " + y);
        System.out.println("z = " + z);
        System.out.printf("Результат h = %.5f\n", h);
    }
}
```
вывод:
```
x = 2.45
y = -0.00423
z = 1232.0
Результат h = 6.75560
```

---

## Индивидеальная работа 2

**2,1  Написать программу проверки знания даты день города Бишкек. В случае неправильного ответа пользователя, программа должна выводить правильную дату**
```java
import java.util.Scanner;
import java.time.LocalDate;

public class DateCheck {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        // Получаем текущую дату из системы
        LocalDate today = LocalDate.now();
        
        System.out.println("Проверка: введите сегодняшнюю дату (день, затем месяц и год)");

        System.out.print("День: ");
        int userDay = sc.nextInt();

        System.out.print("Месяц (числом): ");
        int userMonth = sc.nextInt();

        System.out.print("Год: ");
        int userYear = sc.nextInt();

        if (userDay == today.getDayOfMonth() && 
            userMonth == today.getMonthValue() && 
            userYear == today.getYear()) {
            
            System.out.println("Верно! Сегодня именно " + today);
        } else {
            System.out.println("Ошибка. На самом деле сегодня: " + 
                                today.getDayOfMonth() + "." + 
                                today.getMonthValue() + "." + 
                                today.getYear());
        }
    }
}
```
ввод:
```
4
4
2026
```
вывод:
```
Верно! Сегодня именно 2026-04-04
```

---

## Switch-case 

**2,2  Определение весовой категории боксера**

Условия из задания:
- Легкий вес: до 60 кг;
- Первый полусредний вес: до 64 кг;
- Полусредний вес: до 69 кг.
    
```java
import java.util.Scanner;

public class BoxingWeight {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        double w = sc.nextDouble();
        int category = (int) w;

        switch (category / 10) {
            case 0, 1, 2, 3, 4, 5:
                System.out.println("Категория: Легкий вес");
                break;
            case 6:
                if (w < 64)
                    System.out.println("Категория: Первый полусредний вес");
                else if (w < 69)
                    System.out.println("Категория: Полусредний вес");
                else
                    System.out.println("Вес вне категорий");
                break;
            default:
                System.out.println("Вес вне категорий");
        }

        sc.close();
    }
}
```
ввод:
```
62.5
```
вывод:
```
Категория: Первый полусредний вес
```

---

## Циклы 

**2,3  Даны 10 чисел. Определить максимальное число и его порядковый номер**

```java
import java.util.Scanner;

public class MaxNumber {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Введите 10 чисел:");

        int max = scanner.nextInt();
        int maxIndex = 1;

        for (int i = 2; i <= 10; i++) {
            int current = scanner.nextInt();

            if (current > max) {
                max = current;
                maxIndex = i;
            }
        }

        System.out.println("Макс: " + max + ", Порядковый номер: " + maxIndex);

        scanner.close();
    }
}
```
ввод:
```
10 45 12 67 34 89 21 5 90 11
```
вывод:
```
Макс: 90, Порядковый номер: 9
```

---

**2,4  Вывести триугольний из цифр**
```
        1 
      1 2 
    1 2 3 
  1 2 3 4 
1 2 3 4 5 
  2 3 4 5 
    3 4 5 
      4 5 
        5
```
code:
```java
public class NumberPattern {
    public static void main(String[] args) {
        int n = 5;

        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= n - i; j++) {
                System.out.print("  ");
            }
            for (int j = 1; j <= i; j++) {
                System.out.print(j + " ");
            }
            System.out.println();
        }

        for (int i = 2; i <= n; i++) {
            for (int j = 1; j < i; j++) {
                System.out.print("  ");
            }
            for (int j = i; j <= n; j++) {
                System.out.print(j + " ");
            }
            System.out.println();
        }
    }
}
```

---

# Массивы и матрицы

## Лаб. работа 3

**3,1  Составить программу, которая находит элемент массива, наиболее приближенный к среднему арифметическому элементов массива**
```java
public class NearestToAverage {
    public static void main(String[] args) {

        int[] arr = {10, 25, 30, 45, 50};

        double sum = 0;
        for (int x : arr) sum += x;

        double avg = sum / arr.length;

        int nearest = arr[0];

        for (int x : arr) {
            if (Math.abs(x - avg) < Math.abs(nearest - avg)) {
                nearest = x;
            }
        }

        System.out.println("Среднее: " + avg + ", Ближайшее: " + nearest);
    }
}
```
вывод:
```
Среднее: 32.0, Ближайшее: 30
```

---

**3.2  Дан массив k\*k. Заменить элементы главной диагонали на элементы дополнительной диагонали**
```java
import java.util.Scanner;

public class DiagonalSwap {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Введите размер k: ");
        int k = sc.nextInt();

        int[][] matrix = new int[k][k];

        System.out.println("Исходная матрица:");
        for (int i = 0; i < k; i++) {
            for (int j = 0; j < k; j++) {
                matrix[i][j] = (i + 1) * (j + 1);
                System.out.printf("%4d", matrix[i][j]);
            }
            System.out.println();
        }

        for (int i = 0; i < k; i++) {
            int temp = matrix[i][i];
            matrix[i][i] = matrix[i][k - 1 - i];
            matrix[i][k - 1 - i] = temp;
        }

        System.out.println("\nМатрица после замены:");
        for (int i = 0; i < k; i++) {
            for (int j = 0; j < k; j++) {
                System.out.printf("%4d", matrix[i][j]);
            }
            System.out.println();
        }

        sc.close();
    }
}
```
ввод:
```
3
```
вывод:
```
Введите размер k: 3
Исходная матрица:
   1   2   3
   2   4   6
   3   6   9

Матрица после замены:
   3   2   3
   2   4   6
   3   6   3
```

---

**3,3  Дана квадратная матрица порядка n, заполненная случайными элементами. Присвоить элементам, находящимся выше главной диагонали значение на единицу больше, главную диагональ обнулить, а значение оставшихся элементов умножить на число n. **
```java
import java.util.Random;
import java.util.Scanner;

public class MatrixTransformation {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Random random = new Random();

        System.out.print("Введите порядок матрицы n: ");
        int n = scanner.nextInt();
        int[][] matrix = new int[n][n];

        // 1. Заполнение случайными числами
        System.out.println("Исходная матрица:");
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                matrix[i][j] = random.nextInt(10) + 1;
                System.out.printf("%4d", matrix[i][j]);
            }
            System.out.println();
        }

        // 2. Трансформация
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (i == j) matrix[i][j] = 0;
                else if (j > i) matrix[i][j] += 1;
                else matrix[i][j] *= n;
            }
        }

        // 3. Вывод результата
        System.out.println("\nМатрица после трансформации:");
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                System.out.printf("%4d", matrix[i][j]);
            }
            System.out.println();
        }
    }
}
```
ввод:
```
3
```
вывод:
```
Введите порядок матрицы n: 3
Исходная матрица:
   5   2   8
   4   7   1
   9   3   6

Матрица после трансформации:
   0   3   9
  12   0   2
  27   9   0
```
