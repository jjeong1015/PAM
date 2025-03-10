# PAM

|<img src="https://avatars.githubusercontent.com/u/82391356?v=4" width="120" height="120"/>|
|:-:|
[@이정민](https://github.com/jjeong1015) 

## 기술 스택
<img src="https://img.shields.io/badge/VirtualBox-183A61?style=for-the-badge&logo=VirtualBox&logoColor=black"><img src="https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black"> 

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

## 🔍 교훈 및 적용
보안 정책 적용의 중요성
- 단순한 비밀번호를 거부하고 강력한 비밀번호를 요구하는 정책을 설정하면서,
사용자 계정 보안이 왜 중요한지, 그리고 이를 강제하는 방법이 얼마나 체계적인지 배울 수 있었다.
실제로 짧거나 단순한 비밀번호는 쉽게 거부되는 것을 보며 보안 정책이 실질적으로 작동하는 방식을 확인할 수 있었다.

PAM의 유연성을 직접 경험
- 기존 시스템을 수정하지 않고도 /etc/pam.d/common-password 설정을 변경하는 것만으로 비밀번호 정책을 강화할 수 있었다.
이를 통해 운영체제의 인증 시스템을 중앙에서 제어하는 방식이 얼마나 강력한지 직접 체감할 수 있었다.

## 🚀 발전
단순한 이론 학습이 아닌 직접 PAM 설정을 적용하고 테스트하면서 운영체제의 인증 방식에 대한 실무적인 감각을 키울 수 있었다.
오류 메시지를 분석하며, 시스템이 어떤 기준으로 비밀번호를 평가하는지 이해하는 능력이 향상되었다.
단순한 패스워드 정책 적용을 넘어서 앞으로 MFA나 계정 잠금 정책과 같은 보안 정책도 해보고 싶다는 생각이 들었다.

