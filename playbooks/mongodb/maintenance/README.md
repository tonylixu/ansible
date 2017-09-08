### Backup
```bash
$ sudo mongodump --db newdb --out /var/backups/mongobackups/`date +"%m-%d-%y"`
```

### Restore
```bash
$ sudo mongorestore --db newdb --drop /var/backups/mongobackups/01-20-16/newdb/
```
