Chmod
===
| モード(数字) | モード(アルファベット) | 権限 |
| ----------- | -------------------- | ---- |
|4|r|読み取り|
|2|w|書き込み|
|1|x|実行|

#### ex)
```
chmod 755 파일명

유저(user)   : read 읽기(4) write 쓰기(2) execute 실행(1) = 4 + 2 + 1 = 7
그룹(group)  : read 읽기(4) write 쓰기(2) execute 실행(1) = 4     + 1 = 5
기타(other)  : read 읽기(4) write 쓰기(2) execute 실행(1) = 4     + 1 = 5
```