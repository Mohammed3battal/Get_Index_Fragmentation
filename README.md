## Script: Get_Index_Fragmentation

**Description**:
This script analyzes index fragmentation for both a single database and all user databases on the SQL Server instance. It helps identify fragmented indexes that may benefit from reorganization or rebuild to improve performance.

---

### 🔹 Single Database Version:
- Scans the current database using `sys.dm_db_index_physical_stats`.
- Returns index fragmentation data for:
  - Table name
  - Schema name
  - Index name
  - Average fragmentation percentage
  - Page count
- Excludes system tables and system indexes.
- Output is sorted by `avg_fragmentation_in_percent DESC`.

---

### 🌐 All Databases Version:
- Loops through all **online user databases** using a cursor.
- Dynamically builds and executes a cross-database fragmentation query.
- Uses `SAMPLED` mode for performance (adjustable to `DETAILED` if needed).
- Returns:
  - `DatabaseName`
  - `SchemaName`
  - `TableName`
  - `IndexName`
  - `IndexType` (Clustered, Non-clustered, XML, Spatial)
  - `AvgFragmentationPercent`
  - `FragmentCount`
  - `PageCount`
- Sorts the output by `AvgFragmentationPercent DESC`.

---

### Use Case:
- Schedule and prioritize index maintenance jobs.
- Identify heavily fragmented indexes to REBUILD or REORGANIZE.
- Improve overall SQL Server I/O and query performance.

---

### ⚙️ Requirements:
- SQL Server 2005 or later.
- `VIEW SERVER STATE` permission required.
- Access to all user databases.

---

### 🔐 Notes:
- System databases (`master`, `model`, `msdb`, `tempdb`) are excluded.
- Heaps (index_id = 0) are excluded from the results.
- Fragmentation thresholds (e.g. >10%, >30%) are not enforced in this script but can be added.


