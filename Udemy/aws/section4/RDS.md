## RDS

Relational DB Service

***

관계형 데이터베이스에 대한 설명은 넘어가도록 하겠다.

### Data warehousing

+ 엄청난 양의 데이터를 불러올때 사용되는 빅데이터이다.
+ 어떤 목적을 위해 데이터를 분석할때 사용된다. 
+ Business Intelligence에서 주로 사용됨
+ 보통 서로 다양한 소스로부터 데이터가 합쳐지며, 필요시 불러와진다.
+ 따라서 Transaction processing에는 적합하지 않다.


### OLTP와 OLAP

+ OLTP (Online Transaction Processing)
    + INSERT와 같이 종종 사용되어지는, 혹은 규모가 작은 데이터를
      (실시간으로) 불러올때 사용
    + 흔히 말하는 "트랜잭션 처리"를 OLTP라고 부른다.
        + ex) Order # 210번에만 해당하는 정보를 가져오는 쿼리
      
+ OLAP (Online Analytical Processing)
    + 매우 큰 데이터를 불러올때 사용
    + 주로 대용량의 Select 문을 통한 데이터 스캔이 주가 된다. 데이터의
    양이 너무 방대하기 때문. INSERT/UPDATE가 수행되는 OLTP와 대조된다.
      
***

### RDS - Database Backups

RDS에는 2가지 백업 방법이 존재한다.

+ Automated Backups (자동 백업)
+ DB Snapshots (데이터베이스 스냅샷)

#### Automated Backups (AB)

+ Retention Period (1 - 35일) 안의 어떤 시간으로 돌아가게 할 수 있음
+ AB는 백업 희망일에 생성된 스냅샷과 Transaction logs(TL)을 참고함
+ 디폴트로 AB 기능이 설정되어 있으며 백업 정보는 S3에 저장
  + 여기서 S3는 RDS 용량 만큼은 제공이 된다. 물론 초과하면 과금이 된다.
  + 만약 10GB만큼 RDS를 할당했다면, 10GB 만큼의 S3가 제공된다.
+ AB동안 약간의 I/O suspension이 존재할 수 있음 -> Latency
    + 즉 S3 버킷에 데이터를 저장하는 동안에는 약간의 딜레이가
    존재하게 된다.
우리는 이걸 ***PIT(Point In Time)*** 이라고 부름

#### Database Snapshots

카메라가 어떤 사진을 저장하기 위해 사진을 찍듯, 데이터베이스도
데이터를 저장하기 위해 스냅샷을 찍는 것.

+ 주로 사용자에 의해 실행됨
+ 원본 RDS Instance를 삭제해도 스냅샷은 존재함
    + 앞에서 살펴본 AB의 경우는 인스턴스를 삭제하면 백업도 없어진다.
    
***

![img.png](img.png)

백업된 데이터베이스의 경우 사진과 같이 식별할 수 있다.  
원본의 경우 original이 붙은 반면 복원된 데이터베이스는 restored가 붙는다.
시험에 종종 언급된다고 하는데 넘어가겠다.

