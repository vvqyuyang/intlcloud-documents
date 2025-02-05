## 설정 시나리오

Tencent Cloud CDN은 후불 과금 방식입니다. 악성 사용자의 도용으로 인해 대량의 대역폭이 발생하여 요금 급증이 우려된다면, 대역폭 상한을 설정하여 사용량을 제어(대역폭 과금 사용자 대상)할 수 있습니다.

대역폭 상한 설정은 통계 주기(5분 단위)마다 발생한 대역폭을 점검하여 지정된 임계 값을 초과하면 설정에 따라 강제로 원본을 가져오거나, CDN 서비스를 비활성화(모든 요청에 404 반환)함으로써 더 많은 CDN 가속 요금이 발생하는 것을 방지합니다.

>!대역폭 상한 설정은 적용되기까지 일정 시간(10분 전후)이 소요되며, 해당 기간 동안 발생한 소비 내역에 대해서는 정상 과금됩니다.

## 설정 가이드
### 설정 조회
[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 메뉴에서 [도메인 관리]를 선택하고 도메인 오른쪽의 [관리]를 클릭하면 도메인 설정 페이지로 이동할 수 있습니다. [고급 설정]에서 대역폭 상한 설정을 확인할 수 있습니다. 설정은 기본적으로 비활성화 상태입니다.
![](https://main.qcloudimg.com/raw/2dc4d64a3c1f4054471a31681c19765e.png)

### 수정 구성
#### 1. 설정 변경
on-off 스위치를 클릭하여 임계 값의 최댓값을 설정할 수 있습니다:
- COS 원본 도메인은 임계 값에 도달한 후에만 모든 액세스에 404를 반환합니다.
- 도메인 대역폭이 임계 값을 초과했음을 확인한 후, 액세스 요청 또는 액세스 404 응답 설정이 모두 적용되기까지 전체 네트워크 노드는 점진적으로 전달되기 때문에 일정 시간 지연될 수 있습니다.

![](https://main.qcloudimg.com/raw/7520963775f790d2adaf588b9418bd7c.png)

#### 2. 설정 비활성화
대역폭 상한 on-off 스위치를 통해 클릭 한 번으로 설정을 비활성화할 수 있습니다. on-off 버튼이 비활성화 상태일 때 아래에 기존 설정이 존재하더라도 현재 네트워크에 적용되지 않습니다. 다음번에 활성화하는 경우, 전체 네트워크에 적용되도록 즉시 배포하지 말고 설정에 대한 2차 확인을 먼저 진행하십시오.
![](https://main.qcloudimg.com/raw/1a18d747e269347c90aa17f116601509.png)

#### 3. 리전 특수 설정
사용자의 가속 도메인 서비스 지역이 글로벌 가속이며, 중국 내/중국 외 가속 구역에 다른 대역폭 상한을 설정하고자 한다면 설정 아래의 [특수 설정 추가]을 클릭하여 설정할 수 있습니다.
![](https://main.qcloudimg.com/raw/1a855e379a90af8de76c0ee26727e632.png)

>!
>- 지역 특수 설정을 추가한 후에는 현재 직접 삭제할 수 없습니다. 비활성화를 통해 사용하지 않도록 설정할 수 있습니다.

## 설정 예시
가속 도메인 `cloud.tencent.com`의 대역폭 상한 설정이 아래와 같을 경우
![](https://main.qcloudimg.com/raw/772256e11f3c1c9a85ae9cc57315c4f6.png)
실제 액세스 상황은 다음과 같습니다.
중국 내 대역폭이 11Gbps에 달하고 중국 외 대역폭이 4Gbps에 달하는 경우, 모든 중국 내 사용자의 액세스에 대해 404가 직접 반환됩니다. 중국 외 사용자는 계속해서 가속 서비스를 누릴 수 있습니다.

