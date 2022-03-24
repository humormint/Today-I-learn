- Git setup

`Q` → 다시 돌아가기

`code . ->` vs code 실행

`git config --global core.autocrlf input` → 맥과 윈도우 줄바꿈 기호 호환되게

`mkdir git` → git 이라는 폴더 만들기

`ls -al` → 현재 폴더 상태 보여줌

`open .git` → .git 폴더 열기

`명령어 —h` → 명령어 설명 ex) git config —h

- Sourcetree

**새로 만들기 >> 로컬저장소 생성 > /Users/chae/projects/git_second  (레퍼지토리 만들기)**

![스크린샷 2021-12-29 오후 1.21.08.png](./img/스크린샷_2021-12-29_오후_1.21.08.png)

- Git Basic

Working directory → staging area → (`commit`) → .git directory

.git directory → (checkout) → working directory

로컬 → (`push`) → 서버(github)

서버 → (`Pull`) → 로컬

`tracked`  : git이 이미 알고 있는 파일 >> modified와 unmodified로 나눔

`untracked` : 새로 만들어진 파일 or 초기화 이후 생성한 파일

- git add

git 폴더 우클릭 → 터미널 실행 

`echo hello world! > a.txt` 

hello world!를 a라는 텍스트 파일에 저장

`open .` → 폴더 생성했는지 확인

`ls` → git 폴더 안에 a. txt 생성 됐는지  터미널에 보여줌

`git status` → 현재 상태 보여줌

![스크린샷 2021-12-29 오후 1.18.04.png](./img/스크린샷_2021-12-29_오후_1.18.04.png)

a.txt, b.txt, c.txt 파일이 untracked된 채로 남아 있음, commit은 아직 진행되지 않음

→ `git add`를 통해 staging area로 옮길 수 있음

![스크린샷 2021-12-29 오후 1.22.29.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7054a6d6-4c51-419e-a864-ca3ea6dda4b6/스크린샷_2021-12-29_오후_1.22.29.png)

a텍스트 파일은 커밋할 준비하 완료됨, b와 c는 아직 untracked

![스크린샷 2021-12-29 오후 1.25.20.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/03f861f3-2970-4a7d-94b9-96f5147b691e/스크린샷_2021-12-29_오후_1.25.20.png)

`git add *.txt` → 모든 txt파일 staging area로 보내기

![스크린샷 2021-12-29 오후 1.27.12.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ee610925-0e02-4376-889a-84d8f1d65be6/스크린샷_2021-12-29_오후_1.27.12.png)

echo ellie → a.txt (새로운 문자열 ellie를 a텍스트에 추가)

a 텍스트가 수정된 것을 확인할 수 있음

![스크린샷 2021-12-29 오후 1.31.08.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3ca5e687-cdf3-40b4-a5fa-8d8d4ee1c073/스크린샷_2021-12-29_오후_1.31.08.png)

sourcetree 에서 유동적인 스테이지 →  변경 사항 시각적으로 확인할 수 있음

![스크린샷 2021-12-29 오후 1.34.44.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/46f086a8-59cc-469e-88e3-db21c451d0fb/스크린샷_2021-12-29_오후_1.34.44.png)

`git add a.txt` → 수정된 a텍스트를 staging area로 보내기

![스크린샷 2021-12-29 오후 1.36.25.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/09f55648-1152-4f35-b6a0-5152b2e7cef3/스크린샷_2021-12-29_오후_1.36.25.png)

`git rm --cached *` → 전부 staging area에서 제거

`git add .` →모든 파일 staging area로 보내기

- git ignore

![스크린샷 2021-12-29 오후 1.42.35.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1e0aef80-0042-4b54-93d1-a98ee09ba9de/스크린샷_2021-12-29_오후_1.42.35.png)

style.css와 log.log 파일 추가

![스크린샷 2021-12-29 오후 1.43.04.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ec9a3032-1c96-4c90-a0f0-9104ce7754bb/스크린샷_2021-12-29_오후_1.43.04.png)

`git add *.css` → css파일만 staging area로 옮기기

![스크린샷 2021-12-29 오후 1.48.47.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e3c3715e-d8f0-4147-b408-f0713b00c546/스크린샷_2021-12-29_오후_1.48.47.png)

git에 포함하고 싶지 않을 때 → `git ignore`

`echo *.log >.gitignore`

![스크린샷 2021-12-29 오후 1.59.17.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/41db8a9d-eeda-45ac-af67-b3ed533e6849/스크린샷_2021-12-29_오후_1.59.17.png)

log 파일이 사라짐

`git diff --stage`

- 파일 비교 diff

git diff

![스크린샷 2021-12-29 오후 2.05.53.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/26924c82-d9b7-4a8c-ab31-438e921bb00c/스크린샷_2021-12-29_오후_2.05.53.png)

`git diff --staged`

- 첫번째 커밋 git commit

git commit

![스크린샷 2021-12-29 오후 2.29.12.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5a74fecf-10ec-4ad2-be47-8368c8d1ed6d/스크린샷_2021-12-29_오후_2.29.12.png)

타이틀과 description 작성

![스크린샷 2021-12-29 오후 2.30.51.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7c347da9-eddf-43cd-aa6b-7f460ff087a4/스크린샷_2021-12-29_오후_2.30.51.png)

타이틀과 변경사항 나옴

git log( 히스토리 알 수 있음)

![스크린샷 2021-12-29 오후 2.32.04.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3b5a8ad3-5cd9-442e-b419-46a20c294a1f/스크린샷_2021-12-29_오후_2.32.04.png)

![스크린샷 2021-12-29 오후 2.34.50.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/87fc926a-aac4-46e8-9c74-821f8fa3d11e/스크린샷_2021-12-29_오후_2.34.50.png)

![스크린샷 2021-12-29 오후 2.35.23.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/45c79966-ea9f-49f7-9be8-1cf9d223f1a8/스크린샷_2021-12-29_오후_2.35.23.png)

두 번째 커밋 확인 가능

git commit -am "third commit” >> 모든 파일들을 메시지와 함께 커밋

![스크린샷 2021-12-29 오후 2.40.58.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6fed90f5-0761-433d-af1a-5d63e44dde18/스크린샷_2021-12-29_오후_2.40.58.png)

![스크린샷 2021-12-29 오후 2.40.43.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/18db31ea-c80b-4fbc-b976-fbf74ca7e6f5/스크린샷_2021-12-29_오후_2.40.43.png)

staging area와 working directory 파일 모두 커밋됨

- 커밋 팁

ex)

![스크린샷 2021-12-29 오후 2.50.58.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/88c8716b-caae-4757-b6f2-6c2031e31439/스크린샷_2021-12-29_오후_2.50.58.png)

작은 단위로, 의미 있는 이름으로 커밋하는 것이 좋음 why? 수정하기 용이함

커밋 메시지에 맞게 해당하는 내용만 커밋할 것, 여러가지 수행하지 말고

- UI, 소스트리로 커밋하기

![스크린샷 2021-12-29 오후 2.55.04.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9c5f9072-c354-4a21-baab-a9f362640fc7/스크린샷_2021-12-29_오후_2.55.04.png)

체크 누르면 staging area로 이동

![스크린샷 2021-12-29 오후 2.56.46.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3caf2d84-4b22-4558-a690-57f2a511a113/스크린샷_2021-12-29_오후_2.56.46.png)

커밋하고 싶은 내용 클릭 → 바뀐줄 스테이지 올리기 → 해당 내용만 커밋됨

![스크린샷 2021-12-29 오후 2.59.48.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/49eb3ee4-562e-4ee2-acd2-74d936fe092e/스크린샷_2021-12-29_오후_2.59.48.png)

파일상태 → 커밋 메시지 입력하면 커밋 완료