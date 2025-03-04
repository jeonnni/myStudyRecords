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