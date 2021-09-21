# AWS CloudFront VS Global Accelerator

**사전 지식**

엣지 로케이션

리전(대한민국 서울)과 가용영역(a, b, c)과 별개로 취급하는데, AWS의 **CDN 서비스인 CloudFront와 DNS 서비스인 Route53의** **캐시서버**를 의미한다.

<br/>

## 용도

CloudFront 는 CDN(콘텐츠 전송 네트워크) 역할을 한다. 따라서 CloudFront 는 정적 리소스를 빠르게 전달하기 위해 사용된다.

![image](https://user-images.githubusercontent.com/13347548/134183318-45f77098-5ea4-4b5e-9c0c-20ef684234ce.png)

Global Accelerator 는 엣지 로케이션을 이용해서 사용자에게 애플리케이션까지의 최적 경로를 제공해준다. 다시말해 사용자에게 가장 가까운 위치에서 호스팅되고 있는 애플리케이션으로 엣지 로케이션을 라우팅 후 리전 엔드포인트를 라우팅한다.

![image](https://user-images.githubusercontent.com/13347548/134183377-27fb3010-b21f-4678-a2cd-5544525b6926.png)

## 차이점

| 구분     | CloudFront                    | Global Accelerator                |
| -------- | ----------------------------- | --------------------------------- |
| 용도     | 정적 자원 캐싱(프리티어 제공) | 트래픽을 최적의 엔드포인트로 연결 |
| 프로토콜 | HTTP                          | TCP, UDP                          |
| 과금     | HTTP 요청 기반                | 사용량만큼                        |
| 진입점   | 동적 IP 주소                  | 고정 IP 주소                      |

<br/>

## DDos 방어

Amazon CloudFront, AWS Shield(Global Accelerator가 사용한다.), AWS Web Application Firewall(WAF), Amazon Route 53는 네트워크 및 애플리케이션 계층 DDoS 공격을 비롯한 여러 유형의 공격에 대해 유연한 계층형 보안 방어를 구축하기 위해 원활하게 협력합니다.

