# ffmpeg
FFmpeg는 음성파일, 영상파일을 기록하거나 변환하는 오픈소스 프로그램입니다.
회사에서 가장 많이 하는 일은 jpg같은 이미지 시퀀스로 동영상을 생성하는 일 입니다.

## 설치 : 이미 빌드되어있는 ffmpeg 설치하기
```
$ cd ~
$ mkdir -p app/ffmpeg
$ cd app/ffmpeg
$ wget http://johnvansickle.com/ffmpeg/builds/ffmpeg-git-64bit-static.tar.xz
$ tar xpvf ffmpeg-git-64bit-static.tar.xz --strip 1
```

## 명령어의 구성
- ffmpeg : 영상, 음성을 변환하는 툴
- ffprobe : 데이터를 분석하는 툴

## 지원하는 포멧과 코덱을 알아보기
자주 사용하게 될 코덱과 포멧을 지원하는지 grep을 통해서 체크해보겠습니다.
```
$ ffmpeg -codecs
$ ffmpeg -codecs | grep prores
$ ffmpeg -codecs | grep dnxhd
$ ffmpeg -codecs | grep h264
$ ffmpeg -codecs | grep hevc
$ ffmpeg -codecs | grep vp9
$ ffmpeg -codecs | grep av1
$ ffmpeg -formats | grep mov
$ ffmpeg -formats | grep mp4
$ ffmpeg -formats | grep webm
$ ffmpeg -formats | grep ogg
```

예) AV1 코덱의 옵션을 알아보는 명령어는 아래와 같습니다.
```
$ ffmpeg -h encoder=libaom-av1
```

## 사용법
mp4를 avi로 변환하기
```
$ ffmpeg -i input.mp4 output.avi
```

jpg시퀀스를 H.264, fps 23.98 .mp4로 만들기
```
$ ffmpeg -f image2 -i /path/filename.%04d.jpg -c:v libx264 -r 23.98 output.mp4
```

input.mp4 영상 분석하기
```
$ ffprobe -v quiet -print_format json -show_format -show_streams input.mp4
```

## Burn-in
ffmpeg를 이용해서 동영상에 글씨를 넣는 방법입니다. 이 방식은 라이센스를 사용하지 않고 동영상에 Burn-In을 할 수 있는 장점이 있습니다.

![ffmpeg_slate](../figures/ffmpeg_slate.png)

예제 소스를 받습니다.
```bash
$ cd ~
$ git clone http://github.com/cgiseminar/examples
```

```bash
$ ffmpeg -f image2 -start_number 100 -i ~/examples/FOO_0010/FOO_0010.%4d.jpg  -vcodec libx264 -cmp 22 -vf "drawtext=fontfile=/usr/share/fonts/gnu-free/FreeMono.ttf: text='CIRCLE, FOO_0010, PLATE, WOONG\ ': timecode='09\:57\:00\:00': fontsize=30: r=23.976: x=(w-tw)/2: y=h-(2*lh): fontcolor=white: box=1: boxcolor=0x00000099" -y output.mov
```
drawtext를 사용하기 위해서는 ffmpeg를 컴파일할 때 configure 옵션에 --enable-libfreetype 옵션을 달아서 컴파일 한 ffmpeg를 사용해야 합니다. 위에서 설치한 ffmpeg는 이미 위 옵션이 활성화되어 컴파일된 ffmpeg 입니다.

#### 자주 사용되는 폰트 경로
슬레이트에 사용하는 폰트는 모노스페이스 폰트를 보통 사용합니다.
모노스페이스 폰트는 각 글자의 가로 길이가 같은 폰트이고 글씨가 애니메이션되더라도 자간이 흔들리지 않는 특징이 있습니다.

- CentOS : /usr/share/fonts/gnu-free/FreeMono.ttf
- macOS : /Library/Fonts/Courier New.ttf

#### 실습
대량의 데이터를 각각 다른 Slate가 처리되도록 스크립트를 작성해봅시다.

#### Reference
- https://video.stackexchange.com/questions/14924/ffmpeg-drawtext-clipping-to-a-bounding-box

## FFmpeg 컴파일 설치방법
직접 ffmpeg를 설치하는 문서입니다.

https://trac.ffmpeg.org/wiki/CompilationGuide/Centos


## 레퍼런스
- ffmpeg와 비슷한 명령어 libav : https://www.libav.org
- ffmpeg와 libav의 분쟁 : http://klutzy.nanabi.org/blog/2012/11/16/ffmpeg-libav/