# WooriFISA-PAM

|<img src="https://avatars.githubusercontent.com/u/82391356?v=4" width="120" height="120"/>|
|:-:|
[@이정민](https://github.com/jjeong1015) 

# PAM (Pluggable Authentication Module)

## 1. PAM이란?
PAM(Pluggable Authentication Module)은 **리눅스 및 유닉스 시스템에서 인증(Authentication) 과정을 모듈화하여 관리하는 프레임워크**이다.  
즉, 시스템의 인증 방식(비밀번호, 키 인증, 바이오메트릭 등)을 유연하게 설정하고 관리할 수 있도록 돕는다.

## 2. 왜 PAM을 사용하는가?
운영체제에서 사용자 인증을 처리하는 방식이 고정되어 있다면, 새로운 인증 방법(예: OTP, LDAP, 생체 인식 등)을 도입할 때마다 시스템을 수정해야 한다.  
PAM을 사용하면 **기존 애플리케이션을 수정하지 않고도 인증 방식을 변경하거나 확장할 수 있다.**  

PAM의 주요 장점:
- **유연성**: 다양한 인증 방법을 쉽게 추가 및 변경 가능
- **보안 강화**: 비밀번호 정책, 로그인 제한, 계정 잠금 등 다양한 보안 정책 적용 가능
- **중앙 집중화**: 모든 인증 관련 설정을 하나의 프레임워크에서 관리 가능

## 3. PAM이 사용되는 상황
PAM은 다양한 사용자 인증 및 접근 제어가 필요한 환경에서 활용된다. <br>대표적인 사용 사례는 비밀번호 정책 적용, SSH 로그인 보안 강화, 계정 잠금 정책 적용, 다중 인증(MFA) 적용이 있다.

### 비밀번호 정책 적용
사용자의 비밀번호 복잡성을 강제하기 위해 `libpam-pwquality` 모듈을 사용한다.


```bash
# 사용자의 인증을 담당하는 모듈
$ sudo apt-get install libpam-pwquality
```

```bash
# 비밀번호 관련 정책을 정의하고 관리하는 설정 파일 (3회 재시도 가능, 최소 길이 8자, root 계정에도 정책 적용)
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

## 결론
PAM은 리눅스 시스템에서 유연하고 강력한 인증 관리를 제공하는 프레임워크이다.
비밀번호 정책 강화, SSH 보안 설정, 계정 잠금, MFA 적용 등 다양한 인증 관련 기능을 손쉽게 설정할 수 있으며, 이를 통해 시스템 보안을 한층 강화할 수 있다.
