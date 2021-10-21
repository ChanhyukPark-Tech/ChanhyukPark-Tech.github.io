---
title:  "[ChunK] 소리 파일과 소리 조작"

categories:
  - ChunK
tags:
 - [ChunK, Music, Sound]

toc: false
toc_sticky: true

---

> 이 포스트는 한양대학교 음악프로그래밍(CSE2020) 도경구 교수님 수업을 참조하였습니다. 개인적으로 공부하면서 참조하려고 만든 포스트입니다.



# 5. 소리 파일과 소리 조작
 - 채집/합성한 소리를 디지털 데이터로 변환하여 소리 파일에 기록 
 - 인간이 소리를 기록할 수 있는 것은 과거에는 녹음기, Tape , LP record 같은 것은 physical 한 것들이였다.
 - 컴퓨터가 생기고 나서는 소리를 전자적으로 기록 할 수 있게 되었다.
 - 소리 파일(sound files) = 샘플(samples)
 - 파일로 저장되어 있는 샘플을 프로그램에서 읽어와서 음악 프로그램에 소리 데이터로 활용 

> 사운드 샘플 : 전체가 아니라 일부분, 프로그래밍으로 음악을 만드는데 내가 갖고 있는 일부의 샘플들을 이용하여, 반복해서 사용하여 음악에 집어넣는것


# 5-1. 샘플링
![image](https://user-images.githubusercontent.com/69495129/135948752-86673eef-5a22-4a46-8f8b-aa4e549f9e70.png)

>컴퓨터 프로그램에서 소리(음파,sound waveform)를 처리하기 위해서, 
> 소리를 디지털 데이터인 수로 표현한 디지털 시그널(digital signal)로 변환해야 하는데 이 변환 장치를 ADC(Analog-to-Digital Converter, 아날로그/디지털 변환기)라고 한다. 
> ADC의 변환 작업을 샘플링(sampling)이라고 하고, 
> 변환한 디지털 데이터를 샘플(sample)이라고 한다.
> 샘플링 기간(sampling period)를 정하고 이 기간 동안의 소리 정보를 수로 변환하여 하나의 샘플로 저장한다.
> 샘플 하나를 저장하는 공간의 크기는 8비트(일반), 16비트(음악)(일반 표준), 24비트(고음질 음악) 중 하나를 선택한다. 저장 공간이 클수록 원음과 가까운 소리를 표현할 수 있다. 샘플링 기간은 얼마나 빈번하게 소리를 샘플링하는지에 따라서 결정되는데, 보통 초당 44,100개의 샘플을 채취한다. 
> 이를 샘플링 비율이라고 하는데, 높을수록 (초당 더 샘플을 더 많이 채취할수록) 음질이 좋아진다.

>1/44,100 초에 하나의 소리를 일반적으로 16비트에 저장한다.
>super audio cd 같은 경우에는 1/88,200 초에 하나의 소리를 일반적으로 16비트에 저장한다.
>더 실제와 같은 소리를 내기 위해서는 짧은 sample period 를 사용해야한다.


# 5-2 . 샘플을 담는 장치 `SndBuf`
![image](https://user-images.githubusercontent.com/69495129/135948763-b80f3519-5596-4402-8692-b0e85c7d9b38.png)
<br>

[Unit Generators 에 대한 설명](https://chuck.cs.princeton.edu/doc/program/ugen.html)
>UGen 중에 하나인 Sound Buffer 에다가 소리를 저장할 수 있다.

지금 어디를 Play(소리를 가르키나)는 playhead 로 가르키고 있다.


| 메소드 | 값의 범위    | 설명                                     |
| ------ | ------------ | ---------------------------------------- |
| .read  |              | SndBuf에 로딩                            |
| .pos   | 0~.samples() | playhead 의 위치                         |
| .gain  | 0.0~1.0      | 소리 크기                                |
| .rate  | float        | 1.0이 정상 진행 속도, 음수는 거꾸로 진행 |

rate를 음수로 설정하면, 거꾸로 진행되는 것이 신기하다.

- 소리 파일의 종류
  - ```.wav``` (from wave or waveform)
  - ```.aif``` (from audio interchange file or format)


```java
SndBuf sample => dac;   // SndBuf 선언
me.dir() + "audio/snare_01.wav" => string filename; // audio sound file 경로
filename => sample.read; // 파일을 읽어준다.
0.5 => sample.gain;   // 소리의 크기를 0.5로 한다.
0 => sample.pos;    //
second => now;        // 소리를 내준다.
```

```스테레오``` : 소리의 소스는 하나인데 두개의 귀로 듣기 때문에 어느정도의 입체감을 줄 수 있다.

지금까지 dac 을 사용했을 때는 소리가 한쪽으로만 나오지만, dac.left , dac.right 로 처리하면 입체감을 얻을 수 있다.

```java
SndBuf sample1 => dac.left;  
SndBuf sample2 => dac.right;
me.dir() + "/audio/snare_01.wav" => sample1.read;
me.dir() + "/audio/hihat_01.wav" => sample2.read;
0.5 => sample1.gain => sample2.gain;
0 => sample1.pos => sample2.pos;
second => now;
```

***

![image](https://user-images.githubusercontent.com/69495129/135948795-c1bb2b43-3d6b-4dcd-8df2-b24cc62ce6d1.png)


```패닝(panning)``` : 녹음할 때의 기술. 다양한 소리의 소스의 위치를 지정해 줄 수 있다. 가장 정중앙의 위치를 0.0 으로 한다. 내가 특정 소스를 특정 위치에서 소리내게 할 수 있다.
<br>
```Pan2``` 라는 Unit Generators 를 사용한다.
- spread mono signal to stereo


```java
Noise n => Pan2 p => dac;
0.2 => n.gain;
float position;
while (true) {
    Math.sin(now/second) => position;
    <<< position >>>;
    position => p.pan;
    ms => now;
}
```

***

1초에 10번 북소리가 나는데 한번 소리가 날 때마다 pan 의 위치를 이동시켜준다.
5초동안 맨 왼쪽에서 1초에 10번 북을 두드리면서 중간을 거쳐서 오른쪽 끝으로 간다.
```java
SndBuf sample => Pan2 p => dac;
0.5 => sample.gain;
me.dir() + "/audio/snare_01.wav" => sample.read;
-0.1 => float position;
while (position < 1.0) {
    0 => sample.pos;
    position => p.pan;
    <<< position >>>;
    0.02 +=> position;
    100::ms => now;
} 
```

재생 속도 변화(rate를 사용)

```java
SndBuf sample => Pan2 p => dac;
0.5 => sample.gain;
me.dir() + "/audio/cowbell_01.wav" => sample.read;
while (true) {
    Math.random2f(0.1,1.0) => sample.gain; // volume
    Math.random2f(-0.1,1.0) => p.pan; // panning
    Math.random2f(0.2,1.8) => sample.rate; // speed
    0 => sample.pos;
    500::ms => now;
} 
```

***

![image](https://user-images.githubusercontent.com/69495129/135948866-9430cc41-26ae-4c66-b8ea-b02f60eaa940.png)


거꾸로 재생
.pos를 맨 뒤로 가져다두고 rate를 음수로 지정한다.

```java
SndBuf sample => dac;
0.5 => sample.gain;
me.dir() + "/audio/hihat_04.wav" => sample.read;  // 드럼에서 징

0 => sample.pos;  // move the play head to the front  // 처음 위치로 지정
sample.length() => now; // play     // 파일의 길이를 처음부터 읽어라 length 는 dur type
  
sample.samples() => sample.pos; // move the play head to the end // samples() 는 int type
-1.0 => sample.rate; // set the play direction backward
sample.length() => now; // play
```
***
배열을 활용하면 여러가지 사전 소리들을 편하게 사용할 수 있다.

```java
SndBuf sample => dac;
string snare_samples[3];
me.dir() + "/audio/snare_01.wav" => snare_samples[0];
me.dir() + "/audio/snare_02.wav" => snare_samples[1];
me.dir() + "/audio/snare_03.wav" => snare_samples[2];

while (true)
    for (0 => int i; i < snare_samples.size(); i++) {
        snare_samples[i] => sample.read;
        0.5::second => now;
    }

```

Sound Buffer 자체도 배열로 선언이 가능하다.

```java
SndBuf sample[3];
sample[0] => dac.left;
sample[1] => dac;
sample[2] => dac.right;
me.dir() + "/audio/snare_01.wav" => sample[0].read;
me.dir() + "/audio/snare_02.wav" => sample[1].read;
me.dir() + "/audio/snare_03.wav" => sample[2].read;

while (true)
    for (0 => int i; i < sample.size(); i++) {
        0 => sample[i].pos;
        0.5::second => now;
    }

```
***
SndBuf 는 자체가 mono 이다 SndBuf2 는 사운드 파일 자체가 스테레오 라면 그대로 사용할 수 있도록한다.
스테레오 소리 파일 재생

```java
SndBuf2 stereo_sample => dac;
me.dir() + "/audio/stereo_fx_01.wav" => stereo_sample.read;
stereo_sample.length() => now;
```

***

`Gain` 이라는 Unit Generator 을 사용할 수 있다. 순전히 Volume 을 Control 하기 위한 Unit generator 이다.
왼쪽 채널의 볼륨조절, 오른쪽 채널의 볼륨조절을 따로하고 싶은경우
```java
SndBuf2 stereo_sample;
me.dir() + "/audio/stereo_fx_01.wav" => stereo_sample.read;
Gain bal[2];
stereo_sample.chan(0) => bal[0] => dac.left;
stereo_sample.chan(1) => bal[1] => dac.right;
stereo_sample.length() => now;
```

***

볼륨을 조절해보자. balance control 을 해보자
> balance control : 지금 스테레오는 왼쪽에서 오른쪽으로 소리가 이동하는 상황이다. 
> 효과를 극대화 시키기위해 오른쪽에 소리가 있을때에는 오른쪽의 소리를 크게 하고 왼쪽에 소리가 있다면 왼쪽의 소리를 크게해주자.



```java
SndBuf2 stereo_sample;
me.dir() + "/audio/stereo_fx_01.wav" => stereo_sample.read;
Gain bal[2];
stereo_sample.chan(0) => bal[0] => dac.left;
stereo_sample.chan(1) => bal[1] => dac.right;
stereo_sample.length() => now;

second => now;

0 => stereo_sample.pos;
float balance, volume_right;
-1.0 => balance;
stereo_sample.length() / 21 => dur length;
while (balance <= 1.0 ) {
    (balance + 1) / 2.0 => volume_right;
    volume_right => bal[0].gain;
    1 - volume_right => bal[1].gain;
    length  => now;
    0.1 +=> balance;
}
```

***
계속 해서 소리를 듣고 싶다.
loop 을 1로 세팅해주면 pos를 0으로 원위치 시켜야할 필요가 없다. 자동으로 pos을 0 으로해준다.
```java
SndBuf2 stereo_sample;
me.dir() + "/audio/stereo_fx_03.wav" => stereo_sample.read;
Gain bal[2];
stereo_sample.chan(0) => bal[0] => dac.left;
stereo_sample.chan(1) => bal[1] => dac.right;
1 => stereo_sample.loop; // 자동 반복

float balance, volume_right;
while (true) {
    Math.random2f(0.2, 1.8) => stereo_sample.rate; 
    Math.random2f(-1.0, 1.0) => balance; 
    (balance + 1) / 2.0 => volume_right;
    volume_right => bal[0].gain;
    1 - volume_right => bal[1].gain;
    0.3::second => now;
}
```
***

타입 변환 메소드

| 메소드 | 값의 범위    | 설명                                     |
| ------ | ------------ | ---------------------------------------- |
| .read  |              | SndBuf에 로딩                            |
| .pos   | 0~.samples() | playhead 의 위치                         |
| .gain  | 0.0~1.0      | 소리 크기                                |
| .rate  | float        | 1.0이 정상 진행 속도, 음수는 거꾸로 진행 |




## Summary
***


🌜 주관적인 견해가 담긴 글입니다. 다양한 의견이 있으실 경우
언제든지 댓글 혹은 메일로 지적해주시면 감사하겠습니다! 😄

