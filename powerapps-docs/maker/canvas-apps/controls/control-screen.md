---
title: '화면 컨트롤: 참조 | Microsoft Docs'
description: 속성 및 예제를 포함한 화면 컨트롤 관련 정보
author: fikaradz
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 10/25/2016
ms.author: fikaradz
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 15264a783922891a84e805cea211f2945bca3f3e
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2018
ms.locfileid: "42863900"
---
# <a name="screen-control-in-powerapps"></a>PowerApps의 화면 컨트롤
앱에서 하나 이상의 다른 컨트롤을 포함하는 UI 요소입니다.

## <a name="description"></a>설명
대부분의 **[레이블](control-text-box.md)** 컨트롤, **[버튼](control-button.md)** 컨트롤 및 기타 데이터를 표시하고 탐색을 지원하는 컨트롤 등을 포함하는 여러 **화면** 컨트롤이 있습니다.

## <a name="key-properties"></a>주요 속성
**[BackgroundImage](properties-visual.md)** – 화면의 배경에 표시되는 이미지 파일의 이름입니다.

**[Fill](properties-color-border.md)** - 컨트롤의 배경색입니다.

## <a name="additional-properties"></a>추가 속성
**[ImagePosition](properties-visual.md)** – 이미지와 같은 크기가 아닌 경우 컨트롤 또는 화면에 있는 이미지의 위치입니다(**채우기**, **맞춤**, **늘이기**, **타일** 또는 **가운데**).

**OnHidden** – 사용자가 화면에서 나갈 때 앱의 동작입니다.

**OnVisible** – 사용자가 화면으로 들어올 때 앱의 동작입니다.

**OnStart** – 사용자가 앱을 열 때 앱의 동작입니다.

* 이 속성이 설정된 수식은 앱의 첫 화면이 표시되기 전에 실행됩니다. [**Navigate**](../functions/function-navigate.md) 함수를 호출하여 앱을 시작할 때 처음 표시하는 화면을 변경합니다.
* 아직 화면이 표시되지 않았으므로 [**UpdateContext**](../functions/function-updatecontext.md) 함수로 [컨텍스트 변수](../working-with-variables.md)를 설정할 수 없습니다. 그러나 **Navigate** 함수에서 컨텍스트 변수를 전달하고 [**Collect**](../functions/function-clear-collect-clearcollect.md) 함수를 사용하여 [컬렉션](../working-with-variables.md)을 만들고 채울 수 있습니다.
* 앱을 업데이트하면 이 속성을 설정할 수식은 앱이 PowerApps Studio로 로드될 때 실행됩니다. 이 속성 변경의 결과를 확인하려면 앱을 저장하고 종료한 다음 다시 로드해야 합니다.
* **OnStart** 속성은 실제로는 화면이 아닌 앱의 속성입니다. 편집 편의를 위해 이 속성을 앱의 첫 화면에서 속성처럼 보고 수정할 수 있습니다. 첫 화면을 제거하거나 화면 순서를 변경한 경우 이 속성을 찾기 어렵습니다. 이 경우 앱을 저장하고 닫은 다음 다시 로드하면 속성이 첫 화면의 속성으로 다시 표시됩니다.

## <a name="related-functions"></a>관련된 함수
[**Distinct**( *DataSource*, *ColumnName* )](../functions/function-distinct.md)

## <a name="example"></a>예
1. **[라디오](control-radio.md)** 컨트롤을 추가하고 이름을 **ScreenFills**로 지정한 다음, **[Items](properties-core.md)** 속성을 다음 값으로 설정합니다.<br>
   **["Red", "Green"]**
   
    [컨트롤을 추가, 이름을 지정하고, 구성](../add-configure-controls.md)하는 방법을 모르시나요?
2. 기본 **화면** 컨트롤의 이름을 **Source**로 지정한 다음, 다른 **화면** 컨트롤을 추가하고 이름을 **Target**으로 지정합니다.
3. **Source**에서 **[셰이프](control-shapes-icons.md)** 컨트롤(예: 화살표)을 추가하고 **[OnSelect](properties-core.md)** 속성을 다음 수식으로 설정합니다.<br>
   **Navigate(Target, ScreenTransition.Fade)**
   
    **[Navigate](../functions/function-navigate.md)** 함수 또는 [다른 함수](../formula-reference.md)에 대해 더 알고 싶으신가요?
4. **Target**에서 **[셰이프](control-shapes-icons.md)** 컨트롤(예: 화살표)을 추가하고 **[OnSelect](properties-core.md)** 속성을 다음 수식으로 설정합니다.<br>
   **Navigate(Source, ScreenTransition.Fade)**
5. **Target**의 **[Fill](properties-color-border.md)** 속성을 다음 수식으로 설정합니다.<br>
   **If("Red" in ScreenFills.Selected.Value, RGBA(255, 0, 0, 1), RGBA(54, 176, 75, 1))**
6. **Source**에서 F5 키를 누르고 **[라디오](control-radio.md)** 컨트롤의 옵션을 하나 클릭하거나 탭한 다음, **[셰이프](control-shapes-icons.md)** 컨트롤을 클릭하거나 탭합니다.
   
    **Target**이 선택한 색으로 나타납니다.
7. **Target**에서 **[셰이프](control-shapes-icons.md)** 컨트롤을 클릭하거나 탭하여 **Source**로 돌아갑니다.
8. (선택 사항) **[라디오](control-radio.md)** 컨트롤의 다른 옵션을 클릭하거나 탭한 다음 **[세이프](control-shapes-icons.md)** 컨트롤을 클릭하거나 탭하여 다른 색으로 **Target**이 표시되는지 확인합니다.
9. 기본 작업 영역으로 돌아가려면 Esc 키를 누릅니다.


## <a name="accessibility-guidelines"></a>접근성 지침
### <a name="color-contrast"></a>색 대비
**화면**이 텍스트의 효과적인 배경인 경우 다음 사이에 적절한 색 대비가 있어야 합니다.
* **[채우기](properties-color-border.md)** 및 텍스트
* **[BackgroundImage](properties-visual.md)** 및 텍스트(해당하는 경우)

예를 들어 **화면**에 **[레이블](control-text-box.md)** 이 포함되어 있고 레이블에 투명한 채우기가 있는 경우 화면의 **[채우기](properties-color-border.md)** 는 효과적으로 레이블의 배경색이 됩니다.

텍스트 외에도 **[평가](control-rating.md)** 컨트롤의 별표 이미지 같은 필수 그래픽 개체에 대한 색 대비를 확인하는 것이 좋습니다.

### <a name="screen-reader-support"></a>화면 판독기 지원
* 각 **화면**에 대한 의미 있는 이름이 있어야 합니다. [컨트롤] 창의 트리 뷰 또는 [속성] 창의 헤더에서 다른 컨트롤과 동일한 방법으로 화면 이름을 보고 편집할 수 있습니다.

    > [!NOTE]
  > 새 **화면**이 로드되면 화면 읽기 프로그램이 해당 이름을 알립니다. 
