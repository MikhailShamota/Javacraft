# **Урок 12: Основы олимпиадного программирования на Java**  
### **Ввод-вывод и простые алгоритмы для начинающих**  

Этот урок посвящен **базовым алгоритмам**, которые часто встречаются в олимпиадах по программированию. Мы научимся:  
1. 📥 Эффективно считывать входные данные  
2. 📤 Выводить результаты  
3. 🔢 Работать с числами и строками  
4. 🔍 Решать простые задачи на поиск и сортировку  

**Для кого:** Ученики 6-8 классов, начинающие участвовать в олимпиадах  

---

## **1. Быстрый ввод/вывод в Java**  

В олимпиадных задачах важно быстро считывать данные. Используем `Scanner` или `BufferedReader`.  

### **Способ 1: Scanner (проще)**  
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();      // Число
        String s = scanner.next();      // Слово
        String line = scanner.nextLine(); // Вся строка
    }
}
```

### **Способ 2: BufferedReader (быстрее)**  
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine()); // Число
        String s = br.readLine();               // Строка
    }
}
```

---

## **2. Разбор простых задач**  

### **Задача 1: Сумма двух чисел**  
**Условие:**  
Даны два числа. Выведите их сумму.  

**Решение:**  




```java
import java.util.Scanner;

public class Sum {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        int b = sc.nextInt();
        System.out.println(a + b);
    }
}
```


**Ввод:**  
```
5 8
```
**Вывод:**  
```
13
```

---

### **Задача 2: Поиск минимума**  
**Условие:**  
Даны три числа. Найдите минимальное.  

**Решение:**  




```java
import java.util.Scanner;

public class MinNumber {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        int b = sc.nextInt();
        int c = sc.nextInt();
        
        int min = Math.min(a, Math.min(b, c));
        System.out.println(min);
    }
}
```


**Ввод:**  
```
4 1 7
```
**Вывод:**  
```
1
```

---

### **Задача 3: Четные числа**  
**Условие:**  
Дано число `N`. Выведите все четные числа от 1 до N.  

**Решение:**  




```java
import java.util.Scanner;

public class EvenNumbers {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        
        for (int i = 2; i <= n; i += 2) {
            System.out.print(i + " ");
        }
    }
}
```


**Ввод:**  
```
10
```
**Вывод:**  
```
2 4 6 8 10 
```

---

## **3. Алгоритмы поиска**  

### **Линейный поиск**  
Проверяем элементы **последовательно**.  

**Задача:** Есть ли число X в массиве?  
```java
import java.util.Scanner;

public class LinearSearch {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int[] arr = {3, 8, 5, 9, 2};
        
        int x = sc.nextInt();
        boolean found = false;
        
        for (int num : arr) {
            if (num == x) {
                found = true;
                break;
            }
        }
        
        System.out.println(found ? "Да" : "Нет");
    }
}
```

---

## **4. Сортировка**  

### **Сортировка пузырьком**  
Попарно сравниваем элементы.  

```java
import java.util.Scanner;
import java.util.Arrays;

public class BubbleSort {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] arr = new int[n];
        
        // Чтение массива
        for (int i = 0; i < n; i++) {
            arr[i] = sc.nextInt();
        }
        
        // Сортировка
        for (int i = 0; i < n-1; i++) {
            for (int j = 0; j < n-i-1; j++) {
                if (arr[j] > arr[j+1]) {
                    int temp = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = temp;
                }
            }
        }
        
        System.out.println(Arrays.toString(arr));
    }
}
```

**Ввод:**  
```
5
4 2 5 1 3
```
**Вывод:**  
```
[1, 2, 3, 4, 5]
```

---

## **5. Практические задания**  

### **Задание 1: Количество делителей**  
Дано число N. Найдите, сколько у него делителей.  

**Решение:**  




```java
import java.util.Scanner;

public class Divisors {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int count = 0;
        
        for (int i = 1; i <= n; i++) {
            if (n % i == 0) {
                count++;
            }
        }
        
        System.out.println(count);
    }
}
```


---

### **Задание 2: Палиндром**  
Дано слово. Определите, является ли оно палиндромом.  

**Решение:**  




```java
import java.util.Scanner;

public class Palindrome {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String s = sc.next();
        boolean isPalindrome = true;
        
        for (int i = 0; i < s.length()/2; i++) {
            if (s.charAt(i) != s.charAt(s.length()-1-i)) {
                isPalindrome = false;
                break;
            }
        }
        
        System.out.println(isPalindrome ? "Да" : "Нет");
    }
}
```


---

## **6. Что дальше?**  
В следующих уроках:  
- 📊 **Сортировка слиянием** и **быстрая сортировка**  
- 🔎 **Бинарный поиск**  
- 🧮 **Основы динамического программирования**  

**Следующий урок: эффективные алгоритмы сортировки!**  

---

### **Итоги урока**  
- 📥 Научились быстро считывать данные  
- 🔢 Разобрали простые алгоритмы  
- 🔍 Поняли принципы поиска и сортировки  
- 💡 Решили несколько олимпиадных задач  

Попробуй решить эти задачи на [Codeforces](https://codeforces.com/) или [acmp.ru](https://acmp.ru/)!