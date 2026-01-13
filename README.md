# pyDBMS — Lightwork In-Memory User Database with Caching & Persistence

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

## Benchmarks(50 Iterations):

```python
Operation                   Count(Users)   Avg(s)     Min(s)     Max(s)    StdDev
_________________________________________________________________________________
Add Users                     100,000     0.4275     0.3687     2.2489     0.2632
Search Users by Name          100,000     0.1804     0.1690     0.2082     0.0086
Check Users by ID             100,000     0.0593     0.0542     0.0738     0.0038
Remove Users by ID            100,000     0.0565     0.0488     0.1737     0.0172
Remove Users by Name          100,000     0.0649     0.0563     0.1736     0.0161
Save Database                1,000,000    1.7574     1.3116     3.0439     0.4318
Backup Database              1,000,000    0.0384     0.0331     0.0454     0.0035
Load Database                1,000,000    5.1135     4.2678     6.5465     0.5048

```
