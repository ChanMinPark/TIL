# Java Servlet에서 HTTP Request에 대한 Response의 언어 설정하기.

## 1. 언어 속성 설정
Http Servlet에서 response로 원하는 출력을 하고자 할때 아래의 코드를 작성합니다.  
```
@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		
		PrintWriter out = resp.getWriter();
		out.println("Basic Get 요청에 대한 응답입니다.");
	}
```

이때 출력에 한글이 있는데 이대로 출력하면 웹브라우저에서 물음표(?)로 출력됩니다.  

이 문제를 해결하려면, 아래와 같이 언어 속성을 설정하는 코드(setContentType)를 추가해주어야 합니다.  
```
@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		resp.setContentType("text/plain;charset=UTF-8");
		
		PrintWriter out = resp.getWriter();
		out.println("Basic Get 요청에 대한 응답입니다.");
	}
```
