---
title: PowerShell 지원(미리 보기) | Microsoft Docs
description: 다양한 PowerShell cmdlet에 대한 설명 및 cmdlet을 설치 및 실행하는 방법에 대한 연습
author: jamesol-msft
manager: kvivek
ms.service: powerapps
ms.component: pa-admin
ms.topic: reference
ms.date: 08/23/2018
ms.author: jamesol
search.audienceType:
- admin
search.app:
- D365CE
- PowerApps
- Powerplatform
ms.openlocfilehash: 0d5d2cee770e03c4e587db0bff624f34395ed92c
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2018
ms.locfileid: "42864431"
---
# <a name="powershell-support-for-powerapps-preview"></a>PowerApps에 대한 PowerShell 지원(미리 보기)
최근에 앱 작성자 및 관리자용 PowerShell cmdlet 미리 보기가 제공되면서 [PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) 또는 [PowerApps 관리 센터](https://admin.powerapps.com)에서 현재는 수동으로만 가능한 다양한 모니터링 및 관리 작업을 자동화할 수 있습니다.

## <a name="installation"></a>설치
앱 작성자용 PowerShell cmdlet을 실행하려면 다음을 수행합니다.

1. [PowerShell 스크립트 파일](https://go.microsoft.com/fwlink/?linkid=2006349)을 다운로드합니다.

2. 폴더에 파일의 압축을 풉니다.

3. 같은 폴더에서 관리자 권한으로 PowerShell 명령 창을 엽니다.

4. 다음 일회성 PowerShell 명령을 실행합니다(이는 현재 컴퓨터에서 PowerShell 명령을 실행한 적이 없다고 가정함).

    ```
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Force
    ```

5. 다음 명령을 사용하여 필요한 모듈을 가져옵니다.

    ```
    Import-Module .\Microsoft.PowerApps.Administration.PowerShell.psm1 -Force
    Import-Module .\Microsoft.PowerApps.PowerShell.psm1 -Force
    ```

6.  현재 다음 명령을 사용하여 PowerShell 파일을 수동으로 차단 해제해야 할 수 있는 [알려진 문제](https://powerusers.microsoft.com/t5/Administering-PowerApps/Getting-errors-when-I-try-to-import-the-preview-powerapps/td-p/109036)가 있습니다.

    ```
    dir . | Unblock-File
    ```
7. 명령에 액세스하기 전에 다음 명령을 사용하여 자격 증명을 제공합니다. cmdlet을 계속 사용하기 위해 다시 로그인하기 전에 이러한 자격 증명을 새로 고치는 데는 최대 8시간이 걸립니다.

    ```
    # This call will open a prompt to collect the credentials (AAD account & password) that will be used by the commands
    Add-PowerAppsAccount
    ```

    ```
    # Here is how you can pass in credentials (avoiding opening a prompt)
    $pass = ConvertTo-SecureString "password" -AsPlainText -Force
    Add-PowerAppsAccount -Username foo@bar.com -Password $pass
    ```


## <a name="powerapps-cmdlets-for-app-creators-preview"></a>앱 작성자용 PowerApps cmdlet(미리 보기)

### <a name="prerequisite"></a>필수 조건
유효한 PowerApps 라이선스를 보유한 사용자는 이러한 cmdlet으로 작업을 수행할 수 있지만, 이러한 사용자는 함께 만들거나 자신과 공유된 리소스(예: 앱, 흐름 등)에만 액세스할 수 있습니다.

### <a name="cmdlet-list"></a>Cmdlet 목록
> [!NOTE]
> 충돌을 방지하기 위해 적절한 접두사를 추가하기 위해 최신 릴리스의 일부 cmdlet 함수 이름을 업데이트했습니다. 변경된 사항에 대한 개요는 아래 표를 참조하세요.

| 용도 | Cmdlet |
| --- | --- |
| 환경 읽기 | Get-PowerAppEnvironment *(이전의 Get-PowerAppsEnvironment)* <br> Get-FlowEnvironment
| 캔버스 앱 읽기, 업데이트 및 삭제 | Get-PowerApp *(이전의 Get-App)* <br> Remove-PowerApp *(이전의 Remove-App)* <br> Publish-PowerApp *(이전의 Publish-App)* <br> Set-AppDisplayName *(이전의 Set-PowerAppDisplayName)*<br> Get-PowerAppVersion *(이전의 Get-AppVersion)* <br> Restore-PowerAppVersion *(이전의 Restore-AppVersion)*
| 캔버스 앱 권한 읽기, 업데이트 및 삭제 | Get-PowerAppRoleAssignment *(이전의 Get-AppRoleAssignment)* <br> Set-PowerAppRoleAssignment *(이전의 Set-AppRoleAssignment)* <br> Remove-PowerAppRoleAssignment *(이전의previously Remove-AppRoleAssignment)*
| 흐름 읽기, 업데이트 및 삭제 | Get-Flow <br> Get-FlowRun <br> Enable-Flow <br> Disable-Flow <br> Remove-Flow
| 흐름 권한 읽기, 업데이트 및 삭제 | Get-FlowOwnerRole <br> Set-FlowOwnerRole <br> Remove-FlowOwnerRole
| 흐름 승인 읽기 및 응답 | Get-FlowApprovalRequest <br> Get-FlowApproval <br> RespondTo-FlowApprovalRequest
| 연결 읽기 및 삭제 | Get-PowerAppConnection *(이전의 Get-Connection)* <br> Remove-PowerAppConnection *(이전의 Remove-Connection)*
| 연결 권한 읽기, 업데이트 및 삭제 | Get-PowerAppConnectionRoleAssignment *(이전의 Get-ConnectionRoleAssignment)* <br> Set-PowerAppConnectionRoleAssignment *(이전의 Set-ConnectionRoleAssignment)* <br> Remove-PowerAppConnectionRoleAssignment *(이전의 Remove-ConnectionRoleAssignment)*
| 커넥터 읽기 및 삭제 | Get-PowerAppConnector *(이전의 Get-Connector)* <br> Remove-PowerAppConnector *(이전의 Remove-Connector)*
| 사용자 지정 커넥터 권한 읽기, 업데이트 및 삭제 | Get-PowerAppConnectorRoleAssignment *(이전의 Get-ConnectorRoleAssignment)* <br> Set-PowerAppConnectorRoleAssignment *(이전의 Set-ConnectorRoleAssignment)* <br> Remove-PowerAppConnectorRoleAssignment *(이전의 Remove-ConnectorRoleAssignment)*


> [!NOTE]
> 다음 명령을 사용하여 각 cmdlet에 대한 구문을 이해하고 샘플을 봅니다.
>```
>Get-Help Get-PowerAppEnvironment
>Get-Help Get-PowerAppEnvironment -Examples
>Get-Help Get-PowerAppEnvironment -Detailed
>```

## <a name="powerapps-cmdlets-for-administrators-preview"></a>관리자용 PowerApps cmdlet(미리 보기)

### <a name="prerequisite"></a>필수 조건
관리자 cmdlet에서 관리 작업을 수행하려면 다음이 필요합니다.

* 유료 PowerApps 요금제 2 라이선스 또는 PowerApps 요금제 2 평가판 라이선스. [http://web.powerapps.com/trial](http://web.powerapps.com/trial)에서 30일 평가판 라이선스를 등록할 수 있습니다. 평가판 라이선스가 만료된 경우 갱신할 수 있습니다.

* 다른 사용자의 리소스를 검색해야 하는 경우 [Office 365 전역 관리자](https://support.office.com/article/assign-admin-roles-in-office-365-for-business-eac4d046-1afd-4f1a-85fc-8219c79e1504) 또는 [Azure Active Directory 전역 관리자](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) 권한. (환경 관리자는 권한이 있는 환경 및 환경 리소스에만 액세스할 수 있습니다.)

### <a name="cmdlet-list"></a>Cmdlet 목록
> [!NOTE]
> 충돌을 방지하기 위해 적절한 접두사를 추가하기 위해 최신 릴리스의 일부 cmdlet 함수 이름을 업데이트했습니다. 변경된 사항에 대한 개요는 아래 표를 참조하세요.

| 용도 | Cmdlet
| --- | ---
| 앱 데이터베이스용 환경 및 Common Data Service 읽기, 업데이트 및 삭제 | New-AdminPowerAppEnvironment **\*신규\*** <br> Set-AdminPowerAppEnvironmentDisplayName **\*신규\*** <br> Get-AdminPowerAppEnvironment *(이전의 Get-AdminEnvironment)* <br> Remove-AdminPowerAppEnvironment *(이전의 Remove-AdminEnvironment)* <br> New-AdminPowerAppCdsDatabase **\*신규\*** <br> Get-AdminPowerAppCdsDatabaseLanguages **\*신규\*** <br> Get-AdminPowerAppCdsDatabaseCurrencies **\*신규\*** <br> Get-AdminPowerAppEnvironmentLocations **\*신규\***
| 환경 읽기, 업데이트 및 삭제 권한 <br><br> *이러한 cmdlet은 현재 앱용 CDS(Common Data Service) 데이터베이스가 없는 환경에서만 작동합니다.* | Get-AdminPowerAppEnvironmentRoleAssignment *(이전의 Get-adminenvironmentroleassignment)* <br> Set-AdminPowerAppEnvironmentRoleAssignment *(이전의 Set-AdminEnvironmentRoleAssignment)* <br> Remove-AdminPowerAppEnvironmentRoleAssignment *(이전의 Remove-AdminEnvironmentRoleAssignment)*
| 캔버스 앱 읽기, 업데이트 및 제거 | Get-AdminPowerApp *(이전의 Get-AdminApp)* <br> Remove-AdminPowerApp *(이전의 Remove-AdminApp)* <br> Get-AdminPowerAppConnectionReferences **\*신규\*** <br> Set-AdminPowerAppAsFeatured **\*신규\*** <br> Clear-AdminPowerAppAsFeatured **\*신규\*** <br> Set-AdminPowerAppAsHero **\*신규\*** <br> Clear-AdminPowerAppAsHero **\*신규\*** <br> Set-AdminPowerAppApisToBypassConsent **\*신규\*** <br> Clear-AdminPowerAppApisToBypassConsent **\*신규\***
| 캔버스 앱 권한 읽기, 업데이트 및 삭제 | Get-AdminPowerAppRoleAssignment *(이전의 Get-AdminAppRoleAssignment)* <br> Remove-AdminPowerAppRoleAssignment *(이전의 Remove-AdminAppRoleAssignment)* <br> Set-AdminPowerAppRoleAssignment *(이전의 Set-AdminAppRoleAssignment)* <br> Set-AdminPowerAppOwner *(이전의 Set-AdminAppOwner)*
| 흐름 읽기, 업데이트 및 삭제 | Get-AdminFlow <br> Enable-AdminFlow <br> Disable-AdminFlow <br> Remove-AdminFlow <br> Remove-AdminFlowApprovals **\*신규\***
| 흐름 권한 읽기, 업데이트 및 삭제 | Get-AdminFlowOwnerRole <br> Set-AdminFlowOwnerRole <br> Remove-AdminFlowOwnerRole
| 연결 읽기 및 삭제 | Get-AdminPowerAppConnection *(이전의 Get-AdminConnection)* <br> Remove-AdminPowerAppConnection *(이전의 Remove-AdminConnection)*
| 연결 권한 읽기, 업데이트 및 삭제 | Get-AdminPowerAppConnectionRoleAssignment *(이전의 Get-AdminConnectionRoleAssignment)* <br> Set-AdminPowerAppEnvironmentConnectionRoleAssignment *(이전의 Set-AdminConnectionRoleAssignment)* <br> Remove-AdminPowerAppConnectionRoleAssignment *(이전의 Remove-AdminConnectionRoleAssignment)*
| 사용자 지정 커넥터 읽기 및 삭제 | Get-AdminPowerAppConnector *(이전의 Get-AdminConnector)* <br> Remove-AdminPowerAppConnector *(이전의 Remove-AdminConnector)*
| 사용자 지정 커넥터 권한 읽기, 업데이트 및 삭제 | Get-AdminPowerAppConnectorRoleAssignment *(이전의 Get-AdminConnectorRoleAssignment)*<br> Set-AdminPowerAppConnectorRoleAssignment *(이전의 Set-AdminConnectorRoleAssignment)* <br> Remove-AdminPowerAppConnectorRoleAssignment *(이전의 Remove-AdminConnectorRoleAssignment)*
| 사용자의 PowerApps 사용자 설정, 사용자 앱 설정 및 알림 읽기 | Get-AdminPowerAppsUserDetails
| 사용자에게 표시되지 않는 사용자의 Microsoft 흐름 설정을 읽고 삭제하지만 흐름 실행을 지원합니다. | Get-AdminFlowUserDetails <br> Remove-AdminFlowUserDetails
| 조직에 대한 데이터 손실 방지 정책 만들기, 읽기, 업데이트 및 삭제 | Get-AdminDlpPolicy *(이전의 Get-AdminApiPolicy)* <br> Add-AdminDlpPolicy *(이전의 Add-AdminApiPolicy)* <br> Remove-AdminDlpPolicy *(이전의 Remove-AdminApiPolicy)* <br> Set-AdminDlpPolicy *(이전의 Set-AdminApiPolicy)* <br> Add-ConnectorToBusinessDataGroup <br>  Remove-ConnectorFromBusinessDataGroup

> [!NOTE]
> 다음 명령을 사용하여 각 cmdlet에 대한 구문을 이해하고 샘플을 봅니다.
>```
>Get-Help Get-AdminPowerAppEnvironment
>Get-Help Get-AdminPowerAppEnvironment -Examples
>Get-Help Get-AdminPowerAppEnvironment -Detailed
>```

## <a name="version-history"></a>버전 기록
| 버전 | 날짜 | 업데이트 |
| --- | --- | --- |
| 1.0 | 04/23/2018 | <ol> <li> 환경, 앱, 흐름, 흐름 승인, 연결 및 사용자 지정 커넥터에 대한 관리 cmdlet을 포함하여 앱 작성자를 위한 PowerApps cmdlet의 초기 시작(미리 보기) </li> <li> 환경, 앱 및 흐름에 대한 관리 cmdlet을 포함하여 관리자를 위한 PowerApps cmdlet의 초기 시작(미리 보기) </li></ol>|
| 2.0 | 05/24/2018 | <ol> <li> 앱 작성자 및 관리자용 cmdlet의 사소한 버그 수정 </li> <li> 다음과 같은 새로운 관리 cmdlet을 추가했습니다. <br> Get-AdminConnection <br> Remove-AdminConnection <br> Get-AdminConnectionRoleAssignment <br> Set-AdminConnectionRoleAssignment <br>Remove-AdminConnectionRoleAssignment <br>Get-AdminConnector  <br>Remove-AdminConnector <br>Set-AdminConnectorRoleAssignment  <br>Get-AdminConnectorRoleAssignment  <br>Remove-AdminConnectorRoleAssignment <br>Get-AdminPowerAppsUserDetails <br>Get-AdminFlowUserDetails <br>Remove-AdminFlowUserDetails <br>Get-AdminApiPolicy  <br>Add-AdminApiPolicy <br>Remove-AdminApiPolicy <br>Set-AdminApiPolicy <br>Add-ConnectorToBusinessDataGroup  <br>Remove-ConnectorFromBusinessDataGroup </li> </ol>
| 3.0 | 07/30/2018 | <ol> <li> Add-PowerAppsAccount에 자격 증명을 전달하는 기능 추가(반복 스크립팅을 사용 가능) </li> <li>  앱 작성자 및 관리자용 cmdlet의 사소한 버그 수정 </li> <li> 앱 작성자를 위한 각 cmdlet에 "PowerApp" 또는 "흐름" 접두사 추가 </li> <li>  앱 작성자를 위한 각 cmdlet에 "AdminPowerApp" 또는 "AdminFlow" 접두사 추가 </li> <li> 다음과 같은 새로운 관리 cmdlet을 추가했습니다. <br> New-AdminPowerAppEnvironment <br> Set-AdminPowerAppEnvironmentDisplayName <br> New-AdminPowerAppCdsDatabase <br> Get-AdminPowerAppCdsDatabaseLanguages <br> Get-AdminPowerAppCdsDatabaseCurrencies <br> Get-AdminPowerAppEnvironmentLocations <br> Get-AdminPowerAppConnectionReferences <br> Set-AdminPowerAppAsFeatured <br> Clear-AdminPowerAppAsFeatured <br> Set-AdminPowerAppAsHero <br> Clear-AdminPowerAppAsHero <br> Set-AdminPowerAppApisToBypassConsent <br> Clear-AdminPowerAppApisToBypassConsent <br> Remove-AdminFlowApprovals </li></ol>
| 4.0 | 08/15/2018 | 함수가 동기화되도록 New-AdminPowerAppCdsDatabase에 선택적 매개 변수 추가(예: 데이터베이스가 성공적으로 프로비저닝될 때까지 반환되지 않음)
| 5.0 | 08/24/2018 | 보안 설정에 따라 일부 데이터를 반환하지 않는 흐름 관리자 cdmlet 문제 해결

## <a name="questions"></a>질문

의견, 제안 또는 질문이 있는 경우 [PowerApps 커뮤니티 게시판 관리](https://powerusers.microsoft.com/t5/Administering-PowerApps/bd-p/Admin_PowerApps)에 게시해 주세요.
