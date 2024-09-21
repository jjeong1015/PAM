# WooriFISA-PAM

|<img src="https://avatars.githubusercontent.com/u/82391356?v=4" width="120" height="120"/>|
|:-:|
[@이정민](https://github.com/jjeong1015) 


```bash
# 사용자의 인증을 담당하는 모듈
$ sudo apt-get install libpam-pwquality
```

```bash
# 비밀번호 관련 정책을 정의하고 관리하는 설정 파일
$ sudo vi /etc/pam.d/common-password
password        requisite                       pam_pwquality.so retry=3 minlen=8 enforce_for_root
```

![1](https://github.com/user-attachments/assets/d57d80eb-c0dc-4964-8b85-c462955b6aa1)

```bash
# user0 사용자 생성
$ sudo adduser user0
```

![2](https://github.com/user-attachments/assets/b057c423-83c1-477c-8988-c3c2e7bd6741)

```bash
# 비밀번호를 000으로 할 경우, The password is a palindrome
# 비밀번호를 asdf로 할 경우, The password is shorter than 8 characters
# 비밀번호를 jjeongjjeong으로 할 경우, 통과
```

![3](https://github.com/user-attachments/assets/d0e85dbb-9296-4a4d-965f-cd66089892af)
