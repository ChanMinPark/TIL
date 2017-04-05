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

<br>
## CSS
### background-image
- 예시
```
.walkin-main-bg-1 {
  background-image: url("../img/main_bg_1.png");
  background-color: #cccccc;
  background-size: cover;
}
```
- 참고 링크 : http://visualize.tistory.com/404
- url()로 상대경로 이미지 위치를 지정할 수 있습니다.

- 함께 쓰는 속성
 - ```background-color``` : 이미지를 로드하지 못했을 때 표시될 색상입니다.
 - ```background-size: cover``` : 이미지를 창 크기에 맞추서 축소시킨다. 어느정도 축소되면 축소되지 않고 잘립니다.


### opacity
- 예시
```
.walkinpcm-img-opacity {
  opacity: 0.5;
}
```
- 참고 링크 : https://www.w3schools.com/cssref/css3_pr_opacity.asp
- 투명도를 설정합니다. 0.0~1.0 의 값을 가집니다.  


### display
- 예시
```
display: inline-block;
```
- 요소를 어떻게 보여줄지를 결정합니다.
- 속성값
 - none : 보이지 않음
 - block : 블록 박스로 만듬
 - inline : 인라인 박스로 만듬
 - inline-block : block 박스로 만들어지나, inline 처럼 배치가 된다.

### box-sizing
- 예시
```
box-sizing: border-box;
```
- width와 height의 기준을 정합니다.
- 속성값
 - ```content-box``` : 기본값입니다. border, padding, margin을 제외한 순수 content 영역을 기준으로 합니다.
 - ```border-box``` : margin을 제외한 content, padding, border를 포함함 영역을 기준으로 합니다.

### list-style-type
- 예시
```
list-style-type: none;
```
- li 태그의 불릿 속성을 지정할 수 있습니다.
- 속성값
  - lower-roman : 로마숫자 소문자으로된 목록
  - upper-roman : 로마숫자 대문자으로된 목록
  - lower-alpha : 알파벳 소문자으로된 목록
  - upper-alpha : 알파벳 대문자으로된 목록
  - disc : 점으로 된 목록
  - circle : 속이 하얀색 원으로 된 목록
  - square : 사각형으로 된 목록
  - decimal : 숫자로 된 목록
  - none : 아무 표시 없음
