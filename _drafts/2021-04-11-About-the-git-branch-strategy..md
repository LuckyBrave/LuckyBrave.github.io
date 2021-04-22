---
layout: post
title:  "Git 브랜치 전략에 대해서"
author: "Lucky Father & Brave Papa"
comments: true
tags: [git, git flow, github flow, gitlab flow, git workflow]
---
![SVN to Git](/assets/img/About-the-git-branch-strategy/gitworkflow.png){: width="700"}

# Git 브랜치 전략들
git flow, github flow, gitlab flow

## Git이란?
Git은 오픈소스로 공개된 버전 컨트롤 시스템이다.
소프트웨어를 반복적으로 개선해 나가고, 그 과정 중에 동료들과 리뷰를 통해 더 나은 코드로 배포될 수 있도록 도와준다.
Git 문법에 조금 익숙해 질 만하니, Git 배포에도 전략을 필요로 하니 복잡하고 배울게 많다.
우선, git flow 부터 천천히 살펴 보겠다.

## git flow 란?
git flow는 Vincent Driessen을 통해 알려진 git을 활용한 배포 전략이다.
릴리즈 브랜치, 기능 브랜치, 메인라인(상용 브랜치), 개발브랜치, 핫픽스 브랜치 등으로 구성되어,
데스크탑 어플리케이션처럼 사용자가 다운로드 받아 사용하는 소프르웨어에 적합한 전략으로 알려져 있다.

### git flow 주의사항
일반적인 웹사이트에서는 git flow 전략은 불필요한 과정들이 수반될 수 있다.
예를 들면, 핫픽스 브랜치와 기능 브랜치가 동일한 프로세스로 운영 시 큰 의미를 갖지 않게 될 수도 있다.
또한 버전 관리를 하지 않음에도 릴리즈 브랜치 생성 후 기능 브랜치와 병합 단계를 거쳐야 된다.

### git flow 키워드
릴리즈 브랜치

### git flow 사용해볼까요?

### git flow 선택 기준
현재 개발하는 소프트웨어가 데스크탑 애플리케이션, 라이브러리등 사용자가 다운로드하는 애플리케이션이라면 git flow에 적합할 수 있고,
또한 한명 이상의 동료와 같은 기능을 개발한다면 git flow 도입을 검토해도 좋다.

### git flow 리뷰 전략
Pull Request 시점은 특정 custom 브랜치(sandbox, cbt등) 병합 시점이 될 수도 있고,
개발 중인 기능 브랜치를 릴리즈 브랜치에 병합 시점이 Pull Request 시점으로 리뷰 할 타이밍이 된다.
만약 Pull Request가 승인(approve)가 된다면, 이력이 개발자 본인 이력으로 남기기 위해 병합은 개발자 본인이 진행한다.
- Pull Request가 Request Changes로 보완사항이 있으면, pull Request를 닫고, 수정 후 Reopen된 pull request로 이어서 진행하면 된다.

### git flow 롤백 전략
롤백 전략은 태깅 정보 기반으로 재빌드를 통해서 서비스 복구를 할수도 있고,
hot fix 브랜치 생성을 통해서 재배포로 코드 이력 및 서비스 복구를 할 수 있다.

master 브랜치의 태그는 git push --tags 명령어로 실행할 수 있다
git push --atomic origin <branch name> <tag>
git push --tags. (Not recommended!) : 개인들의 모든 태그가 올라가서 뒤죽박죽이 될 수 있지 않을까?

#2 시작해봅니다.
### git flow feature가 개발기간이 길어진다면...


## github flow란?
github 에서 사용하는 워크플로우이다.
하루에도 몇번씩 배포하는 운영 환경를 위한 심플한 워크플로우로 이해하면 된다.
위에 언급된 git flow에서 세가지 부분이 단순화 되었다.
1. release 브랜치가 없다.
2. hot fix 브랜치없이 기능 브랜치를 사용한다.
3. develop 브랜치 없이 master만 존재한다.

## github flow 키워드는?
master 브랜치와 master merge 권한이라 하겠다.

## github flow 좋은 점
pull request를 언제든 열 수 있다. (release 브랜치 생성 없이 말이다)
git fetch를 통해, 업데이트된 브랜치명만으로도 브랜치명이 곧 작업 타이틀이 되기 때문에 진행하는 작업 파악이 가능하다.

github flow 사용 예)

## gitlab flow 란?
GitLab Flow는 Git Flow보다 심플한 대안 전략입니다. 
기능 중심 개발과 이슈트래킹이 용이합니다. 
production 브랜치와 stable 브랜치를 사용하면서 모든 기능 브랜치를 main브랜치로 병합합니다. 
production 브랜치와 stable 브랜치는 아래에서 좀 더 자세히 살펴보겠습니다. 


### gitlab flow 키워드
프로덕션 환경 배포 흐름 제어.


### gitlab flow 왜 썼는가? 장단점
출시시가를 제어하거나, 배포환경에 따른 분기가 필요할 때 마지막으로 외부에 릴리즈 되는 소프트웨어라면
production, pre-preduction, stable 브랜치를 활용해서 적합한 플로우를 만들 수 있다. 

### gitlab flow 사용 예)

기준 : 배포편의성, 코드리뷰, 롤백, 특징


우리
ft-branch -> sandbox
ft-branch -> cbt

gitlab
ft-branch -> master -> cherry -> pre-production -> cherry -> production

## 처음엔 단순히 SVN에서 Git으로.
![SVN to Git](/assets/img/About-the-git-branch-strategy/svntogit.png){: width="500"}
5년 전 우리는 VCS를 SVN으로 사용하고 있었다. 그러다 Git 유행을 틈타 Git으로 넘어갔고  
한동안 Git을 SVN처럼 사용했다. 하지만 다른 팀처럼 Git 자체를 도입했다는 생각에 뿌듯했다.  
게다가 당시 팀 내 개발 환경은 로컬, 스테이징, QA, 릴리즈 서버와 상용 서버로 구성되어 있어서  
각 단계별로 별도의 브랜치로 운영할 수 있어서 상당히 마음에 들었다.  
하지만 쏟아지는 업무로 Git에 대한 이해는 부족한 채로 브랜치 운영의 편의성만을 보고 Git을 도입했다.

## 일단 Git flow 도입.
![SVN to Git](/assets/img/About-the-git-branch-strategy/gitflow.png){: width="400"}
SVN에 익숙한 팀원들은 Git의 개념들을 완전히 이해하진 못했지만 큰 불편함을 느끼지도 않았다.  
가끔 문제가 발생했을 때는 어떻게든 해결해 나갈 수 있었다. (이런 방치는 결국 문제를 일으켰다.)  
그러다 1년 후 팀원 중 한 명의 제안으로 Git flow를 도입했고 사용하기 시작했다.  
당시 개발 환경과 Git flow의 브랜치 전략이 어느 정도 맞는다고 생각했고 또 특별히 이견도 없었다.  
정확히는 Git flow를 기반으로 한 우리만의 Git flow였지만 기존 Git flow 사상을 최대한 따르기로 했다.

## Git flow 사용 그리고 문제점.
그로부터 4년 동안 팀에서 Git flow를 기본으로 한 Git 브랜치 전략을 사용했고  
사용하는 동안 사소한 불편한 점과 모호한 역할의 브랜치 등을 빼곤 사실 나쁘지 않았다.  
그러다 몇 년 전 팀 내부에서 코드 리뷰에 대한 요구 사항이 생겨났고 우리는 코드 리뷰를 적극적으로 도입하기로 했다.  
그렇게 도입된 코드 리뷰를 할 때 동료의 런타임 오류도 잡아주고 서로의 코드에 대해 코멘트하며   
성장하는 느낌과 성취감을 느낄 수 있었다.  
우린 열정적이었다. 하지만 일주일이 지나자 다들 지치기 시작했고 심지어 코드 리뷰를 꺼리기 시작했다.  
우리의 의지나 열정이 금세 식은 게 부끄러웠지만 아무도 그 얘기를 꺼내진 않았다.  
시간이 지나고 체력이 회복될 즘, 다시 코드 리뷰에 대한 열정을 불태웠지만 이번에는 더 빨리 식어버렸다.  
그렇게 몇 년 간 코드 리뷰에 대한 열정은 애간장을 태우는 여느 주식처럼 오르고 내리고를 반복할 뿐 목표에 도달하지 못했다.  
실력은 둘째 치더라도 2000년대 중반까지만 해도 우리는 철야하고 다음 날 아침에 팀장이 사준 도가니탕을 특근 수당으로 받고  
다시 회사로 들어가 라꾸라꾸도 없이 잠깐 눈을 붙인 후 일어나 다시 개발할 정도로 열정과 의지가 있었다.  
그런데 왜 우리의 코드 리뷰는 항상 실패할까?   
늙어서 그런 건가? 영향이 없다고 할 수는 없지만, 그렇다면 들어온 지 얼마 안 된 신입은 왜 힘들어하는 걸까?  
남의 코드를 보는 게 힘든 걸까? 물론 힘들지만 우린 늘 남의 코드를 봐왔다.  
내 일이 아니라는 인식 때문인가? 아직 이런 개발 문화가 익숙하지 않아서일까?  
그럴 수도 있다고 생각했다.  
우리는 온종일 걸리는 코드 리뷰를 하면서도 코드 리뷰 자체를 업무에 포함하지 않았다.  
그럼 업무에 포함하면 코드 리뷰가 될까?  
시간이 어느 정도 지난 후에야 우린 이런 부분을 의식하기 시작했다.

## Git flow의 문제?
우리는 서로의 열정과 의지만을 의심했다. 우리가 처한 상황과 환경, 방식에 대해선 별다른 의심은 하지 않았다.     
그러다 점검하는 차원에서 Git flow를 창시한 **Vincent Driessen**이 작성한,  
[A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/) 포스팅을 다시 보게 됐다.  
그리고 포스팅에 반성 노트라는 주석이 포함된 걸 발견했다.    
**Vincent Driessen**는 Git flow가 업계 표준이 되고 많은 인기를 얻었지만,   
지금은 상황이 달라졌고 소프트웨어 유형에 따라 다르지만 어찌 됐든 Git flow는  
웹 서비스에 적합하지 않다고 반성 노트에 남겼다.

_'어라? 우린 웹 서비스를 개발하며 Git flow를 쓰고 있는데'_

우리도 Git flow를 쓰면서 사상을 그대로 가져오다 보니  
억지로 끼워 맞추는 방식으로 적용하기도 했고 flow에 불필요한 과정도 있었다.  
그럼에도 불구하고 우리는 경험이 부족해서 우리가 모르는 뭔가 있겠지? 라는 생각에 대부분을 그대로 받아들였다.    
그럼 Git flow가 문제였을까? 나는 사실 그러길 바랐다. Git flow가 문제라면 flow를 다른 거로 바꾸기만 하면 해결될테니깐.  
하지만 계속되는 점검에 결국 우리의 문제들은 Git flow의 문제라고 보기 어려웠다.  
웹 서비스와 맞지 않는 Git flow를 선택한 약간의 부작용은 있었겠지만, 근본적으로 Git flow의 문제가 아닌 건 확실했다.

**첫번째 문제는 우리의 문제의식이었다.**  
단지 대중적으로 사용된다고 해서 고민과 조사 없이 우리가 운영하는 소프트웨어 유형과   
적합하지 않은 Git flow를 그대로 가져와 사용했고  
당시 운영하고 있는 환경에 맞춰 Git flow를 적용하면서 우리는 최적화하지 못 했다.  
그때 만약 이런 질문을 했었다면 어땠을까?

_'우리한테 develop 브랜치가 필요할까?'_    
_'우리한테 release 브랜치가 필요할까?'_

**두번째, 우리는 feature 브랜치의 life cycle을 너무 길게 가져갔다.**    
메이저 feature 브랜치 하나에는 다음에 배포될 모든 기능이 담겨져 있었다.   
그런 방대한 양을 과연 매번 코드 리뷰할 수 있을까?  
또, 테스트 케이스를 돌릴 수 있을까?  
물론 Git flow 사상을 따르다 보니 feature 브랜치의 life cycle이 커진 것도 있었지만   
사실 이건 어디까지나 우리가 조절할 수 있는 문제였다.

그 외에도 여러 문제가 있지만(CI/CD등) 가장 큰 문제는 역시 우리의 문제의식이었다.

## 결국 우리에게 맞는 Git 브랜치 전략을 설계해야 한다.
우린 뒤 늦게 Git flow와 관련된 기술 부채를 청산하려고 현재 노력 중이다.  
이미 검증된 전략들의 장점을 충분히 검토해서 취하고 우리에게 불필요한 과정은 생략하며 찾아가고 있다.  
**Vincent Driessen**의 말처럼 모든 걸 해결해 줄 수 있는 만병통치약은 없다.  
우리 스스로 판단하고 결정해야 한다.

우리가 겪는 여러 문제들로 우선 이 정도 결론은 내릴 수 있었다.

**첫째**, feature 브랜치는 동료들이 코드 리뷰를 할 수 있을 정도의 규모여야 한다.  
기준을 정하는 게 쉽지 않지만 우선 feature 브랜치의 life cycle을 최대 하루나 이틀 정도로 정하고 실험해보자.  
숙련된다면 의미 있는 단위로 짧게 가져갈 수 있도록 실험해보자

**둘째**, P.R(or M.R)을 강화하기 위해서는 사실 그 누구도 어드민 권한을 가질 이유가 없다.  
모든 코드는 예외 없이 리뷰되어야 하고 동료들의 동의가 필요하다.  
팀웍을 발휘해보자. 내 코드처럼 리뷰하고 코멘트하자.

**셋째**, 빌드와 테스트는 당연하고 코드 리뷰는 필수 과정이며  
대상의 리뷰 코멘트가 모두 처리되고 동료들이 승인하면 메인 브랜치로 병합이 진행된다.  
메인 브랜치 병합 전략은 히스토리 정리를 위해 필수적으로 **rebase merge** 한다.

우선 어느 정도 목표에 도달하기 위해 언급한 세 가지 규칙을 실행하는 것부터 시작하려고 한다.  
점점 규칙들은 늘어날 수 있겠지만 이렇게 규칙들을 나열하고 그걸로 우리에게 필요한 것과 필요 없는 것들을 구분해서  
우리에게 맞는 Git 브랜치 전략을 설계하는 시도가 중요하다.  
여러분들도 여러분 환경과 상황에 맞게 브랜치 전략이 설정되어 있는지 점검해보고  
약한 부분은 강화하고 불필요한 부분은 제거해서 효율적인 Git 브랜치 전략을 세울 수 있길 바란다.

**대다수의 잘하고 있는 개발팀보다 우리처럼 준비하지 않아 고생하는 소수의 순진한 개발팀을 위해 작성한다.**

---

### 참고문헌
- [https://nvie.com/posts/a-successful-git-branching-model/?fbclid=IwAR2wGrhnYfQpeBGi0lLXQcdJsSo3WT5jLSnN5_i99xIsC1VRg7pLvR2vW54](https://nvie.com/posts/a-successful-git-branching-model/?fbclid=IwAR2wGrhnYfQpeBGi0lLXQcdJsSo3WT5jLSnN5_i99xIsC1VRg7pLvR2vW54)
- [http://scottchacon.com/2011/08/31/github-flow.html](http://scottchacon.com/2011/08/31/github-flow.html)
- [https://docs.gitlab.com/ee/topics/gitlab_flow.html](https://docs.gitlab.com/ee/topics/gitlab_flow.html)
- [https://guides.github.com/introduction/flow/](https://guides.github.com/introduction/flow/)