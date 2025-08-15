Отличный вопрос! Давайте разберём эти строки подробно и уточним, куда именно их нужно вставить.

---

## **1. Загрузка напоминаний при старте приложения**
```java
// В onCreate после инициализации адаптера
reminders = DataHelper.getReminders();
adapter = new ReminderAdapter(reminders);
```

### **Что это делает?**
- `DataHelper.getReminders()` — получает список всех сохранённых напоминаний из нашего временного хранилища (класса `DataHelper`).
- `adapter = new ReminderAdapter(reminders)` — создаёт адаптер и передаёт ему этот список, чтобы отобразить в `RecyclerView`.

### **Куда это вставить?**
В `MainActivity.java`, внутри метода `onCreate()`, **после** настройки `RecyclerView`, но **до** установки адаптера. Вот полный код:

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    recyclerView = findViewById(R.id.recyclerView);
    fabAdd = findViewById(R.id.fabAdd);

    // 1. Настройка RecyclerView
    recyclerView.setLayoutManager(new LinearLayoutManager(this));
    
    // 2. Загружаем напоминания из DataHelper
    reminders = DataHelper.getReminders();  // ← Вот эта строка
    adapter = new ReminderAdapter(reminders);  // ← И эта
    
    // 3. Устанавливаем адаптер
    recyclerView.setAdapter(adapter);

    // Остальной код...
}
```

---

## **2. Сохранение нового напоминания**
```java
// В onActivityResult после добавления
DataHelper.addReminder(new Reminder(text, date));
```

### **Что это делает?**
- `DataHelper.addReminder(...)` — добавляет новое напоминание в наше хранилище (`DataHelper`), чтобы оно не пропадало после перезапуска приложения.
- `new Reminder(text, date)` — создаёт объект напоминания с текстом и датой, которые мы получили из `AddReminderActivity`.

### **Куда это вставить?**
В `MainActivity.java`, внутри метода `onActivityResult()`, **после** проверки `resultCode`, но **перед** обновлением адаптера. Вот полный код:

```java
@Override
protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    
    if (requestCode == 1 && resultCode == RESULT_OK && data != null) {
        String text = data.getStringExtra("text");
        String date = data.getStringExtra("date");
        
        // 1. Добавляем напоминание в DataHelper
        DataHelper.addReminder(new Reminder(text, date));  // ← Вот эта строка
        
        // 2. Обновляем список
        reminders.add(new Reminder(text, date));
        adapter.notifyItemInserted(reminders.size() - 1);
    }
}
```

---

## **Почему это важно?**
Без этих строк:
1. При перезапуске приложения все напоминания пропадут (так как они хранятся только в оперативной памяти).
2. Новые напоминания не будут сохраняться для последующих сеансов.

---

## **Проверка работы**
1. Добавьте новое напоминание через кнопку (+).
2. Закройте и снова откройте приложение — напоминания должны остаться на месте!
3. Если что-то не работает, проверьте:
   - Корректно ли создан класс `DataHelper`.
   - Передаются ли `text` и `date` из `AddReminderActivity` (должны быть в `Intent`).

---

## **Дополнительно**
Если хотите сделать хранилище более надёжным (чтобы напоминания сохранялись даже после перезагрузки устройства), в следующих уроках мы заменим `DataHelper` на базу данных **SQLite** или **Room**. 

Сейчас всё работает в памяти приложения — этого достаточно для обучения! 😊