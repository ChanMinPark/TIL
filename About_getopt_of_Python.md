###Python의 getopt 함수  

Python에서는 getopt함수를 이용해서 command 명령에 작성하는 파라미터를 입력받을 수 있다.  

####사용법  
간편하면서 장점인 것이, 한 줄안에서 command 명령에 사용될 옵션을 정의함과 동시에 변수에 할당하는 것이다.  
예는 아래와 같다.  

```python
opts, args = getopt.getopt(argv[1:],"hi:o:",["ifile=","ofile="])
```

예에 따르면, 우선 변수는 opts와 args를 받는다.  
opts는 옵션 이름을 선언하고 값을 적는 파라미터에 대한 값을 저장하고,  
args는 옵션 이름 없이 바로 값만 적는 파라미터에 대한 값을 저장한다.  

즉, --ifile 'sample.txt' 와 같이 command 명령에 적는 것은 opts에 sample.txt 문자열이 들어가고,  
그냥 'test.txt' 와 같이 command 명령에 적는 것은 args에 test.txt 문자열이 들어간다는 것이다.  


다음으로 getopt함수의 인자들을 보면,  
첫번째 인자는 command 명령에서 입력받는 파라미터들이고,  
두번째 인자는 단문자 옵션 이름이다.  ```hi:o:```라고 되어 있느면 command 명령에서는 ```-h -i -o``` 라고 쓸수 있는 것인데, i와 o에는 : 가 붙어 있다. 이는 옵션 이름만 쓰겠다는 것이 아니라 해당 옵션에 대해서 값을 입력 받겠다는 것이다.  
세번째 인자는 장문자 옵션 이름이다. command 명령에서는 ```--ifile, --ofile``` 과 같이 쓰인다. 뒤에 = 가 붙어 있는 것도 옵션만 쓴다는게 아니고 값을 받겠다는 것이다.  


입력받은 opts와 args를 사용하는 방법은 다음과 같다.  
우선 opts는 2가지 방법이 있는데 첫번째는 아래와 같이 for문과 if문을 사용하는 방법이다.  
```python
for opt, arg in opts:
      if opt == '-h':
         print 'test.py -i <inputfile> -o <outputfile>'
         sys.exit()
      elif opt in ("-i", "--ifile"):
         inputfile = arg
      elif opt in ("-o", "--ofile"):
         outputfile = arg
```
opts는 (key, value)쌍으로 이루어진다. 그래서 ```for opt, arg in opts:```는 옵션쌍을 순서대로 하나씩 확인하겠다는 것이다.  

두번째 방법은 python의 dict함수를 이용하는 방법이다.  
```opts=dict(opts)```라고 하면 opts가 dictionary구조로 바뀐다.  
이렇게 하면, ```opts.get('-i', 'sample.txt')```와 같이 사용할 수 있다. 의미는 '-i'키와 매핑되는 값을 get하겠다는 것인데, 만약 값이 없다면 'sample.txt'를 디폴트 값으로 사용하겠다는 것이다.  
개인적으로는 두번째 방법이 마음에 든다.  
