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
