"# backup" 
 Backup Script (backup.sh)

A powerful yet simple Bash-based backup automation script that lets you back up your project files, compress them, restore old backups, and maintain backup history — all in one place.

 Features

 Creates timestamped backups
 Supports compression (.tar.gz)
 Dry-run mode (preview actions)
 Backup only recently changed files
 List available backups
 Restore from any backup
 Keeps a limited number of old backups automatically
 Logs everything into backup.log and backup.txt
 Supports configuration via backup.conf

 Default Folder Structure
project-folder/
│
├── backup.sh          # The main script
├── backup.log         # Detailed log of all backup runs
├── backup.txt         # Output log for current session
├── backup.conf        # Optional configuration file
└── backups/           # Backup storage folder

 Configuration File (Optional)

You can create a backup.conf file in the same directory to customize defaults:

# backup.conf
BACKUP_DESTINATION="/path/to/your/backups"
EXCLUDE_PATTERNS=".git node_modules .cache temp"
DAILY_KEEP=7
WEEKLY_KEEP=4
MONTHLY_KEEP=3

 How to Use
 Make it executable
chmod +x backup.sh

 Run a full backup
./backup.sh


Backups will be created inside the backups/ folder by default.

 Available Options
Option	Description
--compress	Compress the backup into a .tar.gz archive
--dry-run	Preview what files will be backed up (no changes made)
--recent Xd	Backup only files modified in the last X days (e.g., --recent 2)
--list	List all available backups
--restore <file>	Restore a backup file
--to <path>	Destination folder for restore
--help	Show usage information
 Example Commands
 Run a basic backup
./backup.sh

 Run with compression
./backup.sh --compress

 Test the backup process without saving files
./backup.sh --dry-run

 Backup only files changed in the last 3 days
./backup.sh --recent 3

 List all available backups
./backup.sh --list

 Restore a backup
./backup.sh --restore backups/backup_2025-11-07_14-30-10.tar.gz --to ./restored

 How It Works

Creates a new folder in backups/ with the current date and time.

Copies or compresses all specified files (or all in data/ by default).

Logs progress into backup.txt and backup.log.

Optionally compresses the folder into .tar.gz.

Generates a sha256 checksum file for data integrity.

Deletes older backups beyond the set limit (KEEP_COUNT=5 by default).

 Example Output
[Fri, Nov 7, 2025 02:45:12 PM]  Starting backup...
[Fri, Nov 7, 2025 02:45:13 PM]  Backed up: data/file1.txt
[Fri, Nov 7, 2025 02:45:14 PM]  Compressed backup created: backup_2025-11-07_14-45-14.tar.gz
[Fri, Nov 7, 2025 02:45:15 PM]  Checksum file created: backup_2025-11-07_14-45-14.tar.gz.sha256
[Fri, Nov 7, 2025 02:45:15 PM]  Backup process completed successfully.

 Auto Cleanup

To prevent storage overflow, the script automatically keeps only the latest 5 backups (configurable via KEEP_COUNT in script).
