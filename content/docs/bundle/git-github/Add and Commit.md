# Add and Commit

프로젝트 상태를 관리하는 방법에 대해 알아봅니다.

## Add
작성한 소스코드를 Git을 통해 추적하기 위해서는 add 명령어를 사용합니다.

소스코드의 변화를 Git에게 알려주기 위해서는 아래의 명령어를 사용해야 합니다.

```
git add <path>
```

이때 프로젝트 전체를 Add 하기 위해서는 아래와 같이 사용할 수 도 있습니다.

```
git add .
```

이러한 Add 명령어는 변화가 감지된, 즉 파일의 수정이 일어날 경우 사용할 수 있습니다. 이러한 상태를 확인하고 싶을 때는 아래의 명령어를 사용합니다.

```
git status
```


## 변경사항 커밋하기
커밋은 로컬 저장소에 코드 변경 이력을 남기고 싶을 때 사용합니다.

앞서 살펴본 Add 명령어로 변경사항을 Git이 변경사항을 추적한 상태에서 해당 변경 사항을 커밋하고 싶을 경우 아래의 명령어를 사용합니다.

```
git commit
```

보통의 경우 해당 커밋 내용을 표시하기 위해 메시지와 함께 사용하며, 이럴 경우 아래의 명령어를 사용할 수 있습니다.

```
git commit -m "커밋 메시지"
```

적절한 커밋 메시지를 사용하여 팀원에게 효과적으로 작업 내용을 표현할 수 있습니다. 이러한 커밋 메시지는 보편적인 규칙이 있는데, 이는 [[]] 에서 확인할 수 있습니다.
