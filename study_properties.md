# 속성 공부
<br>
## HTML
### viewport
- 예시 : ```<meta name="viewport" content="width=device-width, initial-scale=1">```
- 참고 링크 : http://aboooks.tistory.com/352  
- viewport 설정을 하게되면 다양한 모바일 기기에서도 페이지의 너비나 배율을 설정할수있다.

- 함께 쓰는 속성
 - ```content="width=device-width"``` : 너비를 기기의 너비에 맞추어 표시합니다.
 - ```content="initial-scale=1"``` : viewport의 초기배율입니다. 1이 100%입니다.


### data-toggle
- 예시
```
<button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#myNavbar">
    <span class="icon-bar"></span>
    <span class="icon-bar"></span>
    <span class="icon-bar"></span>
</button>
```
- 참고 링크 : http://maczniak.github.io/bootstrap/javascript.html , http://min-blog.tistory.com/1865
- 특정 영역을 숨기고 펼치고 할 수 있습니다.

- 함께 쓰는 속성
 - ```data-target``` : data-target에 지정한 식별자를 숨기거나 펼칩니다.
