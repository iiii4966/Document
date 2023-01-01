# Password

- plain password 를 DB 에 저장하지 마라.
- plain password 를 해싱하기 위해 암호화 해시 함수를 사용하자.
  - bcrypt, scrypt, PBKDF2, Argon2
- password 해시 함수로 다음 함수를 사용하지 말자.
  - MD5, SHA1, SHA256, SHA512, RipeMD, WHIRLPOOL, SHA3
- password 암호화 해시를 직접 만들지 말자.
- plain password 에 salt 값을 붙여 해시값을 유추하기 어렵도록 하자.
- salt 값 생성은 일반 랜덤 함수가 아닌 CSPRNG 랜덤 함수를 사용하자.
  - python: secrets
- salt 값을 재사용하지 마라. 사용자마다 다르게 설정하라.
- 적절한 길이의 salt 값을 생성하라. (SHA256 - 32bytes) 
- 비밀번호 생성 시 복잡한 비밀번호 규칙을 강제하자.
- 비밀번호 변경 시 이메일이나 모바일 기기를 통해 사용자를 식별할 수 있는 2차 수단을 사용하자.
- 비밀번호 변경 시 이메일을 통해 변경 링크를 제공하는 경우 유추할 수 없는 유저 고유 식별 토큰을 사용하라.
- 비밀번호 변경 제한 시간을 두어라.
- 비밀번호 유출 시 신속하게 사용자에게 알리고 비밀번호를 변경하도록 유도하라.