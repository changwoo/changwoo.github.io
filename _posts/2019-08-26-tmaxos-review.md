---
layout: post
title:  "티맥스OS 리뷰: 대체 왜?"
date:   2019-08-26 00:00:00 +0900
tags: tmaxos linux debian opensource
categories: hacks
---

2019년 8월 14일에 공개된 티맥스OS 버전을 이제야 제대로 실행해 보고 드는 생각.
물론 오랜 리눅스 사용자, 데비안 개발자, 소프트웨어 엔지니어로서 단순히 실행한
것은 아니고 각 부분이 어떻게 돌아가는지, 어떤 부분이 리눅스와 데비안의 기능을
이어받았고, 어떤 부분을 바꾸고 추가했는지, 왜 이러한 선택을 했을까 생각하면서
살펴봤다. 오픈소스가 아닌 부분은 어느 정도는 짐작할 수밖에 없었지만 그래도 꽤
많은 것을 알 수 있었다.

결과적으로 보면 티맥스OS에는 흔히 생각하는 것보다 많은 노력이 들어갔다. 안
보고 리눅스에 껍데기만 씌웠다 정도라고 말하기는 쉽지만, 실제 여기저기를
뜯어보면 티맥스에서 그런 말을 듣기에는 억울할 것 같을 정도로 많은 부분을
티맥스에서 자체적으로 만들었다. 물론 거짓 홍보를 남발하던 지난 역사가 있었기
때문에 티맥스OS와 관련된 모든 것을 의심하는 게 당연하고, 나 역시 계속 의심을
하면서 살펴봤지만 실체를 보면 티맥스 측에서 자체 개발했다고 발표했던 부분을
자체 개발한 것은 꽤 사실이었다.

티맥스OS에서는 리눅스의
[DRM](https://en.wikipedia.org/wiki/Direct_Rendering_Manager)
[GBM](https://www.systutorials.com/docs/linux/man/7-drm-gem/)을 이용해 버퍼를
전달하고 [Mesa](https://www.mesa3d.org/)를 통해
[EGL](https://en.wikipedia.org/wiki/EGL_(API))을 사용하는, 2D/3D 하드웨어
가속을 하는 자체 컴포지트 디스플레이 서버를 만들었다. 정확한 방식은 알 수
없었지만
[Wayland](https://en.wikipedia.org/wiki/Wayland_(display_server_protocol))
프로토콜을 사용하지도 않는다. 기존의 오픈소스 툴킷 라이브러리는 여기에
호환되지 않고 자체적인 GUI 툴킷도 들어 있다. [GTK](https://www.gtk.org/)에서
[Cairo](https://cairographics.org/)를 사용하는 것처럼 2D 드로잉은
[Skia](https://skia.org/) 그래픽 라이브러리를 사용한다.

[WINE](https://www.winehq.org/)의 껍데기 정도로 생각했던 윈도우 에뮬레이션
기능도 WINE 프로젝트의 결과물을 여기 저기에서 사용하기는 하지만, 커널 레벨에서
PE 바이너리를 디텍트하고 (여기까지는 리눅스의
[binfmt](https://en.wikipedia.org/wiki/Binfmt_misc) 기능) 변환하는 것까지 하는
기묘한 자체적인 방법을 사용한다.

tnetd라는 자체 네트워크 관리 서버가 돌아간다. 지금은 리눅스 시스템에서
일반화되어 있는
[NetworkManager](https://wiki.gnome.org/Projects/NetworkManager)는 사용하지
않는다.

[크로미움](https://www.chromium.org/)에서 이름만 바꾼 브라우저로 생각했던
ToGate 브라우저도 위에서 말한 자체 GUI 덕분에 GTK 프론트엔드를 빼고 자체 GUI용
라이브러리를 붙여놨다.

정말 많은 노력을 기울였다는 사실은 인정해야 한다. 문제는 이렇게 실제로 노력을
한 것들이 무슨 의미가 있는지이다. 그냥 리눅스 데스크톱 쓰는 것과 비교해서 뭐가
더 낫길래 티맥스는 그 시간과 돈과 인력을 투입한 것일까?

자체 디스플레이 서버를 만드는 일이 아주 불가능한 일은 아니다. 우분투를 만든
[캐노니컬](https://canonical.com/)도
[Mir](https://en.wikipedia.org/wiki/Mir_(software)) 디스플레이 서버를
만들었었으니까. 하지만 Mir가 망한 것처럼 하드웨어 벤더들의 지원을 받으면서
새로운 환경의 생태계를 만들기는 쉽지 않다. 티맥스 측에서는 "무거운 X 윈도우
시스템"을 대체한다고 어떤 언론 기사에서 밝혔지만, 이는 몇년 전에나 할 수 있는
이야기이다. 비슷한 목표를 가지고 비슷한 기술 스택으로 구성된 Wayland가
기본으로 탑재되는 배포판/데스크톱이 많아진
([Fedora](https://fedoramagazine.org/fedora-25-released/) 및
[Debian](https://www.debian.org/News/2019/20190706)) 지금 이 때에 이런 문제
제기는 유효하지 않다.

가상머신에서 똑같이 2D 가속을 위해 DRM 드라이버를 설치한 상태에서 아무리 봐도
[GNOME+Wayland](https://wiki.gnome.org/Initiatives/Wayland) 환경보다 빠르거나
가볍다고 느껴지지 않았고, 파이어폭스와 그놈 터미널을 띄운 GNOME/Wayland 세션과
ToGate와 터미널을 띄운 티맥스OS 세션을 비교해 보면 티맥스OS 쪽이 1.4배나 더
많은 메모리를 사용했다. (ToGate는 크로미움이니까 파이어폭스보다 메모리를
차지하는 거야 어쩔 수 없다고 쳐도 software_center 프로세스가 브라우저만큼 많은
메모리를 차지하는 건 이상했다.) X11 호환성으로
[Xvfb](https://www.x.org/releases/X11R7.6/doc/man/man1/Xvfb.1.xhtml)를
이용하고 있는데, 내가 아는 Xvfb라면 여기서 실행한 X 호환 프로그램은 Wayland의
[Xwayland](https://wayland.freedesktop.org/docs/html/ch05.html)와는 다르게
하드웨어 가속 효과도 받지도 못한다. 소프트웨어 개발 측면에서 훌륭한 구조를
보여주는 것도 아니다. (지난 5월 유출된 티맥스OS 헤더 파일을 보고 GUI API가
저급하다고 평가한 트위터 글이 있었는데, 그것을 의식했는지 이번에는 개발용 헤더
파일도 깔끔하게 지워놨다.)

리눅스 WINE보다 잘 돌아가는 윈도우 프로그램은 카카오톡을 비롯한 테스트한 몇 개
밖에 없는 것 같다. 파일 구조는 [XDG Base Directory
Specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html)을
따르는 프로그램 덕분에 ```~/.local``` 폴더도 들어 있었고, 일부 티맥스 앱은 XDG
표준의 ```~/.config``` 폴더에 설정을 저장하기도 하지만, 윈도우 이름을
무비판적으로 따라한 티가 나는 자체적인 ```~/AppData```, ```~/Favorite```,
```~/Local Settings```, ```~/.Recyclebin```과 같은 폴더 구조도 동시에 있었다.
파일 관리자의 C 드라이브는 진짜 C 드라이브도 아니고 윈도우 에뮬레이션에
사용하는 듯한 ```/tos``` 폴더를 가리켰다. NetworkManager에서 VPN, 본딩, 브릿지
같은 다양한 기능들은 고사하고 티맥스OS에서 새로 만든 네트워크 설정은 IPv6
설정도 할 수 없는 20년 전 네트워크 설정 UI를 다시 시작하고 있다. 지금 2019년에
윈도우 글꼴과 비슷한 느낌의 커스텀 폰트를 사용하고 윈도우처럼 만들기만 하면
사람들이 윈도우처럼 쓸 것이라고 생각했을까?

행정용 PC면 이 정도면 충분하다는 의견이 있지만, 그런 이유라면 애초에 새로 만들
이유가 없었다. 데비안 기반 배포판에서 패키지를 잘 취사선택하고 이슈를 해결하고
브랜딩을 잘 씌우면 되고, 그렇게 하더라도 제품으로 사용할 정도가 되려면 많은
노력이 필요하다. 그런데 정작 풍부하게 들어 있던 데비안 10 buster의 패키지들은
티맥스OS의 APT 아카이브에는 올려놓지도 않았다. (그래서 VirtualBox guest OS
드라이버 패키지를 데비안 아카이브에서 따로 받아서 설치했다.)

티맥스는 리눅스 데스크톱을 보고 느낀 문제가 무엇이었길래 이러한 작업을
시작했을까? 대체 WINE에서 안 되는 무슨 문제를 해결하겠다고 PE 바이너리 처리에
커널 모듈까지 동원해야 했는지? Wayland compositor를 직접 만들려고 했어도 쉽게
만들 수 있는 충분한 오픈소스 재료가 있었음에도 왜 바닥부터 그래픽 서버를
만들어야 했는지? 기존 GUI 툴킷의 백엔드를 작성한다든가 하는 방법이 아니라 왜
GUI 툴킷도 자체적으로 만들어야 했는지? 어떤 근거로 티맥스가 앞으로 이 방향으로
더 나은 데스크톱을 만들 수 있다고 생각하는 것일까? 설령 미래에 미국이나 유럽이
대한민국에 대한 소프트웨어 수출 규제를 하더라도 리눅스를 못 쓰게 될 일은 없을
것인데, 멀쩡히 잘 돌아가고 앞으로도 못 쓰게 될 가능성이 없는 오픈소스의
대체품을 왜 다시 다른 기반 오픈소스를 이용해서 일개 기업이 만드는 국산
소프트웨어로 개발해야 하는 것일까? 아무리 봐도 이런 곳에 자원을 투자해서
달성할 수 있는 가치가 무엇인지 알 수 없다.

티맥스OS 회사 입장에서 내가 생각할 수 있는 다른 종류의 가치라면 수익 뿐일텐데,
공공 시장이 이런 방식으로 수익이 날 수 있는 시장이라면 안타까울 따름이다.
