# Ex-1_INSTALLING-AND-RUNNING-APPLICATIONS-ON-ANDROID-STUDIO
**Name:** SRI SRINIVASAN K

**Register Number:** 212224220104

**Department:** B.Tech Information Technology

## 1. AIM:
To develop an Android-based Student Management System using Java that allows users to add, edit, delete, and manage student details, attendance, and marks, while displaying average attendance and marks statistics.

## 2. SOFTWARE REQUIREMENTS:

1. Android Studio IDE
2. Java programming language
3. XML for user interface design
4. Android SDK
5. Android Emulator or Android mobile device
6. Windows operating system

## 3. ALGORITHM:
1. Start the application and initialize the main activity.
2. Load the main dashboard layout and initialize the UI components.
3. Create an ArrayList to store student details.
4. Display the initial student records in the RecyclerView.
5. Click the Add Student button to enter student details.
6. Validate the entered details and save the new student record.
7. Allow users to edit existing student details.
8. Allow users to delete student records when required.
9. Update student attendance and marks information.
10. Calculate the total number of students, average attendance, and average marks.
11. Display the updated statistics and student details on the dashboard.
12. Stop the application.

## 4. PROGRAM:
## A. XML Code – activity_main.xml
```JAVA
<?xml version="1.0" encoding="utf-8"?>
<androidx.coordinatorlayout.widget.CoordinatorLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <com.google.android.material.appbar.AppBarLayout
        android:id="@+id/appBarLayout"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <com.google.android.material.appbar.MaterialToolbar
            android:id="@+id/toolbar"
            android:layout_width="match_parent"
            android:layout_height="?attr/actionBarSize"
            app:title="@string/app_name"
            app:titleCentered="true" />
    </com.google.android.material.appbar.AppBarLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical"
        app:layout_behavior="@string/appbar_scrolling_view_behavior">

        <!-- Summary Dashboard Card -->
        <com.google.android.material.card.MaterialCardView
            android:id="@+id/cardDashboard"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_margin="12dp"
            app:cardCornerRadius="16dp"
            app:cardElevation="3dp"
            app:strokeWidth="0dp">

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:background="@color/primary"
                android:orientation="vertical"
                android:padding="16dp">

                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/dashboard_title"
                    android:textAppearance="?attr/textAppearanceTitleMedium"
                    android:textColor="@color/white"
                    android:textStyle="bold" />

                <LinearLayout
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:layout_marginTop="12dp"
                    android:baselineAligned="false"
                    android:orientation="horizontal">

                    <!-- Stat 1: Total Students -->
                    <LinearLayout
                        android:layout_width="0dp"
                        android:layout_height="wrap_content"
                        android:layout_weight="1"
                        android:gravity="center"
                        android:orientation="vertical">

                        <TextView
                            android:id="@+id/tvStatTotalStudents"
                            android:layout_width="wrap_content"
                            android:layout_height="wrap_content"
                            android:textColor="@color/white"
                            android:textSize="22sp"
                            android:textStyle="bold"
                            tools:text="5" />

                        <TextView
                            android:layout_width="wrap_content"
                            android:layout_height="wrap_content"
                            android:text="@string/total_students"
                            android:textColor="#E0E0E0"
                            android:textSize="12sp" />
                    </LinearLayout>

                    <!-- Stat 2: Avg Attendance -->
                    <LinearLayout
                        android:layout_width="0dp"
                        android:layout_height="wrap_content"
                        android:layout_weight="1"
                        android:gravity="center"
                        android:orientation="vertical">

                        <TextView
                            android:id="@+id/tvStatAvgAttendance"
                            android:layout_width="wrap_content"
                            android:layout_height="wrap_content"
                            android:textColor="@color/white"
                            android:textSize="22sp"
                            android:textStyle="bold"
                            tools:text="82.4%" />

                        <TextView
                            android:layout_width="wrap_content"
                            android:layout_height="wrap_content"
                            android:text="@string/avg_attendance"
                            android:textColor="#E0E0E0"
                            android:textSize="12sp" />
                    </LinearLayout>

                    <!-- Stat 3: Avg Marks -->
                    <LinearLayout
                        android:layout_width="0dp"
                        android:layout_height="wrap_content"
                        android:layout_weight="1"
                        android:gravity="center"
                        android:orientation="vertical">

                        <TextView
                            android:id="@+id/tvStatAvgMarks"
                            android:layout_width="wrap_content"
                            android:layout_height="wrap_content"
                            android:textColor="@color/white"
                            android:textSize="22sp"
                            android:textStyle="bold"
                            tools:text="78.5%" />

                        <TextView
                            android:layout_width="wrap_content"
                            android:layout_height="wrap_content"
                            android:text="@string/avg_marks"
                            android:textColor="#E0E0E0"
                            android:textSize="12sp" />
                    </LinearLayout>
                </LinearLayout>

            </LinearLayout>
        </com.google.android.material.card.MaterialCardView>

        <!-- RecyclerView for Student List -->
        <androidx.recyclerview.widget.RecyclerView
            android:id="@+id/recyclerViewStudents"
            android:layout_width="match_parent"
            android:layout_height="0dp"
            android:layout_weight="1"
            android:clipToPadding="false"
            android:paddingBottom="80dp"
            tools:listitem="@layout/item_student" />

    </LinearLayout>

    <!-- FAB to Add New Student -->
    <com.google.android.material.floatingactionbutton.ExtendedFloatingActionButton
        android:id="@+id/fabAddStudent"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="bottom|end"
        android:layout_margin="16dp"
        android:contentDescription="@string/add_student"
        android:text="@string/add_student"
        android:textColor="@color/white"
        app:backgroundTint="@color/primary"
        app:icon="@drawable/ic_person"
        app:iconTint="@color/white" />

</androidx.coordinatorlayout.widget.CoordinatorLayout>


```

## B. Java Code – MainActivity.java
```JAVA

package com.example.sample;

import android.os.Bundle;
import android.text.TextUtils;
import android.view.LayoutInflater;
import android.view.View;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AlertDialog;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;
import androidx.recyclerview.widget.LinearLayoutManager;
import androidx.recyclerview.widget.RecyclerView;

import com.google.android.material.floatingactionbutton.ExtendedFloatingActionButton;

import java.util.ArrayList;
import java.util.List;
import java.util.Locale;
import java.util.UUID;

public class MainActivity extends AppCompatActivity implements StudentAdapter.OnStudentActionListener {

    private final List<Student> studentList = new ArrayList<>();
    private StudentAdapter adapter;

    private TextView tvStatTotalStudents;
    private TextView tvStatAvgAttendance;
    private TextView tvStatAvgMarks;

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

        tvStatTotalStudents = findViewById(R.id.tvStatTotalStudents);
        tvStatAvgAttendance = findViewById(R.id.tvStatAvgAttendance);
        tvStatAvgMarks = findViewById(R.id.tvStatAvgMarks);

        RecyclerView recyclerView = findViewById(R.id.recyclerViewStudents);
        recyclerView.setLayoutManager(new LinearLayoutManager(this));

        populateInitialData();

        adapter = new StudentAdapter(studentList, this);
        recyclerView.setAdapter(adapter);

        ExtendedFloatingActionButton fabAddStudent = findViewById(R.id.fabAddStudent);
        fabAddStudent.setOnClickListener(v -> showStudentDialog(null));

        updateDashboardStats();
    }

    private void populateInitialData() {
        studentList.clear();
        studentList.add(new Student(UUID.randomUUID().toString(), "Alex Johnson", "CS202401", 30, 27, 18.5, 26.0, 44.0));
        studentList.add(new Student(UUID.randomUUID().toString(), "Sophia Martinez", "CS202402", 30, 22, 16.0, 21.5, 35.0));
        studentList.add(new Student(UUID.randomUUID().toString(), "Ethan Williams", "CS202403", 30, 28, 19.5, 28.5, 47.0));
        studentList.add(new Student(UUID.randomUUID().toString(), "Liam Brown", "CS202404", 30, 20, 12.0, 18.0, 29.0));
        studentList.add(new Student(UUID.randomUUID().toString(), "Emma Davis", "CS202405", 30, 25, 17.0, 24.0, 39.5));
    }

    private void updateDashboardStats() {
        int total = studentList.size();
        if (total == 0) {
            tvStatTotalStudents.setText("0");
            tvStatAvgAttendance.setText("0.0%");
            tvStatAvgMarks.setText("0.0%");
            return;
        }

        double sumAttendance = 0;
        double sumMarks = 0;

        for (Student s : studentList) {
            sumAttendance += s.getAttendancePercentage();
            sumMarks += s.getMarksPercentage();
        }

        double avgAttendance = sumAttendance / total;
        double avgMarks = sumMarks / total;

        tvStatTotalStudents.setText(String.valueOf(total));
        tvStatAvgAttendance.setText(String.format(Locale.US, "%.1f%%", avgAttendance));
        tvStatAvgMarks.setText(String.format(Locale.US, "%.1f%%", avgMarks));
    }

    @Override
    public void onAttendanceUpdated(Student student) {
        updateDashboardStats();
        Toast.makeText(this, "Updated attendance for " + student.getName(), Toast.LENGTH_SHORT).show();
    }

    @Override
    public void onEditRequested(Student student) {
        showStudentDialog(student);
    }

    private void showStudentDialog(Student existingStudent) {
        AlertDialog.Builder builder = new AlertDialog.Builder(this);
        View dialogView = LayoutInflater.from(this).inflate(R.layout.dialog_student, null);
        builder.setView(dialogView);

        TextView tvDialogTitle = dialogView.findViewById(R.id.tvDialogTitle);
        EditText etName = dialogView.findViewById(R.id.etStudentName);
        EditText etRoll = dialogView.findViewById(R.id.etRollNumber);
        EditText etAttended = dialogView.findViewById(R.id.etAttendedClasses);
        EditText etTotal = dialogView.findViewById(R.id.etTotalClasses);
        EditText etAssignment = dialogView.findViewById(R.id.etAssignmentMarks);
        EditText etMidterm = dialogView.findViewById(R.id.etMidtermMarks);
        EditText etFinal = dialogView.findViewById(R.id.etFinalMarks);

        if (existingStudent != null) {
            tvDialogTitle.setText(R.string.edit_student);
            etName.setText(existingStudent.getName());
            etRoll.setText(existingStudent.getRollNumber());
            etAttended.setText(String.valueOf(existingStudent.getAttendedClasses()));
            etTotal.setText(String.valueOf(existingStudent.getTotalClasses()));
            etAssignment.setText(String.valueOf(existingStudent.getAssignmentMarks()));
            etMidterm.setText(String.valueOf(existingStudent.getMidtermMarks()));
            etFinal.setText(String.valueOf(existingStudent.getFinalMarks()));
        } else {
            tvDialogTitle.setText(R.string.add_student);
        }

        builder.setPositiveButton(R.string.save, (dialog, which) -> {
            String name = etName.getText().toString().trim();
            String roll = etRoll.getText().toString().trim();

            if (TextUtils.isEmpty(name)) {
                Toast.makeText(this, "Student Name is required", Toast.LENGTH_SHORT).show();
                return;
            }

            int attended = parseOrDefaultInt(etAttended.getText().toString(), 0);
            int totalClasses = parseOrDefaultInt(etTotal.getText().toString(), 1);
            double assignment = parseOrDefaultDouble(etAssignment.getText().toString(), 0);
            double midterm = parseOrDefaultDouble(etMidterm.getText().toString(), 0);
            double finalMarks = parseOrDefaultDouble(etFinal.getText().toString(), 0);

            if (existingStudent != null) {
                existingStudent.setName(name);
                existingStudent.setRollNumber(roll);
                existingStudent.setTotalClasses(totalClasses);
                existingStudent.setAttendedClasses(attended);
                existingStudent.setAssignmentMarks(assignment);
                existingStudent.setMidtermMarks(midterm);
                existingStudent.setFinalMarks(finalMarks);

                int index = studentList.indexOf(existingStudent);
                if (index != -1) {
                    adapter.notifyItemChanged(index);
                }
                Toast.makeText(this, "Updated " + name, Toast.LENGTH_SHORT).show();
            } else {
                Student newStudent = new Student(
                        UUID.randomUUID().toString(),
                        name,
                        roll,
                        totalClasses,
                        attended,
                        assignment,
                        midterm,
                        finalMarks
                );
                studentList.add(newStudent);
                adapter.notifyItemInserted(studentList.size() - 1);
                Toast.makeText(this, "Added student " + name, Toast.LENGTH_SHORT).show();
            }

            updateDashboardStats();
        });

        if (existingStudent != null) {
            builder.setNeutralButton(R.string.delete_student, (dialog, which) -> {
                int index = studentList.indexOf(existingStudent);
                if (index != -1) {
                    studentList.remove(index);
                    adapter.notifyItemRemoved(index);
                    updateDashboardStats();
                    Toast.makeText(this, "Deleted student " + existingStudent.getName(), Toast.LENGTH_SHORT).show();
                }
            });
        }

        builder.setNegativeButton(R.string.cancel, (dialog, which) -> dialog.dismiss());
        builder.create().show();
    }

    private int parseOrDefaultInt(String val, int def) {
        try {
            return Integer.parseInt(val.trim());
        } catch (Exception e) {
            return def;
        }
    }

    private double parseOrDefaultDouble(String val, double def) {
        try {
            return Double.parseDouble(val.trim());
        } catch (Exception e) {
            return def;
        }
    }
}

```
## PROCEDURE:
1. Create a new Android project in Android Studio using Java.
2. Design the main dashboard using XML layouts.
3. Create a Student class to store student details and marks.
4. Create a StudentAdapter class to display student records using RecyclerView.
5. Initialize UI components and student records in MainActivity.
6. Implement the Add Student feature using an AlertDialog.
7. Implement Edit and Delete operations for student records.
8. Calculate attendance and marks percentages.
9. Update dashboard statistics whenever student details change.
10. Run and test the application on an Android emulator or device.

## OUTPUT:

<img width="1920" height="1200" alt="Screenshot (93)" src="https://github.com/user-attachments/assets/fa245b79-8b1b-4d05-b951-72c5edcbffa4" />


## RESULT:

Thus, the Student Management System was developed successfully to manage student details, attendance, and marks efficiently.
