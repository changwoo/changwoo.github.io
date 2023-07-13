---
layout: post
title:  "해설: 레드햇이 RHEL의 오픈소스를 중지하는가? (답: 그렇지 않다)"
date:   2023-07-07 00:00:00 +0900
tags: redhat rhel rockylinux almalinux
categories: hacks
---

 * 2023년 6월 21일 레드햇 블로그, "[Furthering the evolution of CentOS Stream (CentOS Stream의 계속된 진화)](https://www.redhat.com/en/blog/furthering-evolution-centos-stream)"
 * 2023년 6월 26일 레드햇 블로그, "[Red Hat’s commitment to open source: A response to the git.centos.org changes (레드햇의 오픈소스에 대한 약속: git.centos.org 변화에 대한 답)](https://www.redhat.com/en/blog/red-hats-commitment-open-source-response-gitcentosorg-changes)"

요악하면, 레드햇이 분위기를 흔들었지만 RHEL 기반 배포판 사용자 입장에서는
당장은 사정이 달라질 것이 없다. RockyLinux 등 RHEL 기반 배포판 버전 8 또는
버전 9 사용자는 아마도 이 버전의 지원이 끝날 때까지 계속 사용할 수 있을
것이다. 하지만 이러한 방향이 계속된다면 버전 10 이후는 어떻게 될지 알 수 없다.

## 복기: CentOS 종료

[2020년 12월 글(해설: CentOS 종료)](https://changwoo.xyz/hacks/2020/12/09/end-of-centos.html)에서
설명했다시피 레드햇은 RHEL 배포판의 다운스트림 배포판으로서의 CentOS를
종료했다. CentOS 버전 8의 EOL까지 단축하는 등 갑작스러운 이 시도는 커뮤니티의
강한 반발을 낳았고, 결국 CentOS와 같은 또 다른 RHEL 기반 배포판 프로젝트가
다수 탄생하게 되었다. 그 중에서도 많이 쓰이는
[RockyLinux](https://rockylinux.org/) 및 [AlmaLinux](https://almalinux.org/)와
같이 비영리 재단과 펀딩 구조까지 갖춘 배포판이 나와 오늘날에 이르렀다.


## 레드햇의 발표

레드햇에서 RHEL 개발을 총괄하는 코어 플랫폼 부사장 마이크 맥그레이쓰는
[2023년 6월 21일 블로그](https://www.redhat.com/en/blog/furthering-evolution-centos-stream)에서, 
앞으로 RHEL의 git 저장소를 RHEL 고객 계정으로 로그인해야만 접속할 수 있게 변경한다고 발표했다.
이 발표 내용을 보고 많은 사람들은 레드햇이 "오픈소스를 그만둔다"고 호들갑을
떨면서 반응하기도 했지만, 이는 사실이라고 볼 수 없다.

오픈소스인데 고객에게만 소스 코드를 공개하는 것이 허용되나? 사실 그렇다.
"오픈소스"라는 용어는 언제나 사람들에게 혼동을 일으키는데, 소스를 널리
"오픈/공개"하는 것 여부는 그 소프트웨어가 오픈소스냐 여부와는 직접 상관이 없기
떄문이다.

[오픈소스 정의(Open Source Definition)](https://opensource.org/osd/) "2. Source Code" 
내용을 보면, 오픈소스 소프트웨어는 소스 코드를 직접 배포하거나 바이너리 형태로 배포하는 경우

> "Where some form of a product is not distributed with source code, there
> must be a well-publicized means of obtaining the source code for no more
> than a reasonable reproduction cost, preferably downloading via the Internet
> without charge."
>
> "어떤 제품이 소스 코드 형태로 배포되지 않을 경우, 합리적인 복제 비용 이하로
> 소스 코드를 얻을 수 있는 잘 알려진 방법이 있어야 합니다. 인터넷을 통해 비용
> 없이 다운로드하는 방법이 좋습니다."

즉 RHEL의 배포 대상에 대해 소스를 전달해야 할 뿐, 불특정 다수에 대한 소스
공개를 해야 한다는 뜻은 아니다. 단,

> "must allow distribution in source code"
>
> "소스 코드 형태의 배포를 허용해야 합니다"

그 소스 코드에 대한 배포를 제한할 수는 없다. 전달받은 소스 코드를 제3자에게
배포하는 것도 막을 수는 없다는 뜻이다.

## 레드햇의 조치가 별 문제가 없는 이유

앞에서 말한 것처럼 레드햇이 배포하는 RHEL의 소프트웨어는 여전히
오픈소스이므로, 그 정책을 포기하지 않는 한, RHEL의 소스 코드를 감출 수는 없다.

또 2021년부터 RHEL 구독 프로그램 중에 무료 티어가 생겼기 때문에, 무료 구독
권한으로도 얼마든지 소스 저장소에 접속할 수 있다. 소스 코드에 대한 배포를
제한할 수 없으므로, RHEL 고객 자격으로 소스 코드를 다운로드해서 전달하면
끝나는 일이다.

레드햇이 RHEL 빌드에 사용하는 git 저장소를 막았을 뿐이지 RHEL 소스(SRPM)의
배포를 막기는 쉽지 않은 일이며, 실제로
[RockyLinux에서는](https://rockylinux.org/news/keeping-open-source-open/)
문제의 여지를 없애기 위해 레드햇의 서버에 접속하지 않고 소스 코드를 구할 수
있는 몇 가지 방법을 설명하기도 했다.


## 하지만 레드햇의 조치가 짜증이 나는 이유 (대체 왜 이러는 걸까?)

아무런 효과가 없는 일임에도 왜 그러는 것일까? 이유를 명확히 드러내지 있지만
레드햇의 포스트를 보면 RHEL 파생 배포판에 대한 불만에서 시작된 일임을
알 수 있다.
[레드햇의 두 번째 포스트](https://www.redhat.com/en/blog/red-hats-commitment-open-source-response-gitcentosorg-changes)를
보면 RockyLinux와 같은 RHEL 파생 배포판에 대한 ("rebuilders") 불만을 볼 수 있다.

> "I feel that much of the anger ... comes from either those who do not want
> to pay for the time, effort and resources going into RHEL or those who want
> to repackage it for their own profit. This demand for RHEL code is
> disingenuous. "
>
> "... 분노의 대부분은 RHEL에 들어가는 시간, 노력 및 자원에 대해 비용을
> 지불하고 싶지 않은 사람들 또는 자기 이익을 위해 RHEL을 재패키징하려는
> 사람들에서 온 것이라고 생각합니다. RHEL 코드에 대한 이러한 요구는 솔직하지
> 않습니다."
>
> "More recently, we have determined that there isn’t value in having a
> downstream rebuilder ... The generally accepted position that these free
> rebuilds are just funnels churning out RHEL experts and turning into sales
> just isn’t reality."
>
> "최근 우리는 다운스트림 리빌더를 보유하는 일이 가치가 없다고 판단했습니다 ...
> 이러한 무료 리빌드 배포판이 RHEL 전문가를 배출하고 (레드햇의) 매출로
> 이어진다는 일반론은 현실과 달랐습니다."

레드햇 입장에서 도움이 안 된다는 건 사실일 수 있다. (CentOS를 인수하고
운영하면서 그걸 깨닫는데 7년이 걸렸단 말인가?) CentOS 배포판에 익숙해진
엔지니어는 고객이 RHEL을 사용한다면 RHEL 지원을 할 수도 있지만 일부러 RHEL을
구입하라고 권하지는 않을 것이다. 그러한 엔지니어는 대부분 RHEL보다 CentOS
사용을 통해 이득을 보았을 것이다. CentOS를 비롯한 파생 배포판이 RHEL의 노력을
이용한 무임승차(free loader)였다고 말한다면 어느 정도 사실이라고 볼 수 있다.

하지만 파생 배포판이 없었다고 해서 그 고객이 RHEL의 고객이 되었을 것 같지는
않다.

시스템마다 수백불에서 (클러스터링 등 옵션을 추가하면) 수천불에 달하는 RHEL
구독 비용을 지불하는 일이 합리적인지는 각각의 사정마다 다를 수 있다. 그러나
2020년 내 글과 같이 CentOS의 사용자는 "엔터프라이즈"답게 높은 RHEL의 구독
비용을 낼 의사가 없기 때문에 사용자가 되었거나, 내지 않는다는 가정 하에 적절한
가격에 배포판에 번들된 추가 솔루션을 판매하고 있는 곳이거나, RHEL 구독에서
제공되는 고객 지원도 필요가 없는 고급 사용자로 자체 지원이 가능한 곳이었을
것이다.

무료 RHEL 배포판이 없어지면 이들은 과연 RHEL 구독을 할 것인가? 어느 정도는
당장은 익숙함을 찾아 구독할 수도 있다. 하지만 그들 대부분은 멋들어진
엔터프라이즈 리눅스를 선택한 사람이 아니기 때문에 결국 대안을 찾아 빠져나갈
것이다. 사실 리눅스 배포판은 대안이 너무 많다.

> "In a healthy open source ecosystem, competition and innovation go
> hand-in-hand. Red Hat, SUSE, Canonical, AWS and Microsoft all create Linux
> distributions with associated branding and ecosystem development efforts."
>
> "건전한 오픈 소스 생태계에서 경쟁과 혁신은 함께 가는 것입니다. 레드햇, SUSE,
> 캐노니컬, AWS 및 마이크로소프트는 모두 관련된 브랜딩 및 생태계 개발 노력을 통해
> Linux 배포판을 만듭니다."

배포판 개발자인 내가 보기에도 이는 절반의 진실이다. RockyLinux나 AlmaLinux와
같은 파생 배포판도 나름의 브랜딩을 하고 자체 커뮤니티를 구축한다. 위에서
언급된 배포판들은 이슈가 생길 때마다 서로의 패치를 카피하고 "리빌드"를 한다.
물론 패치가 단순히 카피한다고 되는 것도 아니고 본인의 작업을 추가하며 가치를
쌓아 나가는 점에서는 마찬가지이다. 레드햇은 대체 어디부터 단순 "리빌더"라고
말하는 것일까?

또 데비안의 일종의 "리빌더"라고 할 수 있는 파생 배포판 우분투를 만드는
캐노니컬이 여기 포함된 이유는 무엇일까? 거대한 비영리 업스트림 배포판의 존재를
언급하고 싶지 않았던 것일까? 계속해서 보면,

> "This is a real threat to open source, and one that has the potential to
> revert open source back into a hobbyist- and hackers-only activity. ... We
> don’t want that and I know our community members, customers and partners
> don’t want that."
>
> "이것은 오픈 소스에 대한 진정한 위협이며, 오픈 소스를 다시 취미나 해커
> 전용 활동으로 되돌릴 가능성이 있는 것입니다. ... 우린 이를 원하지 않으며
> 커뮤니티 구성원, 고객 및 파트너도 원하지 않는 것을 알고 있습니다."

누가 봐도 RockyLinux나 AlmaLinux이 운영하는 비영리 재단을 통한 오픈소스
프로젝트가 문제가 있는 것처럼 은근히 비판을 하고 있다.

이렇게 말하는 게 정당할까? 꽤 알려진 파생 배포판 중에서 정말 단순 리빌드만
하는 파생 배포판 같은 것은 없다. 당연히 RockyLinux/AlmaLinux도 버그를 수정하고
업스트림에 기여한다. 물론 레드햇은 오픈소스 기여가 매우 많은 회사이므로
자신있게 말할 자격이 있지만, 다운스트림을 상대로 이렇게 말할 수는 없다고
생각한다. 이러한 논리로 말하자면 레드햇 역시 다운스트림으로서 수많은 업스트림
오픈소스 때문에 기업으로서 많은 이익을 보고 있지만, 그렇다고 레드햇이 그 수백
수천의 업스트림의 몫을 정당하게 챙겨 줬다고 할 수 있을까? 이것이 오픈소스
생태계가 동작하는 방식이고 시장이 동작하는 방식이라고 정당화할 수 있겠지만,
그렇게 말할 수 있으려면 파생 배포판들도 그러한 생태계의 일원일 뿐이라고 말할
수 있어야 한다.

대체 왜 이러는 것일까? 회사가 돈을 못 벌어서 문제가 되는 상황을 걱정할 수도
있겠지만, 레드햇은 IBM이 인수하기 전에도 수조원 수준의 매출과 꾸준한 이익을
가져가고 있는 안정적인 회사로, 망할 가능성이나 수익성 때문에 레드햇의
아이덴티티인 배포판 사업을 포기할 가능성은 없다고 봐도 된다. 아니면 모회사
IBM에서 압박이 왔던 것일까?

## 앞으로는 & 생각

실제 RHEL 파생 배포판의 사용에는 별 문제가 없을 것으로 보인다. 하지만 이런
방향으로 가게 된다면 앞으로 부정적인 변화가 또 있을 수 있고, 2025년에 릴리스할
RHEL 10에는 어떻게 될지 알 수 없다.

한편 이 사건을 가지고 RHEL 리셀러들이 엉뚱하게 RHEL 다운스트림 배포판이 마치
불법인 것처럼 공포 마케팅을 시작할 수도 있으니 속지 말기를 바란다.

레드햇이 진짜 클로즈드 소스로 가게 되는 최악의 경우를 상상하더라도, GPL 또는
MPL과 같이 소스 코드의 배포를 강제하는 라이선스가 있는 소프트웨어가 RHEL 안에
필수적으로 들어가야 하고, 그 소스 코드의 배포를 제한할 수 없기 때문에 부분적인
클로즈드 소스가 될 것이다. 특히 레드햇은 RHEL 내용 중에서 레드햇이 직접 만드는
소프트웨어의 배포를 제한할 수 있다. 하지만 이렇게 부분적으로 비공개 소스로
가려면 OS의 구성도 많이 달라져야 할 것이다. 또 배포판 사업에서 부분적인 비공개
정책은 부정적인 결과가 많았기 때문에 레드햇이 그러한 선택을 하기는 쉽지가
않다.

비슷하게 여러가지 비공개 소스 번들 소프트웨어를 포함해 배포판을 구성했던
[칼데라 리눅스](https://en.wikipedia.org/wiki/Caldera_OpenLinux)같은 경우는
무엇보다도 그 특유의 폐쇄성과 라이선스 정책 때문에 고객에게 외면당했었다. 이를
만든 회사는 나중에 SCO라는 이름으로 바뀌면서 악명 높은 [SCO - 리눅스 법적
공방](https://en.wikipedia.org/wiki/SCO%E2%80%93Linux_disputes)을 시작했고
파산으로 이어졌다. 당시 SCO의 소송에 대항해서 승리한 당사자이기도 한 레드햇과
IBM이 이렇게까지 흑화하지는 않을 것으로 보인다.

진짜로 RHEL 파생 배포판을 만들 수 없는 일이 벌어진다고 하면, 이용자 대부분은
결국 RHEL 구독보다는 다른 대안을 찾아갈 것이다. 언제나처럼 데비안과 그 파생
배포판들을 선택할 수 있고 어떤 선택을 할 지는 이용자들의 몫이다.

나는 오픈소스를 판매하고 요금을 부과하는 것에 반대하지 않는다. 하지만 어떻게
해도 매출에 도움이 될 의사가 없는 다운스트림을 상대로 적대시하고 그들의 활동을
방해한다고 한다고 해서 회사가 이득을 볼 수 있는 부분은, 적어도 리눅스 배포판에
대해서는 거의 없다고 생각한다. 이렇게 해서 달라지는 건 지금까지 레드햇
본인들이 30년간 쌓아 온 생태계가 파괴되는 것 뿐이다.

## 여담

이번 뉴스 이후 합성 이미지 (레드햇 HQ 로비에 있는 마하트마 간디의 문구인데,
원래 이미지는 5년 전 IBM의 인수 직후 
[원문의 "THEN YOU WIN"을 "THEN THEY BUY YOU"라고 덧붙인 이미지](https://www.reddit.com/r/linuxmasterrace/comments/9skt93/who_did_this_red_hat_office/)다):

![Then Switch To Debian](/assets/img/2020-07/2020-07-07-redhat_office_then_switch_debian.jpg)

