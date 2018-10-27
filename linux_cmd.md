# 리눅스 명령어
파이썬 스크립트를 짜기전에 리눅스 명령어를 잘 알고 있으면 코드를 이해하는데 많은 도움이 됩니다.
우리가 배우는 명령어도 결국 C로 짜여진 프로그램이기 때문이죠.

### ls
현재경로의 파일을 출력하는 명령어.

- 모든 파일(숨김파일포함)을 출력하며 list 형태로 출력하는 방법
```
$ ls -al
```

- 현재경로의 exr 파일을 출력.
```
$ ls *.exr
```

- 현재경로에서 1000 프레임의 시퀀스만 검색
```
$ ls filename.1???.exr
```

### . / ..
`.` 문자는 현재경로라는 뜻을 가진 문자입니다.
`..` 문자는 상위경로라는 뜻을 가진 문자입니다.
리눅스의 모든 경로는 언제나 현재경로와 상위 경로를 가지기 때문에 `ls -al` 명령어를 타이핑하면 항상 이 두개의 문자가 먼저 출력됩니다.
```
$ ls -al
```
![image](https://user-images.githubusercontent.com/1149996/47605489-03b9b900-da42-11e8-828d-4cf2ea705057.png)

### ~
홈디렉토리 경로를 의미하는 문자입니다. 

- 터미널에서 `~` 문자만 타이핑하면 어떤 경로인지 친절하게 알려줍니다.
```
[woong@localhost ~]$ ~
-bash: /home/woong: 디렉터리입니다
```

### cd
경로를 이동하는 명령어입니다.

- 현재 경로로 이동하는 명령은 아래와 같습니다.
```
$ cd .
```

- 상위 경로로 이동하는 명령어.
```
$ cd ..
```

- 홈디렉토리로 이동하는 명령어. 아주 많이 사용됩니다.
```
$ cd ~
```

### /
경로를 구분하는 문자입니다.
유닉스, 리눅스는 `/`문자로 폴더를 구분합니다.
윈도우즈는 `\` 문자를 경로의 문자로 사용합니다.

- 상위의 상위 경로로 이동하는 명령어
```
$ cd ../..
```

### cp

### mv

### mkdir

### 숨김폴더, 숨김파일 만들기

### rm, rmdir

### pwd

### df, du

### cat

### more, head, tail

### which, whereis

### touch

### echo

### reboot

### shutdown now