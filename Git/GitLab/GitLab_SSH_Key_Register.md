# GitLab에 SSH Key 등록하기

<img src="/Users/jeoncheolho/Desktop/개인파일/ImageBox/Git-logo.png" width="100%">

[![npm](https://camo.githubusercontent.com/f9423913a0a2104581c00dbe8067aeb6d18d0010/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f76657273696f6e2d323031382e33352d627269676874677265656e2e737667)](https://github.com/CheolhoJeon/TIL/blob/master)



## Intro

최근에 버전 관리 도구로 Git 을 많이 사용하는데, Git 을 사용할 경우 필수라고 할 수 있는 [GitHub](https://github.com/)와 [GitLab](https://gitlab.com/) 같은 온라인 저장소 서비스들이 모두 SSH 를 기본으로 지원하고 있습니다. **이 문서에서는 GitLab에 SSH key를 등록하는 방법을 다룹니다.** SSH 생성 방법은 기본 (default) 생성 방법과 더불어 GitLab 등을 위해 적당히 옵션을 주고 생성하는 방법도 별도로 설명합니다.



## SSH Key 생성하기

### SSH Key 확인하기

새로운 SSH Key를 생성하기 전에 시스템에 이미 SSH Key가 있는지 확인합니다. 터미널에서 아래와 같은 명령을 실행합니다.

~~~bash
$ cat ~/.ssh/id_rsa.pub
~~~

만약 `ssh-rsa` 로 시작하는 문자열이 보이면 이미 SSH 키 쌍(key pair) 를 가지고 있는 것이므로 새로 SSH 를 만들 필요없이 공개 SSH 키를 바로 사용하면 됩니다.

하지만 아래와 같은 결과가 나오면 아직 SSH 키가 없는 것이므로 새로 SSH 키 쌍을 만들어야 합니다.

~~~bash
cat: /.../.ssh/id_rsa.pub: No such file or directory
~~~



### SSH Key 생성하기

SSH 키를 만드는 것은 아주 쉽습니다. 아래와 같이 간단한 명령으로 새로운 SSH 키를 만들 수 있습니다. 

~~~bash
$ ssh-keygen
~~~

명령어를 실행하면 아래와 같이 키 쌍을 저장할 파일 이름을 입력하라고 나옵니다.

~~~bash
Enter file in which to save the key (/Users/.../.ssh/id_rsa):
~~~

보통의 경우 그대로 엔터키를 눌러서 디폴트 값인 `is_rsa` 를 사용합니다. 만약 같은 파일이 있다면 다른 이름을 지정하면 됩니다. 그 다음에는 비밀 번호를 입력하라고 나오는데 보통의 경우에는 따로 비밀번호를 입력하지 않고 넘어갑니다. 원한다면 비밀번호를 등록하면 됩니다.



###GitLab에 적합하게 생성하기

GitLab 을 위해서 SSH 를 생성할 때는 보통의 SSH 생성과는 다르게 옵션이 추가됩니다. 터미널에 다음과 같이 입력해서 SSH 키를 만듭니다.

```bash
$ ssh-keygen -t rsa -C "GitLab" -b 4096
```

`-t` 옵션은 SSH 키의 타입을 지정하기 위한 것으로 `rsa` 로 지정했습니다. `-C` 옵션은 주석을 뜻하면 `"GitLab"` 을 위해 만들었음을 표시합니다.  `-b` 옵션은 비트수를 지정하는 부분인데 원래 기본값은 2048이지만, GitLab 은 그 두 배인 4096 을 사용해서 키를 만듭니다.



##GitLab에 SSH 키 등록하기

이제 만들어진 공개키를 접속 하려는 Git에 등록하면 됩니다.



###SSH 키 복사하기

맥에서 다음과 같은 명령을 사용해서 공개키를 클립보드로 복사할 수 있다고 합니다. 이렇게 하면 터미널 명령으로 바로 파일 내용을 복사할 수 있습니다.

```bash
$ pbcopy < ~/.ssh/id_rsa.pub
```

물론 아래처럼 `cat` 명령을 실행한 다음 보여지는 공개키를 마우스로 복사해도 전혀 상관없습니다.

```bash
$ cat ~/.ssh/id_ras.pub
```



###SSH 키 등록하기

GitLab의 경우에는 계정에서 **Profile Settings > SSH Keys** 메뉴를 선택하면 나타나는 페이지의 **Key**섹션에 공개키를 복사해 넣으면 됩니다. 복사한 공개키를 **Key** 섹션에 붙여 넣습니다. **Title** 부분에는 구분 가능한 적당한 이름을 붙여줍니다. 예를 들어, `"My MacBook - macOS"` 이나 `"Home Desktop - Linux"` 같은 것을 입력할 수 있습니다.