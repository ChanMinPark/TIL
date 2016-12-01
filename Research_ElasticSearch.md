# ElasticSearch
(참고 : http://www.slideshare.net/seunghyuneom/elastic-search-52724188 )  
(참고 : http://opennote46.tistory.com/143 )  
(참고 : 설치 및 자바에서 사용 http://i5on9i.blogspot.kr/2015/04/elastic-search-java.html?m=1 )  
(공식 가이드 : https://www.elastic.co/guide/en/elasticsearch/reference/current/_installation.html )  
(설명 완전 잘되어 있는 곳 : http://d2.naver.com/helloworld/273788 )  

## 1. ElasticSearch 란?
Elasticsearch is a search engine based on Lucene. It provides a distributed, multitenant-capable full-text search engine with an HTTP web interface and schema-free JSON documents. Elasticsearch is developed in Java and is released as open source under the terms of the Apache License. Elasticsearch is the most popular enterprise search engine followed by Apache Solr, also based on Lucene.  
(Wiki pedia)

## 2. ElasticSearch 특징
- 아파치 루씬 기반  
- 실시간 분석  
- 분산 시스템  
- 높은 가용성  
- 멀티 테넌시  
- 전문검색  
- Json 문서 기반  
- RESTful API  

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
압축을 해제한 폴더 안의 bin폴더에 들어가서 아래 명령어로 ElasticSearch를 실행한다.  
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
- 사전 작업 : 클러스터 이름 변경  

엘라스틱서치 폴더 내부에서 config폴더로 갑니다.  
내부에 elasticsearch.yml 파일이 있는데 이 파일 내부에 cluster.name 부분의 주석을 없애고 원하는 이름으로 변경합니다.  
그리고 엘라스틱서치를 재시작합니다.  
(재시작 방법을 몰라서 kill로 죽이고 실행시켰습니다.)  

(1) Java API  
(참고 : https://dzone.com/articles/elasticsearch-java-api )  
(참고 : https://www.elastic.co/guide/en/elasticsearch/client/java-api/current/java-docs-index.html )

- ElasticSearch 라이브러리 추가  

(참고 : https://mvnrepository.com/artifact/org.elasticsearch/elasticsearch/2.4.1 )  
위의 링크는 Maven Repository 검색사이트 인데 이곳에서는 jar파일도 다운로드 할 수 있습니다.  
위 링크에서 Elasticsearch의 core jar파일을 다운받아서 프로젝트 라이브러리에 추가합니다.  

- ElasticSearch Client객체 생성  

```java
// ElasticSearch Client 객체 생성
TransportClient esclient = null;
		
// 클러스터 이름을 직접 지정하도록 설정.
Settings settings = Settings.settingsBuilder().put("cluster.name", PCM_CLUSTER).build();
		
// 직접 지정한 클러스터 셋팅을 적용하고 설치된 ElasticSearch에 접속.
// 주소는 로컬호스트, 포트는 9200
esclient = TransportClient.builder().settings(settings).build()
		.addTransportAddress(
				new InetSocketTransportAddress(
						InetAddress.getLocalHost(),9300));
```

## Tips.
- ElasticSearch를 Java에서 사용하려면 dependency를 모두 추가해주어야 합니다. 라이브러리를 직접 추가하려면 모든 jar파일들을 다운받아서 WEB-INF/lib에 추가해줘야합니다. Maven을 사용하면 dependency만 추가해주면 됩니다.  
- ElasticSearch는 RESTful API를 위해서 9200번 포트를 사용하고, 노드 내부에서 Java API를 위해서 9300번 포트를 사용합니다.  
- 설정파일인 elasticsearch.yml에서 cluster.name은 사용중인 클러스터의 이름을 설정하는것이 아니라 기본으로 사용할 클러스터의 이름을 지정하는 것입니다.  

## 5. Query
(참고 : http://knight76.tistory.com/entry/elasitcsearch-DFS-Query-Then-Fetch )  
(참고 : https://www.elastic.co/blog/understanding-query-then-fetch-vs-dfs-query-then-fetch )

- DFS Query Then Fetch
 - DFS = Document Frequency Statics
 - 미리 질의 (Prequery) 하여 다큐먼트 질의를 하고, 전체적인 득점(score)을 계산한다.
 - 얼마나 중요한 단어가 나타나는지 통계를 구해서 좋은 품질의 키워드의 점수를 높이는데 있다. 따라서, 속도는 좀 느릴 수 있지만, 좋은 품질을 얻을 수 있다. 

- Query Then Fetch
 - 각 샤드별 득점만 계산한다.
 
### 6. Kibana
(참고 : http://teamsmiley.xgridcolo.com/?p=884 )  
(참고 : http://aoruqjfu.fun25.co.kr/index.php/post/741 )  
?키바나 설치 후에 엘라스틱서치도 재시작 해야하나?  

Step 1. Kinaba Download  
https://www.elastic.co/downloads/kibana  
위 링크에서 자신이 사용하는 운영체제의 설치파일을 다운받습니다.  

저는 우분투에서 설치하기 때문에 아래와 같이 다운로드 받습니다.  
```
$ wget https://artifacts.elastic.co/downloads/kibana/kibana-5.0.0-linux-x86_64.tar.gz
```

Step 2. Kibana 설치  
다운로드 받은 kibana를 설치합니다.  
말이 설치지 그냥 압축해제입니다.  
```
$ tar -xvf kibana-5.0.0-linux-x86_64.tar.gz
```

Step 3. Kibana 설정  
Kibana를 압축해제하고 나면 사용하는 ElasticSearch와 연결해주어야합니다.  
```{키바나 압축 해제 폴더}/config/kibana.yml```을 에디터로 열어서  
**elasticsearch.url**에 연결하려는 ElasticSearch가 설치된 주소를 입력해 줍니다.  
ex) "http://localhost:9200"  
바꾸지 않으면 기본적으로 로컬호스트의 9200번 포트로 설정됩니다.  

AWS를 사용하면 Kibana설치는 클라우드에서 하고 웹브라우저는 윈도우 등 로컬pc에서 해야할텐데...  
이 경우에는 Kibana를 로컬호스트의 5601포트로 열어두면 로컬 pc에서 접속할 수가 없다.  
또한 AWS EC2의 public IP로 설정해도 안된다.  
결론적으로는 EC2의 private IP로 설정해야지 로컬pc의 웹브라우저에서 ```public IP:5601```로 접속할 수 있다.

Step 4. Kibana 실행  
Kibana 압축 해제한 폴더에서 아래 명령어로 실행시킵니다.  
```
bin/kibana
```

Step 5. Kibana 종료  
elasticsearch는 ```ps -ef | grep elasticsearch```로 찾으면 PID를 알수 있고 이걸로 kill 할수 있다.  
하지만 kibana는 ps 목록에서 확인이 안된다.  
```netstat -pln | grep 5601```를 통해서 PID를 확인할 수 있다.

Step 6. Kibana 사용  
kibana를 사용하기 위해서는 로그스태시로 생성하는 index가 필요하다(?)고 한다.  
(참고 : http://rea1man.tistory.com/entry/ELK-elasticsearch-logstash-kibana-%EC%84%A4%EC%B9%98-%EB%B0%8F-%EC%82%AC%EC%9A%A9 )  
(참고 : http://brownbears.tistory.com/74 )  
(Time-Field name의 목록에 아무것도 안 나타날때 해결방법 : http://doswlf.tistory.com/738 )  
