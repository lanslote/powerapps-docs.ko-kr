---
title: IsMatch 함수 | Microsoft Docs
description: PowerApps에서 IsMatch 함수에 대한 구문을 포함한 참조 정보
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 02/05/2017
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: f7612b648b3f1f5228fce93054f8732ec47767a8
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2018
ms.locfileid: "42833519"
---
# <a name="ismatch-function-in-powerapps"></a>PowerApps의 IsMatch 함수
텍스트 문자열이 패턴과 일치하는지 여부를 테스트합니다.

## <a name="description"></a>설명
**IsMatch** 함수는 텍스트 문자열이 일반 문자, 미리 정의된 패턴 또는 [정규식](#regular-expressions)을 구성할 수 있는 패턴과 일치하는지 여부를 테스트합니다.  

**IsMatch**를 사용하여 사용자가 **[Text input](../controls/control-text-input.md)** 컨트롤에 입력한 것의 유효성을 검사합니다. 예를 들어, 결과가 데이터 원본에 저장되기 전에 사용자가 유효한 이메일 주소를 입력했는지 여부를 확인할 수 있습니다. 항목이 조건과 일치하지 않는 경우 사용자에게 항목을 수정하도록 하는 다른 컨트롤을 추가합니다.

기본적으로 **IsMatch**는 전체 텍스트 문자열에 대한 대/소문자 구분 일치를 수행합니다. 하나 이상의 [**MatchOptions**](#match-options)를 지정하여 이 동작을 수정할 수 있습니다.

**IsMatch**는 텍스트 문자열이 패턴과 일치하는 경우 *true*를 반환하고 그렇지 않은 경우 *false*를 반환합니다.

## <a name="patterns"></a>패턴
**IsMatch**를 사용하는 핵심은 일치시킬 패턴을 설명하는 것에 있습니다. 다음의 조합으로 텍스트 문자열에서 패턴을 설명합니다.

* **"abc"** 또는 **"123"** 과 같은 일반 문자
* **Letter**, **MultipleDigits** 또는 **Email**과 같은 미리 정의된 패턴 (**Match** 열거는 이러한 패턴을 정의합니다.)
* **"\d+\s+\d+"** 또는 **"[a-z]+"** 와 같은 정규식 코드

[문자열 연결 연산자 **&**](operators.md)를 사용하여 이러한 요소를 결합합니다. 예를 들어, **"abc" & Digit & "\s+"** 는 "a", "b" 및 "c", 그 뒤에 0~9의 숫자, 그 뒤에 최소 하나의 공백 문자가 오는 문자와 일치하는 유효한 패턴입니다.

### <a name="ordinary-characters"></a>일반 문자
가장 간단한 패턴은 정확히 일치되는 일반 문자의 시퀀스입니다.

예를 들어, 문자열 "Hello"는 패턴 **"Hello"** 와 정확하게 일치합니다. 그 이상 그 이하도 아닙니다. 문자열 "hello!" 는 끝에 느낌표가 오고 문자 "h"에 대한 대/소문자가 잘못됐으므로 패턴과 일치하지 않습니다. (이 동작을 수정하는 방법은 [MatchOptions](#match-options)를 참조하세요.)

패턴 언어에서 특정 문자는 특별한 용도로 예약되어 있습니다. 이러한 문자를 사용하려면 문자가 문자 그대로 해석되어야 하거나 미리 정의된 패턴 중 하나를 사용해야 함을 나타내도록 **\\**(백슬래시)로 문자에 접두사를 덧붙입니다. 이 테이블은 특수 문자를 나열합니다.

| 특수 문자 | 설명 |
| --- | --- |
| **.** |점 또는 마침표 |
| **?** |물음표 |
| **&#42;** |별표 |
| **\+** |더하기 |
| **( )** |괄호 |
| **[ ]** |대괄호 |
| **{ }** |중괄호 |
| **^** |캐럿 |
| **$** |달러 기호 |
| **&#124;** |세로 막대 또는 파이프 |
| **\\** |백슬래시 |

예를 들어 "Hello?"를 찾아 볼 수 있습니다. 패턴을 사용 하 여 **"Hello\\?"** 물음표 앞에 백슬래시와.

### <a name="predefined-patterns"></a>미리 정의된 패턴
미리 정의된 패턴은 문자 집합 중 하나 또는 여러 문자의 시퀀스와 일치시키는 간단한 방법을 제공합니다. [문자열 연결 연산자 **&**](operators.md)를 사용하여 **Match** 열거의 구성원과 사용자 고유의 텍스트 문자열을 결합합니다.

| 일치 열거 | 설명 | 정규식 |
| --- | --- | --- |
| **Any** |문자와 일치합니다. |**.** |
| **Comma** |쉼표와 일치합니다. |**,** |
| **Digit** |단일 숫자("0"부터 "9")와 일치합니다. |**\\d** |
| **Email** |"at" 기호("\@")를 포함하는 이메일 주소 및 점(".")을 포함하는 도메인 이름과 일치합니다. |**.+\@.+\\.[^\\.]{2,}** |
| **Hyphen** |하이픈과 일치합니다. |**\\-** |
| **LeftParen** |왼쪽 괄호"("와 일치합니다. |**\\(** |
| **Letter** |문자와 일치합니다. |**\\p{L}** |
| **MultipleDigits** |하나 이상의 숫자와 일치합니다. |**\\d+** |
| **MultipleLetters** |하나 이상의 문자와 일치합니다. |**\\p{L}+** |
| **MultipleNonSpaces** |공백(공백, 탭, 줄 바꿈)을 추가하지 않는 하나 이상의 문자와 일치합니다. |**\\S+** |
| **MultipleSpaces** |공백(공백, 탭, 줄 바꿈)을 추가하는 하나 이상의 문자와 일치합니다. |**\\s+** |
| **NonSpace** |공백을 추가하지 않는 단일 문자와 일치합니다. |**\\S** |
| **OptionalDigits** |0개, 1개 또는 더 많은 숫자와 일치합니다. |**\\d** |
| **OptionalLetters** |0개, 1개 또는 더 많은 문자와 일치합니다. |**\\p{L}** |
| **OptionalNonSpaces** |공백을 추가하지 않는 0개, 1개 또는 더 많은 문자와 일치합니다. |**\\S** |
| **OptionalSpaces** |공백을 추가하는 0개, 1개 또는 더 많은 문자와 일치합니다. |**\\s** |
| **Period** |마침표 또는 점(".")과 일치합니다. |**\\.** |
| **RightParen** |오른쪽 괄호")"와 일치합니다. |**\\)** |
| **Space** |공백을 추가하는 문자와 일치합니다. |**\\s** |

예를 들어, 패턴 **"A" & MultipleDigits**는 하나 이상의 숫자가 뒤에 오는 문자 "A"와 일치합니다.  

### <a name="regular-expressions"></a>정규식
**IsMatch**에서 사용되는 패턴은 *정규식*입니다. 위에서 설명된 일반 문자 및 미리 정의된 패턴은 정규식을 작성하도록 돕습니다.  

정규식은 매우 강력하고 여러 프로그래밍 언어에서 사용할 수 있으며 다양한 목적에 사용됩니다. 이 문서는 정규식의 모든 측면을 설명할 수 없지만 풍부한 정보와 자습서가 사용자를 도울 수 있도록 웹에 게시됩니다.  

정규식에는 서로 다른 방언이 있으며 PowerApps는 다양한 JavaScript 방언을 사용합니다. 자세한 내용은 [정규식 구문](http://msdn.microsoft.com/library/1400241x.aspx)을 참조하세요.

위의 **Match** 열거 테이블에서 각 열거는 정규식으로 확장하고 "정규식" 열에 있는 텍스트 문자열은 해당 식을 정의합니다.

## <a name="match-options"></a>일치 옵션
문자열 연결 연산자(**&amp;**)를 사용하여 결합할 수 있는 하나 이상의 옵션을 지정하여 **IsMatch**의 동작을 수정할 수 있습니다.  

기본적으로 **IsMatch**는 전체 텍스트 문자열의 전체 일치에 대해 테스트합니다.

| MatchOptions 열거 | 설명 | 정규식에 대한 영향 |
| --- | --- | --- |
| **BeginsWith** |패턴은 텍스트의 시작 부분에서 일치해야 합니다. |**^** 를 정규식의 시작 부분에 추가합니다. |
| **Complete** |기본값입니다.  패턴은 처음부터 끝까지 전체 텍스트와 일치해야 합니다. |**^** 를 정규식의 시작 부분에 **$** 를 끝 부분에 추가합니다. |
| **Contains** |패턴은 텍스트의 어딘가에 나타나야 하지만 시작 또는 끝일 필요가 없습니다. |정규식을 수정하지 않습니다. |
| **EndsWith** |패턴은 텍스트의 끝과 일치해야 합니다. |**$** 를 정규식의 끝 부분에 추가합니다. |
| **IgnoreCase** |대/소문자 구분 방식으로 문자의 일치를 처리합니다. 기본적으로 일치는 대/소문자 구분입니다. |정규식을 수정하지 않습니다. |
| **Multiline** |여러 줄과 일치합니다. |정규식을 수정하지 않습니다. |

## <a name="syntax"></a>구문
**IsMatch**( *Text*, *Pattern* [, *Options* ] )

* *Text* – 필수 항목입니다.  테스트할 텍스트 문자열입니다.
* *Pattern* – 필수 항목입니다.  텍스트 문자열로 테스트할 패턴입니다.  **Match** 열거가 정규식을 정의하거나 제공하는 미리 정의된 패턴을 연결합니다.
* *Options* – 선택 사항입니다.  **MatchOptions** 열거 값의 텍스트 문자열 조합입니다.  기본적으로 **MatchOptions.Complete**가 사용됩니다.

## <a name="examples"></a>예
### <a name="ordinary-characters"></a>일반 문자
앱에 **TextInput1**이라는 **Text input** 컨트롤이 포함되어 있다고 가정합니다.  사용자는 데이터베이스에 저장되도록 이 컨트롤에 값을 입력합니다.   

사용자는 **TextInput1**에 **Hello world**를 입력합니다.

| 수식 | 설명 | 결과 |
| --- | --- | --- |
| **IsMatch( TextInput1.Text, "Hello world" )** |사용자의 입력이 문자열 "Hello world"와 정확히 일치하는지 여부를 테스트합니다. |**true** |
| **IsMatch( TextInput1.Text, "Good bye" )** |사용자의 입력이 문자열 "Good bye"와 정확히 일치하는지 여부를 테스트합니다. |**false** |
| **IsMatch( TextInput1.Text, "hello", Contains )** |사용자의 입력이 단어 "hello"(대/소문자 구분)를 포함하는지 여부를 테스트합니다. |**false** |
| **IsMatch( TextInput1.Text, "hello", Contains & IgnoreCase )** |사용자의 입력이 단어 "hello"(대/소문자 구분하지 않음)를 포함하는지 여부를 테스트합니다. |**true** |

### <a name="predefined-patterns"></a>미리 정의된 패턴

|                                                            수식                                                            |                                                                설명                                                                |  결과   |
|-------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|-----------|
| **IsMatch( "123-45-7890", Digit & Digit & Digit & Hyphen & Digit & Digit & Hyphen & Digit & Digit & Digit & Digit & Digit )** |                                              미국 사회 보장 번호와 일치합니다.                                               | **true**  |
|                                           **IsMatch( "joan@contoso.com", Email )**                                            |                                                         이메일 주소와 일치합니다.                                                          | **true**  |
|                              **IsMatch( "123.456", MultipleDigits & Period & OptionalDigits )**                               |                                   숫자, 마침표, 0개 이상의 숫자 시퀀스와 일치합니다.                                   | **true**  |
|                                **IsMatch( "123", MultipleDigits & Period & OptionalDigits )**                                 | 숫자, 마침표, 0개 이상의 숫자 시퀀스와 일치합니다. 마침표가 텍스트에 표시되지 않으므로 이 패턴은 일치하지 않습니다. | **false** |

### <a name="regular-expressions"></a>정규식

|                                                                              수식                                                                              |                                                                                                                                  설명                                                                                                                                   |  결과   |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|
|                                                                    **IsMatch( "986", "\d+" )**                                                                    |                                                                                                                    0보다 큰 정수와 일치합니다.                                                                                                                     | **true**  |
|                                                               **IsMatch( "1.02", "\d+(\.\d\d)?" )**                                                               |                                        양수 통화 금액과 일치합니다. 입력에 소수점이 포함되는 경우 입력은 소수점 뒤에 2개의 숫자도 포함해야 합니다. 예를 들어, 3.00은 유효하지만 3.1은 유효하지 않습니다.                                         | **true**  |
|                                                            **IsMatch( "-4.95", "(-)?\d+(\.\d\d)?" )**                                                             |                                                        양수 또는 음수 통화 금액과 일치합니다. 입력에 소수점이 포함되는 경우 입력은 소수점 뒤에 2개의 숫자도 포함해야 합니다.                                                        | **true**  |
|                                                         **IsMatch( "111-11-1111", "\d{3}-\d{2}-\d{4}" )**                                                         | 미국 사회 보장 번호와 일치합니다.  제공된 입력 필드의 형식, 유형 및 길이의 유효성을 검사합니다. 일치시킬 문자열은 3개의 숫자 뒤에 대시가 오고, 2개의 숫자 뒤에 대시가 온 다음 4개의 숫자로 구성되어야 합니다. | **true**  |
|                                                         **IsMatch( "111-111-111", "\d{3}-\d{2}-\d{4}" )**                                                         |                                                                                               이전 예제와 같지만 하이픈 중 하나가 입력에서 제자리에 있지 않습니다.                                                                                               | **false** |
|                                         **IsMatch( "weakpassword", "(?!^[0-9]\*$)(?!^[a-zA-Z]\*$)([a-zA-Z0-9]{8,10})" )**                                         |                                        8, 9 또는 10자의 문자 및 하나 이상의 숫자와 하나 이상의 영문자를 포함해야 하는 강력한 암호의 유효성을 검사합니다. 문자열은 특수 문자를 포함할 수 없습니다.                                        | **false** |
| **IsMatch( "<http://microsoft.com>", "(ht&#124;f)tp(s?)\:\/\/\[0-9a-zA-Z\]([-.\w]\*[0-9a-zA-Z])\*(:(0-9)\*)\*(\/?)([a-zA-Z0-9\-\.\?\,\'\/\\\+&amp;%\$#_]\*)?" )** |                                                                                                                     http, https 또는 ftp URL의 유효성을 검사합니다.                                                                                                                      | **true**  |

