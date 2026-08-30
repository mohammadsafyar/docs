# SQL Server Backup

## مقدمه

Backup یکی از مهم‌ترین بخش‌های نگهداری SQL Server است و باید به‌صورت منظم اجرا و به‌صورت دوره‌ای Restore آن تست شود.

## Full Backup

نمونه دستور برای گرفتن Full Backup:

```sql
BACKUP DATABASE [MyDatabase]
TO DISK = 'D:\SQLBackups\MyDatabase_FULL.bak'
WITH
    COMPRESSION,
    CHECKSUM,
    STATS = 10;
```

## بررسی Backup

برای بررسی Backupهای ثبت‌شده در SQL Server می‌توان از Query زیر استفاده کرد:

```sql
SELECT
    database_name,
    backup_start_date,
    backup_finish_date,
    type,
    backup_size
FROM msdb.dbo.backupset
ORDER BY backup_finish_date DESC;
```

## نکات مهم

* Backup باید طبق یک Schedule مشخص اجرا شود.
* فایل Backup باید روی Storage مناسب نگهداری شود.
* Backupها باید از نظر موفقیت بررسی شوند.
* Restore تستی باید به‌صورت دوره‌ای انجام شود.
* نگهداری Backup باید مطابق سیاست Retention سازمان باشد.
