---
title: 앱용 Common Data Service의 필드 데이터 유형 | MicrosoftDocs
description: 앱에 사용할 수 있는 다양한 필드 데이터 유형 이해
keywords: ''
ms.date: 06/27/2018
ms.service: crm-online
ms.custom: null
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - powerapps
author: Mattp123
ms.assetid: 734b4ffa-5543-4f88-8517-299589f433f7
ms.author: matp
manager: kvivek
ms.reviewer: null
ms.suite: null
ms.tgt_pltfrm: null
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="types-of-fields"></a>필드 유형

형식에 사용되는 이름은 사용되는 디자이너에 따라 달라집니다. [PowerApps 포털](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)에서는 데이터의 형식이 지정되는 방식을 포함하는 규칙을 사용합니다. 솔루션 탐색기 형식은 형식 한정자가 있는 데이터베이스 데이터 형식과 일치하는 이름을 사용합니다. 다음 표에는 해당 `AttributeTypeDisplayName`API 유형이 나와 있습니다.

|포털 데이터 유형 |솔루션 탐색기 유형| API 유형|
|--|--|--|
|**정수(Big)**|**타임스탬프**|`BigIntType`|
|**통화**|**통화**|`MoneyType`|
|**고객**|**고객**|`CustomerType`|
|**날짜 및 시간**|**날짜 및 시간**<br />*날짜 및 시간* 형식|`DateTimeType`|
|**날짜만**|**날짜 및 시간**<br />*날짜만* 형식|`DateTimeType`|
|**10진수**|**10진수**|`DecimalType`|
|**기간**|**정수**<br />*기간* 형식|`IntegerType`|
|**Email**|**한 줄 텍스트**<br />*전자 메일* 형식|`StringType`|
|**부동 소수점 수**|**부동 소수점 수**|`DoubleType`|
|**이미지**|**이미지**|`ImageType`|
|**언어**|**정수**<br />*언어* 형식|`IntegerType`|
|**조회**|**조회**|`LookupType`|
|**다중 선택 옵션 집합**|**MultiSelect 옵션 집합**|`MultiSelectPicklistType`|
|**여러 줄 텍스트**|**여러 줄 텍스트**|`MemoType`|
|**옵션 집합**|**옵션 집합**|`PicklistType`|
|**담당자**|**담당자**|`OwnerType`|
|**전화**|**한 줄 텍스트**<br />*휴대폰* 형식|`StringType`|
|**상태 설명**|**상태 설명**|`StatusType`|
|**상태**|**상태**|`StateType`|
|**텍스트 영역**|**한 줄 텍스트**<br />*텍스트 영역* 형식|`StringType`|
|**텍스트**|**한 줄 텍스트**<br />*텍스트* 형식|`StringType`|
|**주식 종목 코드**|**한 줄 텍스트**<br />주식 종목 코드 형식|`StringType`|
|**표준 시간대**|**정수**<br />*표준 시간대* 형식|`IntegerType`|
|**두 개의 옵션**|**두 개의 옵션**|`BooleanType`|
|**고유 식별자**|**고유 식별자** 또는 **기본 키**|`UniqueidentifierType`|
|**URL**|**한 줄 텍스트**<br />*URL* 형식|`StringType`|
|**정수**|**정수**<br />*없음* 형식|`IntegerType`|

추가하거나 편집할 수 있는 각 형식에 대한 자세한 설명은 해당 디자이너에 대한 항목을 참조하십시오.
 - [PowerApps 포털을 사용하여 앱용 Common Data Service에 대한 필드 만들기 및 편집: 필드 데이터 형식](create-edit-field-portal.md#field-data-types)
 - [PowerApps 솔루션 탐색기를 사용하여 앱용 Common Data Service에 대한 필드 만들기 및 편집: 필드 데이터 형식](create-edit-field-solution-explorer.md#field-data-types)

API에서 필드 데이터 형식이 정의되는 방법에 대한 자세한 내용은 [특성 메타데이터](/powerapps/developer/common-data-service/entity-attribute-metadata)를 참조하십시오.

## <a name="field-types-used-by-the-system"></a>시스템에서 사용 하는 필드 형식

시스템에서 사용하는 일부 필드는 디자이너를 사용하여 추가할 수 없습니다.

|그런 다음|설명|
|--|--|
|**큰 정수** 또는 **타임 스탬프**|시스템에서 버전 번호를 캡처하고 엔터티에 대한 업데이트를 관리하는 데 사용됩니다.|
|**고객**|거래처 또는 연락처 등의 고객을 지정하는 데 사용할 수 있는 조회 필드입니다.<br />**참고**: 이 특성은 솔루션 탐색기 디자이너를 사용하여 추가할 수 있습니다.|
|**담당자**|사용자 또는 팀 담당 엔터티 레코드가 할당되는 사용자 또는 팀을 참조하는 시스템 조회 필드입니다.|
|**상태 설명**|상태 필드에 대한 추가 정보를 제공하는 옵션이 있는 시스템 필드입니다. 각 옵션은 사용 가능한 상태 옵션 중 하나와 연결됩니다. 옵션을 추가하고 편집할 수 있습니다. <br /><br /> 사용자 지정 상태 전환을 포함하여 특정 엔터티에 대해 사용할 수 있는 상태 옵션을 제어할 수 있습니다. 추가 정보: [사용자 지정 엔터티에 대한 상태 설명 전환 정의](define-status-reason-transitions.md)|
|**상태**|일반적으로 활성 및 비활성 상태에 해당하는 옵션이 있는 시스템 필드입니다. 일부 시스템 특성에는 추가 옵션이 있지만 모든 사용자 지정 특성에는 **활성** 및 **비활성** 상태 옵션만 있습니다.  |
|**고유 식별자**|시스템 필드는 각 레코드의 GUID(Globally Unique Identifier) 값을 저장합니다.|

  
## <a name="multiselect-option-set"></a>MultiSelect 옵션 집합

다중 선택 필드를 추가하여 양식(기본, 빨리 만들기 및 빠른 보기) 및 전자 메일 템플릿을 사용자 지정할 수 있습니다. MultiSelect 옵션 집합 필드를 추가할 때 사용자가 선택할 수 있는 여러 값을 지정할 수 있습니다. 사용자가 양식에 데이터를 입력할 때 드롭다운 목록에 표시되는 값을 하나, 여러 개 또는 모두 선택할 수 있습니다.

예를 들어 조직이 여러 지역 또는 국가에서 운영되는 경우 '작업 영역' 필드에 여러 위치 또는 국가를 포함할 수 있습니다. 사용자는 사용 가능한 값 목록에서 하나 또는 둘 이상의 위치를 선택할 수 있습니다.

다중 선택 옵션 집합은 읽기 전용 표, 편집 가능한 표 및 양식에서만 사용할 수 있습니다. 다중 선택 옵션 집합은 다음에서 지원되지 않습니다. 
- 워크플로, 동작, 대화 상자, 롤업, 차트 및 계산 필드
- 보고서, SLA 및 라우팅 규칙

다중 선택 필드는 다음과 같은 형식의 양식에서 지원됩니다.

|양식 유형|사용 가능성|
|--|--|
|**터보 양식**|예|
|**새로 고침 양식**|읽기 전용(필드를 사용할 수 있지만 편집할 수는 없음)|
|**레거시 양식**|아니요|
|**대량 편집 양식**|아니요|

조직에 정의된 전역 옵션 집합을 사용하여 다중 선택 옵션 집합에 대한 값을 구성할 수 있습니다.


<a name="BKMK_UsingTheRightTypeOfNumber"></a>
  
## <a name="using-the-right-type-of-number"></a>올바른 숫자 유형 사용

사용할 올바른 유형의 숫자 필드를 선택할 때 **정수** 또는 **통화** 유형을 사용하도록 선택하면 매우 간단합니다. **부동 소수점** 또는 **10진수** 숫자를 사용한다고 선택하면 좀더 주의가 필요합니다.  
  
10진수는 지정된 대로 정확히 데이터베이스에 저장됩니다. 부동 소수점은 값과 매우 근사한 값을 저장합니다. 정확한 값을 사용할 수 있을 때 매우 근사한 값을 선택하는 이유는 무엇입니까? 다른 시스템 성능을 갖기 때문입니다.  
  
매우 정확한 계산을 요구하는 보고서를 제공해야 하거나 또는 일반적으로 다른 값과 같거나 같지 않은 값을 찾는 쿼리를 사용할 경우 10진수를 사용합니다.  
  
일반적으로 연산자보다 크거나 작은 값을 사용하여 다른 값과 비교하여 쿼리하는 분수 또는 값을 나타내는 데이터를 저장할 때 부동 소수점 숫자를 사용합니다. 대부분의 경우 10진수와 부동 소수점 간에는 차이가 거의 없습니다. 가능한 한 가장 정확한 계산이 필요한 경우가 아니면 부동 소수점을 사용할 수 있습니다.  
  
<a name="BKMK_UsingCurrencyFields"></a>
 
## <a name="using-currency-fields"></a>통화 필드 사용

통화 필드를 사용하면 조직에서 조직의 레코드에 사용할 수 있는 여러 통화를 구성할 수 있습니다. 조직에서 여러 통화를 사용하는 경우 기본 통화를 사용하여 값을 제공하는 계산을 수행하려고 할 수 있습니다. 다른 통화 필드가 없는 엔터티에 통화 필드를 추가하면 다음과 같은 추가 필드 2개가 추가됩니다.  
  
- 조직에 구성된 활성 통화로 설정할 수 있는 조회 필드 **통화**. **설정** > **비즈니스 관리** > **통화**에서 조직의 활성 통화를 여러 개 구성할 수 있습니다. 거기서 통화와 조직에 설정된 기본 통화와의 환율을 지정할 수 있습니다. 활성 통화가 여러 개 있을 경우 통화 필드를 양식에 추가할 수 있고 사용자는 이 레코드의 화폐 값에 적용해야 하는 통화를 지정할 수 있습니다. 이 경우 양식의 통화 필드에 표시되는 현재 기호를 변경합니다.  
  
  개인이 만든 레코드의 기본 통화를 선택하도록 개인 옵션을 변경할 수도 있습니다.
  
- 기본 통화를 기준으로 엔터티와 연결된 선택한 통화의 환율을 제공하는 10진수 필드 **환율**. 양식에 이 필드를 추가하면 사용자는 값을 볼 수 있지만 편집할 수 없습니다. 환율은 통화로 저장됩니다.  
  
추가하는 각 통화 필드에 대해 이름에 `_Base` 접미사가 추가된 다른 통화 필드가 추가됩니다. 이 필드는 추가한 통화 필드의 값 계산과 기본 통화를 저장합니다. 이 필드를 양식에 추가하면 편집할 수 없습니다.  
  
통화 필드를 구성하면 정밀도 값을 선택할 수 있습니다. 다음 표와 같이 3개 옵션이 있습니다.  
  
|옵션|설명|  
|------------|-----------------|  
|가격 산정 소수점 정밀도|**설정** > **관리** > **시스템 설정** > **일반 탭**에서 찾은 가격에 사용되는 단일 조직 정밀도입니다.|  
|통화 정밀도|이 옵션은 레코드의 통화에 정의된 정밀도를 적용합니다.|  
|특정 정밀도 값|이러한 설정은 0과 4 사이의 값을 사용하여 특정한 집합 정밀도를 정의할 수 있도록 합니다.|  
  
<a name="BKMK_DifferentTypesOfLookups"></a> 
  
## <a name="different-types-of-lookups"></a>다른 유형의 조회  

새 조회 필드를 만들 때 작업 중인 엔터티와 조회에 정의된 **대상 레코드 유형** 간에 새 다대일(N:1) 엔터티 관계를 만듭니다. [엔터티 간 관계 만들기 및 편집](create-edit-entity-relationships.md)에서 설명하는 이 관계에 대한 추가 구성 옵션이 있습니다. 하지만 모든 사용자 지정 조회는 단일 대상 레코드 종류의 단일 레코드에 대한 참조만 가능합니다.  
  
하지만 모든 조회 동작이 이런 방식은 아니라는 것을 알고 있어야 합니다. 다음과 같이 다양한 유형의 시스템 조회가 있습니다.  
  
|조회 유형|설명|  
|-----------------|-----------------|  
|**단순 모드**|특정 엔터티에 대한 단일 참조를 허용합니다. 모든 사용자 지정 조회는 유형입니다.|  
|**고객**|거래처 또는 연락처 레코드에 대한 단일 참조를 허용합니다.|  
|**담당자**|팀 또는 사용자 레코드에 대한 단일 참조를 허용합니다. 모든 팀 또는 사용자 담당 엔터티에 이 중 하나를 사용합니다.|  
|**당사자 목록**|여러 엔터티에 대한 여러 참조를 허용합니다. 이러한 조회는 전자 메일 엔터티 **받는 사람** 및 **참조** 필드에서 발견됩니다. 전화 및 약속 엔터티에도 사용됩니다.|  
|**관련 항목**|여러 엔터티에 대한 단일 참조를 허용합니다. 이러한 조회는 작업에 사용되는 관련 항목 필드에서 발견됩니다.|  

<a name="BKMK_ImageFields"></a>

## <a name="image-fields"></a>이미지 필드  

응용 프로그램에서 레코드 당 하나의 이미지를 표시하려면 이미지 필드를 사용합니다. 각 엔터티에는 하나의 이미지 필드를 사용할 수 있습니다. 이미지 필드를 사용자 지정 엔터티에는 추가할 수 있지만 표준 엔터티에는 추가할 수 없습니다. 일부 표준 엔터티에는 정의된 이미지 필드가 있습니다.
  
엔터티에 이미지 필드가 있어도 모델 기반 앱에 해당 이미지를 표시하려면 추가 단계가 필요합니다. 엔터티 정의에서 **기본 이미지** 필드 값은 **[없음]** 또는 **엔터티 이미지**입니다. **엔터티 이미지**를 선택하여 응용 프로그램에 이미지를 표시합니다.  
  
엔터티에 대한 이미지 표시가 활성화되면 이미지가 없는 다른 레코드는 자리 표시자 이미지를 표시합니다. 예를 들면 다음과 같습니다.

![자리 표시자 이미지](../common-data-service/media/lead-entity-form.PNG)
  
사용자는 기본 이미지를 선택하여 컴퓨터에서 사진을 업로드할 수 있습니다. 이미지는 5120KB 미만이어야 하고 다음 형식 중 하나여야 합니다.  
  
- jpg
- jpeg
- gif
- tif
- tiff
- bmp
- png
  
이미지를 업로드하면 .jpg 형식으로 변환되고 다운로드한 이미지도 모두 이 형식을 사용합니다. 애니메이션 .gif를 업로드하면 첫 번째 프레임만 저장됩니다.  
  
이미지를 업로드하면 최대 144x144 픽셀로 크기가 조정됩니다. 사용자는 이 크기를 사용하여 이미지를 잘 표시하도록 업로드하기 전에 크기를 조정하거나 잘라내야 합니다. 모든 이미지는 정사각형으로 잘립니다. 양쪽 모두 144픽셀보다 작은 이미지의 경우 이미지는 작은 쪽 크기에 맞게 정사각형으로 잘립니다.  

이미지 데이터로 작업하는 개발자를 위한 추가 정보:
- [엔터티 메타데이터 > 엔터티 이미지](/powerapps/developer/common-data-service/entity-metadata#entity-images)
- [Dynamics 365 Customer Engagement 개발자 가이드: 이미지 특성](/dynamics365/customer-engagement/developer/image-attributes)
