# WooriFISA-PAM

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

![2](https://github.com/user-attachments/assets/e8a5a673-05c3-4307-870a-379a07c8f96c)

```bash
# 비밀번호를 000으로 할 경우, The password is a palindrome
# 비밀번호를 asdf로 할 경우, The password is shorter than 8 characters
# 비밀번호를 jjeongjjeong으로 할 경우, 통과
```
