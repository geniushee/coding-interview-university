# 소켓의 본질에 대한 이해
- 소켓(Socket)은 OS커널에 구현되어 있는 프로토콜 요소에 대한 추상화된 인터페이스
- 장치 파일의 일종으로 이해할 수 있음
- 일반 파일에 대한 개념이 대부분 적용됨

소켓은 파일이다. 대부분의 파일은 어떤 데이터이지만 어떤 파일이 추상화된 인터페이스라면 그것을 소켓이라고 한다.

소켓 프로그래밍에 다른 의미는 TCP 파일에 대한 입출력을 말하는 것이다.

파일과 같이 생각해야할 것은 데이터 단위이다.(Stream)