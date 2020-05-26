# mac-cpu-recorder
A small 10 mint bash disaster to record the top 10 %CPU for a MacOS issue. 

## Requierments

 - sqlite3
 - bash
 - awk

### Create the DB

```
sqlite3 proc.db "create table proc (date text,USER text,PID int, CPU real,MEM real, VSZ int, RSS
int, STAT text,COMMAND text)"
```

### Run colection

```
while true ; do ps aux | sort -rnk 3,3 | head -n 10 |  awk -v date=$(date "+%Y-%m-%dT%H:%M:%S")
'{system("sqlite3 proc.db \x22INSERT INTO proc VALUES
(\x27"date"\x27,\x27"$1"\x27,"$2","$3","$4","$5","$6",\x27"$8"\x27,\x27"$11$12"\x27\)\x22")}'; sleep
60;done
```
