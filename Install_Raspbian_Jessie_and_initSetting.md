##Raspbian Jessie 초기설정  

###Step 1 ) Raspbian Jessie 다운로드
https://www.raspberrypi.org/downloads/raspbian/  
링크에서 RASPBIAN JESSIE를 다운받는다. ‘Download ZIP’을 눌러서 다운받으면 된다. Torrent를 이용해도 되지만 피어가 별로 없어서 다운로드가 느리다.  

###Step 2 ) Micro SD 카드에 Raspbian Jessie 이미지 업로드하기.
이미지를 MicroSD 카드에 업로드할 때는 ‘Win32DiskImager’를 이용한다.  
https://sourceforge.net/projects/win32diskimager/  
여기서 다운 받을 수 있다. 설치하고 실행시킨다.  

실행하면 아래와 같은 창이 나타난다.  
![](https://github.com/ChanMinPark/TIL/blob/master/image/Install_Raspbian_Jessie_and_initSetting/image1.png)

이 프로그램을 이용하면 이미지를 Micro SD카드에 쓰는 것(업로드)도 되지만 읽는 것도 가능하다.  
업로드 할 때는 업로드 할 장치를 ‘Device’에서 선택하고, 업로드 할 이미지를 ‘Image File’에 선택한다. 그리고 ‘Write’를 누르면 된다.  
읽을 때는 ‘Image File’에 읽어서 저장할 경로와 저장할 파일이름을 지정해주고, ‘Device’는 읽어올 장치를 선택한다. 그리고 ‘Read’를 누르면 Micro SD카드에 있는 이미지를 저장할 수 있다. 보통 초기설정 후의 이미지나 중요 point 이후의 이미지를 저장해 놓고 두고두고 사용한다. Tip으로는, 초기설정 후에 이미지를 한번 저장해 둘 거면 파일시스템 크기는 확장하지 않은 상태에서 저장해 두는 것이 좋다. 그래야 사이즈가 작으니깐!  
파일 시스템을 확장하지 않은 상태의 라즈비안은 4GB정도 된다. 그래서 Read해 와도 4GB가 된다. 그런데 파일 시스템을 확장하면 Micro SD카드의 용량에 따라 크기가 커져서(ex. 16GB) 읽어올 때 시간도 오래 걸리고 이미지 파일 크기도 커져서 저장공간이 아깝다.  
