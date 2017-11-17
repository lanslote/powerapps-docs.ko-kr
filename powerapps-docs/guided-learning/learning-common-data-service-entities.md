---
title: "Common Data Service 엔터티 이해 | Microsoft Docs"
description: "비즈니스 데이터 및 프로세스에 매핑되는 엔터티 정의 및 사용"
services: 
suite: powerapps
documentationcenter: na
author: mgblythe
manager: anneta
editor: 
tags: 
featuredvideoid: JJa6n_YaD-w
courseduration: 8m
ms.service: powerapps
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: mblythe
ms.openlocfilehash: 3239a2c90edcd4274f9fabbbb47bd110c3ebcee6
ms.sourcegitcommit: 43be6a4e08849d522aabb6f767a81c092419babc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2017
---
# <a name="understand-entities"></a>엔터티 이해
이 섹션의 첫 번째 항목에서 일반적인 데이터 모델을 포함하는 Common Data Service에 대해 소개했습니다. 모델에는 엔터티가 순서대로 포함됩니다. 엔터티는 수정, 저장, 검색 및 상호 작용할 수 있는 공유 데이터 청크입니다. 이 항목에서는 엔터티, 필드 및 데이터 형식에 대해 자세히 설명합니다.

## <a name="standard-entities"></a>표준 엔터티
공통 데이터 모델은 다양한 일반 비즈니스 요구 사항을 다루는 일단의 표준 엔터티를 제공합니다. 표준 엔터티 일부는 다음과 같습니다.

![Common Data Service 표준 엔터티](./media/learning-common-data-service-entities/standard-entities.png)

엔터티는 범주로 분류되어 일반적으로 어떤 솔루션이 함께 작동하는지 쉽게 알 수 있습니다.

| 기능 그룹 | 설명 |
| --- | --- |
| 고객 서비스 |고객 서비스 엔터티는 추적, 에스컬레이션 및 문서화를 포함하여 고객의 문제를 관리합니다. |
| 기본 사항 |기본 사항 엔터티는 거의 모든 다른 엔터티 그룹과 관련된 정보를 포함합니다. 이 그룹은 주소, 통화와 같은 엔터티를 포함합니다. |
| 사용자, 조직 및 그룹 |이러한 엔터티에는 직원, 계약자, 기부자, 지원자, 팬, 동문, 가족 등을 포함해 상호 교류가 가능한 다양한 사용자와 조직으로 구성되어 있습니다. |
| 구매 |구매 엔터티로 구매 솔루션을 만들 수 있습니다. |
| 영업 |영업 엔터티를 사용하면 잠재 고객과 기회에 대한 추적에서부터 연락처를 이용한 작업 수행, 주문 접수 및 전달, 송장 발송에 이르는 종단 간 판매 솔루션을 만들 수 있습니다. |

## <a name="fields-and-data-types"></a>필드 및 데이터 형식
각 엔터티에는 변경할 수 없거나 삭제할 수 없는 일단의 기본 필드가 있습니다. **연락처 ID**와 같은 일부 필드는 엔터티와 관련이 있습니다. **만든 날짜/시간**과 같은 다른 항목은 모든 항목에 공통적으로 적용됩니다. 필드를 추가하여 표준 엔터티를 확장할 수 있습니다. 단지 **필드 추가**만 클릭하거나 탭하여 새 필드의 속성을 지정합니다.

![연락처 엔터티 필드 및 데이터 형식](./media/learning-common-data-service-entities/contact-entity-fields.png)

완전히 다른 엔터티가 필요한 경우, 예를 들어 표준 엔터티를 확장하는 것만으로는 충분하지 않을 경우 사용자 지정 엔터티를 만듭니다. 여기에 대해서는 다음 항목에서 설명하겠습니다.

엔터티의 필드에는 각각 숫자와 같은 데이터 형식이 적용됩니다. 일반적인 단일 데이터 형식이 아닌 다른 데이터 형식을 사용하면 앱에서 모든 종류의 멋진 작업을 수행할 수 있으므로 도움이 됩니다. 예를 들어 숫자 형식의 필드가 있으면 해당 필드를 편집할 때 앱에서 슬라이더 컨트롤을 사용할 수 있습니다. 12개 이상의 데이터 형식 중에서 선택할 수 있으며, 다음 목록에서 몇 가지 대표적인 형식을 보여 줍니다.

* 기본 형식: 텍스트 및 숫자
* 복잡한 형식: 전자 메일 및 휴대폰
* 특수 형식: 조회(관계 만들기용) 및 선택 목록(필드에 고정된 값 집합 포함)  

## <a name="working-with-entities"></a>엔터티 작업
엔터티를 열면 많은 정보와 수행할 수 있는 몇 가지 작업이 표시됩니다. 사용할 수 있는 탭과 엔터티 데이터를 관리하기 위해 수행할 수 있는 작업에 대해 간략하게 살펴보겠습니다.

![엔터티 탭](./media/learning-common-data-service-entities/entity-tabs.png)

* **필드**: 앞에서 설명한 모든 필드 및 데이터 형식을 보고 필드를 추가합니다.
* **키**: 엔터티의 각 행을 식별하는 필드입니다(예: 연락처 엔터티의 연락처 ID).
* **관계**: 제품 및 제품 범주와 같은 관련 엔터티 간의 연결입니다. 다음 항목에서 한 예를 살펴보겠습니다.
* **필드 그룹**: PowerApps에서 앱 화면을 만들 때 자동으로 표시할 필드와 같이 다양한 동작을 제어하는 데 사용됩니다.
* **데이터**: 샘플 데이터와 가져온 데이터를 탐색합니다.

![엔터티 작업](./media/learning-common-data-service-entities/entity-actions.png)

* **Excel에서 열기**: PowerApps 추가 기능이 설치되어 있는 경우 이 옵션을 사용하여 Excel에서 데이터를 탐색하고 편집합니다.
* **데이터 가져오기**: Excel 및 CSV 파일에서 데이터를 가져옵니다.
* **데이터 내보내기**: Excel 파일로 데이터를 내보냅니다.
* **템플릿 내보내기**: 엔터티의 구조를 Excel 파일로 내보내 파일을 채우고 엔터티로 다시 가져올 수 있습니다.
* **설정** 및 **삭제**: 표준 엔터티에는 사용할 수 없습니다.

## <a name="connecting-to-a-standard-entity-in-powerapps-studio"></a>PowerApps Studio에서 표준 엔터티에 연결
엔터티에 대해 이해했으므로 PowerApps Studio에서 연락처 엔터티에 연결하는 방법을 살펴보겠습니다. **새로 만들기**를 클릭한 다음 **Common Data Service**에서 **휴대폰 레이아웃**을 클릭합니다. 왼쪽에는 사용할 수 있는 데이터 연결이 표시되고, 오른쪽에는 엔터티 목록이 표시됩니다. 직접 연결을 시도하고 엔터티에서 앱을 생성합니다.

![PowerApps Studio에서 엔터티에 연결](./media/learning-common-data-service-entities/connect-to-standard-entity.png)

다음 항목에서는 엔터티 간의 관계뿐만 아니라 사용자 지정 엔터티를 만드는 방법에 대해서도 살펴보겠습니다.
