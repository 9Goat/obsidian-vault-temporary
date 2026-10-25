# Syntax

```bash
hadoop fs -<command> [options] <path>
```

# Commands

| Command  | Description                      | Example                                     |
| -------- | -------------------------------- | ------------------------------------------- |
| `-ls`    | List files/directories           | `hadoop fs -ls /user`                       |
| `-mkdir` | Create directory                 | `hadoop fs -mkdir /data`                    |
| `-put`   | Upload file from local to HDFS   | `hadoop fs -put local.txt /data/`           |
| `-get`   | Download file from HDFS to local | `hadoop fs -get /data/file.txt`             |
| `-cat`   | Display file content             | `hadoop fs -cat /data/file.txt`             |
| `-cp`    | Copy file within HDFS            | `hadoop fs -cp /data/a.txt /backup/`        |
| `-mv`    | Move/rename file                 | `hadoop fs -mv /data/old.txt /data/new.txt` |
| `-rm`    | Delete file                      | `hadoop fs -rm /data/file.txt`              |
| `-rm -r` | Delete directory recursively     | `hadoop fs -rm -r /data/old/`               |
| `-chmod` | Change permissions               | `hadoop fs -chmod 755 /data/file`           |
| `-chown` | Change owner                     | `hadoop fs -chown user:group /data`         |

