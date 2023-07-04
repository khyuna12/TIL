## 리눅스 Linux
> OS(운영체제) = kernel(운영체제의 핵심적인 프로그램 구현) + App

- 하드웨어 제어하는 데 필요

  - 하드웨어 핵심
    - CPU
    - RAM: 임시저장공간
    - disk: 영구저장공간
    - Network

- 상업용인 Windows, ios과 달리 무료, **오픈소스**
- 플랫폼에 대한 제약이 거의 없음

- **리눅스 배포판**
  - 슬랙웨어: 하드웨어 호환성 좋음, GUI 지원 안됨(마우스 X)
  - 수세: 슬랙웨어 개량한 배포판
  - 데비안: GNU
  - **우분투**: 데비안 개량, Unity 데스크탑 환경 -> GNOME, 클라우드와 가상화 환경에서 많이 사용 
  - **레드햇**: 서버환경에서 주로 사용, 유지 보수 관리 상용화 정책 따름
  - 페도라: 레드햇의 테스트 버전
  - 센트오에스: 레드햇이 공개한 소스코드 커스터마이징해서 사용할 수 있도록 하는 배포판

<br>

---

<br>

### 명령어
> 바탕화면에서 오른쪽 마우스 -> terminal
   
- 명령어 라인 구성
```
$ command [-options] [argument]
```

- 명령어 종류
  - `id`: 사용자의 UID, GID
    - `g`: 기본 그룹의 GID 출력
    - `G`: 기본 그룹과 추가 그룹의 GID 출력

  - 현재 로그인된 사용자 정보
    - `users`
    - `who`
    - `finger`
    - `last`
    
  - `passwd`: 사용자 암호 변경

  - `su`: 사용자 전환
    - `su - root`: 관리자 계정
  - `sudo`: 다른 사용자의 권한으로 실행
    - `sudo useradd [username]`: 사용자 계정 추가(관리자일 때 가능)

  - `clear`: 전 명령어 다 삭제

  - 운영체제 버전과 하드웨어 정보
    - `lsb_release -a`: ubuntu 버전
    - `cat /etc/os-release`: 버전
    - `uname -a`: kernel 버전
    - `uname -r`: kernel 버전
    - `lscpu`: cpu 정보 확인
    - `free -h`: 메모리 정보 확인
    - `lsscsi`: disk 정보 확인
  
  - 네트워크 정보
    - `hostname`
    - `ip address`
  
  - **디렉토리 관리**
    - `pwd`: 디렉토리 확인
    - 절대경로: 최상위 노드(/)를 기준으로 정의한 경로(/home/tux/test.c)
    - 상대경로: 현재 사용자 위치 기준으로 정의한 경로(./test.c)
    - `ls [directoryname]`: 현재 디렉토리에 있는 것들만 보여줌
    - `tree [directoryname]`: 현재 디렉토리뿐만 아니라 전체적으로 볼 수 있음

    - `cd [경로]`: 사용자 위치 변경
      - `..` : 한단계 상위 디렉토리로 이동
      - `/` : 최상위 디렉토리로 이동
      - `~` : 자신의 홈 디렉토리로 이동
      - `~사용자계정`: 지정된 사용자 계정의 홈 디렉토리로 이동
      - `-` : 작업 디렉토리 이전 작업 디렉토리로 변경

    - `mkdir [directoryname]`: 디렉토리 생성
      - `mkdir -p [newdirectory/newdirectory/...]`: 한번에 디렉토리 여러개 만들기(옵션 `-p` 없으면 하나씩 만들어야 함)
    - `rmdir`: 디렉토리 삭제(복원 불가), 빈 디렉토리만 가능, 현재 위치하고 있는 디렉토리는 삭제 불가
      - `rm [filename]`: 파일 삭제
      - `rm -r [directoryname/filename]`: 디렉토리부터 안에 있는 것들까지 다 삭제

  - **파일 관리**
    - `ls`
      - `-a`: 숨김파일 출력
        - `ls -a /boot`: boot 폴더의 숨김 파일 출력
      - `-l`: 자세한 정보 출력
      - 출력물: 타입(l은 바로가기, -는 파일, d는 디렉토리)과 접근 권한, 링크 수, 소유자, 소유 그룹, 용량(byte), 마지막 수정일자, 파일/디렉토리명

    - `cat`: 파일 내용 출력(파일 전체)
    - `less`: 파일 내용 출력(터미널창 크기 만큼,화살표로 더 볼 수 있음, `q`로 그만보기 가능)
    - `touch`: 사이즈가 0인 빈 파일 만듬
      - `mt`: 시간 바꾸기
        - `touch mt 07040300 emptyfile`: emptyfile의 수정일자를 7월 4일 3시로 바꿈 
    - `echo`
      - `echo [문자열] > newfile`: newfile이 생성되고 `cat newfile`치면 문자열 나옴
    - `cp`: 파일/디렉토리 복사
      - `cp f1 f2`: f1를 복사해서 f2이름으로 저장
      - `cp f1 f2  backup`: backup 폴더에 f1 f2 복사 붙여넣기(backup파일 만들어져 있어야 함)
      - `-r`: 디렉토리 하위의 내용 모두 복사
    - `mv`: 파일의 이동(잘라내서 붙여넣기) 및 이름 변경
      - `mv f1 f.new`: f1를 잘라내서 현재 경로에 f.new이름으로 붙여 넣는 것(이름 바꾸는 거랑 똑같음)
    - `rm [filename]`: 파일 삭제
      - `rm -r [directoryname/filename]`: 디렉토리부터 안에 있는 것들까지 다 삭제

  - **소유권(Ownership)**
    - 파일 소유자 변경: `chown`
      - `sudo chown root newfile`: newfile의 소유자를 root로 바꿈(`ls -l newfile`로 확인 가능)
    - 파일 그룹 변경: `chgrp`
    - `sudo chown ubuntu:ubuntu newfile`: 소유자와 소유그룹 한번에 변경

  - **허가권**
    - `r`: 읽기(read)
    - `w`: 쓰기(write)
    - `x`: 실행(execute) (실행 권한없으면 cd 안됨 )
    예:
    ```
    rwxrwxrwx

    3글자씩
    소유자/소유그룹/기타사용자
    ```
    기타사용자: 소유자도 아니고 소유그룹도 아닌 나머지

    - `chmod`
      - `-u`: 파일의 소유자
      - `-g`: 파일의 소유그룹
      - `-o`: 소유자도 그룹도 아닌 기타사용자
      - `-a`: 모든 사용자
      - 예: `chmod u+x,g=rx,o-r file`
      - 8진수로도 표현 가능: `chmod 755 file`

  - **프로세스**
    - 실행 중인 프로그램
    - `ps`
      - `top`: 프로세스의 실행 정보 출력
      - `kill`: 프로세스의 종료

