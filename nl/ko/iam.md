---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Access Group Writer role, CIS instance, IAM

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# IAM 및 CIS
{:#iam-and-cis}

IBM Cloud Internet Services(CIS)는 IAM을 활용하여 권한 부여 및 인증을 수행합니다.

CIS 인스턴스에 아무도 추가하지 않으려는 경우 이 페이지를 무시할 수 있습니다.
{:note}

탐색 트리에 따라 3개의 CIS 기능 범위로 액세스 제한: 
* 안정성 - 예: DNS, GLB
* 보안 - 예: 인증서, IP 방화벽 규칙 및 속도 제한
* 성능 - 예: 페이지 규칙, 캐싱 및 라우팅

이 절에서는 인스턴스의 세분화된 액세스 제어를 제공하는 방법을 설명합니다.

## 역할
{:#iam-and-cis-roles}

다음 세 역할을 사용하여 IAM 활용
* 독자 - 인스턴스 및 도메인에 대한 정보를 가져올 수 있음
* 작성자 - 기존 구성을 변경할 수 있음
* 관리자 - 인스턴스, 도메인, 구성을 작성하거나 삭제할 수 있음

## 액세스 그룹 및 사용자
{:#iam-and-cis-access-groups-users}

사용자에게 직접 또는 액세스 그룹에 정책을 지정할 수 있습니다.
액세스 그룹에 지정하여 작성된 정책의 수를 최소화하고 이러한 정책을 관리하는 노력을 줄일 것을 권장합니다.

## 캐시
{:#iam-and-cis-cache}

권한 부여 결과를 캐시하고 동일한 요청이 다시 도달하면 캐시를 사용하여 의사결정을 내립니다. 캐시는 10분이라는 TTL(Time to Live)에 도달하면 만료됩니다.

## 우수 사례
{:#iam-and-cis-best-practices}

1. 정책을 수정하는 대신 기존 정책을 삭제한 다음 새로 작성하십시오.

## 시나리오
{:#iam-and-cis-scenarios}

이 절에서는 CIS를 통해 작성된 액세스 정책의 여러 예제를 설명합니다. 

### `구성` 유형의 도메인 레벨
{:#iam-and-cis-scenarios-domain-level}

#### 액세스 그룹에서 `보안 구성`이 있는 단일 도메인에 대한 액세스
##### 작성자 역할

Bob은 하나의 CIS 인스턴스 `cis-test-instance` 및 두 개의 도메인, `bob.com`과 `bob-ibm.com`을 가지고 있습니다.
Bob은 **`bob.com`**의 **보안 구성**에 대한 작성자 역할의 액세스 권한만 회사의 모든 보안 엔지니어(sec-group)에 제공하려고 합니다.

다음 단계는 이 시나리오를 가능하게 하는 IAM 정책을 작성하는 방법을 보여줍니다.

Bob은 cis-test-instance에 로그인한 후 다음을 수행합니다.
1. 탐색줄에서 **계정 > 액세스** 탭을 클릭합니다.
1. 액세스 권한을 제공할 **액세스 그룹** - **sec-group**을 선택합니다.
1. **`bob.com`**을 선택합니다.
1. **작성자** 역할을 선택합니다.
1. **보안 구성** 옵션을 선택합니다.
1. **정책 작성**을 클릭합니다.

관리 탭에서
**sec-group**에 대한 다음 정책이 작성됩니다.

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e

Service Instance 
    name: cis-test-instance  
    id: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9 
Domain 
    name: bob.com
    id: 4b23ec772965f672f96f05670e36827e 
Config Type
    cfgType: security
```

이제 sec-group은 `bob.com`만 볼 수 있는 액세스 권한을 갖게 되며 보안 관련 값을 수정할 수 있습니다. 

##### 액세스 그룹의 역할을 작성자에서 관리자로 업데이트

Bob이 sec-group의 역할을 작성자에서 관리자로 업데이트하려면 기존 정책을 삭제해야 합니다. 
1. **IAM 관리 탭 > 액세스 그룹 > sec-group > 액세스 정책**으로 이동합니다.
1. 다음 정책을 삭제합니다. 
  ```
  Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
  ```

그런 다음 Bob은 정책을 새로 작성해야 합니다. 
1. 탐색줄에서 **계정 > 액세스** 탭을 클릭합니다.
1. 액세스 권한을 제공할 **액세스 그룹** - **sec-group**을 선택합니다.
1. **`bob.com`**을 선택합니다.
1. **관리자** 역할을 선택합니다.
1. **보안 구성** 옵션을 선택합니다.
1. **정책 작성**을 클릭합니다.

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

기존 정책(작성자)이 삭제되지 않은 경우, 관리자에 대한 정책 작성 시도에 실패합니다.

##### 보안과 함께 성능을 포함하도록 구성 업데이트

Bob이 보안과 함께 `bob.com`의 성능 구성에 대한 관리자 sec-group 액세스를 제공하려고 하는 경우 다음을 수행합니다.
1. 탐색줄에서 **계정 > 액세스** 탭을 클릭합니다.
1. 액세스 권한을 제공할 **액세스 그룹** - **sec-group**을 선택합니다.
1. **`bob.com`**을 선택합니다.
1. **관리자** 역할을 선택합니다.
1. **성능 구성** 옵션을 선택합니다.
1. **정책 작성**을 클릭합니다.

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: performance, domainId: 4b23ec772965f672f96f05670e36827e

```

#### `보안 구성`의 모든 도메인에 액세스

이전 예제에서 `bob.com` 및 `bob-ibm.com`에 대한 보안 조치를 제공하려는 경우 각 도메인에서 단계를 반복하여 정책을 새로 작성해야 합니다. 유일한 차이는 각 정책에 대해 해당 도메인을 선택하는 것입니다.

1. 탐색줄에서 **계정 > 액세스** 탭을 클릭합니다.
1. 액세스 권한을 제공할 **액세스 그룹** - **sec-group**을 선택합니다.
1. **`bob.com`**을 선택합니다.
1. **관리자** 역할을 선택합니다.
1. **보안 구성** 옵션을 선택합니다.
1. **정책 작성**을 클릭합니다.

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

1. 탐색줄에서 **계정 > 액세스** 탭을 클릭합니다.
1. 액세스 권한을 제공할 **액세스 그룹** - **sec-group**을 선택합니다.
1. **`bob-ibm.com`**을 선택합니다.
1. **관리자** 역할을 선택합니다.
1. **보안 구성** 옵션을 선택합니다.
1. **정책 작성**을 클릭합니다.

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 7ad7341865246f5df482ad9f76aafb5a
```



#### `보안 구성` 및 `안정성 구성`의 단일 도메인에 액세스

Bob은 하나의 CIS 인스턴스 cis-test-instance 및 두 개의 도메인, `bob.com`과 `bob-ibm.com`을 가지고 있습니다.
Bob은 **`bob-ibm.com`**의 **보안 및 안정성 조치**에 대한 작성자 역할의 액세스 권한만 Tony에게 제공하려고 합니다.

Bob은 cis-test-instance에 로그인한 후 다음을 수행합니다.
1. 탐색줄에서 **계정 > 액세스** 탭을 클릭합니다.
1. 액세스 권한을 제공할 **Tony**를 선택합니다.
1. **`bob-ibm.com`**을 선택합니다.
1. **작성자** 역할을 선택합니다.
1. **보안 및 안정성** 옵션에 대한 선택란을 선택합니다. 
1. **정책 작성**을 클릭합니다.

그러면 각 구성 유형에 대해 백엔드에 두 개의 정책이 작성됩니다.

### 모든 구성 유형이 있는 도메인 레벨
{:#iam-and-cis-scenarios-domain-level-all-config-types}

Bob은 Tony에게 도메인 레벨의 읽기/쓰기/관리 권한을 부여하려고 합니다.

#### 작성자
Bob은 cis-test-instance에 로그인한 후 다음을 수행합니다.
1. 탐색줄에서 **계정 > 액세스** 탭을 클릭합니다.
1. 액세스 권한을 제공할 **Tony**를 선택합니다.
1. **`bob.com`**을 선택합니다.
1. **작성자** 역할을 선택합니다.
1. CIS 기능 범위에 대한 상자를 모두 선택합니다.
1. **정책 작성**을 클릭합니다.

```
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: security	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: performance	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: reliability	
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

#### 관리자
Bob은 cis-test-instance에 로그인한 후 다음을 수행합니다.
1. 탐색줄에서 **계정 > 액세스** 탭을 클릭합니다.
1. 액세스 권한을 제공할 **Tony**를 선택합니다.
1. **`bob.com`**을 선택합니다.
1. **관리자** 역할을 선택합니다.
1. CIS 기능 범위에 대한 상자를 모두 선택합니다.
1. **정책 작성**을 클릭합니다.

```
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: security	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: performance	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: reliability	
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

#### 독자
Bob은 cis-test-instance에 로그인한 후 다음을 수행합니다.
1. 탐색줄에서 **계정 > 액세스** 탭을 클릭합니다.
1. 액세스 권한을 제공할 **Tony**를 선택합니다.
1. **`bob.com`**을 선택합니다.
1. **독자** 역할을 선택합니다.
  1. 모든 선택란은 사용자에게 전체 도메인에 대한 *최소* 읽기 액세스 권한이 필요하다고 표시하도록 미리 체크 표시가 되어 있으며 도메인에 대한 부분 액세스 권한은 제공할 수 없습니다.
1. **정책 작성**을 클릭합니다.


```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

### 인스턴스 레벨 - 모든 도메인
{:#iam-and-cis-scenarios-instance-level}

이 정책은 IAM 관리 페이지를 통해 작성하고 관리해야 합니다.

인스턴스 레벨 액세스는 Bob이 Tony에게 10개의 인스턴스 중 1개의 인스턴스에 대한 권한을 제공할 수 있음을 의미합니다.
Tony는 이 인스턴스의 모든 도메인을 볼 수 있습니다. 

Bob이 다음에 액세스할 수 있도록 작성자 또는 관리자 역할을 제공하려는 경우 인스턴스 레벨 액세스 권한을 제공해야 합니다.
* 로드 밸런서 - 풀 및 상태 검사
* 방화벽 액세스 규칙
* 작업자 

IAM 관리 페이지에서 서비스 인스턴스 cis-test-instance에 대한 작성자/관리자 정책을 작성합니다.

```
Manager	Resource	Only service instance cis-test-instance of CIS 	
or
Writer	Resource	Only service instance cis-test-instance of CIS 	
```

## IAM 정책 관리 
{:#manage-iam-policies}

CIS를 사용하면 사용자가 IAM 정책을 작성할 수 있지만 [IAM 페이지](
https://{DomainName}/iam#/overview)를 통해 관리해야 합니다.

## 참고
{:#iam-note}
CIS 인스턴스의 액세스 페이지에 작성된 모든 정책에 대해 2 - 3개의 정책이 차례로 작성됩니다.

1. 서비스 인스턴스 플랫폼 뷰어 역할을 사용하면 추가된 사용자가 대시보드에서 인스턴스를 볼 수 있습니다.

**예제**
```
Viewer	Resource	Only service instance cis-instance-instance of CIS 	
```

2. 도메인 레벨 읽기 액세스는 세분화된 작업 액세스에 필요한 최소 요구사항입니다.

**예제**
```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
```
3. 구성 유형으로 작성한 정책이 있습니다.

**예제**
```
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

**FAQ**
1. 내 서비스 인스턴스 ID를 어떻게 가져옵니까?

   개요 페이지에서 CRN을 복사하십시오.
   ```
   crn:v1:test:public:internet-svcs:global:a/2c38d9a9913332006a27665dab3d26e8:836f33a5-d3e1-4bc6-876a-982a8668b1bb::
   ```
   CRN의 마지막 파트가 서비스 인스턴스입니다. `836f33a5-d3e1-4bc6-876a-982a8668b1bb`.
   
   또는
   
   리소스 목록 기본 페이지에서 CIS 인스턴스가 포함된 행을 클릭하고 서비스 인스턴스 ID의 GUID를 복사하십시오.

2. 정책을 삭제했지만 정책을 제공받은 사용자는 여전히 해당 조치를 수행합니다.

   CIS는 권한 부여 결과를 캐시하고 캐시의 TTL은 10분입니다.  
   
   IAM이 권한을 부여하는 경우 의사결정을 하기 전에 액세스 그룹의 액세스 정책과 사용자 고유 정책을 사용합니다.

3. Internet Services를 프로비저닝하는 데 필요한 권한은 무엇입니까?

   리소스를 작성하여 리소스 그룹에 추가할 수 없는 경우 액세스 문제로 처리할 가능성이 높습니다. 최소한 리소스 그룹 자체에 대한 뷰어 역할과 계정의 서비스에 대한 편집자 역할이 있어야 합니다. 계정 관리자에게 문의하여 계정에서 지정된 액세스 권한을 확인할 수 있습니다. 자세한 정보는 [리소스에 대한 액세스 관리](/docs/iam?topic=iam-iammanidaccser)를 참조하십시오.
   
 
