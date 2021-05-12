https://nvie.com/posts/a-successful-git-branching-model/?fbclid=IwAR2wGrhnYfQpeBGi0lLXQcdJsSo3WT5jLSnN5_i99xIsC1VRg7pLvR2vW54

A successful Git branching model
성공적인 Git 브랜치 모델

Note of reflection (March 5, 2020)
회고록

This model was conceived in 2010, now more than 10 years ago, and not very long after Git itself came into being.
git-flow 모델은 10년 전인 2010년에 구상되었으며, Git이 생긴지 얼마되지 않은 시점이었다.  

In those 10 years, git-flow (the branching model laid out in this article) has become hugely popular in many a software team to the point where people have started treating it like a standard of sorts — but unfortunately also as a dogma or panacea.
지난 10년 동안 git-flow는 많은 소프트웨어 팀에서 사람들이 이를 일종의 표준처럼 취급하기 시작할 때까지 엄청난 인기를 얻었지만 안타깝게도 비판적인 수용없는 맹신에 이르렀다.  

During those 10 years, Git itself has taken the world by a storm, and the most popular type of software that is being developed with Git is shifting more towards web apps — at least in my filter bubble. 
Git이 세계적으로 전파되었고, Git으로 개발 중인 소프트웨어는 웹앱 유형이 많아지는 것으로 보였다.  

Web apps are typically continuously delivered, not rolled back, and you don't have to support multiple versions of the software running in the wild.
웹앱은 롤백없이 지속적인 배포지향하고 소프트웨어 버전관리를 지원할 필요가 없다. 

This is not the class of software that I had in mind when I wrote the blog post 10 years ago. 
10년전 git flow 관련된 블로그를 작성했을때 염두했던 소프트웨어 유형이 아니었다.  

If your team is doing continuous delivery of software, I would suggest to adopt a much simpler workflow (like GitHub flow) instead of trying to shoehorn git-flow into your team.
만약 지속적인 배포로 운영되는 소프트웨어를 관리중이라면, git-flow를 도입하는 거보다 훨씬 더 간단한 워크 플로( [GitHub flow](https://guides.github.com/introduction/flow/) )를 고려해보길 바란다.  
If, however, you are building software that is explicitly versioned, or if you need to support multiple versions of your software in the wild, then git-flow may still be as good of a fit to your team as it has been to people in the last 10 years. In that case, please read on.
그러나 버전별로 소프트웨어를 빌드하거나 다양한 환경에서 여러 버전의 소프트웨어를 지원해야하는 경우 git-flow 가 적합할 수 있다. 

To conclude, always remember that panaceas don't exist. Consider your own context. Don't be hating. Decide for yourself.
결론적으로 만병통치약이 존재하지 않는다는 것을 항상 염두해서, 자신의 상황을 고려하고, 스스로 상황에 맞게 결정해야 한다. 


In this post I present the development model that I’ve introduced for some of my projects (both at work and private) about a year ago, 
이 글은 약 1년전에 직장과 개인적으로 진행했던 프로젝트에 적용한 성공적이었던 개발모델에 대해 소개한다.
and which has turned out to be very successful.

I’ve been meaning to write about it for a while now, but I’ve never really found the time to do so thoroughly, until now. 
그 동안 경험한 것들에 대해 글을 쓰려고 했지만, 지금까지 쓸 기회가 없었다.

I won’t talk about any of the projects’ details, merely about the branching strategy and release management.
프로젝트의 상세한 내용을 이야기 할 생각은 없고, 단지 브랜치 전략과 릴리즈 관리에 대한 이야기를 하고자 한다. 

![이미지변경필요](https://nvie.com/img/git-model@2x.png)

Why git? 
## 왜 Git을 사용해야 하는가?
 

그러나 Git을 사용하면 이러한 작업은 매우 저렴하고 간단 하며 실제로 일상적인 워크 플로 의 핵심 부분 중 하나로 간주됩니다 . 
예를 들어 CVS / Subversion 책 에서 분기 및 병합은 이후 장 (고급 사용자 용)에서 먼저 논의되는 반면, 모든 Git 책 에서는 이미 3 장 (기본)에서 다룹니다.

단순성과 반복적 특성으로 인해 분기 및 병합은 더 이상 두려워 할 것이 아닙니다. 버전 제어 도구는 무엇보다 분기 / 병합을 지원해야합니다.

도구에 대해 충분히 알고 있으므로 개발 모델로 넘어가겠습니다. 
여기서 소개 할 모델은 기본적으로 모든 팀원이 관리 형 소프트웨어 개발 프로세스에 도달하기 위해 따라야하는 일련의 절차에 지나지 않습니다.

For a thorough discussion on the pros and cons of Git compared to centralized source code control systems, see the web.
중앙 집중식 소스 코드 관리 시스템과 비교한 Git의 장단점에 대한 자세한 내용은 웹을 참조하면 된다. 

There are plenty of flame wars going on there. As a developer, I prefer Git above all other tools around today.
Git really changed the way developers think of merging and branching. 
From the classic CVS/Subversion world I came from, 
merging/branching has always been considered a bit scary (“beware of merge conflicts, they bite you!”) and
something you only do every once in a while.
거기에서 많은 논쟁들이 진행되고 있다. 개발자로서 나는 다른 모든 VCS도구보다 Git을 선호한다. 
Git은 실제로 개발자가 병합 및 분기에 대해 사고 방식 바꿨다.  
기존에 CVS / Subversion 에서 병합 / 브랜치는 항상 작업을 두렵게 했다.( "병합 충돌을 조심하세요. 짜증유발!") 가끔씩 만하는 일로 생각했다. 


But with Git, these actions are extremely cheap and simple, and they are considered one of the core parts of your daily workflow,
really. For example, in CVS/Subversion books, branching and merging is first discussed in the later chapters (for advanced users),
while in every Git book, it’s already covered in chapter 3 (basics).
그러나 Git을 사용하면 이러한 작업은 짧은 시간과 간단한 방법으로 일상적인 워크플로 중 하나로 만들어 버렸다. 
예를 들어 CVS / Subversion 책 에서 브랜치 및 병합은 이후 장 (고급 사용자편)에서 먼저 논의되는 반면, 모든 Git 책 에서는 이미 3 장 내에서 (기본편)에서 다룬다.

As a consequence of its simplicity and repetitive nature, branching and merging are no longer something to be afraid of. 
Version control tools are supposed to assist in branching/merging more than anything else.
단순성과 반복적 특성으로 인해 브랜치 및 병합은 더 이상 두려워 할 것이 아니다. 버전 제어 도구는 무엇보다 브랜치 / 병합을 우선적으로 지원해야합니다.

Enough about the tools, let’s head onto the development model.
The model that I’m going to present here is essentially no more than a set of procedures that 
every team member has to follow in order to come to a managed software development process.
도구에 대해 충분히 알고 있으므로 개발 모델로 넘어가보자. 
여기서 소개 할 모델은 기본적으로 소프트웨어 개발하기 위해 모든 팀원이 따라야할 일련의 과정에 불과하다. 


## Decentralized but centralized
## 분산된 중앙집중형
The repository setup that we use and that works well with this branching model, is that with a central “truth” repo. 
Note that this repo is only considered to be the central one (since Git is a DVCS, there is no such thing as a central repo at a technical level). 
We will refer to this repo as origin, since this name is familiar to all Git users.
우리가 사용하고 있는 현재 브랜치 모델과 잘 동작하는 방법은 중앙 저장소라고 여겨지는 저장소를 설정하는 것입니다. 
중앙 저장소라고 여겨질 뿐 사실 분산형 VCS인 GIT에서는 중앙 저장소 같은 거 없습니다. 
<origin> 저장소는 Git 사용자에게 친숙하기 때문에 중앙 저장소를 <origin>으로 합니다. 

![](https://nvie.com/img/centr-decentr@2x.png)

Each developer pulls and pushes to origin. 
But besides the centralized push-pull relationships, each developer may also pull changes from other peers to form sub teams. 
For example, this might be useful to work together with two or more developers on a big new feature, 
before pushing the work in progress to origin prematurely. 
In the figure above, there are subteams of Alice and Bob, Alice and David, and Clair and David.
각 개발자는 <origin>브랜치에서 pull, push 할 수 있습니다. 
그러나 중앙집중식 push-pull관계 외에도, 각 개발자는 다른 동료의 변경사항을 가져와 하위단위를 구성 할 수 있습니다.
예를 들어, <origin> 브랜치에 작업한 것을 push하기 전에, 하나의 큰 기능을 여러 명이 작업을 하는 경우 유용할 수 있습니다.
위 그림에는 Alice와 Bob, Alice와 David, Clair와 David의 하위 단위로 정의했습니다.
Technically, this means nothing more than that Alice has defined a Git remote, named bob, 
pointing to Bob’s repository, and vice versa.
기술적으로 Alice가 Bob의 저장소명 <bob>을 가리키라는 Git 원격 브랜치를 정의하는 것 이상의 의미가 아니며, 그 반대의 경우도 마찬가지 입니다. 

## The main branches
## 메인 브랜치

At the core, the development model is greatly inspired by existing models out there. 
The central repo holds two main branches with an infinite lifetime:
개발 모델을 핵심사항은 기존모델에서 큰 영감을 받아 만들어 졌다.  
그리고 중앙 저장소는 항상 유지되는 두 개의 메인 브랜치를 갖게 된다.
master
develop

![](https://nvie.com/img/main-branches@2x.png)

The master branch at origin should be familiar to every Git user. 
Parallel to the master branch, another branch exists called develop.
<origin>원본 원격저장소의 <master>은 모든 Git 사용자에게 익숙해져야할 브랜치이고,
<master>브랜치와 같은 또다른 메인 브랜치로 <develop> 브랜치가 있다. 

We consider origin/master to be the main branch where the source code of HEAD always reflects a production-ready state.
origin/master 브랜치는 항상 상용 배포가 가능한 HEAD 소스코드로 메인브랜치입니다.  

We consider origin/develop to be the main branch where the source code of HEAD always reflects a state with the latest delivered development changes for the next release.
Some would call this the “integration branch”. This is where any automatic nightly builds are built from.
origin/develop 브랜치는 다음 릴리즈를 할 수 있도록 가장 최근 작업 이력의 HEAD 소스코드로 메인 브랜치 입니다. 
통합브랜치로 불리기도 합니다. 자동빌드가 생성되는 곳이기도 합니다. 

When the source code in the develop branch reaches a stable point and is ready to be released, 
all of the changes should be merged back into master somehow and then tagged with a release number. 
How this is done in detail will be discussed further on.
develop 브랜치 코드가 릴리즈할 준비가 되면, master브랜치에 병합한 후 릴리즈 번호로 태그를 생성합니다. 
어떤 방식으로 수행되는지는 아래서 설명합니다. 

Therefore, each time when changes are merged back into master, 
this is a new production release by definition. We tend to be very strict at this, 
so that theoretically, we could use a Git hook script to automatically 
build and roll-out our software to our production servers everytime there was a commit on master.
master브랜치에 변경작업들 병합될때마다, 새로운 상용 릴리즈가 정의됩니다.
master브랜치에 커밋될 때마다, Git 훅 스크립트를 통해 자동으로 소프트웨어를 빌드하고 상용서버에 배포 할 수 있습니다.

Supporting branches

Next to the main branches master and develop, our development model uses a variety of supporting branches to aid parallel development between team members, 
ease tracking of features, prepare for production releases and to assist in quickly fixing live production problems. Unlike the main branches, these branches always have a limited life time, since they will be removed eventually.

The different types of branches we may use are:

Feature branches
Release branches
Hotfix branches
Each of these branches have a specific purpose and are bound to strict rules as to which branches may be their originating branch and which branches must be their merge targets. We will walk through them in a minute.

By no means are these branches “special” from a technical perspective. The branch types are categorized by how we use them. They are of course plain old Git branches.

Feature branches



May branch off from:
develop
Must merge back into:
develop
Branch naming convention:
anything except master, develop, release-*, or hotfix-*
Feature branches (or sometimes called topic branches) are used to develop new features for the upcoming or a distant future release. When starting development of a feature, the target release in which this feature will be incorporated may well be unknown at that point. The essence of a feature branch is that it exists as long as the feature is in development, but will eventually be merged back into develop (to definitely add the new feature to the upcoming release) or discarded (in case of a disappointing experiment).

Feature branches typically exist in developer repos only, not in origin.

Creating a feature branch

When starting work on a new feature, branch off from the develop branch.

$ git checkout -b myfeature develop
Switched to a new branch "myfeature"
Incorporating a finished feature on develop

Finished features may be merged into the develop branch to definitely add them to the upcoming release:

$ git checkout develop
Switched to branch 'develop'
$ git merge --no-ff myfeature
Updating ea1b82a..05e9557
(Summary of changes)
$ git branch -d myfeature
Deleted branch myfeature (was 05e9557).
$ git push origin develop
The --no-ff flag causes the merge to always create a new commit object, even if the merge could be performed with a fast-forward. This avoids losing information about the historical existence of a feature branch and groups together all commits that together added the feature. Compare:



In the latter case, it is impossible to see from the Git history which of the commit objects together have implemented a feature—you would have to manually read all the log messages. Reverting a whole feature (i.e. a group of commits), is a true headache in the latter situation, whereas it is easily done if the --no-ff flag was used.

Yes, it will create a few more (empty) commit objects, but the gain is much bigger than the cost.

Release branches

May branch off from:
develop
Must merge back into:
develop and master
Branch naming convention:
release-*
Release branches support preparation of a new production release. They allow for last-minute dotting of i’s and crossing t’s. Furthermore, they allow for minor bug fixes and preparing meta-data for a release (version number, build dates, etc.). By doing all of this work on a release branch, the develop branch is cleared to receive features for the next big release.

The key moment to branch off a new release branch from develop is when develop (almost) reflects the desired state of the new release. At least all features that are targeted for the release-to-be-built must be merged in to develop at this point in time. All features targeted at future releases may not—they must wait until after the release branch is branched off.

It is exactly at the start of a release branch that the upcoming release gets assigned a version number—not any earlier. Up until that moment, the develop branch reflected changes for the “next release”, but it is unclear whether that “next release” will eventually become 0.3 or 1.0, until the release branch is started. That decision is made on the start of the release branch and is carried out by the project’s rules on version number bumping.

Creating a release branch

Release branches are created from the develop branch. For example, say version 1.1.5 is the current production release and we have a big release coming up. The state of develop is ready for the “next release” and we have decided that this will become version 1.2 (rather than 1.1.6 or 2.0). So we branch off and give the release branch a name reflecting the new version number:

$ git checkout -b release-1.2 develop
Switched to a new branch "release-1.2"
$ ./bump-version.sh 1.2
Files modified successfully, version bumped to 1.2.
$ git commit -a -m "Bumped version number to 1.2"
[release-1.2 74d9424] Bumped version number to 1.2
1 files changed, 1 insertions(+), 1 deletions(-)
After creating a new branch and switching to it, we bump the version number. Here, bump-version.sh is a fictional shell script that changes some files in the working copy to reflect the new version. (This can of course be a manual change—the point being that some files change.) Then, the bumped version number is committed.

This new branch may exist there for a while, until the release may be rolled out definitely. During that time, bug fixes may be applied in this branch (rather than on the develop branch). Adding large new features here is strictly prohibited. They must be merged into develop, and therefore, wait for the next big release.

Finishing a release branch

When the state of the release branch is ready to become a real release, some actions need to be carried out. First, the release branch is merged into master (since every commit on master is a new release by definition, remember). Next, that commit on master must be tagged for easy future reference to this historical version. Finally, the changes made on the release branch need to be merged back into develop, so that future releases also contain these bug fixes.

The first two steps in Git:

$ git checkout master
Switched to branch 'master'
$ git merge --no-ff release-1.2
Merge made by recursive.
(Summary of changes)
$ git tag -a 1.2
The release is now done, and tagged for future reference.

Edit: You might as well want to use the -s or -u <key> flags to sign your tag cryptographically.

To keep the changes made in the release branch, we need to merge those back into develop, though. In Git:

$ git checkout develop
Switched to branch 'develop'
$ git merge --no-ff release-1.2
Merge made by recursive.
(Summary of changes)
This step may well lead to a merge conflict (probably even, since we have changed the version number). If so, fix it and commit.

Now we are really done and the release branch may be removed, since we don’t need it anymore:

$ git branch -d release-1.2
Deleted branch release-1.2 (was ff452fe).
Hotfix branches


May branch off from:
master
Must merge back into:
develop and master
Branch naming convention:
hotfix-*
Hotfix branches are very much like release branches in that they are also meant to prepare for a new production release, albeit unplanned. They arise from the necessity to act immediately upon an undesired state of a live production version. When a critical bug in a production version must be resolved immediately, a hotfix branch may be branched off from the corresponding tag on the master branch that marks the production version.

The essence is that work of team members (on the develop branch) can continue, while another person is preparing a quick production fix.

Creating the hotfix branch

Hotfix branches are created from the master branch. For example, say version 1.2 is the current production release running live and causing troubles due to a severe bug. But changes on develop are yet unstable. We may then branch off a hotfix branch and start fixing the problem:

$ git checkout -b hotfix-1.2.1 master
Switched to a new branch "hotfix-1.2.1"
$ ./bump-version.sh 1.2.1
Files modified successfully, version bumped to 1.2.1.
$ git commit -a -m "Bumped version number to 1.2.1"
[hotfix-1.2.1 41e61bb] Bumped version number to 1.2.1
1 files changed, 1 insertions(+), 1 deletions(-)
Don’t forget to bump the version number after branching off!

Then, fix the bug and commit the fix in one or more separate commits.

$ git commit -m "Fixed severe production problem"
[hotfix-1.2.1 abbe5d6] Fixed severe production problem
5 files changed, 32 insertions(+), 17 deletions(-)
Finishing a hotfix branch

When finished, the bugfix needs to be merged back into master, but also needs to be merged back into develop, in order to safeguard that the bugfix is included in the next release as well. This is completely similar to how release branches are finished.

First, update master and tag the release.

$ git checkout master
Switched to branch 'master'
$ git merge --no-ff hotfix-1.2.1
Merge made by recursive.
(Summary of changes)
$ git tag -a 1.2.1
Edit: You might as well want to use the -s or -u <key> flags to sign your tag cryptographically.

Next, include the bugfix in develop, too:

$ git checkout develop
Switched to branch 'develop'
$ git merge --no-ff hotfix-1.2.1
Merge made by recursive.
(Summary of changes)
The one exception to the rule here is that, when a release branch currently exists, the hotfix changes need to be merged into that release branch, instead of develop. 
Back-merging the bugfix into the release branch will eventually result in the bugfix being merged into develop too, when the release branch is finished.
(If work in develop immediately requires this bugfix and cannot wait for the release branch to be finished, you may safely merge the bugfix into develop now already as well.)

Finally, remove the temporary branch:

$ git branch -d hotfix-1.2.1
Deleted branch hotfix-1.2.1 (was abbe5d6).
Summary

While there is nothing really shocking new to this branching model, the “big picture” figure that this post began with has turned out to be tremendously useful in our projects. It forms an elegant mental model that is easy to comprehend and allows team members to develop a shared understanding of the branching and releasing processes.

A high-quality PDF version of the figure is provided here. Go ahead and hang it on the wall for quick reference at any time.

Update: And for anyone who requested it: here’s the gitflow-model.src.key of the main diagram image (Apple Keynote).