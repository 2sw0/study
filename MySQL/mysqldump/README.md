### Export
```
mysqldump -u[사용자아이디] -p 데이터베이스명 [테이블명] > 저장될 파일명 
ex) mysqldump -u root -p --all-databases > alldb.sql
```

### Import
```
mysql -u[사용자아이디] -p [디비명] < 덤프파일명 
ex) mysql -u root -p < alldb.sql
```

### 直接S3にバックアップ
```
例）mysqldump -u 유저명 -p -h 엔드포인트 --default-character-set=문자포맷 --all-databases | aws s3 cp - s3://위치/파일명.dmp
例）mysqldump -u 유저명 -p --default-character-set=문자포맷 --databases 스키마명 | aws s3 cp --expected-size=예상사이즈(byte) - s3://위치/파일명.dmp
```


### dump命令
```
1. mysqldump [options] db_name [table_name ...]
: 하나의 databse안에 tables를 dump 합니다.


2. mysqldump [options] --databases db_name ...
: 하나의 Instance안의 여러 databases를 dump 합니다.

 
3. mysqldump [options] --all-databases
: 전체를 전부 다 dump 합니다.
```
### Options
#### 接続options
```
--host=host name, -h host name
: 접속 하려는 서버의 host 정보를 입력 합니다. default값은 localhost 입니다.

--password[=password], -p[password]
: 접속 하려는 서버의 user의 패스워드를 입력 합니다.

--port=port num,-P port num
: 접속하려는 서버의 port를 지정 합니다.

--socket=path, -S path
: localhost로 접속하려는 경우 접속에 사용할 소켓 파일을 지정합니다.

--user=user name, -u user name
: 접속하려는 서버의 user명을 기술 합니다.
```

#### DDL_options
```
--events, -E
: dump 파일에 이벤트관련 정보도 같이 dump받게 합니다.

--ignore-table=dbname.tbl name
: 백업 받지 않을 테이블을 명시합니다. 여러 번 사용이 가능합니다.

--no-data, -d
: 데이터를 입력하지 않습니다. create 구문을 전부 제외 합니다.

--routines, -R
: stored routines 정보를 모두 포함하여 dump 합니다.

--triggers
: 트리거 정보를 모두 포함하여 dump 합니다.

--where='where condition', -w'where condition'
: 데이터를 dump할 때 where구문에 맞는 데이터만 dump받고 싶은 경우에 사용합니다.

--add-drop-database
: Create database 구문 전에 Drop database구문을 추가 합니다.

--add-drop-table
: Create table 구문 전에 drop table 구문을 추가 합니다.

--add-drop-trigger
: Create trigger 구문 전에 drop trigger 구문을 추가 합니다.

--create-options
: Create table구문 안에 모든 테이블 옵션을 추가 합니다.

--no-create-db,-n
: Create database구문을 추가하지 않습니다.

--no-create-info, -t
: Create table구문을 작성하지 않습니다.

--replace
: insert 구문 대신에 replace 구문을 사용하여 insert하게 설정합니다.
```

#### DATA_options
```
--events, -E
: dump 파일에 이벤트 관련 정보도 같이 dump 받게 합니다.

--ignore-table=dbname.tbl name
: 백업 받지 않을 테이블을 명시합니다. 여러 번 사용 가능합니다.

--no-data, -d
: 데이터를 입력하지 않습니다.

--routines, -R
: stored routines 정보를 모두 포함하여 dump 합니다.

--triggers
: 트리거 정보를 모두 포함하여 dump 합니다.

--where='where condition', -w'where condiiton'
: 데이터를 dump 할 때 where 구문에 맞는 데이터만 dump 받고 싶은 경우에 사용 합니다.
```

#### 性能
```
--delayes-insert
: 트랜잭션을 지원 하지 않는 테이블(MyISAM)과 같은 테이블을 위한 지원 옵션 입니다. INSERT 대신 INSERT_DELAYED를 사용하도록 dump 파일을 작성 합니다.

--disable-keys, -K
: 테이블의 Insert 구문을 작성할 때 /*!40000 ALTER TABLES tbl_name DISABLE KEYS */; /*!40000 ALTER TABLE tbl_name ENABLE KETS */;를 추가하여 작성하게 합니다.
로딩할 때 Key에 대한 제약사항을 체크하지 않게 하여 좀 더 빨리 로딩될 수 있게 합니다. 이 옵션은 nonunique index를 사용하는 MyISAM테이블인 경우 효과가 좋습니다

--extended-insert, -e
: 여러 데이터를 한 문장의 insert문으로 insert되도록 구문을 작성 합니다.

--insert ignore
: dump파일 작성시 Insert 대신에 Insert Ignore 구문을 사용하도록 작성 됩니다.

--opt
: -add-drop-table, --add-locks, --create-options, --disable-keys, --extended-insert, --lock-tables, --quick, --set-charset의 기능을 하는 옵션으로 
일반적으로 dump받을 때 사용하는 옵션입니다. 사람들이 가장 많이 사용하는 옵션들을 모아 놓은 것입니다. 
이 옵션은 default로 명시하지 않아도 사용됩니다. 만약 사용하고 싶지 않다면 skip-opt를 사용하면 됩니다.

--quick, -q
: 이 옵션은 mysqldump 실행 시 데이터를 메모리에 로딩하지 않고 직접 읽어서 작성하게 하여 성능을 향상 시킬 수 있는 옵션 입니다.

--skip-opt
: --opt 옵션을 사용하고 싶지 않은 경우 사용합니다. 대부분의 MySQL 5.x는 --opt 옵션이 default로 enable 되어 있습니다.
```

#### Transaction_options
```
--add-locks
: dump 작성시 각 테이블의 앞 뒤에 LOCK TABLES와 UNLOCK TABLES 구문을 삽입합니다. 이렇게 하면 리로드 성능이 향상 됩니다.

--flush-logs, -F
: dump 작업을 시작하기 전에 MySQL의 lgo file들을 flush 합니다. 이 옵션은 RELOAD권한이 있어야 실행할 수 있습니다. 
--all-databases옵션과 같이 사용하는 경우 각 database를 dump 할때 마다 flush가 일어나게 되고, 
--lock-all-tables, --master-data, --single-transaction과 같이 실행되는 경우 정확히 같은 순간에 flush와 dump가 같이 일어나게 됩니다.

--flush-privileges
: mysql database를 dump한 후 dump파일에 FLUSH PRIVILEGES구문이 추가 됩니다.

--lock-all-tables, -x
: 모든 database의 table들을 모두 lock 합니다. dump가 진행되는 동안 global read lock을 실행합니다. 
이 옵션은 --single-transaction 과 --lock-table 옵션을 동시에 사용하는 경우 자동적으로 disable 시킵니다.

--lock-tables, -l
:각각의 database가 dump되는중 dump하기 전 대상 테이블들을 모두 lock합니다. MyISAM테이블의 경우 concurrent insert를 하기 위해 READ LOCAL로 lock을 겁니다.
만약 InnoDB와 같은 트랜잭션을 지원하는 테이블인 경우 --single-transaction 옵션을 사용해야 합니다. 트랜잭션을 지원하는 테이블은 굳이 이 옵션을 사용하지 않아도 됩니다. 
이 옵션은 database별로 각각 lock tables를 진행하기 때문에 전체 스냅샷은 지원하지 않습니다. 즉, 각각의 database는 각각 다른 시점의 데이터를 가지고 있게 되는 것입니다.
--opt 옵션을 사용하게 되면 자동적으로 --lock-tables도 enable된다. 그래서 원치 않는 경우 --skip-lock-tables를 option list의 가장 마지막에 작성하면 됩니다.

--no-autocommit
:각각의 dump되는 table의 앞 뒤에 SET autocommit=0 과 COMMIT 구문을 넣어 작성 합니다.

--order-by-primary
: 데이터를 primary key 또는 가장 첫 번째 unique index에 맞게 정렬되어 작성됩니다. 이것은 MyISAM이나 InnoDB에서 유용하게 사용 됩니다. 
하지만, dump 작업은 시간이 더 오래 걸릴 수 있습니다.

--single-transaction
: dump를 하기 전에 transaction isolaton level을 REPEATABLE READ로 변경하고, START TRANSACTION을 실행하게 합니다. 
이것은InnoDB와 같은 트랜잭션을 지원하는 테이블을 dump하기에 좋습니다. 이는 block 없이 snapshot 데이터를 dump 할 수 있도록 합니다. 
이 옵션은 InnoDB만 snapshot이 가능합니다. 이 옵션을 사용하여 dump하는 동안 적법한 dump 파일을 만들기 위해, 다른 접속을 통해 DDL작업을 진행해서는 안됩니다. 
또한 이 옵션은 --lock -tables와 같이 사용되어서는 안됩니다. 데이터의 크기가 크다면 --quick 옵션을 추가하여 사용하도록 합니다.
```

#### 出力_formet_options
```
--compact
: 이 옵션은 다음의 옵션들을 enable 합니다.
--skip-add-drop-table, --skip-add-locks, --skip-comments, --skip-disable-keys, --skip-set-charset

--compatible=name
: 이 옵션은 다른 DBMS나 MySQL 이전 버전에 맞게 dump 파일을 만들고자 하는 경우 사용 합니다.
MySQL : mysql323, mysql40
다른 DBMS : postgresql, oracle, mssql, db2, maxdb
그 외 : ansi, no_key_options, no_table_options, no_field_options
여러 값들을 사용하기 위해, 콤마로 구분하여 사용할 수 있습니다. 이 옵션을 사용함으로서 호환성이 보장되는 것은 아니고 호환성을 높여줄 수 있습니다.

--complete-insert, -c
: INSERT 구문 작성시 컬럼 이름을 전부 포함하여 작성하도록 합니다.

--hex-blob
: BINARY, VARBINARY, BLOB, BIT 컬럼에 대해서 값을 명시할 때 hexadecimal 형태로 기술하게 합니다.

--quote-names, -O
: 식별자를 "'"를 사용하여 모두 감쌉니다. 만약, ANSI_QUOTES SQL MODE인 경우네는 """를 사용하여 감쌉니다. enable 이 기본 입니다.
```

#### Replication Options
```
--apply-slave-statements
: --dump-slave옵션과 같이 dump하는 경우에 STOP SLAVE와 CHANGE MASTER TO 구문과 START SLAVE 구문이 같이 작성됩니다.

--delete-master-logs
: master서버인 경우 dump받은 후 바이너리 로그는 모두 삭제합니다. 이 옵션은 자동적으로 --master-data를 활성화 합니다.

--dump-slave[=value]
: 이 옵션은 --master-data 옵션과 비슷한데, 또 다른 slave서버를 만들기 위해 slave서버를 dump한다는 것만 다릅니다. 
이 옵션은 CHANGE MASTER TO 구문을 dump파일에 추가하게 됩니다. 이 옵션은 --master-data 옵셔노가 같은 방법으로 사용 됩니다.

--master-data[=value]
: dump받은 파일이 어느 바이너리로그의 위치까지 사용한 것인지 내용을 dump파일 안에 change master 구문의 형태로 작성 됩니다. 
Value는 1 또는 2로 작성할 수 있으며 default는 1입니다. 1과 2의 차이는 commnet로 적히느라 아니냐의 차이 입니다. 
2로 지정할 경우 comment로 남습니다. 이 옵션은 RELOAD 권한을 가지고 있어야 하고, binary log는 enable되어 있어야 합니다. 
만약 binary log를 enable 하지 않고 이 옵션을 사용한다면 에러가 발생하게 됩니다. --master-data 옵션은 자동적으로 --lock-tables 옵션을 disable합니다. 
--single-transaction 옵션을 명시했더라도, --lock-all-tables가 enable 됩니다. 
이때, global read lock은 아주 짧은 시간에만 동작하게 되고, 그것은 dump를 시작할 때 잠깐 일어나게 됩니다.

--set-qtid-purqed=value
: 이 옵션을 사용하면 global transaction ID(GTID)정보를 dump file에 기술 합니다. SET 구문을 사용하여 SET @@global.gtid purged 구문으로 작성됩니다. 
기본값은 AUTO이고 다음과 같이 3가지 값 중 하나를 선택할 수 있습니다.
  OFF : Add no SET statement to the output.
  ON : Add a SET statement to the output. An error occurs if GTIDs are not enabled on the server.
  AUTO : Add a SET statement to the output if GTIDs are enabled on the server.
```

#### その他options
```
--default-character-set=charset name
: 기본 character set으로 charset_name을 사용하도록 설정합니다. default는 utf8로 사용 됩니다.

--no-set-names, -N
: --set-names 옵션을 disable 합니다.

--set-charset
: SET NAMES default_char_set을 기술 합니다.

--help, -?
: 도움말을 보여 줍니다.

--version, -V
: 버전 정보를 보여 줍니다.

--verbose, -v
: Verbose 모드로 이 프로그램의 정보를 자세히 보여 줍니다.

--force, -f
: 에러가 발생해도 계속 작업이 진행되게 합니다.

--dump-date
: dump 파일의 생성 일자를 comment로 추가합니다.

--comments
: dump 파일에 추가적인 정보를 기술 합니다.

--allow-keywords
: 컬럼 이름으로 keyword를 사용하는 것을 허용 합니다.
```

### 関連variables
``` 
--max_allowed_packet=2G
: client와 server 사이의 buffer의 max size를 결정하는 variable인데, 이 값은 MySQL과 mysqldump간에도 적용 됩니다. 
dump시에 큰 데이터를 받아야 하는 경우 이 variable의 값을 크게 늘려 줘야 합니다. (最大2Gだった)

net_buffer_length
: 이 variable은 client와 server 사이의 buffer의 initial size를 결정하는 variable이다. 
이 variable은 여러 데이터를 하나의 INSERT 구문으로 작성하고자 하는 경우 늘려줘야 합니다.
```

### 例
```
mysqldump -u root -p --all-databases > alldatabases_2017-01-31.sql
: -u [계정] 을 입력합니다. 모든 데이타를 dump 합니다.

mysqldump -u root -p --all-databases --no-data > allDDL_2017-01-31.sql
: DDL 정보만 dump 합니다.

mysqldump -u root -p --databases [DB명] > DB명_2017-01-31.sql
: 특정 database를 dump 합니다.

mysqldump -u root -p --routines [DB명] > DB명_2017-01-31.sql
: 특정 database를 프로시저와 함께 dump 합니다.

mysqldump -u root -p -n -d -t --routines --triggers [DB명] > procedures_only.sql
: 특정 database의 프로시저만 dump 합니다.

mysqldump -u root -p -n -d -t --routines --triggers --all-databases DB > procedures_only.sql
: 모든 database의 프로시저만 dump 합니다.

mysqldump -u[userId] -p[password] --no-create [디비명] [테이블명]... > [저장될 파일명]
: 테이블구조를 제외한 데이터만 dump 합니다. 여러개의 테이블이 가능 합니다.

mysqldump -u root -p database이름 table이름 > [저장될 파일명]
: database의 table을 dump 합니다.

mysql -u [userId] -p [password] [DB명] < dump이름.sql
: dump를 복원 합니다. 복원할 DB명은 미리 생성되어 있어야 합니다.
```
