# PowerManagerServer

## history

### v1.0.2
  * 스케줄 등록 시 Cron Expression 에서 요일 정보가 ? 가 아닌 다른 것을 사용하면 Crash 나는 문제 Fix
  * HTTP2Switch(HTTP/2 지원 여부), IncludeCipherSuites(TLS 시 키 교환 알고리즘 제한) 설정 추가
  * HTTP/2 통신 지원 추가 - HTTP2Switch true 시 HTTP/2 가 지원되면 HTTP/2 통신, false 이거나 지원되지 않으면 HTTP/1.1 통신
  * IncludeCipherSuites TLS 통신 시 특정 키 교환 알고리즘만 사용하도록 제하는 기능 추가 https://docs.microsoft.com/ko-kr/dotnet/api/system.net.security.tlsciphersuite?view=net-6.0
  * IncludeCipherSuites 설정 시 주의 사항 지원 되지 않는 알고리즘 선택하거나, HTTP2Switch를 true 했는데 HTTP/2에서 지원하지 않는 알고리즘 선택 시 웹서버 비정상 가동

### v1.0.1 
  * MqttMessageSyslogSending, MqttMessageSyslogHost, MqttMessageSyslogPort 설정 추가
  * MQTT 인증 메시지 SYSLOG 발송 기능 추가

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
* MqttMessageSyslogSending: MQTT 인증 메시지 SYSLOG 발송 여부
* MqttMessageSyslogHost: SYSLOG 전송 IP
* MqttMessageSyslogPort: SYSLOG 전송 PORT

## AdminThumbprint 값 입력법

```
openssl x509 -in "클라이언트 인증서 CRT 파일 경로" -noout -fingerprint -sha1
```
값을 소문자로 :을 제외하고 입력

## IncludeCipherSuites 설정 방법
```
IncludeCipherSuites:
  - "TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384"
  - "TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256"
```