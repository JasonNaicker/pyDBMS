# pyDBMS — High-Performance User Database with Caching & Persistence

A high-performance in-memory database for storing, managing, and persisting large numbers of User objects, with support for fast search, autosave, and file persistence.

---

## Overview

| Component | Purpose |
|-----------|---------|
| `User` | Immutable user object with `name`, `age`, `ID`, and optional `extras`. Supports serialization. |
| `DataBase` | In-memory storage for `User` objects with fast lookup by `ID` or `name`. |
| `FileManager` | Saves and loads the database to disk. Supports backups, autosave, and human-readable conversion. |
| Utility functions | Generate random users, names, and ages for testing large datasets. |

---

## User Example

```python

database = DataBase()
file_manager = FileManager(database=db, output_file="users_db.json", autosave_interval=5)
file_manager.save()                     # Save database to file
file_manager.backup("users_backup.json") # Backup
file_manager.load()                     # Load back into database
file_manager.start_autosave()           # Start autosave in background
file_manager.stop_autosave()            # Stop autosave
file_manager.convert_file("users_db.json", "readable_db.json")
