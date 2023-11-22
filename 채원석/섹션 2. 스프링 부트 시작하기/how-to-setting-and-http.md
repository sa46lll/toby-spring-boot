# 환경 설정 
-  amazon correto jdk 11
- ide: intellij community
- Gradle 
- Web dependency
- packaging : jar
- spring boot cli 활용
- sdkman : unix 기반, windows는 git bash로 활용

# 주의할 점
## git bash 외에도 7-zip 패키지를 설치 후 내부에 7z.exe를 붙여넣기 해서 zip.exe를 새로 만들고 시스템 변수에 zip.exe의 해당 경로를 추가하는 과정 필요.(windows 한정)
- 그 이후에 $curl "https://get.sdkman.io" | bash -> $source "$HOME/.sdkman/bin/sdkman-init.sh" ->sdk version 과 같은 명령어를 입력한 뒤 성공했다.
- 출처: https://phoby.github.io/sdkman/

## 명령어 참고
- $sdk list java를 입력하면 설치 가능한 다양한 jdk 버젼이 나온다.
- 이번 수업에서 쓸 jdk 11을 설치하기 위해 $sdk install java 11.0.21amzn이라는 amazon correto jdk를 설치했다.
- $sdk install java 11.0.21-amzn 이라는 명령어로 /helloboot 프로젝트에 jdk 11을 적용시켰다.

# http 요청과 응답 
- 헤더와 메시지 바디를 통해서 다양한 정보를 확인 가능하다.
- status는 200, 300, 400, 500번재로 분류가 된다.
- 1XX: Informational(정보 제공)
- 임시 응답으로 현재 클라이언트의 요청까지는 처리되었으니 계속 진행하라는 의미입니다. HTTP 1.1 버전부터 추가되었습니다.
- 2XX: Success(성공)
- 클라이언트의 요청이 서버에서 성공적으로 처리되었다는 의미입니다.
- 3XX: Redirection(리다이렉션)
- 완전한 처리를 위해서 추가 동작이 필요한 경우입니다. 주로 서버의 주소 또는 요청한 URI의 웹 문서가 이동되었으니 그 주소로 다시 시도하라는 의미입니다.
- 4XX: Client Error(클라이언트 에러)
- 없는 페이지를 요청하는 등 클라이언트의 요청 메시지 내용이 잘못된 경우를 의미합니다.
- 5XX: Server Error(서버 에러)
- 서버 사정으로 메시지 처리에 문제가 발생한 경우입니다. 서버의 부하, DB 처리 과정 오류, 서버에서 익셉션이 발생하는 경우를 의미합니다.

출처: https://hongong.hanbit.co.kr/http-%EC%83%81%ED%83%9C-%EC%BD%94%EB%93%9C-%ED%91%9C-1xx-5xx-%EC%A0%84%EC%B2%B4-%EC%9A%94%EC%95%BD-%EC%A0%95%EB%A6%AC/
