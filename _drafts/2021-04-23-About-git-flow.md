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


# Git 브랜치 전략에 대해서 (안내 포스팅) / 의견 포스팅 제목으로 고려해보면 좋겠다.
- 브랜치 전략
- 코드 리뷰
- CI/CD

# 처음엔 단순히 SVN에서 Git으로.
# 일단 대충 Git 도입.
# Git flow 사용했더니 큰 문제가 없었어.. 코드 레파지토리 관리
# Git flow의 문제인가 점검하다보니, git flow 사상대로 사용하고 있지 않았고, 반성노트도 있었어.
# 찾아보니, 이런  의견들, 정보들이 있더라. (git flow에 대한 단점 의견, github flow, gitlab flow)
    ## git flow 반성노트 내용
    ## git flow 대체 전략들 소개
        ### github flow란?
        ### gitlab flow 란?
# 솔루션은 git flow을 그대로 쓰는게 아니고, 우리에 맞게 사용해 볼 수 있어
# 결국 우리에게 맞는 Git 브랜치 전략을 설계해야 한다. 우리는 그렇게 할꺼야.
# 너희도 한번 해보렴. 우리는 본받아.
### 참고문헌


# Git 브랜치 전략들 (새 포스팅)
    ## Git이란?
    ## git flow 란?
        ### git flow 주의사항
        ### git flow 키워드
        ### git flow 사용해볼까요?
        ### git flow 선택 기준
        ### git flow 리뷰 전략
        ### git flow 롤백 전략
        ### git flow feature가 개발기간이 길어진다면...
    ## github flow란?
        ### github flow 키워드는?
        ### github flow 좋은 점
    ## gitlab flow 란?
        ### gitlab flow 키워드
        ### gitlab flow 왜 썼는가? 장단점
        ### gitlab flow 사용 예)

## git flow 대체 전략들 소개
반성노트를 보고나서, 찾아본 대체 전략은 두가지 정도 있었다.
잠깐 살펴보고 간다면,
### github flow란?
첫번째 대체 전략은 github 에서 사용하는 워크플로우, github flow이다.
하루에도 몇번씩 배포하는 운영 환경를 위한 심플한 워크플로우로 이해하면 된다.
위에 언급된 git flow에서 세가지 부분이 단순화 되었다.
1. release 브랜치가 없다.
2. hot fix 브랜치없이 기능 브랜치를 사용한다.
3. develop 브랜치 없이 master만 존재한다.

### gitlab flow 란?
두번째 대체전략은 GitLab Flow다. Git Flow보다 심플한 대안 전략입니다.
기능 중심 개발과 이슈트래킹이 용이하다는 점이 특징이고,
출시시가를 제어하거나, 배포환경에 따른 분기가 필요할 때 마지막으로 외부에 릴리즈 되는 소프트웨어라면
production, pre-preduction, stable 브랜치를 활용해서 적합한 플로우를 만들 수 있는 배포 전략입니다.