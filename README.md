# Ansible Role: MySQL Community Server

Installs the Holland Backup Manager for RHEL/CentOS and Fedora.

## Requirements

On EL platforms, the EPEL respository is required.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    holland_plugin_dirs:                                /usr/share/holland/plugins
    holland_backup_directory:                           /var/spool/holland
    holland_backupsets:                                 default
    holland_umask:                                      "0007"
    holland_path:                                       "/usr/local/bin:/usr/local/sbin:/bin:/sbin:/usr/bin:/usr/sbin"
    holland_logging_filename:                           /var/log/holland/holland.log
    holland_logging_level:                              info
    holland_mysqldump_holland_mysqldump_mysql_binpath:  /usr/bin/mysqldump
    holland_mysqldump_lock_method:                      auto-detect
    holland_mysqldump_databases:                        "*"
    holland_mysqldump_exclude_databases:
    holland_mysqldump_tables:                           "*"
    holland_mysqldump_exclude_tables:
    holland_mysqldump_dump_routines:                    "no"
    holland_mysqldump_dump_events:                      "no"
    holland_mysqldump_stop_slave:                       "no"
    holland_mysqldump_bin_log_position:                 "no"
    holland_mysqldump_flush_logs:                       "no"
    holland_mysqldump_file_per_database:                "no"
    holland_mysqldump_additional_options:
    holland_mysqldump_compression_method:               gzip
    holland_mysqldump_compression_inline:               "yes"
    holland_mysqldump_compression_level:                1
    holland_mysqldump_compression_bin_path:             /usr/bin/gzip
    holland_mysqldump_client_defaults_extra_file:       "/root/.my.cnf,~/.my.cnf"
    holland_mysqldump_client_user:
    holland_mysqldump_client_password:
    holland_mysqldump_client_socket:
    holland_mysqldump_client_host:
    holland_mysqldump_client_port:

## Dependencies

None.

## Example Playbook

    - hosts: database
      roles:
        - rchouinard.holland-backup
      vars:
        holland_mysqldump_file_per_database: "yes"
        holland_mysqldump_compression_level: "3"
      tasks:
        - name: Configure Holland default backup set
          copy:
            dest: /etc/holland/backupsets/default.conf
            content: |
              [holland:backup]
              plugin = mysqldump
              backups-to-keep = 28
              purge-policy = after-backup
            mode: 0640

## License

MIT

## Author Information

This role was created in 2017 by [Ryan Chouinard](https://www.ryanchouinard.com/).
