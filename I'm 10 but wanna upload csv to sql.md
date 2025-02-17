#dev #rm

The process described does **not** perform an update for each student individually. Instead, it uses **bulk operations** to handle all records in the uploaded file at once.

### **Step 1: Understand the Problem**

- You have a list of students in an Excel file who are "debarred" (not allowed to participate in something).
- You want to update your database with this list without running a separate query for every student. Running one query per student is slow and inefficient.

### **Step 2: Save the Excel File as CSV**

- Computers like working with CSV files because they are simple text files where data is separated by commas.
- Open your Excel file and save it as a `.csv` file (e.g., `debarred_students.csv`).

### **Step 3: Create a Temporary Table**

- Think of this as creating a "scratchpad" in the database where you can quickly dump all the data from your CSV file.
- Run this command in PostgreSQL to create the temporary table:

```sql
CREATE TEMP TABLE temp_debarred (
    studentId UUID,
    adminId UUID,
    reason TEXT,
    isActive BOOLEAN,
    createdAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

- This table will only exist while you're working on this task and will disappear after you're done.

### **Step 4: Load Data into the Temporary Table**

- Now, take all the data from your CSV file and dump it into this "scratchpad" table in one go. Use this command:

```sql
COPY temp_debarred(studentId, adminId, reason, isActive)
FROM '/path/to/debarred_students.csv'
DELIMITER ','
CSV HEADER;
```

- Replace `/path/to/debarred_students.csv` with the actual location of your file.
- This step is super fast because it loads everything at once.

### **Step 5: Update the Main Table in Bulk**

- Now that all your data is in the temporary table, you can update the main `Debarred` table efficiently using a single query. Here's how it works:
  - If a student is already in the `Debarred` table, update their information (like `reason`, `isActive`, etc.).
  - If a student is not already in the `Debarred` table, add them as a new record.

Run this query:

```sql
INSERT INTO Debarred (studentId, adminId, reason, isActive, createdAt, updatedAt)
SELECT studentId, adminId, reason, isActive, CURRENT_TIMESTAMP, CURRENT_TIMESTAMP
FROM temp_debarred
ON CONFLICT (studentId)
DO UPDATE SET
    adminId = EXCLUDED.adminId,
    reason = EXCLUDED.reason,
    isActive = EXCLUDED.isActive,
    updatedAt = EXCLUDED.updatedAt;
```

**How does this work?**

1. The `INSERT INTO ... SELECT ...` part tries to insert all rows from `temp_debarred` into the main `Debarred` table.
2. The `ON CONFLICT (studentId)` part checks if there’s already a record with the same `studentId`.
3. If there’s a conflict (the student already exists), it runs the `DO UPDATE` part to update their information.

This way, everything happens in one operation for all students.

### **Step 6: Clean Up**
- Once you're done updating the database, delete the temporary table to free up space:

```sql
DROP TABLE temp_debarred;
```

---

### **Why Is This Optimized?**

1. **Bulk Loading**: Instead of inserting or updating one row at a time, we load all rows into a temporary table at once.
2. **Single Query for Updates**: The `INSERT ... ON CONFLICT` query handles all updates and inserts in one go.
3. **No Repeated Operations**: We avoid running multiple queries for each student (which would be slow).

This approach minimizes database operations and speeds up the entire process significantly!
