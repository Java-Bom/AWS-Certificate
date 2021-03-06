# Amazon EC2 인스턴스

- EC2의 장점
  - 빠른 제품 출시
    - 어떤 유형의 서버든 즉각 배포 가능
  - 확장성
    - 워크로드에 따라 언제든 스케일업, 스케일 다운이 가능
  - 통제성
  - 신뢰성
  - 보안성
    - VPC와 네트워크 보안 설정을 추가해 보안 수준을 높일 수 있음
  - 다양한 인스턴스 타입
  - 통합
    - AWS의 다른 서비스와 통합해 사용 가능
  - 비용 효율성
    - 온프라미스 환경은 계단식 비용 증가
    - 클라우드 환경은 선형식 비용 증가 (표 이미지)
- 인스턴스 타입과 특징
  - CPU, 메모리, 네트워킹, 스토리지 조합을 고를 수 있음
  - 현 세대 인스턴스 & 이전 세대 인스턴스
    - 현 세대는 최신 기술 반영 인스턴스
    - 이전 세대는 하위 호환성
    - 숫자는 현 세대가 더 높음 (어떤 숫자인지)
  - 인스턴스 타입(알파벳 별 종류 분류 작성)
    - 범용 인스턴스
      - 일반적인 목적으로 설계된 다수의 애플리케이션에 적용 가능
      - 전체적인 리소스의 균형
      - 성능 가속 기능
        - 표준 EC2 인스턴스는 고정 CPU 활성화 기능 사용
          - 미사용 CPU를 활성화 할 수 없음
        - 성능 가속이 추가된 인스턴스는 가속 CPU 활성화 기능 사용
          - 기준치 이상 사용 가능(미사용분)
          - T2, T3 지원
          - 일관된 성능을 보장할 수 없음(운영 환경에서 사용하기엔 위험성 존재)
        - 여기서 미사용분은 CPU 크레딧 사용 기록을 기준
    - 컴퓨트 최적화 인스턴스
      - 고도의 컴퓨팅 파워가 요구되는 워크로드를 처리하기 위한 타입
      - 동시 접속자 다수, 장시간 실행 배치, 게임서버 등
    - 메모리 최적화 인스턴스
      - 고성능 메모리가 요구되는 워크로드를 처리하기 위한 타입
      - 인메모리 데이터베이스, NoSQL 데이터 베이스, 빅데이터 엔진 등
    - 스토리지 최적화 인스턴스
      - 로컬 스토리지에서 대규모 데이터 세트를 순차적으로 읽기 및 쓰기 방식으로 접근하는 것들을 처리하기 위한 타입
      - 매우 낮은 전송 지연
      - 랜덤 IOPS
    - 고성능 컴퓨팅 인스턴스
      - 머신러닝, 세포 모델링, 유전공학, 유체역학, 자율주행, 신약개발, 지질탐사, 금융공학 등
      - 탁월한 수준의 컴퓨팅 파워가 요구되는 워크로드를 처리하기 위한 인스턴스 타입
      - 비용 비례 성능
      - 하드웨어 기반 가석기 지원
  - 네트워크 특징
    - VPC 내부에서 론칭하는 것이 좋음
      - VPC가 IP 주소 공간 관리를 위한 훌륭한 통제기법을 제공
    - 대역폭 최대화와 높은 네트워크 성능을 위해 **배치 그룹(placement group, 플레이스먼트 그룹)**에서 인스턴스 론칭 가능
    - 배치 그룹
      - 단일 AZ 내에서 인스턴스를 논리적 그룹으로 묶는 방법
      - 낮은 지연성과 높은 수준의 네트워크 처리 성능 제공
      - 클러스터 네트워킹 지원
      - 단일 트래픽 흐름 최대 10Gbps 네트워크 처리 성능 활용 가능
      - 배치 그룹 생성에 비용은 없음
      - 가급적 동일한 타입의 인스턴스를 사용하는 것이 좋음
      - 여러 개의 AZ로 확장 사용 불가
      - AWS 유일무이 이름 사용
      - 이를 최대한 활용하기 위해서는 리눅스에서 향상된 네트워킹을 지원하는 인스턴스 타입 선택
  - 스토리지 특징
    - EC2 인스턴스에 부착해 사용하는 블록 스토리지는 EBS(Elastic Block Storage)
    - EBS 볼륨은 EC2 인스턴스의 생명 주기의 영향을 받지 않음
    - EBS 볼륨 타입
      - 범용 스토리지(GP2)
        - 일반적인 목적
        - 기본설정으로 사용 가능
        - PIOPs보다 비용 효율적인 스토리지
      - 프로비전 IOPS(PIOPs) 스토리지
        - 대량의 I/O 작업이 수반되는 컴퓨팅 작업
        - I/O 처리 성능 최대화가 가능하고 데이터베이스나 애플리케이션에서 요구하는 IOPS 성능을 제공할 수 있음
        - PIOPs 스토리지는 범용 스토리지보다 많은 IOPS 자원을 소모해 비용이 더 비쌈
      - 마그네틱 스토리지
        - 기가바이트당 비용이 가장 낮음
        - 중요성이 낮은 워크로드에 적절
    - 인스턴스 스토어
      - EC2 물리적 하드웨어에 로컬 디스크
      - 수명이 짧고 생명주기가 같음
- EC2 사용 방법
  1. AMI 또는 커스텀 AMI를 통해 생성 가능
  2. 네트워킹, 보안 환경 설정 (VPC, 서브넷)
  3. 인스턴스 타입 선택
  4. AZ 선택, EBS 부착
  5. 시작
- EC2 가격 정책
  - 온디맨드 인스턴스
    - 가장 대표적 모델
    - 사용 시간에 따라 시간당 요금제 또는 초당 과금제로 비용 지불
    - 초기 설정비, 예상치 못한 비용 요소 없음
    - 언제든 스케일업, 스케일다운 가능
    - 개발에 필요한 리소스의 양을 예측하기 어려울 경우 적합
  - 예약 인스턴스
    - 온디맨드에 비해 최대 75% 요금 할인을 받을 수 있음
    - 사용량이 거의 확정된 프로덕션 워크로드용 인스턴스 실행에 적합
    - 애플리케이션이 안정적이거나 성능에 대한 요구 수준이 예측 가능한 경우
    - 예약 기간은 1년 또는 3년 약정
    - 리전 또는 특정 AZ 인스턴스 예약 가능
      - 특정 리전의 인스턴스를 예약한 경우 리전 예약 인스턴스
      - 특정 AZ의 인스턴스를 예약한 경우 존 예약 인스턴스
    - 지불 옵션
      - 모두 선불: 모든 비용을 미리 지불
      - 일부 선불: 비용 일부를 미리 지불
      - 선불 없음: 모든 비용을 매월 지불
    - 하위 카테고리
      - 표준 예약 인스턴스
        - 일반적인 케이스
      - 전환 예약 인스턴스
        - 계약 기간동안 컴퓨팅 성능에 대한 요구 수준에 대한 유연성 제공
  - 스팟 인스턴스
    - AWS의 일시적 여유 자원을 사용자에게 경매 입찰 방식으로 제공하는 인스턴스
    - 온디맨드 대비 최대 90% 할인된 금액
    - 스팟 인스턴스 가격 정책
    - 입찰로 가격 흥정 가능 > 입찰 금액을 다른 사람이 높게 쓰면 사용권을 잃게 됨
      - 작업이 중간에 중단되더라도 문제가 되지 않은 워크로드 처리에 적합
    - AWS 고객 상당수는 온디맨드를 기본으로 하고 컴퓨팅 성능을 높이기 위해 스팟 인스턴스를 사용
    - 최선의 방법은 기본 설정의 최대 가격(온디맨드 가격) 옵션을 적용하는 것
      - 사용 시간대에 대한 비용만 지불하면 됨
      - 항상 최대 가격이 입찰되기 때문에 사용권이 넘어갈 걱정 X
        - 작업이 중단될 상황이 발생하지 않음
      - 시장가로 가격 설정(최대가격보다 저렴하게 이용 가능)
- 공유 테넌시, 전용 호스트, 전용 인스턴스
  - AWS는 리소스를 초과해 프로비전 하지 않음
  - 규정 요건 충족 등을 위해 물리적인 서버 수준에 비해 가상화된 인스턴스 성능이 낮아질 경우 아래 방법들로 문제 해결 가능
    - 공유 테넌시
      - EC2 인스턴스를 론칭하면 기본적으로 적용되는 가상화 조건
      - EC2 인스턴스를 멀티 테넌시 하드웨어에서 실행
    - 전용 호스트
      - 특정 사용자에게만 배타적으로 할당된 물리적 서버
      - 기업의 필요에 따라 다양한 소프트웨어를 탑재해 사용할 수 있어 비용 효율성이 높음
        - 라이선스를 가진 소프트웨어를 사용할 경우
      - 할당된 물리적 서버에 원하는 만큼의 VM 생성 가능
      - 온디맨드 또는 예약 인스턴스 방식으로 이용 가능
    - 전용 인스턴스
      - 단일 테넌시 하드웨어에서 EC2 인스턴스를 실행
      - 다른 AWS 사용자와 하드웨어 레벨의 물리적으로 격리된 환경에서 실행
- 인스턴스와 Amazon 머신 이미지(AMI)
  - AMI는 아마존 크라우드에서 실행되는 서버에 대한 모든 소프트웨어 환경 설정 정보를 포함한 기본 설계도와 같음
  - AMI에는 인스턴스의 루트 볼륨이 포함되어 있음
    - 루트 볼륨에는 운영체제, 애플리케이션 서버, LAMP 스택, 기타 소프트웨어가 포함되어 있음
  - 론칭 승인 (AMI를 통해 인스턴스를 론칭할 수 있는지 정의한 정보)
    - 퍼블릭: 소유자가 모든 AWS 계정 사용자에게 론칭 승인을 부여
    - 명시적: 소유자가 특정 AWS 계정 사용자에게만 론칭 승인을 부여
    - 암묵적: 소유자가 암묵적으로 AMI를 통한 론칭 승인을 부여
  - AMI에는 어떤 볼륨 타입을 부착할지를 정의한 블록 디바이스 맵핑 정보가 포함
  - 특정 리전에서는 론칭할 수 있는 인스턴스의 수에 제한이 있음
  - 인스턴스 루트 볼륨
    - 인스턴스 루트 디바이스에는 인스턴스 부팅을 위한 이미지가 포함
    - EC2 인스턴스가 론칭되면, 모든 루트 디바이스는 S3로부터 론칭에 필요한 정보를 가져옴
      - S3를 통해 백업되는 인스턴스 루트 디바이스를 인스턴스 스토어 기반 AMI라 부름
    - EBS 서비스 제공 시점부터는 이미지를 EBS 볼륨 기반으로 제공
      - 인스턴스가 EBS 볼륨에서 론칭
      - EBS 스냅샷을 통해 생성
      - EBS 기반 AMI라 부름
    - 인스턴스 스토어 기반 AMI로 론칭
      - 인스턴스 부팅에 사용되는 이미지는 루트 볼륨에 복사됨
      - 인스턴스가 삭제되면 모든 데이터가 삭제됨
      - 중지 동작이 지원되지 않음
      - 인스턴스가 실패 또는 삭제되면 저장된 데이터는 복구할 수 없음
        - 정기적으로 지속형 스토리지에 백업
      - 재부팅 시에는 데이터가 유지
    - EBS 기반 AMI로 론칭
      - 데이터는 인스턴스의 다양한 상태에서도 그대로 유지
      - 중지 동작 지원
      - 인스턴스는 데이터 소실 위험 없이 언제든 중지, 재시작 가능
      - 인스턴스가 실패, 삭제돼도 데이터가 유지
      - 다른 인스턴스로 루트 볼륨 올길 수 있음
        - 인스턴스 스토어 기반 인스턴스는 불가능
    - EBS 볼륨 기반 인스턴스 사용을 권장
    - 인스턴스 스토어 기반 인스턴스에 EBS 볼륨을 부착해서 데이터를 저장하는 것도 좋은 방법
  - AMI는 다양한 방법으로 선택 가능
    - LAMP 스택을 원할 경우 LAMP 스택 섹션에서 찾아 생성 가능
    - 본인이 커스텀하게 AMI 생성 가능, 이를 커뮤니티에 배포할 수도 잇음
    - 퍼블릭 AMI 를 가져와서 커스터마이징 할 수 있음
    - 프라이빗 속성으로 설정도 가능
    - 커뮤니티에 공유된 AMI를 공유 AMI라 부름
      - 아마존에서는 이에 대한 신뢰성을 보증해주지 않음
    - AMI는 리전별 리소스이기 때문에 다른 리전에서 AMI를 공유하고 싶을 경우 원하는 리전에 복사한 후 공유해야 함(기출)
    - AWS ID를 사용해 특정 사용자와의 공유도 가능
    - AMI를 더 이상 사용하지 않을 경우 등록을 철회
      - 더 이상 해당 AMI로 접근 불가 및 새로운 인스턴스 생성 불가
- AMI 가상화
  - 하드웨어 가상화 머신(HVM)
    - 운영체제는 VM위에서 바로 실행
    - 베어 메탈 하드웨어에서 실행되듯 가상화를 위한 별다른 수행 작업이 필요 없음
      - 베어 메탈 하드웨어: 하드웨어에 아무런 소프트웨어가 설치되지 않은 상태
    - 하드웨어에 대한 완전한 가상화 환경 제공
    - 부팅을 위해 선택한 머신 이미지의 루트 블록 디바이스의 마스터 부트 레코드를 실행
    - 모든 하드웨어 자원을 최대한 활용할 수 있음
      - 높은 성능
      - 신속한 접근 가능
    - 모든 현 세대 인스턴스 타입은 해당 가상화를 지원
  - 부분 가상화(PV)
    - PV-GRUB라는 부트 로더를 이용해 부팅
    - PV의 게스트는 호스트 하드웨어 위에서 실행되므로 완벽한 가상화 기능을 제공하지는 못함
    - HVM 이미지를 사용하기를 권장
- 인스턴스 라이프 사이클
  - 인스턴스 론칭
    - 론칭하면 즉시 대기 중 상태로 나타남
    - 이때 AMI가 해당 인스턴스를 부팅
    - 헬스 체크 진행
    - 별 다른 이슈가 없으면 인스턴스 시작
    - 실행 가능한 상태가 되면 실행 중 상태로 변경
      - 인스턴스 모든 기능이 활성화
      - 과금이 시작
  - 시작 및 정지
    - 헬스 체크가 실패하면 인스턴스는 시작되지 않음
      - 별 다른 이슈가 없으면 인스턴스 시작
    - EBS 백업 인스턴스인 경우만 인스턴스를 정지 가능
      - 인스턴스 스토어 기반일 경우 사용 불가
    - 정지 상태의 인스턴스에는 과금하지 않음
      - 중지 준비 중인 경우 미청구
      - 최대 절전 모드로 전환 준비 중인 경우 청구
        - 메모리를 살려두는 상태
      - EBS 볼륨에 대한 요금은 부과
  - 재부팅
    - 인스턴스 스토어, EBS 볼륨 기반 인스턴스 모두 재부팅 가능
    - 인스턴스 스토어에 저장된 데이터도 그대로 보존
    - ip 주소, 머신 타입, DNS 네임 모두 그대로 유지
  - 인스턴스 삭제
    - 인스턴스를 삭제하면 삭제 중 또는 삭제 상태 정보가 나타남
    - 삭제하면 과금이 중지됨
    - 인스턴스에 삭제 보호 기능이 활성화 돼있으면 추가로 몇 가지 작업이 필요함
      - 또는 삭제 보호 기능 비활성화 필요
    - 삭제 시 연결된 EBS 볼륨도 삭제할 수 있고 그대로 남겨둘 수도 있음
      - DeleteOnTermination 속성을 지원
      - 기본 설정은 EBS 볼륨 유지
  - 인스턴스 폐기
    - 하드웨어에서 복구 불가능한 오류가 발생할 경우 인스턴스를 폐기시키거나 폐기 스케줄에 추가
    - 폐기 일정에 도달하면 인스턴스 작동이 정지되거나 폐기됨
    - 인스턴스 스토어 기반일 경우 인스턴스 삭제 전 저장된 데이터를 백업해야 함
- 인스턴스 연결
  - 퍼블릭 DNS 네임은 자동으로 생성
    - 수정 불가능
  - 퍼블릭 서브넷에서 생성하면 퍼블릭 IP 주소가 할당
    - 수정 불가능
    - 인스턴스 라이프 사이클과 함께 함
  - EIP를 사용할 수 있음
    - 퍼블릭 IP는 인스턴스를 종료할 경우 변경됨
  - 프라이빗 서브넷에 생성하면 프라이빗 IP 주소와 프라이빗 DNS가 할당됨
- 시큐리티 그룹
  - 하나 혹은 다수의 인스턴스에 대한 트래픽을 통제하는 가상의 방화벽
  - 인스턴스에는 다수의 시큐리티 그룹을 연결할 수 있음
  - 특징
    - 모든 아웃바운드 트래픽 허용
    - 허용 여부만 결정 가능하고 거부 여부는 정할 수 없음
    - stateful 속성
    - 언제든 추가 또는 삭제가 가능하고 변경 사항은 모든 인스턴스에 짧은 시간 내에 적용
- ECS 작성하기
  - 하이퍼바이저(EC2)
  - 컨테이너
    - 두 개 차이
    - 각각을 어떠한 상황에서 사용하면 좋은지
    - 비용
    - EKS(쿠버네티스)
