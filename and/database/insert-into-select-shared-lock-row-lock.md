# INSERT INTO SELECT SHARED LOCK(row LOCK)

{% hint style="info" %}
마켓보로에서 일하면서 생긴 트랜잭션 문제에 대해 시니어님과 교류한 내용입니다.
{% endhint %}

## 테스트 1

### &#x20;목표

* `Table단위의 LOCK`이 걸리는가? 아니면 `ROW단위의 LOCK`이 걸리는가? (레코드 락)
* `ROW단위`: 특정 데이터에만 `SHARED LOCK`이 걸리고, 다른데이터의 `CRUD`에는 영향이 없는가?
  * `SHARED LOCK`: 읽기 가능. 수정/삭제 불가

### 시나리오

* Transaction Mode: Manual

```sql
create table test1 (
    col1 int primary key auto_increment,
    col2 char(10)
);
create table test2 select * from test1 limit 0;

insert into test1 (col2) values ('aaa'),('bbb'),('ccc');

## 현재 걸린 lock 조회
select * from performance_schema.data_locks
```

#### 1. Session 1&#x20;

* `col1=1` S락 획득 시도
* `primaryKey=1`  S락 획득 성공&#x20;

```sql
begin;

insert into test2
select *
from test1
where col1 = '1';
```

![](<../../.gitbook/assets/image (7).png>)

#### 2. Session 2&#x20;

* `col1=2` X락 획득 시도
* `primaryKey=2`  X락 획득 성공&#x20;

```sql
update test1
set col2 = '1111'
where col1 = 2;
```

![](<../../.gitbook/assets/image (5).png>)

#### 3. Session 2&#x20;

* `col1=1` X락 획득 시도
* 하지만 **Session 1** 에서 S락을 걸고 있기에 호환되지 않아 WAITING.

```sql
update test1
set col2 = '1111'
where col1 = 1;
```

![](<../../.gitbook/assets/image (3).png>)

#### 4. Session 1 commit, Session 2 commit

### 결과

* 락이 걸리지 않은 레코드에는 update가 가능하다.
* S락이 걸린 레코드에 X락이 들어오면 S락이 해제될 때까지 기다린다.
  * S락과 X락은 호환되지 않는다.
  * timeout의 주범.
* 즉 InnoDB는 레코드락으로 움직인다.

## 하지만..

* 정리하면서 최근 읽은 REAL MySQL의 잠금 파트가 생각나서 다시 읽어봤습니다.

```
이 테이블에 인덱스가 하나도 없다면 어떻게 될까? 
이러한 경우에는 테이블을 풀 스캔하면서 UPDATE 작업을하는데, 
이 과정에서 테이블에 있는 30여만 건의 모든 레코드를 잠그게 된다.
이것이 MySQL의 방식이며, MySQL에서 인덱스 설계가 중요한 이유 또한 이것이다.

- REAL MySQL 1권. 5.3.2 인덱스와 잠금 (172p)
```

* 이 내용을 읽고 앞의 테스트를 다시 보니
  * where 조건의 col1은 PK이기에 unique index로 이미 잡혀있어 단일 레코드락이 걸립니다.
  * 하지만 index가 없는 col2라면?
  * col2에 non unique index를 걸고 조한다면?

## 테스트 2

### 목표

* index가 아닌 col2를 where 조건으로 실행하는 경우 레코드락이 어떻게 잡히는가?

### 시나리오

* 초기 세팅 동

#### 1. Session 1

* `col2=bbb` S락 획득 시도.
* 하지만 모든 레코드에 대해 S락 획득 성공.

```sql
begin;

insert into test2
select *
from test1
where col2 = 'bbb';
```

![](<../../.gitbook/assets/image (14).png>)

#### 2. Session 2

* `col2=ccc` X락 획득 시도.
* 하지만 **Session 1** 에서 모든 레코드에 S락을 걸고 있기에 호환되지 않아 WAITING.

```sql
update test1
set col2 = 'fff'
where col2 = 'ccc';
```

![](<../../.gitbook/assets/image (6).png>)

#### 3. Session 1 commit, Session 2 commit

### 결과

* index가 없다면 모든 레코드가 락에 걸립니다.

## 테스트 3

### 목표&#x20;

* col2에 non unique index를 걸고 where 조건으로 실행하는 경우 레코드락이 어떻게 잡히는가?

### 시나리오

```sql
create table test1
(
    col1 int primary key auto_increment,
    col2 char(10)
);

create table test2
select *
from test1
limit 0;

insert into test1 (col2)
values ('aaa'), ('aaa'),
       ('bbb'), ('bbb'),
       ('ccc'), ('ccc');

create index test1_col2_index on test1(col2); ## 인덱스 생성
```

#### 1. Session 1&#x20;

* `col2=bbb` S락 획득 시도
* `primaryKey=3,4,5`  S락 획득 성공&#x20;
* col2는 non unique index 이지만 `primaryKey=3,4`의 S락을 획득했습니다.
* `primaryKey=5`도 S락이자 GAP락으로 획득했는데 이부분은 좀 더 공부해야됩니다.

```sql
begin;

insert into test2
select *
from test1
where col2 = 'bbb';
```

![](<../../.gitbook/assets/image (15).png>)

#### 2. Session 2&#x20;

* `col2=ccc` X락 획득 시도
* `primaryKey=5,6`  X락 획득 성공&#x20;
* 근데 unique index이던 것과 다르게 **REC\_NOT\_GAP, GAP** 락들이 추가로 획득됩니다.

```sql
update test1
set col2 = 'fff'
where col2 = 'ccc';
```

![](<../../.gitbook/assets/image (10).png>)

#### 3. Session 2&#x20;

* `col2=bbb` X락 획득 시도
* 하지만 **Session 1** 에서 S락을 걸고 있기에 호환되지 않아 WAITING.

```sql
update test1
set col2 = 'ggg'
where col2 = 'bbb';
```

![](<../../.gitbook/assets/image (2).png>)

#### 4. Session 1 commit, Session 2 commit

### 결과

* 테스트 1과 결과는 같지만 락이 걸리는 형태가 매우 다릅니다.

## 최종 결론

#### innoDB에서 unique index에 대한 `INSERT INTO SELECT SHARED LOCK` 는 레코드 락이 맞습니다.

* 하지만 non unique index의 경우 락이 걸리는 형태가 매우 다릅니다.
  * IS, IX, 갭 락등에 대한 공부가 부족해 어떤 차이가 있는지 잘 모르겠습니다.
* 심지어 no index 인 경우는 전체 레코드 락으로 테이블 락과 같은 상태가 됩니다.

#### 하지만 실무에서는 큰 문제가 없을 것으로 예상됩니다.

* 실무에서 사용되는 테이블은 조회 조건에 대해 최소한 non unique index가 걸려있을 것이기 때문입니다.

{% embed url="https://www.letmecompile.com/mysql-innodb-lock-deadlock/" %}
