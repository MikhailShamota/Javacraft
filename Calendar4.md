# **Урок 4: Создаем список напоминаний и сохраняем данные**  
*(Добавляем RecyclerView и временное хранилище в памяти)*  

## **Цель урока**  
1. Создать список для отображения всех напоминаний  
2. Реализовать сохранение данных между запусками приложения  
3. Научиться обновлять список при добавлении новых элементов  

---

## **Шаг 1: Подготовка модели данных**  
1. Создайте новый класс `Reminder.java` (ПКМ по пакету → New → Java Class):  
```java
public class Reminder {
    private String text;
    private String date;
    
    public Reminder(String text, String date) {
        this.text = text;
        this.date = date;
    }
    
    public String getText() { return text; }
    public String getDate() { return date; }
}
```

---

## **Шаг 2: Настраиваем RecyclerView**  
1. Добавьте в `activity_main.xml` вместо текущего содержимого:  
```xml
<androidx.recyclerview.widget.RecyclerView
    android:id="@+id/recyclerView"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="8dp"/>

<com.google.android.material.floatingactionbutton.FloatingActionButton
    android:id="@+id/fabAdd"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_gravity="bottom|end"
    android:layout_margin="16dp"
    android:src="@android:drawable/ic_input_add"/>
```

2. Создайте новый layout `item_reminder.xml` для элементов списка:  
```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    android:padding="16dp"
    android:background="?attr/selectableItemBackground">

    <TextView
        android:id="@+id/textViewReminder"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:textSize="16sp"/>

    <TextView
        android:id="@+id/textViewDate"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:textColor="#757575"
        android:layout_marginTop="4dp"/>
</LinearLayout>
```

---

## **Шаг 3: Создаем Adapter**  
Создайте новый класс `ReminderAdapter.java`:  
```java
public class ReminderAdapter extends RecyclerView.Adapter<ReminderAdapter.ViewHolder> {
    private List<Reminder> reminders;

    public ReminderAdapter(List<Reminder> reminders) {
        this.reminders = reminders;
    }

    @NonNull
    @Override
    public ViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(parent.getContext())
                .inflate(R.layout.item_reminder, parent, false);
        return new ViewHolder(view);
    }

    @Override
    public void onBindViewHolder(@NonNull ViewHolder holder, int position) {
        Reminder reminder = reminders.get(position);
        holder.textViewReminder.setText(reminder.getText());
        holder.textViewDate.setText(reminder.getDate());
    }

    @Override
    public int getItemCount() { return reminders.size(); }

    public static class ViewHolder extends RecyclerView.ViewHolder {
        public TextView textViewReminder;
        public TextView textViewDate;

        public ViewHolder(View view) {
            super(view);
            textViewReminder = view.findViewById(R.id.textViewReminder);
            textViewDate = view.findViewById(R.id.textViewDate);
        }
    }
}
```

---

## **Шаг 4: Обновляем MainActivity**  
Замените код в `MainActivity.java`:  
```java
public class MainActivity extends AppCompatActivity {
    private RecyclerView recyclerView;
    private ReminderAdapter adapter;
    private List<Reminder> reminders = new ArrayList<>();
    private FloatingActionButton fabAdd;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        recyclerView = findViewById(R.id.recyclerView);
        fabAdd = findViewById(R.id.fabAdd);

        // Настройка RecyclerView
        recyclerView.setLayoutManager(new LinearLayoutManager(this));
        adapter = new ReminderAdapter(reminders);
        recyclerView.setAdapter(adapter);

        fabAdd.setOnClickListener(v -> {
            Intent intent = new Intent(MainActivity.this, AddReminderActivity.class);
            startActivityForResult(intent, 1);
        });
    }

    @Override
    protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (requestCode == 1 && resultCode == RESULT_OK && data != null) {
            String text = data.getStringExtra("text");
            String date = data.getStringExtra("date");
            reminders.add(new Reminder(text, date));
            adapter.notifyItemInserted(reminders.size() - 1);
        }
    }
}
```

---

## **Шаг 5: Модифицируем AddReminderActivity**  
Обновите метод `saveReminder()`:  
```java
private void saveReminder() {
    EditText editText = findViewById(R.id.editTextReminder);
    String reminderText = editText.getText().toString();
    
    if (reminderText.isEmpty()) {
        Toast.makeText(this, "Введите текст напоминания", Toast.LENGTH_SHORT).show();
        return;
    }

    Intent resultIntent = new Intent();
    resultIntent.putExtra("text", reminderText);
    resultIntent.putExtra("date", textViewDate.getText().toString());
    setResult(RESULT_OK, resultIntent);
    finish();
}
```

---

## **Шаг 6: Добавляем временное хранилище**  
1. Создайте класс `DataHelper.java`:  
```java
public class DataHelper {
    private static List<Reminder> reminders = new ArrayList<>();

    public static void addReminder(Reminder reminder) {
        reminders.add(reminder);
    }

    public static List<Reminder> getReminders() {
        return new ArrayList<>(reminders);
    }
}
```

2. Обновите `MainActivity`:  
```java
// В onCreate после инициализации адаптера
reminders = DataHelper.getReminders();
adapter = new ReminderAdapter(reminders);

// В onActivityResult после добавления
DataHelper.addReminder(new Reminder(text, date));
```

---

## **Домашнее задание**  
1. Добавьте swipe-to-delete для удаления напоминаний  
2. Реализуйте сортировку по дате  
3. Добавьте проверку на пустую дату при сохранении  

---

## **Что дальше?**  
В **Уроке 5** мы:  
1. Реализуем постоянное хранение данных с помощью SQLite  
2. Добавим возможность редактирования существующих напоминаний  

**Ваше приложение уже умеет показывать список напоминаний!** 🎉