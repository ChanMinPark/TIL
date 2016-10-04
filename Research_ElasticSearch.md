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

1. ElasticSearch 다운로드  
아래 명령어를 이용해서 tar.gz형식의 ElasticSearch 압축파일을 다운로드 받는다.  
```
wget https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/2.4.1/elasticsearch-2.4.1.tar.gz
```

2. 압축해제  
아래 명령어로 압푹을 해제합니다.  
```
tar -xvf elasticsearch-2.4.1.tar.gz
```

3. ElasticSearch 실행  
아래 명령어로 ElasticSearch를 실행합니다.  
```
./elasticsearch
```
**putty에서 실행했을 때 putty를 꺼도 elasticsearch는 꺼지지 않도록 elasticsearch를 실행해야함**
**screen을 이용하면 될듯**
**또는 crontab에 등록**

## 4. Java API

## 5. Query
(참고 : http://knight76.tistory.com/entry/elasitcsearch-DFS-Query-Then-Fetch )  
(참고 : https://www.elastic.co/blog/understanding-query-then-fetch-vs-dfs-query-then-fetch )

- DFS Query Then Fetch
 - DFS = Document Frequency Statics
 - 미리 질의 (Prequery) 하여 다큐먼트 질의를 하고, 전체적인 득점(score)을 계산한다.
 - 얼마나 중요한 단어가 나타나는지 통계를 구해서 좋은 품질의 키워드의 점수를 높이는데 있다. 따라서, 속도는 좀 느릴 수 있지만, 좋은 품질을 얻을 수 있다. 

- Query Then Fetch
 - 
