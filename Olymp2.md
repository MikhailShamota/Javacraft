# **Урок 13: Эффективные алгоритмы сортировки и поиска**  
### **Для олимпиадного программирования (6-8 классы)**  

В этом уроке мы разберём **эффективные алгоритмы**, которые помогут решать сложные задачи на олимпиадах.  

**Что изучим:**  
- ⚡ Быструю сортировку (QuickSort)  
- 🔎 Бинарный поиск  
- 📊 Сортировку слиянием (MergeSort)  

---

## **1. Быстрая сортировка (QuickSort)**  
**Принцип работы:**  
1. Выбираем опорный элемент (pivot)  
2. Делим массив на две части: элементы меньше pivot и больше pivot  
3. Рекурсивно сортируем обе части  

```java
import java.util.Scanner;

public class QuickSort {

    public static void quickSort(int[] arr, int low, int high) {
        if (low < high) {
            int pi = partition(arr, low, high); // Индекс опорного элемента
            
            quickSort(arr, low, pi - 1);  // Сортируем левую часть
            quickSort(arr, pi + 1, high); // Сортируем правую часть
        }
    }
    
    public static int partition(int[] arr, int low, int high) {
        int pivot = arr[high]; // Опорный элемент
        int i = low - 1;       // Индекс меньшего элемента
        
        for (int j = low; j < high; j++) {
            if (arr[j] < pivot) {
                i++;
                // Меняем местами arr[i] и arr[j]
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
        
        // Меняем местами arr[i+1] и опорный элемент
        int temp = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp;
        
        return i + 1;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] arr = new int[n];
        
        for (int i = 0; i < n; i++) {
            arr[i] = sc.nextInt();
        }
        
        quickSort(arr, 0, n - 1);
        
        System.out.println("Отсортированный массив:");
        for (int num : arr) {
            System.out.print(num + " ");
        }
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
1 2 3 4 5
```

---

## **2. Бинарный поиск**  
**Принцип работы:**  
1. Массив должен быть **отсортирован**  
2. Сравниваем искомый элемент с элементом в середине  
3. Если элемент меньше — ищем в левой части, иначе — в правой  

```java
import java.util.Scanner;
import java.util.Arrays;

public class BinarySearch {

    public static int binarySearch(int[] arr, int target) {
        int left = 0;
        int right = arr.length - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            
            if (arr[mid] == target) {
                return mid; // Нашли!
            } else if (arr[mid] < target) {
                left = mid + 1; // Ищем справа
            } else {
                right = mid - 1; // Ищем слева
            }
        }
        
        return -1; // Не нашли
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        System.out.print("Введите размер массива: ");
        int n = sc.nextInt();
        int[] arr = new int[n];
        
        System.out.println("Введите элементы массива (отсортированные!):");
        for (int i = 0; i < n; i++) {
            arr[i] = sc.nextInt();
        }
        
        System.out.print("Введите число для поиска: ");
        int target = sc.nextInt();
        
        int result = binarySearch(arr, target);
        
        if (result == -1) {
            System.out.println("Элемент не найден!");
        } else {
            System.out.println("Элемент найден на позиции: " + result);
        }
    }
}
```

**Ввод:**  
```
5
1 3 5 7 9
5
```
**Вывод:**  
```
Элемент найден на позиции: 2
```

---

## **3. Сортировка слиянием (MergeSort)**  
**Принцип работы:**  
1. Делим массив пополам  
2. Рекурсивно сортируем каждую половину  
3. Сливаем две отсортированные половины  

```java
import java.util.Scanner;

public class MergeSort {

    public static void mergeSort(int[] arr, int left, int right) {
        if (left < right) {
            int mid = (left + right) / 2;
            
            mergeSort(arr, left, mid);      // Сортируем левую часть
            mergeSort(arr, mid + 1, right); // Сортируем правую часть
            merge(arr, left, mid, right);   // Сливаем две части
        }
    }
    
    public static void merge(int[] arr, int left, int mid, int right) {
        // Временные массивы для левой и правой частей
        int[] leftArr = new int[mid - left + 1];
        int[] rightArr = new int[right - mid];
        
        // Копируем данные во временные массивы
        for (int i = 0; i < leftArr.length; i++) {
            leftArr[i] = arr[left + i];
        }
        for (int j = 0; j < rightArr.length; j++) {
            rightArr[j] = arr[mid + 1 + j];
        }
        
        // Слияние
        int i = 0, j = 0, k = left;
        
        while (i < leftArr.length && j < rightArr.length) {
            if (leftArr[i] <= rightArr[j]) {
                arr[k++] = leftArr[i++];
            } else {
                arr[k++] = rightArr[j++];
            }
        }
        
        // Дописываем оставшиеся элементы
        while (i < leftArr.length) {
            arr[k++] = leftArr[i++];
        }
        while (j < rightArr.length) {
            arr[k++] = rightArr[j++];
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Введите размер массива: ");
        int n = sc.nextInt();
        int[] arr = new int[n];
        
        System.out.println("Введите элементы массива:");
        for (int i = 0; i < n; i++) {
            arr[i] = sc.nextInt();
        }
        
        mergeSort(arr, 0, n - 1);
        
        System.out.println("Отсортированный массив:");
        for (int num : arr) {
            System.out.print(num + " ");
        }
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
1 2 3 4 5
```

---

## **4. Практические задания**  

### **Задание 1: Поиск первого вхождения**  
Модифицируйте бинарный поиск, чтобы он находил **первое** вхождение числа в массиве.  

**Подсказка:**  
После нахождения элемента проверяйте, не является ли предыдущий элемент таким же.  

---

### **Задание 2: Сортировка строк**  
Напишите программу, которая сортирует массив строк в алфавитном порядке (используйте `String.compareTo()`).  

**Пример ввода:**  
```
3
banana apple orange
```
**Пример вывода:**  
```
apple banana orange
```

---

## **5. Что дальше?**  
В следующих уроках:  
- 📈 **Динамическое программирование** (решето Эратосфена, числа Фибоначчи)  
- 🧩 **Жадные алгоритмы**  
- 🌲 **Бинарные деревья**  

**Следующий урок: динамическое программирование для начинающих!**  

---

### **Итоги урока**  
- ⚡ **QuickSort** — быстрая сортировка за O(n log n)  
- 🔎 **Бинарный поиск** — поиск за O(log n)  
- 📊 **MergeSort** — стабильная сортировка слиянием  
- 🏆 Теперь вы можете решать сложные задачи на сортировку и поиск!  

Попробуйте решить задачи на [Codeforces](https://codeforces.com/) или [LeetCode](https://leetcode.com/)! 🚀