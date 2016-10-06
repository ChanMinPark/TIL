# ElasticSearch
(참고 : http://www.slideshare.net/seunghyuneom/elastic-search-52724188 )  
(참고 : http://opennote46.tistory.com/143 )  
(참고 : 설치 및 자바에서 사용 http://i5on9i.blogspot.kr/2015/04/elastic-search-java.html?m=1 )  

## 1. ElasticSearch 란?
Elasticsearch is a search engine based on Lucene. It provides a distributed, multitenant-capable full-text search engine with an HTTP web interface and schema-free JSON documents. Elasticsearch is developed in Java and is released as open source under the terms of the Apache License. Elasticsearch is the most popular enterprise search engine followed by Apache Solr, also based on Lucene.  
(Wiki pedia)

## 2. ElasticSearch 특징

## 3. 설치
(참고 : http://bakyeono.net/post/2016-06-03-start-elasticsearch.html#section-5)  

Step 1. ElasticSearch 다운로드  
아래 명령어를 이용해서 tar.gz형식의 ElasticSearch 압축파일을 다운로드 받는다.  
```
wget https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/2.4.1/elasticsearch-2.4.1.tar.gz
```

Step 2. 압축해제  
아래 명령어로 압푹을 해제한다.  
```
tar -xvf elasticsearch-2.4.1.tar.gz
```

Step 3. ElasticSearch 실행  
아래 명령어로 ElasticSearch를 실행한다.  
```
./elasticsearch
```

Step 4. 설치 확인  
아래 명령어로 설치를 확인한다.  
```
curl -X GET http://localhost:9200
```

Step 5. 백그라운드 실행  
터미널을 종료해도 ElasticSearch가 종료되지 않도록 백그라운드로 실행합니다.  
```
cd {엘라스틱서치 폴더 위치}/bin
nohup ./elasticsearch &
```

## 4. Java API
- 사전 작업
(1) 클러스터 이름 변경  
엘라스틱서치 폴더 내부에서 config폴더로 갑니다.  
내부에 elasticsearch.yml 파일이 있는데 이 파일 내부에 cluster.name 부분의 주석을 없애고 원하는 이름으로 변경합니다.  
그리고 엘라스틱서치를 재시작합니다.  
(재시작 방법을 몰라서 kill로 죽이고 실행시켰습니다.)  

## 5. Query
(참고 : http://knight76.tistory.com/entry/elasitcsearch-DFS-Query-Then-Fetch )  
(참고 : https://www.elastic.co/blog/understanding-query-then-fetch-vs-dfs-query-then-fetch )

- DFS Query Then Fetch
 - DFS = Document Frequency Statics
 - 미리 질의 (Prequery) 하여 다큐먼트 질의를 하고, 전체적인 득점(score)을 계산한다.
 - 얼마나 중요한 단어가 나타나는지 통계를 구해서 좋은 품질의 키워드의 점수를 높이는데 있다. 따라서, 속도는 좀 느릴 수 있지만, 좋은 품질을 얻을 수 있다. 

- Query Then Fetch
 - 
