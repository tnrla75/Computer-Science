
# JWT(Json Web Token)

> 인증을 진행하기위한 특정 정보를 저장하던 쿠키, 세션 이후 등장. 진행 구조는 쿠키와 다르지않는다. 
> 
> 공개/개인 키를 쌍으로 사용하여 토큰에 서명할 경우 서명된 토큰은 개인 키를 보유한 서버가 이 서명된 토큰이 정상적인 토큰인지 인증할 수 있다

## JWT의 구조
+ Header
> Header 의 경우 토큰 타입, 서명 생성을 위한 알고리즘을 저장

+ Payload  민감한 정보를 담지 않음. 암호화X 
  + iss: 토큰 발급자(issuer)
  + sub: 토큰 제목(subject)
  + aud: 토큰 대상자(audience)
  + exp: 토큰 만료 시간(expiration)
  + nbf: 토큰 활성 날짜(not before)
  + iat: 토큰 발급 시간(issued at)
  + jti: JWT 토큰 식별자(JWT ID)


+ Signature
  + 유효성 검증을 위한 고유한 암호화 코드, 암호화를 풀려면 서버에있는 개인키로만 암호화를 풀 수 있음
