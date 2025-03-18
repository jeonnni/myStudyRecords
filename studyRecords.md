## JDK 11에서 JDK 17로 변경하기

### JDK 11과 JDK 17이 모두 설치되어 있지만, 현재 설정된 JDK 버전이 11인 상태
#### 현재 설치된 JDK 버전을 확인
```
🐭 ~ ➤ java -version

openjdk version "11.0.23" 2024-04-16 LTS
OpenJDK Runtime Environment Zulu11.72+19-CA (build 11.0.23+9-LTS)
OpenJDK 64-Bit Server VM Zulu11.72+19-CA (build 11.0.23+9-LTS, mixed mode)
```

#### 설치된 JDK 목록 확인
```
🐭 ~ ➤ /usr/libexec/java_home -V                                               
```

#### JAVA_HOME 환경 변수 설정
```
🐭 ~ ➤ export JAVA_HOME=$(/usr/libexec/java_home -v 17)
```


### 하지만 여전히 JDK 11이 출력
#### JAVA_HOME 직접 설정
```
🐭 ~ ➤ export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk-17.jdk/Contents/Home
```

#### PATH 환경 변수 설정
```
export PATH=$JAVA_HOME/bin:$PATH
```


<br/>
<br/>
<br/>
<br/>
<br/>
<br/>


## [3/19] Docker Desktop 오류 해결 방법
갑자기 잘 사용하던 Docker가 삭제가 되어, 다시 설치하고 Docker Desktop을 실행하려고 할 때, 다음과 같은 경고 메시지가 나타나며 실행되지 않는 문제가 발생했다. 닫기 버튼을 눌러도 자꾸만 뜨는 아래와 같은 경고창 ...

```
docker ‘com.docker.socket’에 악성 코드가 포함되어 있어서 열리지 않았습니다. 이 동작은 mac을 손상시키지 않았습니다.
```

이 문제는 Docker Desktop이 악성코드에 영향을 받지 않았지만, 일부 파일이 잘못 서명되어 발생하는 경고라고 한다. 이를 해결하기 위해 다음 단계를 수행했다.

- Docker 프로세스 종료 및 관련 파일 삭제

```
sudo launchctl bootout system/com.docker.vmnetd 2>/dev/null || true
sudo launchctl bootout system/com.docker.socket 2>/dev/null || true

sudo rm /Library/PrivilegedHelperTools/com.docker.vmnetd || true
sudo rm /Library/PrivilegedHelperTools/com.docker.socket || true

ps aux | grep -i docker | awk '{print $2}' | sudo xargs kill -9 2>/dev/null
```

1. 팝업이 완전히 닫혔는지 확인
2. Docker Desktop 최신 버전 다운로드 및 설치
3. Docker Desktop 4.37.2를 다운로드하고 설치
4. Docker Desktop 실행
5. 정상 작동 확인
