# INSERT INTO SELECT SHARED LOCK(row LOCK)

{% hint style="info" %}
마켓보로에서 일하면서 생긴 트랜잭션 문제에 대해 시니어님과 교류한 내용입니다.
{% endhint %}

## 테스트 목표

* `Table단위의 LOCK`이 걸리는가? 아니면 `ROW단위의 LOCK`이 걸리는가? (레코드 락)
* `ROW단위`: 특정 데이터에만 `SHARED LOCK`이 걸리고, 다른데이터의 `CRUD`에는 영향이 없는가?
  * `SHARED LOCK`: 읽기 가능. 수정/삭제 불가

## 테스트 시나리

#### 기초 환경

* Transaction Mode: Manual

```sql
create table test1 (
    col1 int primary key auto_increment,
    col2 char(10)
);
create table test2 select * from test1 limit 0;

insert into test1 (col2) values ('aaa'),('bbb'),('ccc');

// 현재 걸린 lock 조회
select * from performance_schema.data_locks
```

| Session 1                                                                           | Session 2                                                           | Description                                                                                                 |
| ----------------------------------------------------------------------------------- | ------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| begin;                                                                              |                                                                     |                                                                                                             |
| <p>insert into test2 </p><p>select * </p><p>from test1 </p><p>where col1 = '1';</p> |                                                                     | `LOCK_MODE` S,REC\_NOT\_GAP `LOCK_DATA` 1                                                                   |
|                                                                                     | <p>update test1</p><p>set col2 = '1111'</p><p>where col1 = 2;</p>   | Session1과 관련 없는 데이터라 LOCK 걸리지 않고 성공                                                                         |
|                                                                                     | <p>update test1 </p><p>set col2 = '1111' </p><p>where col1 = 1;</p> | <p>Session1과 관련 있는 데이터라 LOCK 획득 대기<br><br><code>LOCK_MODE</code> X,REC_NOT_GAP <code>LOCK_DATA</code> 1</p> |
| commit;                                                                             |                                                                     | Session 2 성공                                                                                                |

#### 결

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

* 이 내용을 읽고 앞의 테스트를 다시 보니&#x20;
  * where 조건의 col1은 PK이기에 unique index로 이미 잡혀있어 단일 레코드락이 걸립니다.
  * 하지만 index가 아닌 col2라면?

## 테스트 목표 2

* index가 아닌 col2를 where 조건으로 실행하는 경우 레코드락이 어떻게 잡히는가?

## 테스트 시나리오 2

* 기초환경 동

| Session 1                                                                             | Session 2                                                            | Description                                                                                                 |
| ------------------------------------------------------------------------------------- | -------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| begin;                                                                                |                                                                      |                                                                                                             |
| <p>insert into test2 </p><p>select * </p><p>from test1 </p><p>where col2 = 'bbb';</p> |                                                                      | <p><code>LOCK_MODE</code> S<br><code>LOCK_DATA</code> 1, 2, 3</p>                                           |
|                                                                                       | <p>update test1</p><p>set col2 = 'fff'</p><p>where col2 = 'ccc';</p> | <p>획ㅡ </p><p><code>LOCK_MODE</code> X<br><code>LOCK_DATA</code> 1</p>                                       |
|                                                                                       | <p>update test1 </p><p>set col2 = '1111' </p><p>where col1 = 1;</p>  | <p>Session1과 관련 있는 데이터라 LOCK 획득 대기<br><br><code>LOCK_MODE</code> X,REC_NOT_GAP <code>LOCK_DATA</code> 1</p> |
| commit;                                                                               |                                                                      | Session 2 성공                                                                                                |

#### 결

