---
layout: post
title: 레가시: 트루타입 글꼴의 family 및 subfamily
date:   2018-06-12 00:00:00 +0900
tags: history truetype font legacy 역사 정보 레가시 트루타입 글꼴
categories: hacks
---

"이롭게 바탕체" 글꼴을 보면 트루타입의 "family" 정보로 "이롭게 바탕체
Medium"이라고 들어 있는 걸 보고, 작은 히스토리.

<https://iropke.com/archive/iropke-batang-launching.html>

트루타입 글꼴에는 글꼴의 정보로 (TTF Name) family와 subfamily 정보가
들어 있다.

<http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&id=iws-chapter08>

family는 흔히 말하는 글꼴의 이름을 말하고, subfamily는 그 스타일을 따위를
말한다. "돋움체"와 "bold"가 있으면 "돋움체"가 family이고 "bold"가
subfamily이다. 많은 애플리케이션에서는 이 두 가지의 분리된 정보를 이용해
"style linking"이라는 이름으로 어떤 글꼴을 사용할지와 어떤 스타일을 사용할지를
독립적으로 결정할 수 있다. 워드프로세서 프로그램을 생각해 보면 어떤 문서에 쓸
글꼴을 정하고, 일정 부분을 선택해서 굵은 글씨로 만드는 과정이 이렇다. 실제
내부적으로는 bold로 지정된 부분은 Bold 글꼴을 사용하게 되겠지만 이렇게
논리적으로 같은 글꼴로 묶어 둘 수 있는 것이다.

문제는 과거 MS 윈도우는 하나의 family에 대해 4개의 고정된 스타일 밖에
("regular", "bold", "italic", "italic bold") 처리하지 못했다. 만약 여기에
"extra bold"를 추가하면 글꼴 목록에서 선택할 방법이 없었다. 그래서 글꼴
디자이너들은 이 제한을 벗어나기 위한 꼼수를 쓰기 시작했는데, 많이 쓰는 4개
스타일만 하나의 family 안에 묶어 놓고 나머지 잘 안 쓰는 스타일은 family를 글꼴
이름만 쓰는 게 아니라 스타일을 붙여 쓰게 했다. 즉 "돋움체 ExtraBold"와 같이
말이다. family가 다르기 때문에 마치 다른 글꼴처럼 목록에 다른 글꼴로 나타나긴
하지만 어쨌거나 이 글꼴을 사용할 수는 있었다.

소프트웨어가 업그레이드되면서 4개의 subfamily만 처리할 수 있었던 윈도우의 이
제한이 없어졌으나 디자이너들이 OS의 버전에 따라 글꼴을 따로따로 제작하기를
기대할 순 없었다. 당장 글꼴이 구 버전 OS 사용자한테 동작 안 하는데 그걸
고려하지 않을 수가 없었기 때문이다. 그래서 "preferred family"와 "preferred
subfamily" 정보가 새로 생겼다. 비록 글꼴 디자이너들이 기존의
"family"/"subfamily"를 의도한 것과는 다르게 잘못 사용하고 있지만, 그 관례는
그대로 인정하고 새로운 시스템에서는 "preferred" 정보를 사용하게 되어 있다.
"preferred family"에서는 "돋움체"로 통일할 수 있고, "preferred subfamily"에는
"ExtraBold"를 넣는 방법을 쓰게 된다.

이 레가시는 족히 20년은 됐지만 여전히 많은 글꼴들이 유지하고 있다. 특정
소프트웨어 기능 때문에 생긴 레가시보다 많은 사람들이 특정 방식으로 사용하면서
생긴 레가시가 더 바꾸기 어렵다.
