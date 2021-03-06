### 많이 사용하는 명령어

[CentOS 항목으로](https://github.com/juneyoung/DEV-INFOS/edit/master/CentOS)

#### 폴더 목록 조회(`ls`)
```
# 보통 -alh 옵션 많이 사용. a 는 all, ㅣ은 링크, h 는 크기 옵션
$> ls
```

#### 폴더 사이즈 조회(`du`)
```
$> du 
```

#### 폴더 소유자 및 권한 변경(`chown`, `chmod`)
```
# 권한변경. 보통 -R 옵션이랑 같이 쓰임. R은 recursive
$> chmod 777 [대상]
# 소유자 변경
$> chown [사용자]:[사용자그룹] [대상]
```

#### 파일의 이동및 복사(`cp`, `mv`) 
`mv` 의 경우 파일명을 변경할 때도 사용. 가령 `mv a.text a1.text`
```
# 일반적으로 -r 옵션으로 하위도 다 적용함
$> cp [현재 파일] [대상경로]
$> mv [현재 파일] [대상경로]
```

#### 파일의 압축 및 해제(`tar`)
`tar` 명령을 사용함
```
# c-compress, v-view,  
$> tar -cvf [압축파일명] [대상]
$> tar -xvf [대상]
```

#### 파일 내용보기(`cat`)
`vi` 로는 드래그가 안되서 답답한 면이 있는데 `cat` 으로 쏘면 긁어 붙일 수 있어서 편하다. 일반적으로 `grep` 명령어로 필요한 정보만 잡는게 일반적
```
$> cat [파일명]
```

#### 프로세스 조회하기(`ps`, `ptree`,  `top`)
`ps` 는 현재 실행중인 프로세스를 볼 수 있다.(`PID`, `PPID`, 및 구동 커맨드를 알 수 있음). `ptree` 는 현재 프로세스의 부모/자식을 보여줌. `top` 은 실시간으로 메모리 사용량 등을 검사하는데 사용됨.
```
# -e 는 전체, f 는 형식. 형식에 맞게 전체 프로세스 노출
$> ps -ef
# 프로세스 부모 자식 노출
$> ptree
# 실시간 프로세스 메모리 사용보기
$> top
```

#### 권한관리(`sudo`, `su`)
```
#사용자 변경> 해당 사용자 비번 요구
$> su [사용자명]
#현재 사용자로 루트권한 사용 > 현재 사용자 비번 요구
$> sudo su 
```

#### History
- 2017.04.29 : 초안작성
