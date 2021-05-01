---
layout: post
title:  "Git 브랜치 전략과 코드 리뷰에 대해서"
author: "Lucky Father & Brave Papa"
comments: true
tags: [git, git flow, github flow, gitlab flow, git workflow]
---
![SVN to Git](/assets/img/About-the-git-branch-strategy/git-workflow.png){: width="700"}

# 처음엔 단순히 SVN에서 Git으로.
5년 전 우리는 버전 관리를 SVN으로 사용하고 있었다. 그러다 Git 유행을 틈타 Git으로 넘어갔고  
한동안 Git을 SVN처럼 사용했다. 제대로 사용하진 않았지만 다른 팀처럼 Git 자체를 도입했다는 생각으로 뿌듯했다.  
당시 팀 내 개발 환경은 로컬, 스테이징, QA, 릴리즈 서버와 상용 서버로 구성되어 있어서  
단계별로 별도의 브랜치를 운영할 수 있어서 상당히 마음에 들었다.  
하지만 쏟아지는 업무로 Git에 대한 이해는 부족한 채 브랜치 운영의 편의성만 이용하며 Git을 계속 사용했다.

![SVN to Git](/assets/img/About-the-git-branch-strategy/server-step.png){: width="700"}

# 일단 Git flow 도입.
SVN에 익숙한 팀원들은 Git의 개념들을 완전히 이해하진 못했지만 큰 불편함을 느끼지도 않았다.  
가끔 문제가 발생했을 때는 어떻게든 해결해 나갈 수 있었다. (이런 방치는 결국 문제를 일으켰다.)  
얼마 후 팀원 중 한 명의 제안으로 Git flow를 도입했고 사용하기 시작했다.  
당시 개발 환경과 Git flow의 브랜치 전략이 어느 정도 맞다고 생각했고 또 특별히 다른 의견도 없었다.  
정확히 Git flow를 기반으로 한 우리만의 Git flow였지만 기존 Git flow 사상을 최대한 따르기로 했다.
![SVN to Git](/assets/img/About-the-git-branch-strategy/gitf-low.png){: width="400"}

# Git flow 사용 그리고 문제점.
그로부터 팀에선 Git flow를 기본으로 한 Git 브랜치 전략을 계속 사용했고  
사용하는 동안 사소한 불편과 모호한 역할의 브랜치 등을 빼곤 사실 나쁘지 않았다.  
그러다 팀 내부에서 코드 리뷰에 대한 요구 사항이 생겨났고 우리는 코드 리뷰를 적극적으로 도입하기로 했다.  
그렇게 도입된 코드 리뷰로 동료의 오류를 서로 잡아주고 코드에 대해 코멘트하며   
성장하는 느낌과 성취감을 느낄 수 있었다.
![SVN to Git](/assets/img/About-the-git-branch-strategy/pr.png){: width="500"}
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
시간이 어느 정도 지난 후에야 코드 리뷰로 인해 우리가 Git을 사용하는 방식을 의식하기 시작했다.

# Git flow의 문제?
![SVN to Git](/assets/img/About-the-git-branch-strategy/doubt.png){: width="600"}
코드 리뷰가 실패를 거듭하던 초기에는 서로의 열정과 의지만을 의심했다.  
우리가 처한 상황과 환경, 방식에 대해선 별다른 의심은 하지 않았다.     
그러다 점검하는 차원에서 Git flow를 창시한 **Vincent Driessen**이 작성한,  
[A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/) 포스팅을 다시 보게 됐고    
포스팅에는 2020년에 추가로 작성된 반성 노트라는 주석을 발견했다.    
**Vincent Driessen**은 Git flow가 업계 표준이 되고 많은 인기를 얻었지만,   
지금은 상황이 달라졌고 소프트웨어 유형에 따라 다르지만 어찌 됐든 Git flow는  
웹 서비스에 적합하지 않다고 남겼다.

_'어라? 우린 웹 서비스를 개발하며 Git flow를 쓰고 있는데'_

우리도 Git flow를 쓰면서 사상을 그대로 가져오다 보니  
억지로 끼워 맞추는 방식으로 적용하기도 했고 flow에 불필요한 과정도 있었다.  
그럼에도 불구하고 우리는 경험이 부족해서 우리가 모르는 뭔가 있겠지? 라는 생각에 대부분을 그대로 받아들였다.    
그럼 Git flow가 문제였을까? 나는 사실 그러길 바랐다.  
Git flow가 문제라면 Git 브랜치 전략을 다른 거로 바꾸기만 하면 해결될테니깐.  
하지만 계속되는 점검에 결국 우리의 문제들은 Git flow의 문제라고 보기 어려웠다.  
웹 서비스와 맞지 않는 Git flow를 선택한 약간의 부작용은 있었겠지만, 근본적으로 Git flow의 문제가 아니었다.

## 첫번째 문제는 우리의 문제의식이었다.
![SVN to Git](/assets/img/About-the-git-branch-strategy/consciousness.png){: width="400"}
대표적인 Git 브랜치 전략들은 Github flow, Gitlab flow, Git flow등이 있다.  
보통 이 중 하나를 선택해서 팀 환경에 맞게 설정한다.  
우리도 이 중 Git flow를 선택해서 우리의 환경에 맞게 설정했다.   
하지만 적합한지 부적합한지 여부도 판단하지 못할 만큼 경험이 부족했고 불필요한 과정들이 추가됐다.    
불필요한 과정들은 사람의 잦은 개입을 발생시켰고 그 개입은 실수를 유발했다.    
실수는 서비스에 문제를 일으켰고 우리는 정신을 바짝 차려야만 했다.  
우리는 이런 과정들을 여러 번 겪고 나서야 스스로 질문하기 시작했다.

_'우리한테 develop 브랜치가 필요할까?'_    
_'우리한테 release 브랜치가 필요할까?'_

우리가 이런 질문을 처음부터 했다면 어땠을까?    
만약 그랬다면 Git flow든 Github flow든 우리에게 맞게 최적화할 수 있었을까?

## 두번째, 우리는 feature 브랜치의 life cycle을 너무 길게 가져갔다.
![SVN to Git](/assets/img/About-the-git-branch-strategy/too-big-feature-branch.png){: width="500"}
메이저 feature 브랜치 하나에는 다음에 배포될 모든 기능이 담겨져 있었다.   
그런 방대한 양을 과연 매번 코드 리뷰할 수 있을까?  
또, 테스트 케이스를 돌릴 수 있을까?  
물론 Git flow 사상을 따르다 보니 feature 브랜치의 life cycle이 커진 것도 있었지만   
이건 어디까지나 우리가 조절할 수 있는 문제였다.

그 외에도 여러 문제가 있지만(CI/CD등) 가장 큰 문제는 역시 우리의 문제의식이었다.

# 결국 우리에게 맞는 Git 브랜치 전략을 설계해야 한다.
![SVN to Git](/assets/img/About-the-git-branch-strategy/git-strategy.png){: width="500"}
우린 뒤 늦게 Git flow와 관련된 기술 부채를 청산하려고 현재 노력 중이다.  
이미 검증된 전략들의 장점을 충분히 검토해서 취하고 우리에게 불필요한 과정은 생략하며 찾아가고 있다.  
**Vincent Driessen**의 말처럼 모든 걸 해결해 줄 수 있는 만병통치약은 없다.  
우리 스스로 판단하고 결정해야 한다.

우리가 겪는 여러 문제로 우선 이 정도 결론은 내릴 수 있었다.

**첫째, feature 브랜치는 동료들이 코드 리뷰를 할 수 있을 정도의 크기여야 한다.**    
기준을 정하는 게 쉽지 않지만 우선 feature 브랜치의 life cycle을 최대 하루나 이틀 정도로 정하고 실험해보자.  
숙련된다면 의미 있는 단위로 짧게 가져갈 수 있도록 실험해보자

**둘째, P.R(or M.R)을 강화하기 위해서는 사실 그 누구도 어드민 권한을 가질 이유가 없다.**      
모든 코드는 예외 없이 리뷰되어야 하고 동료들의 동의가 필요하다.  
팀웍을 발휘해보자. 내 코드처럼 리뷰하고 코멘트하자.

**셋째, 빌드와 테스트는 당연하고 코드 리뷰는 필수 과정이며**     
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
- [https://about.gitlab.com/topics/version-control/what-are-gitlab-flow-best-practices/](https://about.gitlab.com/topics/version-control/what-are-gitlab-flow-best-practices/)