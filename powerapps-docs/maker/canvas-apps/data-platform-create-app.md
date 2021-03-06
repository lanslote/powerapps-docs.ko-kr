---
title: 앱용 Common Data Service에서 캔버스 앱 생성 | Microsoft Docs
description: PowerApps에서 자동으로 캔버스 앱을 생성하여 앱용 Common Data Service의 데이터 관리
author: AFTOwen
manager: kvivek
ms.service: powerapps
ms.topic: quickstart
ms.custom: canvas
ms.reviewer: ''
ms.date: 05/06/2018
ms.author: anneta
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: c8b24c9064e5012ff1ddb15d13dc338ed9565bef
ms.sourcegitcommit: 02d0234bd84352bf1c43d0fc9225ab60947a0add
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2018
ms.locfileid: "49316772"
---
# <a name="generate-a-canvas-app-from-common-data-service-for-apps-in-powerapps"></a>PowerApps의 앱용 Common Data Service에서 캔버스 앱 생성

PowerApps에서 [앱용 CDS(Common Data Service)](../common-data-service/data-platform-intro.md)의 샘플 계정 목록에 따라 캔버스 앱을 자동으로 생성합니다. 이 앱에서는 모든 계정을 찾아보고, 단일 계정의 세부 정보를 표시하며, 계정을 생성, 업데이트 또는 삭제할 수 있습니다.

PowerApps에 등록하지 않은 경우 시작하기 전에 [체험판으로 등록합니다](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc).

## <a name="prerequisites"></a>필수 조건

이 빠른 시작을 수행하려면 앱용 CDS의 데이터베이스가 만들어졌고 데이터가 포함되고 업데이트가 허용되는 [환경](working-with-environments.md)으로 전환해야 합니다. 이러한 환경이 없고 관리자 권한이 있으면 이 요구 사항을 충족하는 [환경을 만들 수 있습니다](../../administrator/environments-administration.md#create-an-environment).

## <a name="generate-an-app"></a>앱 생성

1. [PowerApps](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)에 로그인하고 필요한 경우 이 항목의 앞부분에 지정된 대로 환경을 전환합니다.

1. **고유한 앱 만들기** 아래에서 **데이터로 시작**을 마우스로 가리킨 다음, **이 앱 만들기**를 선택합니다.

    ![앱 만들기 옵션](./media/data-platform-create-app/start-from-data.png)

1. **Common Data Service** 타일에서 **휴대폰 레이아웃**을 선택합니다.

    ![연결 타일](./media/data-platform-create-app/connection-tile.png)

1. **테이블 선택**에서 **계정**을 선택한 다음, **연결**을 선택합니다.

1. **PowerApps Studio 시작** 대화 상자에서 **건너뛰기**를 선택합니다.

앱이 찾아보기 화면에 열리고 계정 목록이 갤러리라는 컨트롤에 표시됩니다. 화면 위쪽에 있는 제목 표시줄에는 갤러리의 데이터 새로 고침, 갤러리의 데이터를 사전순으로 정렬 및 갤러리에 데이터 추가에 대한 아이콘이 표시됩니다. 제목 표시줄 아래의 검색 상자에서 입력하거나 붙여넣을 텍스트를 기준으로 갤러리의 데이터를 필터링하는 옵션을 제공합니다. 

기본적으로 갤러리에는 이메일 주소, 도시 및 계정 이름이 표시됩니다. [다음 단계](data-platform-create-app.md#next-steps)에서 볼 수 있듯이, 데이터의 표시 방법을 변경하거나 다른 데이터 유형을 표시하도록 갤러리를 사용자 지정할 수 있습니다.

![찾아보기 화면](./media/data-platform-create-app/browse-screen.png)

## <a name="save-the-app"></a>앱 저장
이 앱을 사용하거나 다른 사용자와 공유하기 전에 더 많은 변경 작업을 수행하려고 할 것입니다. 가장 좋은 방법은 진행하기 전에 지금까지의 작업을 저장하는 것입니다.

1. 왼쪽 위 모서리 근처에서 **파일** 탭을 선택합니다.

1. **앱 설정** 페이지에서 앱 이름을 **AppGen**으로 설정하고, 배경색을 진한 빨간색으로, 아이콘을 확인 표시로 변경합니다.

    ![앱 설정 페이지](./media/data-platform-create-app/app-settings.png)

1. 왼쪽 가장자리 근처에서 **저장**을 선택한 다음, 왼쪽 아래 모서리에서 **저장**을 선택합니다.

## <a name="next-steps"></a>다음 단계
이 빠른 시작에서 앱용 CDS의 계정에 대한 샘플 데이터를 관리하는 앱을 만들었습니다. 다음 단계에서는 사용자의 요구 사항에 맞게 기본 찾아보기 화면의 갤러리 및 다른 요소를 사용자 지정합니다.

> [!div class="nextstepaction"]
> [갤러리를 사용자 지정](customize-layout-sharepoint.md)합니다.
