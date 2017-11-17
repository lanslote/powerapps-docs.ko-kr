---
title: "Distinct 함수 | Microsoft Docs"
description: "PowerApps의 Distinct 함수에 대한 구문과 예제를 포함한 참조 정보"
services: 
suite: powerapps
documentationcenter: na
author: gregli-msft
manager: anneta
editor: 
tags: 
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/07/2015
ms.author: gregli
ms.openlocfilehash: 2e114671869659c598c81f6069b668449b783f65
ms.sourcegitcommit: 43be6a4e08849d522aabb6f767a81c092419babc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2017
---
# <a name="distinct-function-in-powerapps"></a>PowerApps의 Distinct 함수
[테이블](../working-with-tables.md)의 [레코드](../working-with-tables.md#records)를 요약하여 중복을 제거합니다.

## <a name="description"></a>설명
**Distinct** 함수는 테이블의 각 레코드에서 수식을 계산합니다. **Distinct**는 중복 값이 제거된 결과를 포함하는 단일 열 테이블을 반환합니다.  

[!INCLUDE [record-scope](../../includes/record-scope.md)]

## <a name="syntax"></a>구문
**Distinct**( *Table*, *Formula* )

* *Table* - 필수 항목입니다.  계산 대상 테이블입니다.
* *Formula* - 필수 항목입니다.  각 레코드에 대해 계산할 수식입니다.

## <a name="example"></a>예
**Department** 열이 포함된 **Employees** 테이블이 있는 경우, 이 함수는 각 열에 이름이 나타나는 횟수와 상관없이 열에 있는 고유한 부서 이름을 나열합니다.

**Distinct(Employees, Department)**
