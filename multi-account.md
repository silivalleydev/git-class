## 멀티 계정 git 설정 방법

1. 홈 디렉토리에 `.ssh` 폴더를 만든다.
```
$ mkdir .ssh
```

2. 있는지 확인하고 싶다면 아래처럼 이동해보면된다.
```
$ cd ~/.ssh
```

3. ssh키를 생성해주는 데 형식은 `ssh-keygen -t rsa -C [github 이메일 계정] -f [생성될 key 파일]`이다.
- `abc@gmail.com`이라는 git 계정의 키를 `abc`라는 키파일로 생성한다고 가정
```
$ ssh-keygen -t rsa -C abc@gmail.com -f abc
```

4. `.ssh` 폴더 안에 `config` 파일을 생성하여 아래와 같이 설정한다.
- `config` 파일 생성
```
$ vi config
```

- `i`를 누르고 vi 에디팅 모드가 됐으면 아래 내용을 작성하고 `:`를 누르고 `x!`를 입력한다.  
: 아래내용은 `abc@gmail.com`라는 계정이 회사계정이라고 가정하고 설정해준것.  
    - `Host`: 이 값은 `저장소 주소 불러올 때` 쓰인다. `저장소를 구분하는 일종의 Key`라고 생각하면 된다.
    - `IdentityFile`: `ssh key의 경로`이다. `각 계정의 ssh key의 경로와 이름을 입력`해주면 된다.
```
# 개인 계정
Host github.com-me
        HostName github.com
        User git
        IdentityFile ~/.ssh/id_rsa

# 회사 계정
Host github.com-work
        HostName github.com
        User git
        IdentityFile ~/.ssh/abc
```

5. `ssh agent`에 등록해준다.
```
ssh-add abc
```

6. 자신의 git 계정에 ssh key public key를 등록해준다.

7. git clone을 받을 때에는 `github.com-work`라는 HOST에 `abc@gmail.com` 계정을 설정했으므로 `git@[설정한 HOST]:[user]/[저장소]`로 진행한다.
```
$ git clone git@github.com-work:git1/my.git
```