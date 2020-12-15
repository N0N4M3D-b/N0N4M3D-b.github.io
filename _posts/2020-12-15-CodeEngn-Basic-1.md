---
title: "[CodeEngn] Basic RCE L01"
author: N0N4M3D_b
date: 2020-12-12 20:50:00 +0900
categories: [WarGame, CodeEngn]
tags: [Reversing]
---

![intro Image](/assets/img/postimg/2020-12-15-CodeEngn-Basic-1/prob_intro.PNG "Intro Image")

<br>

# Environment
- OS : Windows 10 Pro
- Tool : Ollydbg v1.10

<br>

# Write-Up
Codeengn Basic 첫번째 문제입니다.
<br>

![intro Image](/assets/img/postimg/2020-12-15-CodeEngn-Basic-1/exec.PNG "Intro Image")

프로그램을 실행해보면 위와같은 메시지박스가 나타나고 확인을 누르면 CD-ROM Driver가 아니라는 메시지박스가 출력되고 확인을 누르면 프로그램이 종료됩니다.

![fail](/assets/img/postimg/2020-12-15-CodeEngn-Basic-1/fail.PNG "Fail Image")

Ollydbg로 이 문제를 분석해보겠습니다.

![EP Image](/assets/img/postimg/2020-12-15-CodeEngn-Basic-1/entry.PNG "EP Image")

위 사진은 Entry Point 입니다.

어셈코드를 보면 프로그램이 시작되면
처음에 봤었던 메시지박스를 출력합니다

그리고 GetDriveTypeA 함수를 실행시키고
ESI와 EAX 레지스터를 연산합니다

두 값을 CMP로 비교해서 다르면 **①**을 
같다면 **②**를 실행시키고 프로그램을 종료합니다.

우리가 원하는 결과는 HD가 CD-ROM으로 인식되었다는 메시지박스인
**②** 부분입니다.

CMP 명령어 다음의 JE 명령어를 JMP로 패치해주면 두 값이 같든 다르든 **②**로 점프하게 됩니다.

![patch Image](/assets/img/postimg/2020-12-15-CodeEngn-Basic-1/patch.PNG "patch Image")

![success Image](/assets/img/postimg/2020-12-15-CodeEngn-Basic-1/success.PNG "success Image")