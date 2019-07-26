## git 사용법

git -> SCM, git을 통해 오픈소스 관리
(분산) 버전관리 시스템 : 개발된 과정과 역사 볼 수 있고, 프로젝트 이전 버전 복원+변경사항 비교가능
git을 통해 각각의 컴퓨터에 있는 내용들을 저장가능 -> 저장소(github:원격으로 관리하는 것)로 옮김
git bash에서 git명령어를 통해 작동시킴

snap shot을 찍는다는 것은 log로 기록해서 
다른 커밋이 있더라도 스냅샷으로 돌아갈 수 잇는 여지를 남겨둠.  -> 버전 관리를 한다. (커밋이 가장 중요!!!!!)
add = commit할 목록에 추가(ex. 로그인, 회원가입 -> 한번에 두가지 기능 함 but 각각 스냅샷으로 커믿하고싶음 -> 어떤 코드만 커밋할지
add로 설정 가능.)
로그인 에드 -> 로그인 커믿 -> 회원가입 에드 -> 회원가입 커믿 -->주석달면 커믿 기록만으로도 팀원들 이해할 수 있고, 그것들을 내려받아서 추가적인 일을 할 수 있음. 
push : 지금까지는 local 에서 커믿함 -> 우리들의 원격저장소 github로 업로드하지 않음. 그 작업이 push이다. -> 이걸 해야 다시 다운받아서 작업을 할 수 있다. 
우리는 day1에 대한 커믿, day2에 대한 커믿 -> 커믿을 쌓아가면서 진행과정 알려주고 코드 내용 확인 가능.
add하는 것 -> 파이썬 파일이라고 생각해라. 그리고 커믿으로 저장하고 깃허브에 저장

$ git add helloworld.py (argument 1개)
$ git commit -m(메세지를 남기겠다는 필수 옵션) -> 뒤에 코텐션 두고 메세지남기기 
$ git config --global user.name "John" (-- : long name 옵션)(arguments 2개)



**git 초기화(2~3 중 택1)**  자리 옮기면 무조건 해야함!!!!!!!!

1. git bash 실행 후, 미리 설정되어있을지 모를 계정 정보 삭제(처음 설치 시 생략 가능)

$ git config --global --unset credential.helper

$git config --system --unset credential.helper

2. windows 자격 증명 관리자에서 git관련 정보 삭제
3. git bash 실행 후

student 안에 있는 폴더 TIL에서 git init을 한 것은 TIL 안의 내용을 github에 push하는 것

git init 전에 해야할 것은 master가 없는 것을 확인해야함!!!

github에 TIL원격저장소 만듦 -> 프로젝트라는 github 새로 만들 수 있음

새롭게 시작하려면 git init을 하게되면 .git이라는 폴더가 있다 이는 git으로 간주되고있다는 것이므로 .git을 삭제시키면 됨

cd. : 지금 현재 폴더

cd.. : 그 위 폴더

git log -> commit한 로그들을 알 수 있음

git status -> 현재상황 알 수 있음

git commit -m "StartCamp Day 01"

어디로 push해야해? -> github의 주소를 복사해야함

git remote -v : 원격 관리

origin -> origin이라는 이름으로 remote의 이름을 만들어줌

원본과 복사본이 있을 수 있다. 원본에 어떤 내용을 추가하려면 이 사람것을 복사해서 복사본을 내 레파지토리로 적어놓고 추가하면 이것은 복사본에 내용이 올라간 것. 이때 원본에도 올릴 수 있음.

origin이라는 걳은 원격저장소의 이름이라 



<시나리오>

집에서 내용 추가했다면,, github에 어제 추가로 작업한 것들을 pull해서 해야함 -> 그래야 내용이 저장됨.**************************************



원격저장소에  til 저장함. 집에서 추가 어케함? -> git init하면 안됨!!! 그래서 그대로 가지고올 줄 알아야함. mkdir Jamsil -> cd Jamsil/ -> (멀캠에서 한거 집에서 받기) 일단 어디서 받아야하는지 알아야하므로 주소가 있어야함 -> git에 드가서 clean of download 누르고 주소 복사 -> git clone "주소" -> ls->cd TIL -> git log -> 추가하고 -> add -> commit -> push 반복



~ TIL 에서 git add . -> 내가 작업한 내용들을 전부 다~~~~ add하겠다.



로그인이라는 branch를 만들어 commit들을 쌓겠다. -> 특정 브랜치를 설정해 작업하다가 원래는 우리가 master brance에서 했기 때문에 작업 끝나면 master에 중간에 병합시키기/



처음 github에 만들면 할 것

$ git -l(list로 볼 수 있음)

$ git init

$ git status

$ git add .

$ git status

$ git commit -m "Initial commit"

$ git log

$ git status

$ git remote add origin 주소(new에서 복사)

$ git remote -v

$ git push origin master

$ cd ~/TIL : TIL로 간다

$ code . : visual studio code를 연다

$ mkdir :  make directory



