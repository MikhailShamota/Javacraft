# **Урок 2: Добавляем кнопку и обработку нажатий**  
*(Создаём основу для будущего календаря с напоминаниями)*  

## **Цель урока**  
Добавить кнопку в приложение и научиться реагировать на её нажатие. Это основа для будущего функционала добавления напоминаний.  

---

## **Шаг 1: Добавляем кнопку в разметку**  
1. Откройте файл **`activity_main.xml`** (в папке `res/layout`).  
2. Переключитесь на вкладку **"Code"** (если находитесь в визуальном редакторе).  
3. Замените весь код внутри `<RelativeLayout>` (или `<ConstraintLayout>`) на:  

```xml
<TextView
    android:id="@+id/textView"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Мой календарь"
    android:textSize="24sp"
    android:layout_centerHorizontal="true"
    android:layout_marginTop="50dp" />

<Button
    android:id="@+id/buttonAddReminder"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Добавить напоминание"
    android:layout_below="@id/textView"
    android:layout_centerHorizontal="true"
    android:layout_marginTop="30dp" />
```

(Если у вас `ConstraintLayout`, используйте `app:layout_constraint...` вместо `layout_below` – попросите помощи, если нужно!)  

---

## **Шаг 2: Подключаем кнопку в Java-коде**  
1. Откройте файл **`MainActivity.java`** (в папке `java/ваш_пакет`).  
2. Добавьте код для работы с кнопкой:  

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Находим кнопку по ID
        Button buttonAddReminder = findViewById(R.id.buttonAddReminder);

        // Вешаем обработчик нажатия
        buttonAddReminder.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // Временное сообщение при нажатии
                Toast.makeText(MainActivity.this, 
                    "Напоминание будет добавлено в следующем уроке!", 
                    Toast.LENGTH_SHORT).show();
            }
        });
    }
}
```

---

## **Шаг 3: Запускаем и проверяем**  
1. Запустите приложение (как в Уроке 1).  
2. Нажмите на кнопку – должно появиться всплывающее сообщение (**Toast**).  

---

## **Шаг 4: Подготовка к следующему уроку**  
Чтобы в будущем добавлять напоминания, нам понадобится:  
- **Выбор даты** (календарь).  
- **Ввод текста напоминания**.  

Создадим новый экран для этого!  

1. В **Android Studio** кликните правой кнопкой на папку `res/layout` → **New → Layout Resource File**.  
2. Назовите файл **`activity_add_reminder.xml`** → OK.  
3. Пока оставьте его пустым (заполним в следующем уроке).  

---

## **Домашнее задание**  
1. Измените текст на кнопке (например, на "✚ Новое напоминание").  
2. Поменяйте цвет кнопки, добавив в её XML-атрибуты:  
   ```xml
   android:backgroundTint="#3F51B5"  <!-- Синий цвет -->
   android:textColor="#FFFFFF"      <!-- Белый текст -->
   ```
3. *Дополнительно*: Попробуйте сделать так, чтобы при нажатии кнопки менялся текст в `TextView` (подсказка: используйте `textView.setText("Новый текст")`).  

---

## **Что дальше?**  
В **Уроке 3** мы создадим экран для ввода напоминания с полем ввода и выбором даты!  

**Готово? Жду ваших вопросов!** 😊