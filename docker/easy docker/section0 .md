```
$ echo "alias docker='winpty docker'">> ~/.bashrc
```
+ git bash에서 컨테이너 쉘로 접속
+ 윈도우는 WSL 이라는 리눅스 가상환경에서 실행

## 모든 컨테이너 삭제
+ docker rm -f $(docker ps -aq) - MAC
+ docker ps -aq | ForEach-Object{docker rm -f $_} - Window(powershell)

