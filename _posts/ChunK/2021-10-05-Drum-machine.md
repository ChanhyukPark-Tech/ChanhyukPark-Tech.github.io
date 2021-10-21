---
title:  "[ChunK] 드럼 머신"

categories:
  - ChunK
tags:
  - [ChunK, Music, Drum,machine]

toc: true
toc_sticky: true

---

> 이 포스트는 한양대학교 음악프로그래밍(CSE2020) 도경구 교수님 수업을 참조하였습니다. 개인적으로 공부하면서 참조하려고 만든 포스트입니다.


# 5.3 사례 학습 : 드럼 머신

### 드럼 머신 1호

```java
Gain master => dac; // master에서 전체볼륨을 조절가능
SndBuf kick => master;  //악기를 master한테 연결한다
SndBuf snare => master;
me.dir() + "/audio/kick_01.wav" => kick.read;
me.dir() + "/audio/snare_01.wav" => snare.read;
kick.samples() => kick.pos; // 처음에는 둘다 소리를 맨뒤에 놓자
snare.samples() => snare.pos; // 처음에는 둘다 소리를 맨뒤에 놓자

0.5::second => dur TEMPO; // constant variable 은 capital letter
while (true) {
    0 => kick.pos;  // 내가 내고싶은 소리의 pos을 0 으로 설정후 시간을 보낸다
    TEMPO => now;
    0 => snare.pos;
    TEMPO => now;
}
```
***

항상 kick 이 소리나는것을 원하지 않고 4번마다 한번 kick 의 소리가 나길 원한다.
이때 for loop 와 나머지연산을 사용하면 다음과 같다.

```java
Gain master => dac;
SndBuf kick => master;
SndBuf snare => master;
me.dir() + "/audio/kick_01.wav" => kick.read;
me.dir() + "/audio/snare_01.wav" => snare.read;
kick.samples() => kick.pos;
snare.samples() => snare.pos;

0.2::second => dur TEMPO;
while (true) {
    for (0 => int beat; beat < 16; beat++) {
        <<< beat >>>;
        if (beat == 0 || beat == 4 || beat == 8 || beat == 12) // 4번마다 한번씩 kick 소리를 낸다 
            0 => kick.pos;      
        if (beat == 2 || beat == 5 || beat == 7 || 
            beat == 9 || beat == 10 || beat == 11 ||
            beat == 13 || beat == 14)  // 이것이 참일때 snare 소리를 낸다
            0 => snare.pos;
        TEMPO => now;
    }
}
```
위의 코드는 하나하나 조건문에 지정을 해줘야하기 때문에 소리를 내고 싶을때 불편한 점이있다.

***

배열을 사용하여 소리를내고 싶을때 1 소리를 안낼때 0 으로 미리 지정을 해두자.


```java
Gain master => dac;
SndBuf kick => master;
SndBuf snare => master;
me.dir() + "/audio/kick_01.wav" => kick.read;
me.dir() + "/audio/snare_01.wav" => snare.read;
kick.samples() => kick.pos;
snare.samples() => snare.pos;

0.2::second => dur TEMPO;
[1,0,0,0, 1,0,0,0, 1,0,0,0, 1,0,0,0] @=> int kick_hits[];
[0,0,1,0, 0,1,0,1, 0,1,1,1, 0,1,1,0] @=> int snare_hits[];

while (true) {
    for (0 => int beat; beat < kick_hits.size(); beat++) {
        <<< beat >>>;
        if (kick_hits[beat]) 
            0 => kick.pos;
        if (snare_hits[beat]) 
            0 => snare.pos;
        TEMPO => now;
    }
}
```

***

`하이햇` 을 추가해서 좀더 다양한 소리를 내보자.
SnbBuf 3개를 지정한 후 각각 파일로부터 소리를 읽어주자.
처음에는 소리를 안나게 하기 위해 세개 모두 pos을 samples() 로 지정해준다.

```java
Gain master => dac;
SndBuf kick => master;
SndBuf snare => master;
SndBuf hihat => master;
me.dir() + "/audio/kick_01.wav" => kick.read;
me.dir() + "/audio/snare_01.wav" => snare.read;
me.dir() + "/audio/hihat_01.wav" => hihat.read;
kick.samples() => kick.pos;
snare.samples() => snare.pos;
hihat.samples() => hihat.pos;
0.3 => hihat.gain;

0.2::second => dur TEMPO;
[1,0,0,0, 1,0,0,0, 1,0,0,0, 1,0,0,0] @=> int kick_hits[];
[0,0,1,0, 0,1,0,1, 0,1,1,1, 0,1,1,0] @=> int snare_hits[];
[0,1,0,1, 0,0,1,1, 0,0,1,1, 0,1,1,1] @=> int hihat_hits[];

while (true) {
    for (0 => int beat; beat < kick_hits.size(); beat++) {
        <<< beat >>>;
        if (kick_hits[beat]) 
            0 => kick.pos;
        if (snare_hits[beat]) 
            0 => snare.pos;
        if (hihat_hits[beat]) 
            0 => hihat.pos;
        TEMPO => now;
    }
}
```

***
master 배열을 선언할 수도 있다.
원하는 소리를 원하는 방향에 지정할 수 있다 (스테레오 효과)

```java

Gain master[3];
master[0] => dac.left; // 채널을 왼쪽에
master[1] => dac;
master[2] => dac.right;

SndBuf kick => master[1];  // 중간에
SndBuf snare => master[1];   //중간에
SndBuf cowbell => master[0];  // 왼쪽
SndBuf hihat => master[2];   // 오른쪽

SndBuf claps => Pan2 p;
p.chan(0) => master[0];
p.chan(1) => master[1];

me.dir() + "/audio/kick_01.wav" => kick.read;
me.dir() + "/audio/snare_01.wav" => snare.read;
me.dir() + "/audio/hihat_01.wav" => hihat.read;
me.dir() + "/audio/cowbell_01.wav" => cowbell.read;
me.dir() + "/audio/clap_01.wav" => claps.read;

[1,0,1,0, 1,0,0,1, 0,1,0,1, 0,1,1,1] @=> int cow_hits[];
cow_hits.size() => int MAX_BEAT;
4 => int MOD;
0.2::second => dur TEMPO;

0 => int beat;
0 => int measure;
while (true) {
    if (beat % MOD == 0) 
        0 => kick.pos;
    if (beat % MOD == 2 && measure % 2 == 1) // 홀수번째 마디 
        0 => snare.pos;
    if (measure > 1) {  //첫두마디는 하지말고, 3번째 마디 이후부터 소리를내라
        if (cow_hits[beat])
            0 => cowbell.pos;
        else {
            Math.random2f(0.0,1.0) => hihat.gain;
            0 => hihat.pos;
        }
    }
    if (beat > 11 && measure > 3) { // 처음 4measure 는 하지말고 그다음 measer부터
        Math.random2f(-1.0,1.0) => p.pan;
        0 => claps.pos;
    }
    TEMPO => now;
    (beat + 1) % MAX_BEAT => beat;
    if (beat == 0)
        measure++;  //measure 는 전체 배열 
}
```
***

[실습1] 소리 샘플 파일 들어보기

다운 받은 audio 폴더에는 소리 파일 샘플이 들어있다. 각 샘플의 소리를 차례로 모두 들어볼 수 있도록 프로그램을 만들어보자. 각 샘플이 내는 소리의 길이는 다양하다. 샘플의 길이는 samples()(샘플의 개수를 int 값으로 리턴) 또는 length()(샘플의 길이를 dur 값으로 리턴) 메소드를 호출하여 알아낼 수 있다. 샘플의 끝까지 소리내야 하고 (방법은 아래 예 참조), 각 샘플 사이에 1초의 간격을 둔다.


[실습2]
아래 프로그램을 다음 요구 사항에 맞추어 수정해보자.

- hihat_01.wav 소리 샘플을 2, 5, 6 박자에 소리나도록 추가한다.
- Gain UGen으로 세 개의 소리를 믹스하는 대신, 스테레오 스피커에서 하나는 중앙, 다른 하나는 오른쪽, 또 다른 하나는 왼쪽에서 소리나도록 분리한다.

`기존코드`
```java
Gain master => dac;
SndBuf kick => master;
SndBuf snare => master;
me.dir() + "/audio/kick_01.wav" => kick.read;
me.dir() + "/audio/snare_01.wav" => snare.read;
kick.samples() => kick.pos;
snare.samples() => snare.pos;

0.2::second => dur TEMPO;
while (true) {
    for (0 => int beat; beat < 16; beat++) {
        <<< beat >>>;
        if (beat == 0 || beat == 4 || beat == 8 || beat == 12) 
            0 => kick.pos;
        if (beat == 4 || beat == 10 || beat == 13 || beat == 14) 
            0 => snare.pos;
        TEMPO => now;
    }
}
```
수정코드

```java
Gain master[3] => dac; // master array 3

master[0] => dac;
master[1] => dac.left;
master[2] => dac.right;


SndBuf kick => master[0];
SndBuf snare => master[1];
SndBuf hihat => master[2];
me.dir() + "/audio/kick_01.wav" => kick.read;
me.dir() + "/audio/snare_01.wav" => snare.read;
me.dir() + "/audio/hihat_04.wav" => hihat.read;

kick.samples() => kick.pos;
snare.samples() => snare.pos;
hihat.samples() => hihat.pos;



0.2::second => dur TEMPO;
while (true) {
    for (0 => int beat; beat < 16; beat++) {
        <<< beat >>>;
        if (beat == 0 || beat == 4 || beat == 8 || beat == 12) 
            0 => kick.pos;
        if (beat == 4 || beat == 10 || beat == 13 || beat == 14) 
            0 => snare.pos;
        if (beat == 2 || beat == 5 || beat == 6 ) 
            0 => hihat.pos;
        TEMPO => now;
    }
}
```
## Summary
***


🌜 주관적인 견해가 담긴 글입니다. 다양한 의견이 있으실 경우
언제든지 댓글 혹은 메일로 지적해주시면 감사하겠습니다! 😄

