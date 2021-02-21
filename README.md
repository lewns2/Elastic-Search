# Elastic-Search

### 실행 
```
ElasticSearch가 실행되면 9200, 9300 포트가 오픈된다.

9200 포트는 HTTP로 바인딩 되고 9300 포트는 TCP로 바인딩 된다.
```
### ELASTIC SEARCH vs RELATIONAL DB

![image](https://user-images.githubusercontent.com/55612222/108634230-0155b580-74bc-11eb-8661-ee7f11169f54.png)

### Rest API

### Create, Delete Index

```
curl -XPUT localhost:9200/index명?pretty

curl -XDELETE localhost:9200/index명
```
- ?pretty는 결과를 깔끔하게 출력하기 위함.

### Create Document

```
Curl -XPOST localhost:9200/index명/type명/id -d' {document}

Curl -XPOST localhost:9200/index명/type명/id -d @파일명.json
```
  
### BULK? Add Document
여러 개의 Document를 ElasticSearch에 삽입한다.
```
curl -XPOST localhost:9200/ bulk?pretty -data-binary @OOO.json
```

### Mapping? 
#### 관계형 데이터베이스의 스키마와 동일
```
curl -XPUT localhost:9200/index명/type명_mapping’ -d @파일명.json
```
### Search
#### - 기본
```
curl -XPUT localhost:9200/index명/type명_search?pretty
```
#### - 방법 1. SEARCH-URI
```
curl -XPUT localhost:9200/index명/type명_search?q=points:30?pretty’
```
#### - 방법 2. SEARCH-REQUEST BODY
```
curl -XPUT localhost:9200/index명/type명_search -d’ {REQUEST BODY}
```
### Aggregation? 
#### ElasticSearch 내 Document 조합을 통해 결과를 도출하기 위해 사용
#### - 구조
```
"aggregations" : {
  "<aggregations_name>" : {
    "<aggregations_type>" : {
      <aggregations_body>
     }
     [,"meta" : { [<meta_data_body>] } ]?
     [,"aggregations" : { [<sub_aggregation>]+ } ]?
   }
   [,"<aggregation_name_2>" : { ... }]*
}
```
#### - 기능에 따라 
```
Metric Aggregation : 산술

Bucket Aggregation : 'group by'
```

