---
title: Shuffle 함수 | Microsoft Docs
description: PowerApps의 Shuffle 함수에 대한 구문과 예제를 포함한 참조 정보
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 11/07/2015
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 3fd93ce6cf9703e9e9fbf69c5826213d9aa78e02
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2018
ms.locfileid: "42863571"
---
# <a name="shuffle-function-in-powerapps"></a>PowerApps의 Shuffle 함수
[테이블](../working-with-tables.md)의 [레코드](../working-with-tables.md#records)를 무작위로 다시 정렬합니다.

## <a name="description"></a>설명
**Shuffle** 함수는 테이블의 레코드 다시 정렬합니다.

**Shuffle**은 인수와 동일한 [열](../working-with-tables.md#columns) 및 동일한 수의 행을 갖는 테이블을 반환합니다.

## <a name="syntax"></a>구문
**Shuffle**( *Table* )

* *Table* - 필수 항목입니다.  순서를 섞을 테이블입니다.

## <a name="example"></a>예
카드 놀이에 대한 세부 정보를 **Deck**라는 [컬렉션](../working-with-data-sources.md#collections)에 저장한 경우, 아래 수식은 무작위로 섞은 컬렉션의 복사본을 반환합니다.

**Shuffle(Deck)**

