---
{"dg-publish":true,"permalink":"/프로젝트/Ubuntu/sudo/","dgPassFrontmatter":true}
---


```shell
sudo apt update && sudo apt upgrade
```
를 한 후에 업데이트 사항이 있다면 
했을 때 파일을 업데이트 하게 된다

```shell
ll
```
ls 명령어에 -l 옵션을 준 형태
상세하게 출력하라는 의미이다
![Pasted image 20240425092209.png](/img/user/첨부파일/Pasted image 20240425092209.png)
-는 파일을 나타내며 d로 시작하는 것은 디렉터리이다
나머지는 사용 권한이 명시되어 있다
숫자 1 부분은 하드링크 수를 나타내고, 디렉터리인 경우 해당 디렉터리를 기준으로 이동 가능한 디렉터리 개수이다
첫번째 j는 소유자를 의미하고 두번째 j는  소유 그룹을 뜻한다
뒤의 0은 파일의 크기이다
그 뒤에는 생성 또는 수정 시간이다