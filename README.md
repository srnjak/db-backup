# Database Backup Script

A bash script that creates a backup of all databases specified in the configuration file. 
It is designed to be a general-purpose backup tool that can be used to back up any MariaDB or MySQL database with minimal configuration. 
The script is used to automate the backup process and can be scheduled to run at specific intervals, making it a useful tool for system administrators who want to ensure that their databases are backed up regularly.

## Features

- Backup one or more MariaDB or MySQL databases
- Store backups in a specified directory
- Log and track failed backups
- Easy to use and configure

## Prerequisites

- A Linux-based operating system (tested on Ubuntu 20.04 LTS)
- MySQL server installed
- Bash shell (default on most Linux-based operating systems)

## Usage

Syntax:

    db-backup [-c CONFIG_DIR][-r RETENTION_POLICY][-m] CONF_NAME
    db-backup -h

### Options

| Short option | Long option    | Description                                                                                                                                  | Default Value    |
|--------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------|------------------|
| `-c`         | `--config-dir` | The path to directory containing configurations.                                                                                             | `/etc/db-backup` |
| `-r`         | `--retention`  | Retention policy type. Possible values: daily, weekly, monthly, yearly. If set, the value will be used as a suffix in the subdirectory name. |                  |
| `-m`         | `--send-mail`  | Send an email notification after the backup is complete. If this flag is set, make sure to set the email address in the configuration file.  |                  |
| `-h`         | `--help`       | Print help message and exit.                                                                                                                 |                  |

## Configuration
Each configuration file should have a ".cfg" extension and contain the following variables:

- `DB_NAMES` - an array of database names to backup
- `DB_HOST` - the hostname or IP address of the database server
- `DB_PORT` - the port number of the database server
- `DB_USER` - the username to use when connecting to the database server
- `DB_PASSWORD` - the password to use when connecting to the database server
- `BACKUP_DIR` - the directory where the backups will be stored

## Installation

### Add `srnjak` apt source

To add the `srnjak` apt source to your system, follow these steps:

1. Update the package index:
    ```
    sudo apt-get update
    ```

2. Install the required packages:
    ```
    sudo apt-get install -y ca-certificates gnupg2 curl
    ```

3. Add the `srnjak` repository to your system's package sources:
    ```
    echo "deb https://ci.srnjak.com/nexus/repository/apt-release release main" | sudo tee /etc/apt/sources.list.d/srnjak.list
    ```

4. Add the repository's GPG key to your system's trusted keys:
    ```
    curl -sSL https://ci.srnjak.com/nexus/repository/public/gpg/public.gpg.key | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/srnjak.gpg
    ```

### Install `db-backup`

To install the `db-backup` package, follow these steps:

1. Update the package index again:
    ```
    sudo apt-get update
    ```

2. Install the `db-backup` package:
    ```
    sudo apt-get install -y db-backup
    ```
## Dependencies
The script uses the following dependencies:

- `gzip`
- `mailutils` (optional)

Note: The script will work without `mailutils`, but won't be able to send mail after the backup process is done. 
`gzip` is required for compressing and archiving the backup files.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
