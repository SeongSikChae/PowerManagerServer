# PowerManagerServer

## Config.yml

* HttpPort: Http 접속 포트 (기본값 80)
* HttpsPort: Https 접속 포트 (기본값 443)
* ServerCertificate: 서버인증서 경로 (p12, pfx, pem 등 - 필수값)
* ServerCertificatePassword: 서버인증서 패스워드 (필수값)
* MqttServerPort: No SSL MQTT Broker 접속 포트 (기본값: 1803, SSL 포트는 8883 고정)
* MqttServerBacklog: MQTT 접속 대기열 (기본값: 100)
* DbPath: Database Sqlite 파일 경로 (필수값)
* AdminThumbprint 대표 관리자 클라이언트 인증서 fingerprint(필수값)
* TelegramToken: Telegram Message 용 봇 Token값
* KeepAlliveInterval: MQTT 통신 유지 Interval (기본값 30000 - millisecond 단위)
* ApiServerUrl: API 인증용 서버 URL (ex) https://10.0.0.5:18443)

## AdminThumbprint 값 입력법

```
openssl x509 -in "클라이언트 인증서 CRT 파일 경로" -noout -fingerprint -sha1
```
값을 소문자로 :을 제외하고 입력