Šī ir versija 2.0
Maksims Jevharitskis
# Label; MountPoint; TotalSize (MB); Used (%)
partitions = [
    "System;/;50000;85",
    "Data;/home;150000;40",
    "Cache;/tmp;5000;10",
    "Backup;/mnt/backup;500000;92",
    "USB-Drive;/media/usb;16000;0",
    "Logs;/var/log;10000;95",
    "Database;/var/lib/mysql;80000;70",
    "Shared;/mnt/shared;200000;15",
    "Win-System;/mnt/win;100000;90",
    "Recovery;/recovery;2000;98"
]
print ("Partition nosaukums:")

for p in partitions:
    label = p.split(",")[0]
    print (label)
$w = Get-WinEvent -LogName Application | Where-Object {
    $_.LevelDisplayName -eq "Warning" -and $_.TimeCreated -gt (Get-Date).AddDays(-3)
}

$path = "$env:USERPROFILE\Documents\Warnings.txt"

$w | Out-File $path

$w | Group-Object ProviderName | Sort Count -Descending | Select -First 3 |
Out-File $path -Append
