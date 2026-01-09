```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

   <TextView
       android:id="@+id/txtResult"
       android:layout_margin="25dp"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:text="0"
       android:gravity="end"
       android:textSize="32dp"/>

    <TableLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content">
        <TableRow>
            <Button
                android:layout_width="100dp"
                android:layout_height="wrap_content"
                android:text="7"
                android:onClick="NumberButton"
                android:layout_weight="1"
                android:layout_margin="10dp"
                android:textSize="20dp"/>
            <Button
                android:layout_width="100dp"
                android:layout_height="wrap_content"
                android:text="8"
                android:onClick="NumberButton"
                android:layout_weight="1"
                android:layout_margin="10dp"
                android:textSize="20dp"/>
            <Button
                android:layout_width="100dp"
                android:layout_height="wrap_content"
                android:text="9"
                android:onClick="NumberButton"
                android:layout_weight="1"
                android:layout_margin="10dp"
                android:textSize="20dp"/>
        </TableRow>
        <TableRow>
            <Button
                android:layout_width="100dp"
                android:layout_height="wrap_content"
                android:text="4"
                android:onClick="NumberButton"
                android:layout_weight="1"
                android:layout_margin="10dp"
                android:textSize="20dp"/>
            <Button
                android:layout_width="100dp"
                android:layout_height="wrap_content"
                android:text="5"
                android:onClick="NumberButton"
                android:layout_weight="1"
                android:layout_margin="10dp"
                android:textSize="20dp"/>
            <Button
                android:layout_width="100dp"
                android:layout_height="wrap_content"
                android:text="6"
                android:onClick="NumberButton"
                android:layout_weight="1"
                android:layout_margin="10dp"
                android:textSize="20dp"/>
        </TableRow>
        <TableRow>
            <Button
                android:layout_width="100dp"
                android:layout_height="wrap_content"
                android:text="1"
                android:onClick="NumberButton"
                android:layout_weight="1"
                android:layout_margin="10dp"
                android:textSize="20dp"/>
            <Button
                android:layout_width="100dp"
                android:layout_height="wrap_content"
                android:text="2"
                android:onClick="NumberButton"
                android:layout_weight="1"
                android:layout_margin="10dp"
                android:textSize="20dp"/>
            <Button
                android:layout_width="100dp"
                android:layout_height="wrap_content"
                android:text="3"
                android:onClick="NumberButton"
                android:layout_weight="1"
                android:layout_margin="10dp"
                android:textSize="20dp"/>
        </TableRow>
        <TableRow>
            <Button
                android:layout_width="100dp"
                android:layout_height="wrap_content"
                android:text="0"
                android:onClick="NumberButton"
                android:layout_weight="1"
                android:layout_margin="10dp"
                android:textSize="20dp"/>
            <Button
                android:layout_width="100dp"
                android:layout_height="wrap_content"
                android:text="+"
                android:onClick="op_button"
                android:layout_margin="10dp"
                android:layout_weight="1"
                android:textSize="20dp"/>
            <Button
                android:layout_width="100dp"
                android:layout_height="wrap_content"
                android:text="-"
                android:onClick="op_button"
                android:layout_weight="1"
                android:layout_margin="10dp"
                android:textSize="20dp"/>
        </TableRow>
        <TableRow>
            <Button
                android:layout_width="100dp"
                android:layout_height="wrap_content"
                android:text="*"
                android:onClick="op_button"
                android:layout_weight="1"
                android:layout_margin="10dp"
                android:textSize="20dp"/>
            <Button
                android:layout_width="100dp"
                android:layout_height="wrap_content"
                android:text="/"
                android:onClick="op_button"
                android:layout_weight="1"
                android:layout_margin="10dp"
                android:textSize="20dp"/>
        </TableRow>
        <TableRow>
            <Button
                android:layout_width="100dp"
                android:layout_height="wrap_content"
                android:text="C"
                android:onClick="clear"
                android:layout_weight="1"
                android:layout_margin="10dp"
                android:textSize="20dp"/>
            <Button
                android:layout_width="100dp"
                android:layout_height="wrap_content"
                android:text="="
                android:onClick="answer"
                android:layout_weight="1"
                android:layout_margin="10dp"
                android:textSize="20dp"/>
        </TableRow>
    </TableLayout>
</LinearLayout>
```



```
package com.example.calculator;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;

public class MainActivity extends AppCompatActivity {
    TextView txtResult;
    double first_num = 0;
    String operator = "";
    boolean isNew = true;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        EdgeToEdge.enable(this);
        setContentView(R.layout.activity_main);
        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {
            Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);
            return insets;
        });
        txtResult = findViewById(R.id.txtResult);
    }

    public void NumberButton(View view) {
        Button btn = (Button) view;
        txtResult.append(btn.getText().toString());
        isNew= false;
        if(isNew){
            txtResult.setText("");
        }
    }

    public void op_button(View view) {
        Button btn = (Button) view;
        first_num = Double.parseDouble(txtResult.getText().toString());
        operator = btn.getText().toString();
        isNew = true;
    }

    public void clear(View view) {
        txtResult.setText("0");
        first_num =0;
        operator = "";
        isNew = true;
    }

    public void answer(View view) {
        double second_num = Double.parseDouble(txtResult.getText().toString());
        double result = 0;
        switch (operator){
            case "+":
                result = first_num + second_num;
                break;
            case "-":
                result = first_num - second_num;
                break;
            case "*":
                result = first_num * second_num;
                break;
            case "/":
                if (second_num!=0){
                    result = first_num / second_num;
                }
                else{
                    txtResult.setText("Error");
                    return;
                }
                txtResult.setText(String.valueOf(result));
                isNew = true;
        }
    }
}
```






