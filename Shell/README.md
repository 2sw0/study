Shell
===
### [Scp](./Scp/README.md)

### 현재 폴더의 폴더, 파일 확인
-a: .으로 시작하는 파일, 폴더를 포함하여 전체 파일 및 폴더를 출력   
-l: 퍼미션, 소유자, 만든 날짜, 용량까지 출력   
-h: 용량을 사람이 읽기 쉽도록 GB, MB 등으로 표현해 주며, -l과 같이 사용
```shell
ls -al
ls -lh
```

### 현재 폴더 경로(절대 경로)
```shell
pwd
```

### Shell Script 실행
```shell
bash 쉘파일
```

### 이동, 이름 변경
```shell
mv 이전파일명 이후파일명
```

### 최근 입력 Shell Command
```shell
history

!history num -> 해당 번호의 command 다시 활용 가능
```

### 콘솔 명령어 별칭 설정
```shell
alias 533='pwd'

533 입력 시 pwd 실행됨
```

### 하위 디렉토리 용량 확인
```shell
du -sh ./* | sort -r
```

### 현재 디렉토리 용량 확인
```shell
df -h
```

### 현재 디렉토리에 있는 파일의 크기를 크기순으로 나열
```shell
du -sk * | sort -nr
```

### 현재 디렉토리에 있는 파일의 크기를 나열
```shell
du -sk ./*
```

### 전체 용량
1. KB 단위
```sql
df -P | grep -v ^Filesystem | awk '{sum += $2} END { print sum " KB" }'
```
2. GB 단위
명령어
```sql
df -P | grep -v ^Filesystem | awk '{sum += $2} END { print sum/1024/1024 " GB" }'
```

### 전체 사용량
1. KB 단위
```sql
df -P | grep -v ^Filesystem | awk '{sum += $3} END { print sum " KB" }'
```
2. GB 단위
명령어
```sql
df -P | grep -v ^Filesystem | awk '{sum += $3} END { print sum/1024/1024 " GB" }'
```

### 전체 남은 용량
1. KB 단위
```sql
df -P | grep -v ^Filesystem | awk '{sum += $4} END { print sum " KB" }'
```
2. GB 단위
명령어
```sql
df -P | grep -v ^Filesystem | awk '{sum += $4} END { print sum/1024/1024 " GB" }'
```

### 리눅스 버전 확인 (3가지 방법)
```sql
1. grep . /etc/*-release
2. grep . /etc/issue*
3. rpm -qa *-release
```

### 리스너 시작되었는지 확인
```sql
lsnrctl status [리스너 이름]
```

### 리스너 가동
```sql
lsnrctl start [리스너 이름]
```

