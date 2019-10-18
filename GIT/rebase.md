https://medium.freecodecamp.org/an-introduction-to-git-merge-and-rebase-what-they-are-and-how-to-use-them-131b863785f

`git push` 했을 때, git pull 받으라는 메시지가 같이 뜬다면, git pull을 할 경우 merge commit이 생겨버린다.
merge commit을 만들지 않고 rebase를 하면 target branch 끝에 커밋들을 붙일 수가 있다.
이 때, 커밋 메시지를 합칠 것과 남길 것을 선택할 수 있다.
```
git rebase -i origin/master
```
