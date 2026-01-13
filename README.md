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

```

## Benchmarks:

```python
#Operation                     Count     Avg(s)     Min(s)     Max(s)     StdDev
________________________________________________________________________________
Add Users                    1000000     0.4277     0.3511     1.9118     0.2809
Search Users by Name           10000     0.0180     0.0162     0.0207     0.0011
Check Users by ID              10000     0.0055     0.0040     0.0063     0.0006
Remove Users by ID             10000     0.0053     0.0039     0.0188     0.0026
Remove Users by Name           10000     0.0056     0.0032     0.0191     0.0027
Save Database                1000000     2.5489     1.6052     3.9423     0.5457
Backup Database              1000000     0.0681     0.0469     0.4139     0.0666
Load Database                1000000     5.9910     4.7610     8.2773     0.7241

```
