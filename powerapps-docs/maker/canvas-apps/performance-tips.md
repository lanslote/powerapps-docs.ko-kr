---
title: 캔버스 앱 성능 최적화 | Microsoft Docs
description: 이 항목의 모범 사례에 따라 PowerApps에서 만든 캔버스 앱의 성능을 향상시킵니다.
author: yingchin
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 08/31/2018
ms.author: yingchin
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 0fa6a8f741ed0e771eeefbbee82a23e876363e55
ms.sourcegitcommit: 469be99b762cd62289a98f058c498ac25ff8801b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44327789"
---
# <a name="optimize-canvas-app-performance-in-powerapps"></a>PowerApps의 캔버스 앱 성능 최적화 | Microsoft Docs
Microsoft는 PowerApps 플랫폼에서 실행되는 모든 앱의 성능 향상을 위해 열심히 노력하고 있습니다. 그러나 이 항목의 모범 사례를 따라 만든 앱의 성능을 향상시킬 수 있습니다.

사용자가 앱을 열면 다음 실행 단계를 거쳐 사용자 인터페이스를 표시합니다. 
1. **사용자 인증** - 이전에 앱을 열지 않은 사용자에게 앱 연결에 필요한 자격 증명을 사용하여 로그인하라는 메시지를 표시합니다. 동일한 사용자가 앱을 다시 열면 조직의 보안 정책에 따라 해당 사용자에게 다시 메시지가 표시될 수 있습니다. 
2. **메타데이터 가져오기** - 앱이 실행되는 PowerApps 플랫폼의 버전 및 데이타를 검색해야 하는 소스와 같은 메타데이터를 검색합니다. 
3. **앱 초기화** - **OnStart** 속성에 지정된 모든 작업을 수행합니다. 
4. **화면 렌더링** - 앱에 데이터로 채워진 컨트롤을 사용하여 첫 번째 화면을 렌더링합니다. 사용자가 다른 화면을 열면 앱은 동일한 프로세스를 사용하여 렌더링합니다.  

## <a name="limit-data-connections"></a>데이터 연결 제한 
**동일한 앱에서 30개를 초과하는 데이터 원본에 연결하지 마세요**. 앱은 새로운 사용자가 각 커넥터에 로그인하도록 유도하므로 모든 추가 커넥터는 앱 시작 시간을 늘립니다. 앱을 실행하면 앱이 해당 소스의 데이터를 요청할 때 각 커넥터는 CPU 리소스, 메모리 및 네트워크 대역폭이 필요합니다. 

앱을 실행하는 동안 [Microsoft Edge](https://docs.microsoft.com/microsoft-edge/devtools-guide/network) 또는 [Google Chrome](https://developers.google.com/web/tools/chrome-devtools/network-performance/)에서 개발자 도구를 사용하도록 설정하여 앱의 성능을 빠르게 측정할 수 있습니다. OneDrive에서 앱, Azure SQL, SharePoint 및 Excel용 Common Data Service와 같은 데이터 원본에서 30개를 초과하는 데이터를 자주 요청하면 앱이 데이터를 반환하는 데 15초보다 오래 걸릴 수 있습니다.  

## <a name="limit-the-number-of-controls"></a>컨트롤 수 제한 
**동일한 앱에 500개를 초과하는 컨트롤을 추가하지 마세요**. PowerApps는 각 컨트롤을 렌더링하는 HTML DOM을 생성합니다. 추가하는 컨트롤이 많을수록 PowerApps에 필요한 생성 시간이 늘어납니다. 

경우에 따라 개별 컨트롤 대신 갤러리를 사용하면 동일한 결과를 얻고 앱을 더 빨리 시작할 수 있습니다. 또한 동일한 화면에서 컨트롤 형식의 수를 줄이는 것이 좋습니다. 일부 컨트롤(예: PDF 뷰어, 데이터 테이블 및 콤보 상자)은 큰 실행 스크립트를 가져오고 렌더링하는 데 오래 걸립니다. 

## <a name="optimize-the-onstart-function"></a>OnStart 함수 최적화
사용자 세션 중에 변경되지 않으면 [**ClearCollect**](functions/function-clear-collect-clearcollect.md) 함수를 사용하여 로컬로 데이터를 캐시합니다. 또한 [**동시**](functions/function-concurrent.md) 함수를 사용하여 데이터 원본을 동시에 로드합니다.

[이 참조 항목](functions/function-concurrent.md)에서 보여 주듯이 **동시** 함수를 사용하면 앱이 데이터를 로드하는 데 필요한 시간을 절반으로 줄일 수 있습니다.

**동시** 함수가 없으면 이 수식은 한 번에 하나씩 4개의 테이블을 로드합니다.

    ClearCollect( Product, '[SalesLT].[Product]' );
    ClearCollect( Customer, '[SalesLT].[Customer]' );
    ClearCollect( SalesOrderDetail, '[SalesLT].[SalesOrderDetail]' );
    ClearCollect( SalesOrderHeader, '[SalesLT].[SalesOrderHeader]' )

브라우저용 개발자 도구에서 이 동작을 확인할 수 있습니다.

![일련의 ClearCollect](./media/performance-tips/perfconcurrent1.png)
    
**동시** 함수에 동일한 수식을 묶어서 작업에 필요한 전체 시간을 줄일 수 있습니다.

    Concurrent( 
        ClearCollect( Product, '[SalesLT].[Product]' );
        ClearCollect( Customer, '[SalesLT].[Customer]' );
        ClearCollect( SalesOrderDetail, '[SalesLT].[SalesOrderDetail]' );
        ClearCollect( SalesOrderHeader, '[SalesLT].[SalesOrderHeader]' ))
        
이렇게 변경하면 앱이 테이블을 병렬로 가져옵니다. 

![병렬 ClearCollect](./media/performance-tips/perfconcurrent2.png)  

## <a name="cache-lookup-data"></a>조회 데이터 캐시
**Set** 함수를 사용하여 소스에서 데이터를 반복적으로 검색하지 않도록 조회 테이블의 데이터를 로컬에 캐시합니다. 이 기술은 세션 중에 데이터가 변경되지 않을 가능성이 있는 경우 성능을 최적화합니다. 이 예에서와 같이 데이터는 소스에서 한 번 검색된 다음, 사용자가 앱을 닫을 때까지 로컬로 참조됩니다. 

    Set(CustomerOrder, Lookup(Order, id = “123-45-6789”));
    Set(CustomerName, CustomerOrder.Name);
    Set(CustomerAddress, CustomerOrder.Address);
    Set(CustomerEmail, CustomerOrder.Email);
    Set(CustomerPhone, CustomerOrder.Phone);

연락처 정보는 자주 변경되지 않으면 기본값과 사용자 정보도 변경되지 않습니다. 따라서 일반적으로 이 기술을 **기본값** 및 **사용자** 함수와 함께 사용할 수도 있습니다. 

## <a name="avoid-controls-dependency-between-screens"></a>화면 간 컨트롤 종속성 방지
컨트롤 값이 다른 화면의 컨트롤 값에 따라 달라지는 경우 변수, 컬렉션 또는 데이터 원본 참조를 사용하여 데이터를 관리합니다.

## <a name="use-global-variables"></a>글로벌 변수 사용
한 화면에서 다른 화면으로 앱 상태를 전달하려면 **탐색** 및 **UpdateContext)** 함수를 사용하는 대신 [**Set**](functions/function-set.md) 함수를 사용하여 글로벌 변수 값을 만들거나 수정합니다.

## <a name="use-delegation"></a>위임 사용
가능한 경우 처리를 위해 데이터를 로컬 장치로 검색하는 대신 데이터 처리를 데이터 원본에 위임하는 함수를 사용합니다. 앱이 로컬로 데이터를 처리해야 하는 경우 작업에 훨씬 더 많은 처리 능력, 메모리 및 네트워크 대역폭이 필요합니다(특히 데이터 집합이 큰 경우).

[이 목록](delegation-list.md)에 표시된 것처럼 서로 다른 데이터 원본은 여러 함수의 위임을 지원합니다.

![위임 사용](./media/performance-tips/perfdelegation1.png)

예를 들어 SharePoint 목록은 [**필터**](functions/function-filter-lookup.md) 함수에서 위임을 지원하지만 [**검색**](functions/function-filter-lookup.md) 함수에서는 지원하지 않습니다. 따라서 SharePoint 목록에 500개를 초과하는 항목이 포함된 경우 갤러리에서 항목을 찾으려면 **검색** 대신 **필터**를 사용해야 합니다. 자세한 팁은 [PowerApps에서 대규모 SharePoint 목록 작업](https://powerapps.microsoft.com/blog/powerapps-now-supports-working-with-more-than-256-items-in-sharepoint-lists/)(블로그 게시물)을 참조하세요. 

## <a name="use-delayed-load"></a>지연된 로드 사용
앱에 10개를 초과하는 화면, 규칙 없음 및 여러 화면에 있고 데이터 원본에 직접 바인딩된 많은 컨트롤이 있는 경우 지연된 로드에 대한 [실험적 기능](working-with-experimental.md)을 사용 설정합니다. 이 유형의 앱을 빌드하고 이 기능을 사용하지 않으면 열려 있지 않은 화면에서도 모든 화면의 컨트롤을 채워야 하므로 앱 성능이 저하될 수 있습니다. 또한 사용자가 레코드를 추가하는 경우와 같이 데이터 원본이 변경될 때마다 앱의 모든 화면을 업데이트해야 합니다.

## <a name="working-with-large-data-sets"></a>큰 데이터 집합 작업
사용자가 필요한 모든 정보에 액세스할 수 있는 반면, 앱의 성능을 유지하려면 위임할 수 있는 데이터 원본과 수식을 사용하고 위임할 수 없는 쿼리에 대한 2000개의 데이터 행 제한을 넘지 마세요. 사용자가 데이터를 검색, 필터링 또는 정렬할 수 있는 레코드 열의 경우 이러한 열의 인덱스는 [SQL Server](https://docs.microsoft.com/sql/relational-databases/sql-server-index-design-guide?view=sql-server-2017) 및 [SharePoint](https://support.office.com/article/Add-an-index-to-a-SharePoint-column-f3f00554-b7dc-44d1-a2ed-d477eac463b0)에 대해 설명한 것처럼 잘 설계되었습니다.  

## <a name="republish-apps-regularly"></a>앱을 정기적으로 다시 게시
[앱을 다시 게시](https://powerapps.microsoft.com/blog/republish-your-apps-to-get-performance-improvements-and-additional-features/)(블로그 게시물)하여 PowerApps 플랫폼에서 성능 향상 및 추가 기능을 가져옵니다.
