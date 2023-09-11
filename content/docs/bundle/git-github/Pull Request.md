# Pull Request(PR)

브랜치 병합에는 PR 방식도 존재합니다. PR 방식에 대해 알아봅니다.

## PR이란?
기존 merge 명령어를 통해 작업한 코드를 합칠 수 있습니다. 하지만, 다른 사람과의 코드 리뷰나 Push 권한이 없는 오픈 소스 프로젝트에서 병합을 수행할 경우 PR 방식을 사용할 수 있습니다.

만약, 브랜치를 생성하고 모든 작업을 완료(commit)한 이후 원격 저장소(github)에 push까지 완료한 상황이라 해보겠습니다.

보통의 경우 merge 명령어를 통해 다른 브랜치와 합칠 수 있겠지만 해당 방식을 사용하게 된다면 즉각적인 병합이 이루어지게 됨으로써 모든 팀원이 합쳐지는 코드를 공유할 수 없게 됩니다.

이러한 문제점을 해결하고자 PR 방식을 사용합니다.

위 상황을 좀 더 구체적으로 나타내보겠습니다.

1. 현재 원격 저장소에는 master, new-branch 가 존재
   두 브랜치의 작업은 서로 다르며 new-branch는 master에서 분기되었다고 가정
2. 사용자는 new-branch를 로컬로 Fetch한 이후, 해당 브랜치에서 작업을 수행함
3. 사용자는 PR 방식으로 new-branch의 결과물을 master 브랜치로 병합하고 싶어함

먼저, 해당 상황에서 사용자는 자신이 로컬에서 작업한 new-branch의 내용을 원격 저장소(github)의 new-branch에 push 해야 합니다.

그러기 위해서는 아래의 명령어를 사용합니다.

```
git add .            // add 수행(반드시 all 하라는 건 아님, add를 수행해야 한다는 의미)
git commit -m "commit message"       // 커밋
git push origin new-branch.      // 원격 저장소의 new-branch로 push
```

add-commit-push 가 끝나고 github을 확인해보면 아래와 같이 PR이 가능하다는 메시지가 출력된 것을 확인할 수 있습니다.

