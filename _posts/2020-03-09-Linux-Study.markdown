---
layout: post
title: "Linux Study (19.08.19 ~ 19.08.29)"
description: 리눅스 공부 요약 (생활코딩)
date:   2020-03-09 15:00:00 +0900
categories: [ Algorithm ]
tags: [ linux ]
---


러시아 여행 도중, 시베리아 횡단열차에서 공부하고, 요약한 내용.
[유튜브 생활코딩의 리눅스 강좌][youtube]를 시청하였음.

-------------------------------------


## Linux - file & directory 1

ls -al  : 현재 디렉토리의 파일들을 보여줌. (list)
1. 문자를 입력해 명령을 한다 > GUI 방식이 아님. (CLI, Command Line Interface)
2. 명령은 현재 머무르고 있는 디렉토리를 대상으로 내려진다
 - 어떤 디렉토리에 머무르고 있는지 확인해야 함  

**pwd** : 현재 있는 디렉토리 위치
**mkdir** hello_linux : hello_linux 디렉토리를  만든다
touch empty_file.txt : 빈 txt 파일을 만든다
**ls** -l : 좀 더 자세히 파일들을 보여줌
ls dir1 : dir1의 파일들을 보여줌
명령어 뒤의 (-) 와 함께 붙는 것을 파라미터 라고 함


## Linux - file & directory 2

**cd** hello : hello 디렉토리로 들어감. (change directory)
tab 키를 통해 자동완성
부모 디렉토리로 들어가는 방법: 

1. /Users 부터 다시 치기 (절대 경로)
2. cd .. (상대 경로)  
..의 의미: 부모 디렉토리  

**rm** file.txt : file 을 삭제함 (remove)  
-> 디렉토리는 삭제가 되지 않는다  
디렉토리 삭제할 때에는 rm -r 으로 해야 함.  
-help: 명령어 도움말  
**clear** : 내용 지우기


## Linux - -help & man

**man**: 매뉴얼을 보여줌. 전용 페이지 (man mkdir)  
화면에서 /sort : sort 단어 검색. n 키 누르면 페이지 변환  
q 누르면 화면 빠져 나옴  
**-help**: 화면 빠져나가지 않고 간단하게  
mkdir -p : 여러 단계 디렉토리 생성 (dir1/dir2/dir3/dir4…)  
숨김파일 앞에는 . 이 붙는다


## Linux - Searching

ex) create directory in linux 구글에 검색  
**cp** cp.txt dir1/cp.txt   : cp.txt를 dir1 밑에 복사 
**mv** hello.txt dir1/hello.txt : hello.txt를 dir1로 이동   
이름 바꾸기: mv a.txt b.txt : a.txt를 b.txt로 이름 바꿈


## Linux - 명령의 빈도수


## Linux - sudo

**sudo** (super user do) : 슈퍼 유저의 권한이 필요할 때 사용 
그 명령어만 슈퍼 유저의 권한으로 실행


## Linux - file edit (nano)

nano : 파일 편집기  
^ 는 control 키를 의미함  
nano hello.html : 파일 열어 편집  
Kut, Unkut 기능 활용 (복붙시에도)   
^W : 찾기 기능


## Linux - package manager

apt, yum 이 대표적인 package manager   
sudo apt -get update: 최신 목록으로 update  
sudo apt -cache search htop : htop 관련으로 검색
(top: 작업관리자)  
sudo apt -get install htop : htop 앱 설치  
sudo apt -get upgrade : 앱 업그레이드  
sudo apt -get remove htop : htop 앱 삭제  


## Linux - file download: wget

wget (주소) : 다운로드 됨  
-help 이용해서 용법 확인할 것


## Linux - Source download: git

github 사이트: 많은 오픈소스의 저장소  
오픈소스의 url 복사한 후, git clone (주소) react_src : react_src의 디렉토리 아래에 다운로드 됨


## Linux - Why using CLI? 1 - GUI vs CLI

CLI가 훨씬 적은 에너지로 동작 가능  
GUI는 노동을 필요로 함. (기다려야 함)  
CLI는 자동화가 가능


## Linux - Why using CLI? -sequence execution (semicolon)

mkdir why ; cd why — ; 를 사용하면 차례차례 할 수 있음. (여러 개의 명령 한 번에 가능)


## Linux - Why using CLI? (pipeline)

**cat** linux.txt : linux.txt의 내용을 화면에 출력  
**grap** lin linux.txt : linux.txt에서 lin 이 포함된 행을 찾아줌  
ls —help | grap sort : ls —help 를 입력해주는 역할 (앞의 출력을 뒤에 입력, 프로그램 연결)  
ex) ls —help | grap sort | grap file   
ps : 프로세스  
ps aux : 현재 실행되고 있는 프로그램


## Linux - IO Redirection 1 : output

ls -l > result.txt : ls -l의 결과를 result.txt에 저장함
( 1> : 표준출력 )  
error는 표준출력이 아니기 때문에,  
rm rename.txt 2> error.log 와 같이 redirection 가능 (에러의 redirection)


## Linux - IO Redirection 2 : input

cat 만 치면, 사용자가 입력하는 정보를 받는다  
ex) cat < hello.txt  
cat hello.txt 와의 차이? 표준 입력으로 받냐 / 인자로 받냐 의 차이  
head : 앞부분만 출력해줌  
head -n1 linux.txt : linux.txt의 첫째 줄만 출력  
ex) head -n1 < linux.txt > one.txt


## Linux - IO Redirection 3 : append

ls -al >> result.txt : 뒤에 추가가 됨. (append)  
ls -al > /dev/null : 출력도 X, 파일 저장도 X


## Linux - Shell 1: intro

hardware ) kernel ) shell  
kernel: 하드웨어를 직접적으로 제어하는 코어  
shell: 사용자  
shell에 명령 입력 -> 해석해서 kernel에게 전달 -> kernel이 hardware 제어 -> 처리해서 kernel에게 전달 -> shell에게 전달


## Linux - Shell 2: bash vs zsh

echo “hello” : 한 번 더 출력해줌  
echo $0 : shell이 뭔지 알려줌 (bash / zsh)
  

## Linux - Shell script 1 : intro

*.log : * 제외한 부분이 공통 부분인 모든 파일을 의미함  
ex) cp *.log bak : a.log, b.log 와 같은 파일들을 bak에 복사


## Linux - Shell script 2 : example

#!/bin/bash : 밑에 작성되는 코드들이 /bin/bash 를 통해 해석된다

ex) 
```linux
nano backup  
if ! [ -d bak ] ; then
 mkdir bak
fi
cp *.log bak
```

**chmod +x** backup : backup을 실행가능한 형태로 만들어줌. (파일 형태 맨 뒤에 x가 붙는다)  
./backup : backup 실행 (현재 디렉토리에 있는 파일일 때)


## Linux - Directory structure 1

root ( / ) 밑에 있는 다양한 디렉토리. (bin, sbin, etc, var, tmp)


## Linux - Directory structure 2

**cd ~** : 현재 사용자의 홈 디렉토리로 이동  
프로그램 어딨는지 확인: **whereis** htop


## Linux - Process 1 : Computer structure

CPU(Processor) / RAM(Memory) / SSD,HDD(Storage)  
Storage의 프로그램 -> 읽어서 Memory에 적재 -> Processor가 읽어서 동작, 데이터 처리


## Linux - Process 2 : ps top htop

ps : 프로세서 목록 ( **ps aux** 하면 백그라운드까지 뜸 )  
grap, pipeline 이용해서 원하는 거 찾기  
sudo kill (PID) 하면 프로그램 정지 가능


## Linux - File find 1 : locate, find

locate *.log : log 확장자 파일을 모두 찾아줌  
locate는 디렉토리를 뒤지지 않고, 데이터베이스(mlocate)를 뒤진다.   
find : 직접 디렉토리를 뒤져서 찾음  
ex) find / -name *.log  : 이름으로 찾기 ( / : root, ~ : home, . : 현재 디렉토리 )  
find . -type f -name *.log : 타입 지정 ( f : file )


## Linux - File find 2 : whereis, $PATH

PATH에 특정 경로 ( bin 등 ) 가 저장되어 있어 어디에서든 ls를 입력해도 실행된다.  
echo $PATH 를 통해 확인 가능


## Linux - background execute (Ctrl+Z, &)

Ctrl+Z : 프로그램을 백그라운드로 돌림  
fg : 백그라운드 프로그램을 포그라운드로  
jobs : 백그라운드 프로그램 확인  
fg %2 : jobs의 2에 해당되는 프로그램 실행  
kill %2 : 2를 삭제 ( 더 센 삭제 : kill -9 %2 )  
명령 맨 뒤에 & 를 붙이면, 백그라운드에서 명령이 실행되며 다른 명령을 바로 할 수 있음.    
ex) ls -alR / > result.txt 2> error.log &


## Linux - daemon 1 : intro

daemon : 항상 켜져 있는 프로그램  
ex) server : client가 browser를 통해 요청 할 때 바로 응답해야 하기 때문에 항상 켜져 있어야 함.


## Linux - daemon 2 : service & auto start

ex) sudo apt -get install apache2 : apache2 다운로드  
sudo **service** apache2 start : apache2 시작  
sudo service apache2 stop : apache2 멈춤   
( ps aux | grap apache2 로 확인 가능 )   
daemon 프로그램은 service를 이용하여 실행해줘야 함   
시작할 때 자동으로 시작하게 하고 싶으면, /etc/rc3.d/ 밑에 링크를 걸면 된다. (S:시작, K:시작안함)


## Linux - Time based job schedule cron 1 : usage

crontab -e : 적어준 대로 cron이 정기적 작업을 실행시켜줌  
분 시 일 달 요일 ( */1 : 1분마다, * : 상관없음 )  
tail -f date.log : 맨 뒤 문장을 출력, 바뀔 때마다 새로고침 ( - f )   
2>&1 : error를 표준 출력으로 redirect 하여 같이 표시


## Linux - Time based job schedule cron 2 : example



[youtube]: https://www.youtube.com/watch?v=DsG-JWrFJTc&list=PLuHgQVnccGMBT57a9dvEtd6OuWpugF9SH