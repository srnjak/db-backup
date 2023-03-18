# Database Backup Script

This script is a bash script for automating MySQL database backups. It allows you to backup one or more databases to a specified directory, while also keeping a specified number of backups and deleting older backups. Additionally, it provides a summary of which databases were successfully backed up and which ones failed.

## Features

- Backup one or more MySQL databases
- Store backups in a specified directory
- Keep a specified number of backups and delete older backups
- Log and track failed backups
- Easy to use and configure

## Prerequisites

- A Linux-based operating system (tested on Ubuntu 20.04 LTS)
- MySQL server installed
- Bash shell (default on most Linux-based operating systems)

## Getting Started

1. Clone the repository to your local machine:

    ```
    git clone https://github.com/srnjak/db-backup-tool.git
    ```

2. Navigate to the repository directory:

    ```
    cd db-backup-tool
    ```

3. Modify the configuration files in the `/etc/db-backup` directory to match your MySQL server settings and backup preferences. The directory containing configurations might also be configured.

4. Run the script with the following command:

    ```
    ./backup.sh [--retention [daily/weekly/monthly/yearly]] [config_name]
    ```

    The `config_name` argument is optional. If not specified, the script will run all configuration files in the `/etc/db-backup` directory.

    The `--retention` switch is optional. If specified, it accepts one of the following values as an argument: `daily`, `weekly`, `monthly`, `yearly`. This argument will be used as a suffix in the subdirectory name. The retention option allows you to specify which retention policy to apply. This determines when and which old backups should be deleted.

5. Check the output to verify that the backups completed successfully.

## Configuration

Each configuration file in the `config/` directory represents a set of databases to be backed up. The configuration files are Bash shell scripts that define several variables:

- `BACKUP_DIR`: The directory where backups will be stored.
- `BACKUP_SUBDIR_PREFIX`: The prefix to use for the backup subdirectory name.
- `DB_NAMES`: An array of MySQL database names to backup.
- `DB_HOST`: The hostname or IP address of the MySQL server.
- `DB_PORT`: The port number of the MySQL server.
- `DB_USER`: The username for the MySQL server.
- `DB_PASSWORD`: The password for the MySQL server.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
