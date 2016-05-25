##Python을 이용한 OpenCV에서 TCP socket을 통해서 Image 전송하기.  

TCP socket통신만 보면 일반적인 Python의 TCP socket통신 기법을 이용한다.  
python의 tcp socket에서는 문자열을 보내고 받을 수 있는데, 이를 따르기 위해서 OpenCV에서는 Image를 문자열(string)으로 변환할 수 있다.  

즉,
이미지 송신단에서는 OpenCV를 이용해서 캡처한 Image를 문자열로 변환한 뒤 TCP Socket으로 전송(send)한다.  
이미지 수신단에서는 TCP Socket으로 수신한 문자열을 OpenCV를 이용해서 Image로 변환한다.  

###client.py (송신단)  
```python
#!/usr/bin/python
import socket
import cv2
import numpy

#연결할 서버(수신단)의 ip주소와 port번호
TCP_IP = 'localhost'
TCP_PORT = 5001

#송신을 위한 socket 준비
sock = socket.socket()
sock.connect((TCP_IP, TCP_PORT))

#OpenCV를 이용해서 webcam으로 부터 이미지 추출
capture = cv2.VideoCapture(0)
ret, frame = capture.read()

#추출한 이미지를 String 형태로 변환(인코딩)시키는 과정
encode_param=[int(cv2.IMWRITE_JPEG_QUALITY),90]
result, imgencode = cv2.imencode('.jpg', frame, encode_param)
data = numpy.array(imgencode)
stringData = data.tostring()

#String 형태로 변환한 이미지를 socket을 통해서 전송
sock.send( str(len(stringData)).ljust(16));
sock.send( stringData );
sock.close()

#다시 이미지로 디코딩해서 화면에 출력. 그리고 종료
decimg=cv2.imdecode(data,1)
cv2.imshow('CLIENT',decimg)
cv2.waitKey(0)
cv2.destroyAllWindows() 
```

###server.py (수신단)  
```python
#!/usr/bin/python
import socket
import cv2
import numpy

#socket 수신 버퍼를 읽어서 반환하는 함수
def recvall(sock, count):
    buf = b''
    while count:
        newbuf = sock.recv(count)
        if not newbuf: return None
        buf += newbuf
        count -= len(newbuf)
    return buf

#수신에 사용될 내 ip와 내 port번호
TCP_IP = 'localhost'
TCP_PORT = 5001

#TCP소켓 열고 수신 대기
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.bind((TCP_IP, TCP_PORT))
s.listen(True)
conn, addr = s.accept()

#String형의 이미지를 수신받아서 이미지로 변환 하고 화면에 출력
length = recvall(conn,16)
#길이 16의 데이터를 먼저 수신하는 것은 여기에 이미지의 길이를 먼저 받아서 이미지를 받을 때 편리하려고 하는 것이다.
stringData = recvall(conn, int(length))
data = numpy.fromstring(stringData, dtype='uint8')
s.close()
decimg=cv2.imdecode(data,1)
cv2.imshow('SERVER',decimg)
cv2.waitKey(0)
cv2.destroyAllWindows() 
```
