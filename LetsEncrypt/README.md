## LetsEncrypt?
* 무료로 공인인증서를 발급해주는 인증기관
* 3개월마다 갱신 필요

## letsencrypt-win-simple? 
* window server에서 LetsEncrypt를 활용할 수 있게 해주는 오픈소스
* https://github.com/PKISharp/win-acme/releases

## 인증서 발급받기
### 준비사항
* letsencrypt-win-simple
* 도메인

### 발급절차
1. exe 실행
2. [M : Create new certificate with advanced options]
3. [1. Manually input host names]
4. 도메인 입력
5. [4. [http-01] Self-host verification files (recommended)]
6. [2. Do not run any installation steps]
7. 완료!

### 생성 파일
* 파일 경로 : 사용자\Appdata\Roaming\letsencrypt-win-simple\httpsacme-v01.api.letsencrypt.org
* 생성 파일 설명
```
 - ca-[domain]-crt.pem : SSLCertificateChainFile
 - [domain]-crt.pem : SSLCertificateFile
 - [domain]-key.pem : SSLCertificateKeyFile
 
 - .der : another representation of the .pem
 - [domain]-all.pfx : encrypted file containing everything
 - [domain]-chain.pem : The Chain of CAs used to create the cerificate
 - [domain]-csr.pem : ...?
 ```
 
