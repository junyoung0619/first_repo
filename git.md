# Git 
* 분산 버전 관리 시스템
* 코드의 '변경 이력'을 기록하고 '협업'을 원활하게 하는 도구
### 버전 관리: 변화를 기록하고 추적하는 것
* 구글 docs에도 버전 관리 기능이 있음
* 각 버전은 이전 버전으로부터의 변경사항을 기록하고 있음

### 중앙 집중식
* 버전은 중앙 서버에 저장되고 중앙 서버에서 파일을 가져와 다시 중앙에 업로드 - 중앙 컴퓨터 터지면 다 날아감

### 분산식
* 버전을 여러 개의 복제된 저장소에 저장 및 관리- 동기화만 주기적으로 잘 해주면 1개의 컴퓨터가 터져도 괜찮다.

## 분산 구조에서의 장점
* 중앙 서버에 의존하지 않고도 동시에 다양한 작업 수행 가능
    * 개발자들 간의 직업 충돌을 줄여주고 개발 생산성을 향상
* 중앙 서버의 장애나 손실에 대비하여 백업과 복구가 용이
* 인터넷에 연결되지 않은 환경에서도 작업을 계속할 수 있음
    * 변경 이력과 코드를 로컬 저장소에 기록하고, 나중에 중앙 서버와 동기화

## Git의 역할
* 코드의 버전(히스토리)를 관리
    * 개발되어 온 과정 파악
* 이전 버전과의 변경 사항 비교 

## Git의 영역
* Working Directory, Staging Area, Repository로 구분됨
### Working Directory
* 실제 작업(수정, 생성, 삭제) 중인 파일들이 위치하는 영역
* `git status` 붉은 색으로 파일 명 표시
* 해당 영역에 있는 파일은 commit에 기록되지 않음 (Staging Area로 이동시켜야 가능)
### Staging Area
* Working Directory에서 변경된 파일 중, 다음 버전에 포함시킬 파일들을 선택적으로 추가하거나 제외할 수 있는 중간 준비 영역
* 실질적으로 버전관리 파일을 선별하는 공간
* `git status`로 확인을 종종할 필요가 있다.
### Repository
* 버전 이력과 파일들이 영구적으로 저장되는 영역
* 모든 버전과 변경 이력이 기록됨.
### Commit
* 버전
* 변경된 파일들을 저장하는 행위이며, 마치 사진을 찍듯이 기록한다 하여 'snapshot'이라고도 함
* `git log`로 commit 이력 확인 가능
## Git의 동작
### git status
* 현재 git의 상태를 보여줌
* 빨간 파일들은 Working Directory 영역에 있는 것 
    * Untracked: 관리x -> 버전이력이 없음 (새로 생성된 파일)
    * Modified: 이미 관리되고 있는 파일 (수정된 파일을 의미)
    * Deleted: 삭제된 파일을 의미
* 초록 파일들은 Staging area 영역에 있는 것
    * New file: 생성된 파일
    * Modified: 수정된 파일
### git log
* commit의 history를 보는 코드
### git init
* (master)가 없는 것에만 git init을 하자
* Project단위로 주로 설정(너무 크면 기능 단위로 설정), 온라인 실습실 문제는 문제단위로 git이 설정되어 있음
* 로컬 저장소 설정(초기화)
    * 해당 폴더를 git으로 관리를 할 준비 (하위 폴더 포함)
    * git의 버전 관리를 시작할 디렉토리에서 진행
* 실행시 해당 폴더에 .git이라는 폴더가 생기고 terminal에 master라는 표시가 생김 
### git add
* git add 파일명
* 변경 사항이 있는 파일을 staging area에 추가 ( Working Directory => Staging area)
    * staging area - 버전을 관리할 파일만 남길 수 있도록 하는 분류소
* git add . : 현재 Working Directory에 있는 모든 파일을 staging area에 추가됨
    * 주의: 버전 관리가 필요없는 파일이나 폴더가 같이 올라갈 가능성이 있어 반드시 Staging area를 확인해야 함
### git commit
* commit 이력을 남기는 명령어
* commit을 할 때 자신이 누구인지를 밝혀야 함
    * 이메일: github에서 쓰는 이메일
* 반드시 commit 메세지를 남겨야 함
* git commit -m '메시지 내용': commit을 찍을 때 메시지를 남긴다. - S.A에 있는 파일들이 Repo로 모두 이동함 - commit 내용과 연관된 메시지로 작성 (한글도 괜찮, -m 여러개 써서 여러 줄 쓰기도 가능)
* git commit만 누르면 vim editor가 나온다
> (참고) vim 에디터 간단 사용법
> vim은 두 가지 모드가 있음
> 1. Command 모듸 저장, 나가기
> 2. Editor 모드 : 텍스트 수정
> * Editor 모드로 전환하는 방법은 키보드 i를 누르면 됨
> * Command 모드로 전환하는 방법은 esc 키
> * 저장하고 나가기: `:wq`
> * 저장하지 않고 강제로 나가기: `:q!`
* git은 commit을 찍을 때 이력 내용(title)을 남겨야 함
* staging area에 있는 파일들을 저장소(Repository)에 기록
    * 해당 시점의 버전을 생성하고 변경 이력을 남기는 것
---
### Commit 수정
* 협업에 있어서 반드시 회의를 거쳐 모든 사람들의 commit 기록을 맞추고 commit을 해야함( 주의 필요)
* 바로 직전 생성한 commit 수정하기
    1. commit 메시지 수정
    2. commit 전체 수정
#### 1. 메시지 수정: git commit --amend (history 꼬일 수도) 하고 난 후 vim에서 수정 가능
#### 2. 전체 수정(놓친 파일을 마지막 commit 파일에 추가로 올릴 때): 추가할 것 S.A에 올리고 git commit --amend한 후 수정하면 같이 Repo로 올라감
### LF와 CRLF
* LF:lineFeed
* CRLF: carriage return LF  두 개 모두 줄바꿈 문자이다. 이를 뭘로 할 것인지에 대한 warning이 나올 수 있으나 무시해도 됨 
### ★git은 로컬 저장소 내 모든 파일의 '변경사항'을 감시하고 있다.

### 로컬
* 현재 사용자가 직접 접속하고 있는 기기 또는 시스템

 ### git log --oneline 
 * commit들이 한 줄씩만 차지함 (내가 원하는 commit을 찾기에 용이함)
 ### git config --global -l (-list도 동일)
 * git global 설정 정보 보기    

