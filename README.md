# TodoApp

### Description

It is a simple Java-based Android app that makes it easy to manage what needs to be done.

___


### Main Concepts with source codes

- RecyclerView & ViewHolder
- ItemTouchHelper
```java
    @Override
    public void onSwiped(@NonNull RecyclerView.ViewHolder viewHolder, int direction) {

        final int position = viewHolder.getBindingAdapterPosition();
        if (direction == ItemTouchHelper.RIGHT) {
            AlertDialog.Builder builder = new AlertDialog.Builder(adapter.getContext());
            builder.setTitle("Delete Task");
            builder.setMessage("Are you sure to delete this task?");
            builder.setPositiveButton("Yes", (dialog, which) -> adapter.deleteTask(position));
            builder.setNegativeButton("Cancel", (dialog, which) -> adapter.notifyItemChanged(position));
            AlertDialog dialog = builder.create();
            dialog.show();
        } else {
            adapter.editItem(position);
        }
    }
```
- SQLiteDatabase CRUD operation
```java
    public void insertTask(ToDoModel model) {
        db = this.getWritableDatabase();
        ContentValues values = new ContentValues();
        values.put(COL_2, model.getTask());
        values.put(COL_3, 0);

        db.insert(TABLE_NAME, null, values);
    }

    public void updateTask(int id, String task) {
        db = this.getWritableDatabase();
        ContentValues values = new ContentValues();
        values.put(COL_2, task);

        db.update(TABLE_NAME, values, "ID=?", new String[]{String.valueOf(id)});
    }

    public void updateStatus(int id, int status) {
        db = this.getWritableDatabase();
        ContentValues values = new ContentValues();
        values.put(COL_3, status);

        db.update(TABLE_NAME, values, "ID=?", new String[]{String.valueOf(id)});
    }

    public void deleteTask(int id) {
        db = this.getWritableDatabase();
        db.delete(TABLE_NAME, "ID=?", new String[]{String.valueOf(id)});
    }
```
- SimpleCallback

### Development Environments

- <em>Java</em>
- Android Studio (2021.1.1 Patch 3 for Windows 64-bit)
- Android Emulator (Samsung Galaxy S21 6.2 inches, 1080 x 2600 resolution)
- SDK API 26: Android 8.0 (Oreo)

___


### Output

![todoApp](https://user-images.githubusercontent.com/96518885/167192796-9e53997b-6ea9-41d4-98cf-7d852b11dbb9.gif)
