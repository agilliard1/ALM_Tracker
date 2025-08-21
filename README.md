# ALM Meta Data Manager

The ALM Meta Data Manager is a Python desktop application for managing and auditing the metadata associated with DAC International ALM optical turning lathes.
It provides a SQLite database backend with a Tkinter GUI for editing, versioning, and exporting metadata in a controlled and auditable way.

Every edit creates a new version of a record, preserving full history with timestamps and Windows user IDs. This ensures traceability of all metadata changes.

## Features

- **Append-only audit log**
  Every update creates a new row in the database with:

  - entity_id (the identifier for the record)
  - metadata fields (stored as JSON)
  - updated_at (timestamp in UTC)
  - updated_by (Windows user ID)
- **Graphical User Interface (GUI)**

  - Edit metadata for any ID in JSON form
  - View all IDs with their most current data
  - Browse historical versions of each ID
  - Search for IDs quickly
- **CSV Export**

  - Current Snapshot: exports only the latest version of each ID
  - Full Audit Log: exports all historical versions for all IDs
- **JSON Import/Export**

  - Load metadata for an ID from a JSON file
  - Save metadata from the editor to a JSON file

## Requirements

- Python 3.10+
- Standard library modules only (sqlite3, tkinter, json, etc.) — no external dependencies

On Windows, Tkinter is included with Python by default.

## Installation

1. Clone or copy this repository to your local machine.
2. Ensure you have Python installed (3.10 or newer recommended).
3. Place the script in a working folder, e.g.:

```bash
alm_meta_data_tracker.py
```

When first run, the app will create a SQLite database file if not already present:

```bash
records.sqlite3
```

## Usage

Run the app from the command line:

```bash
python alm_meta_data_tracker.py
```

This opens the ALM Meta Data Manager GUI.

### Adding a New ID

1. Click New ID in the left panel.
2. Enter the ID (e.g., a part number, work order, or metadata reference).
3. Edit the JSON structure in the editor pane.

Example:

```json
{
  "Name": "ALM01",
  "Asset ID": "45452",
  "SN": "A0704009",
  "ALM Software Ver.": "5.440.6",
  "OS": "Windows 10 Enterprise LTSC 32-Bit",
  "OS Ver.": "1809",
  "PC Name": "DACINTL-P6RLJ6L"
}
```

4. Click Save New Version.

A new row will be added to the database with timestamp and user ID.

### Editing Existing IDs

- Select an ID from the left-hand list.
- The most recent version will load into the editor.
- Modify fields as needed and click Save New Version.
- A new row is created; history is preserved.

### Viewing History

- Select an ID, then click History.
- A window shows all past versions (with timestamps and users).
- You may load any historical version into the editor to review or base new changes on.

### Current View

- Click Current View to see all IDs with their most recent data.

### Exporting to CSV

- From the File menu:
  - Export Current Snapshot to CSV → saves one row per ID (latest).
  - Export Full Audit Log to CSV → saves all versions of all IDs.

### Importing/Exporting JSON

- Load JSON File... → replace editor contents with a JSON file.
- Save JSON File... → save the current editor contents to a JSON file.

## Database Structure

SQLite table: records


| Column     | Type | Description                                  |
| ------------ | ------ | ---------------------------------------------- |
| id         | INT  | Auto-increment primary key                   |
| entity_id  | TEXT | ID for the record (e.g., lens or order code) |
| data_json  | TEXT | Metadata stored as JSON                      |
| updated_by | TEXT | Windows user ID of who made the change       |
| updated_at | TEXT | UTC timestamp of the change                  |

## Notes

- Audit Integrity: No data is overwritten; each edit creates a new version.
- Windows User ID is detected automatically using the environment (USERNAME).

## Maintainer
Internal Use Only - Not for External Distribution Please contact the X-Cel Specialty Contacts for support or deployment instructions.

## License
This project is proprietary and intended for internal use only at X-Cel Specialty Contacts.