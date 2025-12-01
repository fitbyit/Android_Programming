**ListView** of 10 animals. When the user clicks an item, a **Toast** will show the selected animal.

---

### **1. Layout (`activity_main.xml`)**

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:padding="16dp"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <ListView
        android:id="@+id/listViewAnimals"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
</LinearLayout>
```

---

### **2. Activity (`MainActivity.java`)**

```java
package com.example.animallist;

import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.ListView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    ListView listViewAnimals;
    String[] animals = {"Lion", "Tiger", "Elephant", "Monkey", "Giraffe",
                        "Zebra", "Horse", "Dog", "Cat", "Rabbit"};

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        listViewAnimals = findViewById(R.id.listViewAnimals);

        // Set adapter
        ArrayAdapter<String> adapter = new ArrayAdapter<>(
                this,
                android.R.layout.simple_list_item_1,
                animals
        );
        listViewAnimals.setAdapter(adapter);

        // Set item click listener
        listViewAnimals.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
                String selectedAnimal = animals[position];
                Toast.makeText(MainActivity.this, "You selected: " + selectedAnimal, Toast.LENGTH_SHORT).show();
            }
        });
    }
}
```

