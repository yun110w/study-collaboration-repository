# CLI 버전관리
1. CLI 버전관리란 무엇인가?<br>
   -CLI를 사용해서(명령어를 통해서) 깃허브 데스크탑이나 웹페이지에서 했던 작업을 콘솔에서 제어하는 것<br>
   -코드, 파일 혹은 문서의 변경 사항 중 의미있는 지점을 기록하는 것<br><br>
2. git log를 치면 나오는 HEAD는 어떤 의미가 있나요?<br>
   현재 위치한 버전을 의미함<br><br>
3. 아래 그림(fig. 1)에서 최신 버전에서 두번째 버전으로 돌아가려면 어떤 명령어를 써야하나요(커밋 메세지가 "message 1"인 버전)<br>
```bash
...
git reset --hard ae8b # "message2"인 버전 이후에 쌓인 버전은 모두 지우고 "message2"인 버전으로 돌아감
...
```
![git log 시 결과](./sources/commit_log1.png)*fig 1. git log 시 결과* <br><br>

1. main branch의 최신 버전으로 돌아가려면 어떤 명령어를 써야하나요?<br>
   git checkout master<br><br>
2. HEAD, HEAD -> main(혹은 master)는 어떤 차이가 있나요?<br>
   HEAD : 현재 위치한 버전을 의미함<br>
   HEAD -> main(혹은 master) : 현재의 버전이 가장 최신의 버전이다 라는 의미임<br><br><br>

# add 옵션, Editor
1. `git commit -am "message"` 에서 -am은 -a, -m 옵션이 합쳐진 것입니다. 각각은 어떤 의미를 가지는 옵션인지 말해보세요.<br>
   -a : add<br>
   -m : commit<br><br>
2. `git commit -am "message"`에서 -a 옵션은 실수를 방지하기 위한 조건이 있습니다. 조건이 무엇인가요?<br>
   최초 한 번은 add가 되어서 tracked 상태가 되어야지만 사용할 수 있다. untracked 상태에서는 사용이 불가능하다.<br><br>
3. `git config --global core.editor "vim"`의 뜻을 설명해보세요.<br>
   git config : git의 설정(을 바꾼다는 뜻임)<br>
   global : 이 컴퓨터 전체의 설정을 바꾼다는 뜻임<br>
   editor : 에디터를 바꾼다는 뜻임<br>
   'vim'에 실행하고 싶은 에디터의 이름이나 경로를 적으면 에디터가 바뀜<br><br><br>

# git reset, revert
1. 위 그림(fig. 1)에서 `git reset --hard 009fae8d669b3bc7eadb5558d2f6f16b50fa7e6e`을 하면 결과가 어떻게 되나요?<br>
   commit message가 "messsage1"인 버전으로 reset되고, 이 버전 이후에 쌓인 버전들은 모두 지워지게 됨<br><br>
2. `git revert 009fae8d669b3bc7eadb5558d2f6f16b50fa7e6e`을 하면 결과가 어떻게 되나요?<br>
   한 번에 commit message가 "message1"인 버전으로 revert하면 commit message가 "message1"인 버전 이후에 생긴 변화를 git이 처리할 수 없게 되어 충돌이 발생함<br><br>
3. `git reset ...`과 `git revert ...`는 의미가 비슷한데, 용도에 차이를 두고 사용한다면 어떤 차이가 있나요?<br>
   git reset : 버전을 삭제하고 싶을 때/나의 local에서만 사용 가능(push 불가능)<br>
   git revert : history를 남기고 싶을 때/나의 local, remote repository에서 모두 사용 가능<br><br><br>

# tag, branch
1. tag는 왜 쓰이고 무엇을 대신하는 건가요?<br>
   각각의 버전을 식별하는 식별자인 commit ID는 기억하기 쉽지 않으므로 대신에 적당한 이름을 사용하는데 그게 tag임<br>
   tag를 이용하면 버전의 commit ID 뿐만 아니라 거기에 사용자가 이해하기 쉬운 이름을 붙여서 그 이름으로 쉽게 중요한 버전을 찾아갈 수 있게 된다는 장점이 있기 때문에 쓰임<br><br>
2. branch는 생성한다는 것은 어떤 의미인가요?<br>
   하나의 파일로부터 조금씩 다른 내용을 수정할 수 있게 저장소가 여러 상태로 공존하게 된다는 것을 의미함<br><br><br>

# branch
1. branch는 왜 필요한가요?<br>
   branch를 이용하면 여러 번 저장소의 이름을 변경하는 수고를 하지 않고 하나의 저장소에서 다양한 작업을 진행할 수 있음<br>
   하나의 파일로부터 조금씩 다른 내용을 수정할 수 있게 저장소가 여러 상태로 공존하게 되므로 길고 복잡한 문서를 작성할 때 편리함<br><br>
2. 아래 fig 2.와 fig 3.의 그림과 커밋을 순서대로 각각 대응 시켰을 때, 두 번째 그림에서 새로운 그림을 그리기 위해 분기(branch)를 생성하려면 어떻게 해야하는 지 코드를 작성해주세요 (HEAD는 맨 위 그림 즉, 최신 버전을 가르치고 있음.)<br>
   git revert 942e<br>
   git branch pic<br>
   git checkout pic<br>
![alt text](./sources/log_visualization.png) *fig 2.*<br>
![alt text](./sources/commit_log2.png) *fig 3.*<br><br><br>

1. 각자의 main branch의 최신 버전에서 `dev-{이름} (예: dev-junwoo)`이라는 브랜치를 만들고 (branch가 고장난 것 같으면 `dev-junwoo_1`처럼 만들어도 됩니다.)<br>
2. 이 과제를 작성하고 본인의 remote repository로 push 한 뒤<br>
3. 강준우 repository에 `dev`라는 branch에 PR을 날려보세요. (push가 안될 경우 `git push --set-upstream dev-{이름}`로 push 해보세요.)<br>
4. 다했으면 하는 과정 각각을 스크린샷해서 여기에 올려주세요. 드래그앤 드랍으로 하면 됩니다.<br>

### Advanced
1. HEAD 옆 origin/main, origin/dev, origin/HEAD는 무슨 뜻일지 추측해보세요.<br>
   origin/main : 원격 저장소의 master 브랜치의 작업 위치<br>
   origin/dev : 현재 작업 디렉토리가 origin이라는 원격 저장소에 있는 dev라는 이름의 브랜치를 가리키고 있다는 것을 의미<br>
   origin/HEAD : 원격 저장소의 현재 작업 위치<br><br>
2. `git checkout -b {branch_name}`에서 -b 옵션은 '{branch_name}라는 이름으로 새로운 브랜치를 만든다.' 이 명령어 결과와 같은 결과를 만드는 명령어를 찾아보세요.<br>
   git branch -m {branch_name}<br><br>
3. `git config ...`에서 바꿀 수 있는 다른 명령어들은 무엇이 있나요? 맘에 드는 설정을 바꾼 뒤 알려주세요.<br>
   git config : git의 설정(을 바꾼다는 뜻임)<br>
   global : 이 컴퓨터 전체의 설정을 바꾼다는 뜻임<br>
   editor : 에디터를 바꾼다는 뜻임<br>
   'vim'에 실행하고 싶은 에디터의 이름이나 경로를 적으면 에디터가 바뀜<br>
   git config --global core.editor "nano"<br><br>
4. `git reset --hard ...`처럼 `git reset`에는 `--hard` `--mixed` `--soft`등 옵션이 있는데 이 옵션이 어떤 차이가 있는지 알려주세요.<br>
   --hard :  버전 삭제 + 현재 수정하고 있던 것 삭제 / 가장 강력하게 지우기<br>
   --mixed : 버전 삭제 + 현재 수정하고 있던 것 유지/커밋 이후 로컬에 남은 작업 부분은 남아있지만 unstaged 상태<br>
   --soft : 버전 삭제 + 현재 수정하고 있던 것 유지/커밋 이후 로컬에 남은 작업 부분은 staged 상태<br><br>
5. 자주 사용되는 branch의 이름들이 몇 가지가 있습니다. 어떤 것들이 있고 무슨 이유로 그 branch를 사용하는지 2가지만 알려주세요.<br>
   -develop branch : 다음 출시 버전을 개발하는 브랜치/기능 개발을 위한 브랜치들을 병합하기 위해 사용<br>
   -hotfix branch : 출시 버전에서 발생한 버그를 수정하는 브랜치/배포한 버전에 긴급하게 수정을 해야 할 필요가 있을 경우, master 브랜치에서 분기하는 브랜치

