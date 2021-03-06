# Git

git은 분산 버전관리시스템  
git Hub는 git을 공유하는 원격저장소를 의미한다.  
분산은 데이터의 복사함으로서 안정성을 확보하고  
분산된 데이터(브런치)로 작업하고 통합하는 프로세스를 통해 협업을 할 수 있게 돕는다.

```java

//var foo = function()
```

## 버전관리

1. trunk
   - 현재 개발중인 프로젝트
   - merge : 기존기능에 확장된것을 더해서 개발한다.
     - ex) 1.1 snapshot
2. tag
   - 개발완료된 프로젝트를 배포(release)하는 단계.
3. branch
   - 실제버전과 독립적으로 추가 기능을 만들때 branch한다고 한다.
   - 완성버전을 브런치한다.
   - 기본소스를 복사에서 brach를 더한다음에 서버의 소스와 합친다.
   - 이 기본 소스를 master라고 부른다.

## 0. 기초 개념

1. untracked

특정 저장소(repository)를 지정했을때 그 저장의 경로에 있는 모든 파일의 상태  
이력 관리 대상에서 제외댄 파일로 볼 수 있다.

2. tracked

git의 추적상태에 있는 파일  
즉 감시 대상인 파일이다.

3. unstaged

tracked 상태인 파일중에서 수정이 발생했지만 stage에 올라가지 않은 상태이다.  
수정이 발생했지만 아직 commit되지 않은 파일.

4. staged

tracked 파일이면서 stage에 올라간 파일.  
즉 commit된 파일.

## 1.시작하기

1. INIT

저장소 생성 명령어  
소스코드가 있는 경로로 이동하여 local repository를 생성한다.  
.git폴더가 생성되는것을 확인한다.

```
$ git init
```

- 명령어가 동작하지 않을 때 에러 확인
- 내가 작업한 파일 외에 다른 파일이 수정되진 않았는지 확인

2. STATUS

```
$ git status
```

버전관리 대상파일을 확인한다.

- 상태값
  - untrack : git와 관련이 없는 상태. 관리되지 않는다.
  - track : 저장소에 보관되어 관리가 되고 있는 상태.
  - unmodified : 수정안됨.
  - modified : 수정됨
  - staged : 스테이지 상태.

```
$ git status
```

status로 상태변화를 확인할 수 있다.  
commit은 staged상태에서만 가능하다.  
mofied상태에서 staged상태로 이동할때도 add명령어를 사용한다.

3. ADD

```
$ git add (파일명)
```

- 버전관리 파일을 스테이지에 추가한다.
- 파일명을 입력하여 추가할 파일을 선택할 수 있다.
- working directory의 변경된 작업 파일을 staging area로 추가시킵니다.

4. COMMIT

```
$ git commit -m''
```

- staging area의 내용을 local repository에 확정 짓습니다.
- staging단계를 패스하기 위해선 -a를 붙여라.
- 메세지와 함께 커밋한다.
- 저장소에 보관할때는 기록이 필요하다.
- m속성은 메세지를 입력하는데 현재 내가 저장한 내용을 저장소에 보관할때 어떤 내용인지 적어준다.
- m '메세지'를 치면 편집기가 뜨지 않는다.

5. 원격저장소 등록

```
$ git remote add origin {remote repsitory 주소}
```

원격 저장소를 'origin'라는 이름으로 등록한다.  
별칭이라 생각하면 쉽다.  
원격저장소의 주소는 깃허브에서 repository를 생성해야한다.

```
$ git remote - v
```

생성된 remote를 확인해보자.

6. PUSH

```
$ git push origin master
```

- local repository의 내용을 remote repository로 업로드 합니다.
  업로드  
  커밋한 소스를 origin 경로의 원격 레포지토리 master 브랜치에 올린다.
  업로드를 할때는 내가 다운받을때와 같은버전일때만 가능하다.  
  서버에 새로운 업데이트가 되어있다면 새로 받아서 올려야함.  
  원격저장소에 readMe 문서를 만들었으면 pull받고 repository를 시작해야한다.

7. RESET

```
$ git reset
```

스테이지에 올라간 정보를 초기화한다.

## 2. 브런치

1. 브런치 생성

```
$ git branch <브런치명>
```

2. 브랜치 이동

```
$ git checkout <브런치명>
```

3. 브런치 관리.

```
$ git branch
```

브런치 목록 보기.

4. 브런치 삭제

```
$ git branch -d <브런치명>
```

5. MERGE

```
$ git merge <브런치명>
```

## 3.서버의 branch 내려받기

1. CLONE

```
$ git clone <레포지토리 주소>
$ git remote - v
```

.git을 포함한 remote repository의 파일들을 local repository에 복사합니다.

2. PULL

```
$ git pull origin master
```

- pull : 원격저장소의 브런치를 가지고 와서 나의 소스와 합쳐준다.

---

## 롤백, 작업 관리

1. LOG

   ```planetext
   $git log
   ```

2. AMEND

   ```planetext
   $git commit -- amend
   ```

커밋내용 되돌리기.

---

## 용어정리

### 1.영역

- working directory
  - 현재 작업하고 있는 공간을 말합니다.
  - Git이 관리하고 있지만, 아직 추적( track )하고 있지 않은 상태입니다.
- index
  - stage 또는 staging area라고 하며, 준비 공간을 말합니다.
  - Git이 추적하고 있으며, 버전으로 등록되기 전 상태입니다.
- repository
  - 저장소를 의미합니다.
  - 본인 PC에 존재하는 저장소인 local repository
  - Github, Gitlab 같은 원격 저장소인 remote repository가 있습니다.
- Staging Area
  - 실제 저장하기 전에 임시로 보관하는 임시저장소
- .git directory - 내가 작업한 프로젝트가 저장되는 저장소.
  - 네트워크가 연결되어있지않아도 작업을 할 수 있다.

### 2.협업

1. branch

   - 독립된 working directory
   - 브랜치를 통해 프로젝트 참여자마다 브랜치를 가져서 독립된 작업 공간을 갖습니다.
   - 테스트 및 백업 등의 용도.

2. head

   - 지금 작업하고 있는 branch

3. merge

   - 2개의 branch에서 작업한 다른 내용을 하나로 합치는 것을 말하며, 현재 브랜치를 기준으로 병합됩니다.
   - 만약 두 branch가 같은 파일의 같은 곳을 수정했다면, 충돌( merge conflict )이 발생해서 이를 해결해야 합니다.
   - 해당 이슈 관계자들이 상의하여 수동으로 충돌을 해결해줘야 합니다.

4. fetch

   - 서버에서 가지고오는것. 가지고와서 저장만한다.

5. reset
   로컬에 있는 파일을 덮어쓰려는 경우에 사용한다.

```planetext
$git fetch --all
$git reset --hard origin/<branch_name>
```

# 다뤄볼 주제

- 깃 플로우
- gitIgnore
- 롤백.

```planetext
$ git config -- global user.name "CaterJo"
$ git config -- global user.email kin7729@gamil.com
```

## REF

- [GIT 참고서](https://backlog.com/git-tutorial/kr/stepup/stepup2_4.html)
