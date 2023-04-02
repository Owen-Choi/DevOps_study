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

