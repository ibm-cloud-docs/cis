---

copyright:
  years: 2019
lastupdated: "2019-03-28"

keywords: resolve override, Cloud Object Storage, bucket resource

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# COS로 분석 대체
{: #resolve-override-cos}

## 유스 케이스
{: #cos-use-cases}

페이지 규칙과 일치하는 요청이 COS(Cloud Object Storage) 버킷 리소스로 분석되도록 하십시오.


## 전제조건
{: #cos-prerequisites}

다음 단계에서는 공용 액세스를 사용하는 기존 COS 인스턴스 및 버킷을 가지고 있다고 가정합니다. 공용 액세스에 대한 정보는 [공용 액세스 허용](/docs/services/cloud-object-storage/iam?topic=cloud-object-storage-allowing-public-access)을 참조하십시오.


## 페이지 규칙 작성 단계
{: #cos-create-page-rule}

* **성능>페이지 규칙**으로 이동합니다.
* **규칙 작성** 단추를 클릭합니다.
* URL 일치에 대해 원하는 값을 입력합니다. 예를 들어, `*.foo.com/*`입니다.
  * URL 일치가 COS 오브젝트 이름과 일치해야 합니다.
  * 예를 들어, `my-bucket1` 버킷 아래에 reports.txt라는 오브젝트가 있는 경우 다음 URL 일치가 둘 다 유효합니다.
    * `*.foo.com/*`
    * `*.foo.com/reports.txt`
* 드롭 다운을 사용하여 **성능** 섹션에서 **COS로 분석 대체**를 선택합니다.
* **Cloud Object Storage 인스턴스** 드롭 다운을 사용하여 원하는 인스턴스를 선택합니다.
* **버킷** 드롭 다운을 사용하여 원하는 버킷을 선택합니다.
* **1개의 리소스 프로비저닝** 단추를 클릭하여 페이지 규칙을 작성합니다.


## 개념에 대한 자세한 설명
{: #cos-detail-concepts}

**COS로 분석 대체** 페이지 규칙을 작성하는 경우 CIS는 COS 통합을 위해 필요한 다른 리소스를 자동으로 작성합니다. 여기에는 다음이 포함됩니다.

**CNAME**
* `<bucket-name>`으로서 `<bucket-name>.<cos-endpoint>`에 대한 CNAME DNS 레코드.
* 예를 들어, CIS 도메인이 `foo.com`이고 `images`라는 COS 버킷을 갖고 있으며 공용 COS 엔드포인트가 `s3.us-west.objectstorage.uat.test.net`인 경우 CIS는 `images.s3.us-west.objectstorage.uat.test.net`을 가리키는 `images.foo.com`으로서 CNAME을 작성합니다.
COS로 분석 대체 페이지 규칙이 더 이상 필요하지 않은 경우 CNAME을 페이지 규칙과 함께 수동으로 삭제해야 합니다.
{:note}

**호스트 헤더 대체**
* 호스트 헤더 대체 설정은 페이지 규칙과 일치하는 URI의 호스트 헤더를 `<bucket-name>.<cos-endpoint>`로 바꿉니다.
* 이전 예제를 사용하면 호스트 헤더 대체 값이 `images.s3.us-west.objectstorage.uat.test.net`으로 설정됩니다.


## 페이지 규칙 삭제
{: #cos-delete-page-rule}

COS로 분석 대체 페이지 규칙이 더 이상 필요하지 않은 경우 CNAME을 페이지 규칙과 함께 _수동으로_ 삭제해야 합니다.


## 페이지 규칙 편집
{: #cos-edit-page-rule}

페이지 규칙을 편집한 후에는 **COS로 분석 대체**가 페이지에 더 이상 표시되지 않습니다. 하지만 **분석 대체** `<bucket>.<domain>` 및 **호스트 헤더 대체** `<bucket>.<cos-endpoint>`가 **COS로 분석 대체**를 대신합니다.

**분석 대체**를 변경하면 새 CNAME 레코드(예: `<updated-bucket>.<domain>`)가 자동으로 작성되지 _않습니다_. 이는 **COS로 대체 분석**을 사용하는 페이지 규칙을 처음 작성할 때만 수행됩니다. 버킷에 대한 CNAME 레코드를 자동으로 작성하려면 [페이지 규칙 작성](#cos-create-page-rule) 단계를 따르십시오.
