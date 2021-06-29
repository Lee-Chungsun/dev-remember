## Git

###### 개발자로 일한지 5년차가 되어 가는데 지금까지 현업에서 Eclipse, Intellij 를 사용하면서 형상관리를 위해 SVN만 사용했었다. Git은 취업 전 IT학원에서 반 년정도만 사용했었고, 현재 우아한테크캠프 Pro 2기를 진행하면서 미션과제를 Git을 이용해 제출하기 때문에 Git 사용법과 명령어를 다시 익히고 사용했다. 오랜만에 사용하니까 생각보다 재밌기도 하고 편하기도 했다. 

> 이번을 기회로 개인 프로젝트도 진행해보면서 Git에 지속적인 Commit을 하는 습관을 가지면 좋을 것 같고, Git 기능을 간단히 정리하는 것이 이 글의 목적이다. 나는 Tool에서 사용하지 않고 직접 commad 로 실행을 했고 미션 제출과정을 기반으로 정리해 나가겠다. ~~(이미 널리 쓰고 있는 Git을 정리하는 게 늦은 감이 없지않아 있지만..)~~



#### Fork

###### Fork는 다른 사람의 ```Remote Repository```에 있는 소스를 내가 수정하거나 추가하고 싶을 때 내 ```Remote Repository```로 가져오는 것이다. 이 건 Github 홈페이지에서 직접 Fork 버튼을 눌러 내 ```Remote Repository```로 가져온다. ***Local 이 아니라 Remote Repository!!***



#### clone

###### clone 부터는 명령어를 이용했다. Clone은 내 ```Remote Repository```에서 내 ```Local Directory``` 로 끌어오는 것이다.  (난 Window의 명령 프롬포트를 이용했고 Git bash를 설치했다면 Git bash로 사용해도 무방하다.)

###### clone 뒤에 url은 Git에서 복사할 수 있다. GIthub 홈페이지에서 해당 Repository로 들어가게 되면 초록색 Code 버튼이 있을 건데 그 버튼을 누르면 해당 url이 나온다. (.git 확장자는 있어도 되고 없어도 되는 것 같다.)

```bash
c:\devleop> git clone https://github.com/Lee-Chungsun/git-test-project.git
```

![image-20210629163330127](C:\Users\cs.lee\AppData\Roaming\Typora\typora-user-images\image-20210629163330127.png)

###### Cloning이 완료 된 것을 볼 수있다. 옵션을 추가 할 수 있는데, 만약 branch가 여러개가 생성이 되어있다면 원하는 브랜치만 clone 할 수 있다. 

```bash
c:\devleop> git clone -b {브랜치 이름} --single-branch https://github.com/Lee-Chungsun/git-test-project.git
```



#### branch

##### branch -a

###### 형상관리를 하면 master와 branch가 존재한다. 보통 branch에서 작업을 하고 Trunk 로 실제 운영 서버 소스를 관리를 한다. 브런치를 확인해 보자 (여기 부턴 Clone 한 프로젝트 root에서 실행해야 한다.)

```bash
c:\devleop\git-test-project> git branch -a
```

![image-20210629164150617](C:\Users\cs.lee\AppData\Roaming\Typora\typora-user-images\image-20210629164150617.png)

###### branch의 목록이 나오고 branch가 여럿인데 clone시에 해당 branch만 받는 옵션을 주지 않았다면 모든 branch가 다 보일 것이다. 

##### checkout -b

###### 새로운 branch를 생성한다.

```bash
c:\devleop\git-test-project> git checkout -b test-branch
```

![image-20210629164828048](C:\Users\cs.lee\AppData\Roaming\Typora\typora-user-images\image-20210629164828048.png)

###### 해당 Branch가 생성이 되었고 branch -a 명령어로 List를 다시 확인해보면 생성이 되어 있다.

![image-20210629164944410](C:\Users\cs.lee\AppData\Roaming\Typora\typora-user-images\image-20210629164944410.png)

###### -b 옵션을 빼고 실행하면 해당 branch 또는 master 로 Switched 된다. 

```bash
c:\devleop\git-test-project> git checkout master
```

##### branch -D

###### master로 Switch 한 후 branch를 삭제한다.

```bash
c:\devleop\git-test-project> git branch -D test-branch
```

![image-20210629165407444](C:\Users\cs.lee\AppData\Roaming\Typora\typora-user-images\image-20210629165407444.png)

###### 해당 branch가 삭제가 되었고 branch -a 명령어로 List를 다시 확인해보면 삭제가 되어 있다.

![image-20210629165508250](C:\Users\cs.lee\AppData\Roaming\Typora\typora-user-images\image-20210629165508250.png)

---

###### 다음은 소스를 올리고 내려받는 기능에 대한 내용이다

#### push 절차

###### 먼저 push 를 하기 위해선 add를 하고 commit을 하고 push를 해야한다.

#### status

###### status는 내가 수정 또는 추가, 삭제 한 내역을 볼 수 있다. (수정/추가/삭제 절차는 모두 동일하니 추가만 다룬다.)

```bash
c:\devleop\git-test-project> git status
```

![image-20210629172003123](C:\Users\cs.lee\AppData\Roaming\Typora\typora-user-images\image-20210629172003123.png)

###### 추가한 파일이 보인다.

#### add

###### add 명령어는 commit 하기 전 상태인 Staged 상태로 만든다. 실제로 원격에 반영되기 전 상태이다. add 명령어 뒤에 '.' 을 입력해 모든 수정/추가/삭제 소스를 Staged 상태로 만들거나 파일명을 입력해 해당 파일만 Staged 상태로 만들 수 있다.

```bash
c:\devleop\git-test-project> git add .
or
c:\devleop\git-test-project> git add wootechcamp/push_test.md
```

![image-20210629172801543](C:\Users\cs.lee\AppData\Roaming\Typora\typora-user-images\image-20210629172801543.png)

###### status로 확인해보면 staged 상태인 것을 알 수 있다.

#### commit

###### commit 명령어를 통해 staged 상태인 파일들을 commit 상태로 만들고 -m 옵션으로 커밋 메세지를 남길 수 있다. 아직 Remote Repository 에 반영되기 전이다.

```bash
c:\devleop\git-test-project> git commit -m "test : 소스 push test"
```

![image-20210629173030763](C:\Users\cs.lee\AppData\Roaming\Typora\typora-user-images\image-20210629173030763.png)

#### push

###### 마지막으로 push 명령어로 Remote Repository에 반영시킨다.

```bash
c:\devleop\git-test-project> git push origin {브랜치 ID}
```

![image-20210629174853849](C:\Users\cs.lee\AppData\Roaming\Typora\typora-user-images\image-20210629174853849.png)

###### Repository에 잘 반영이 되었는지 확인해보면 커밋 메세지와 함께 잘 반영이 되어 있다.

#### pull

###### push와 반대로 pull 명령어는 서버의 변경 내역들을 내 Local에 반영 시킨다.

```bash
c:\devleop\git-test-project> git pull origin {브랜치 ID}
```



###### 오늘은 이까지,, 추가로 반영해야겠다. 계속

