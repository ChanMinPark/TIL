##Python에서 socket의 setsockopt 옵션 설정하기.

기본적으로 socket을 사용하고 나면 사용한 port는 close로 닫아주는게 맞다.  
그래야 해당 port를 다른데서도 사용할 수 있으니깐.  

근데 port를 닫았다고해도 일정시간 동안은 TIME_WAIT 상태로 대기한다고 한다.  
그리고 이 상태에서는 즉각적으로 다시 바로 사용할 수 없다.  
그래서 socket을 쓰고 close를 했는데도 already in use 에러가 발생하게된다.  

이런 에러를 막기위해서 setsockopt을 사용한다. 사용법은 아래와 같다.  

```python
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
s.bind((HOST, PORT))
```

저렇게 가운데줄에 setsockopt함수에서 socket.SO_REUSEADDR 옵션을 설정해주면 방금 사용하고 close한 port를 즉시 다시 사용할 수 있다.  
