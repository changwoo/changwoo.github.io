---
layout: post
title:  "티맥스오에스 살펴보기"
date:   2019-05-31 00:00:00 +0900
tags: tmax tmaxos debian
categories: hacks
---

(트위터에서 옮김.)

다른 분들의 [@Realignist](https://twitter.com/Realignist)
[@perillamint](https://twitter.com/perillamint)
[@segfault87](https://twitter.com/segfault87) 티맥스오에스 설치기를 보고 알게
된 티맥스오에스의 apt 저장소에 들어 있는 패키지 내용을 내 전문성?을 발휘해
살펴 봤는데, ISO는 없고 온라인 패키지만 살펴본 것이니 한계는 있겠지만. 내용은
일반적인 커스텀 배포판과 다르지 않다.

단 티맥스 전용 소프트웨어는 패키지 목록에 없는 것으로 보아 설치 ISO에만 들어
있는 것 같고 패키지 흔적을 찾을 수 없었다. 패키지 내용은 데비안 10 buster에서
많은 패키지를 줄였다. 남아있는 패키지 목록을 봐도 의미없는 게 많은데 패키지를
뺀 이유는 알 수 없었다.

데비안 10/buster가 릴리스되지 않은 버전이 맞는데, 커스텀 배포판은 원래 이렇게
릴리스 예정 버전 갖고 만드는 게 맞다. 우분투도 그렇게 하고 있고. 2년 전의
데비안 9 썼다면 오히려 그게 바보짓이다. 데비안은 말이 unstable/testing이지
나부터 일상과 업무용으로 쓰고 있고 별다른 문제 없음.

티맥스가 바꾼 부분을 구체적으로 들어가면. 커스텀 배포판에서 당연히 바꾼다고
예상할 수 있는 부분이 있는데 fontconfig의 글꼴 설정, plymouth의 부팅 화면
브랜딩 이런 단골 메뉴를 바꿨다. 또 apt 저장소 키를 배포해야 되니
tmaxos-archive-keyring이라는 패키지를 당연히 추가.

또 배포판을 빌드할 때 꼭 필요한 debootstrap을 수정했는데 (패키지로 부팅 가능
시스템 빌드하는 SW), 버전 1.0.114 수정해서 1.0.114.1 이렇게 버전을 붙여놨다.
ㅁㄴㅇㄹ 이렇게 하는 거 아닌데 본래 버전 혼동되게 하지 말고 우분투처럼
1.0.114tmaxos1 이런 식으로 해 주시면 안 될까요.

티맥스 전용 소프트웨어의 경로를 빌드 경로에 끼워넣는 패치는 여러 군데 들어
있다. 왜 유닉스 관습과 다르게 /system/{include,lib} 경로에 자기들 라이브러리를
설치해 놓고 x고생을 하는지 모를 일이다.

티맥스에서 새로 만든 패키지 중에 이상하게 libopenh264가 있는데, 시스코
OpenH264 코덱은 법적인 문제로 데비안에 안 들어 있고 debian-multimedia에만 들어
있다. 그냥 debian-multimedia에 있는 거 쓰면 되는데 있는지 몰라서 새로 만든 게
아닐까 의심.

또 하나 흥미로우면서도 비판할만한 부분은 사운드서버인 pulseaudio에 추가한
libpulse-mainloop-tos 패키지이다. 유일한 기능 패치라고 할 수 있는데 pulseaudio
코드를 이해해야 정확히 알 수 있겠지만 티맥스 전용 테스크톱과 사운드 입출력을
주고받는 기능을 pulseaudio에 추가한 것으로 보인다.

이 패치의 존재로 즉 티맥스오에스 데스크톱 앱 전용 사운드 API가 있다는 걸
유추할 수 있다. 공공시장의 이른바 "개방형OS"가 티맥스와 함께 언급될 때 우려할
수 있는 부분이 이런 부분이다. 티맥스와 같은 회사가 원하는 건 개방이 아니라 또
다른 락인이다.

이윤을 추구하는 기업으로서 이런 방향을 추구하겠다는 생각이면 그것만 가지고
나쁘다고 말할 수는 없으나, 한편으로는 OS의 MS 종속을 해소하겠다거나 개방성
높이자고 말하는 정책 사업에 티맥스 전용 API가 등장하는 건 모순적이다.
여기까지.