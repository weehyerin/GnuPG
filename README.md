### What is GnuPG
-----------
###### GnuPG : 통신상에서 혹은 데이터를 저장할 때 보안을 지키는 도구

GnuPG는 공개키 방식의 암호화 기법을 사용하므로 더욱 안전하게 통신할 수 있다. 공개키 시스템에서는 사용자마다 비밀키와(private key) 공개키를 쌍으로 가지고 있다. 사용자의 비밀키는 노출되지 않고 안전하게 보관되며 공개키는 사용자와 통신하려는 다른 이들에게 나눠줄 것이다.

출처 : http://www.linuxlab.co.kr/docs/01-01-3.html

### Install GnuPG in Ubuntu

- root 권한으로 상승
~~~
su
~~~
+ passwd 입력 (passwd가 없다면, sudo passwd로 설정하기)

~~~
apt-get install gnupg
~~~

#### Check GnuPG version

```
gpg --version
```

### 새로운 key 생성

~~~
gpg --gen-key
~~~

real name : 입력
email address : 입력
q 입력 --> quit

비밀번호 입력하느 창이 뜸(key에 대하 비밀번호로서 잊어버리면 안됨)
<img width="400" alt="스크린샷 2019-07-23 오후 3 44 49" src="https://user-images.githubusercontent.com/37536415/61688776-dac01d80-ad60-11e9-8550-39fb3e28784f.png">

(만약 3번 모두 틀리면, key 생성이 안됨. 시가 지나면 풀림)


### 해지 인증서 만들기
##### 위에 생성한 비밀 번호를 잃어버렸을 때, 대비

~~~
gpg --output revoke.asc --gen-revoke keyID(위에서 key를 생성할 때, real name에 입력했던 것)
~~~
이 과정을 진행하다 보면, 비밀번호 입력 필요함. 위에서 설정한 key 비밀번호 입력하면 됨.

### 비밀 번호 변경하기
위에서 설정한 비밀 번호 변경하기

~~~
gpg --edit-key (real name에서 입력했던 값)

gpg> passwd

아까 설정한 비밀번호 입력
바꿀 비밀번호 입력
다시 비밀 번호 입력

gpg> save
~~~


### check key list 
~~~
gpg -k
~~~

### export public key

- 나의 공개 키로 암호화한 메시지는 나의 비밀 키로 복호화할 수 있다.
- 따라서 나의 공개 키를 다른 사람에게 주면, 다른 사람은 내 공개 키를 이용해 내게 보낼 메시지를 암호화할 수 있다.
#### 공개키 확인하기
~~~
gpg --armor --export (real name에서 입력했던 값)
~~~

#### 공개키 저장하기

~~~
gpg --armor --export (real name에서 입력했던 값) > testuser.asc
~~~

- testuser.asc로 공개 키가 만들어짐
- 이것을 다른 사용자에게 주면, 다른 사용자는 내 공개 키를 이용하여 자신의 파일을 암호한 다음 나에게 안전하게 보낼 수 있다.
- 암호화된 파일을 받으면, 나는 내 비밀 키로 복호화하여 사용할 수 있다.

<img width="500" alt="스크린샷 2019-07-23 오후 3 55 06" src="https://user-images.githubusercontent.com/37536415/61689525-52db1300-ad62-11e9-995a-7ace553b45d9.png">

### 다른 사용자에게 받은 공개 키를 이용하여, 암호화하기
#### 다른 사용자에게 받은 공개 키 import 하기
~~~
gpg --import (다른 사용자에게 받은 .asc 파일)
~~~

<img width="614" alt="스크린샷 2019-07-23 오후 3 57 49" src="https://user-images.githubusercontent.com/37536415/61689719-aa797e80-ad62-11e9-88f2-4463f21c1ab3.png">


## 암호화
--------------
### 내 비밀 키를 이용해서 암호화한 파일 만들기

~~~
echo 'hello testuser!' | gpg -ea --recipient weehyerin > to_weehyerin.txt
~~~

- hello testuser! 이라는 것을 암호화하여 to_weehyerin.txt 파일에 저장

### 복호화
~~~
gpg --decrypt to_weehyerin.txt
~~~
(+ 비밀번호 입력)

- 아까 암호화하여 만든 것 복호화

### 다른 사용자에게 받은 공개 키를 이용하여 .txt, .wav 파일 암호화하기

~~~
gpg --armor --recipient 2162A0166BA3B8F4 --encrypt (파일 이름)
~~~
<img width="623" alt="스크린샷 2019-07-23 오후 4 06 54" src="https://user-images.githubusercontent.com/37536415/61690284-eeb94e80-ad63-11e9-9278-11908312a44f.png">









