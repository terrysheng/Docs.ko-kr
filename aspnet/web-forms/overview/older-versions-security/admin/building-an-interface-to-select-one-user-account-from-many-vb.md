---
uid: web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-vb
title: "많은 (VB)에서 사용자 계정 하나를 선택 하려면 인터페이스를 작성 | Microsoft Docs"
author: rick-anderson
description: "이 자습서에서는 페이징, filterable 그리드와 사용자 인터페이스를 작성 합니다. 특히 사용자 인터페이스를 일련의 링크에 대 한 단추가 이루어져 있습니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/01/2008
ms.topic: article
ms.assetid: da53380c-a16b-41c7-a20d-24343c735c52
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-vb
msc.type: authoredcontent
ms.openlocfilehash: f0339578291c536a474f1c7314b28668a6519c8c
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="building-an-interface-to-select-one-user-account-from-many-vb"></a>많은 (VB)에서 사용자 계정 하나를 선택 하는 인터페이스를 작성 합니다.
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/VB.12.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial12_SelectUser_vb.pdf)

> 이 자습서에서는 페이징, filterable 그리드와 사용자 인터페이스를 작성 합니다. 특히 사용자 인터페이스 이름과 일치 하는 사용자를 표시 하는 GridView 컨트롤의 시작 문자에 따라 결과 필터링 하기 위한 일련의 링크 단추가 구성 됩니다. GridView에서 사용자 계정을 모두 나열 하 여 시작 합니다. 그런 다음 3 단계에서에서 필터 링크 단추가 추가 합니다. 4 단계에서 필터링 된 결과 페이징 살펴봅니다. -4 단계 2에서 생성 된 인터페이스는 특정 사용자 계정에 대 한 관리 작업 수행은 이후 자습서에서 사용 됩니다.


## <a name="introduction"></a>소개

에 <a id="_msoanchor_1"> </a> [ *사용자에 게 역할 할당* ](../roles/assigning-roles-to-users-vb.md) 관리자 사용자를 선택 하 고 자신의 역할을 관리 하는 기본적인 인터페이스 만든 자습서입니다. 특히, 인터페이스의 모든 사용자의 드롭 다운 목록으로 관리자를 표시 합니다. 이러한 인터페이스는이 있지만 개 정도의 사용자, 계정도 지원 하지만 수백 또는 수천 개의 계정이 사이트에 대 한 하기 어렵고 적합 합니다. 페이징, 필터링 할 표는 대형 사용자 기반이 웹 사이트에 대 한 더 적합 한 사용자 인터페이스입니다.

이 자습서에서는 사용자 인터페이스를 작성 합니다. 특히 사용자 인터페이스 이름과 일치 하는 사용자를 표시 하는 GridView 컨트롤의 시작 문자에 따라 결과 필터링 하기 위한 일련의 링크 단추가 구성 됩니다. GridView에서 사용자 계정을 모두 나열 하 여 시작 합니다. 그런 다음 3 단계에서에서 필터 링크 단추가 추가 합니다. 4 단계에서 필터링 된 결과 페이징 살펴봅니다. -4 단계 2에서 생성 된 인터페이스는 특정 사용자 계정에 대 한 관리 작업 수행은 이후 자습서에서 사용 됩니다.

이제 시작 하겠습니다.

## <a name="step-1-adding-new-aspnet-pages"></a>1 단계: 새 ASP.NET 페이지를 추가합니다.

이 자습서에는 다음 두 우리는 수 다양 한 관리 관련 기능 및 검사 기능입니다. 일련의 전체이 자습서에서 설명 하는 항목을 구현 하는 ASP.NET 페이지가 필요 합니다. 이러한 페이지를 만들고 사이트 맵 업데이트 하겠습니다.

시작 이라는 프로젝트에 새 폴더를 만들어서 `Administration`합니다. 다음에 있는 각 페이지에 연결 하 고 폴더를 두 개의 새 ASP.NET 페이지 추가 `Site.master` 마스터 페이지입니다. 페이지 이름을 지정 합니다.

- `ManageUsers.aspx`
- `UserInformation.aspx`

두 페이지 웹 사이트의 루트 디렉터리를 추가할 수도: `ChangePassword.aspx` 및 `RecoverPassword.aspx`합니다.

이러한 네 개의 페이지,이 시점에서 있어야 마스터 페이지의 contentplaceholders의 마다 하나씩 두 개의 콘텐츠 컨트롤: `MainContent` 및 `LoginContent`합니다.

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample1.aspx)]

에 대 한 마스터 페이지의 기본 태그를 표시 하려고는 `LoginContent` ContentPlaceHolder 이러한 페이지에 대 한 합니다. 따라서 태그에 대 한 선언적 태그를 제거는 `Content2` 콘텐츠 컨트롤을 합니다. 이렇게 한 다음 페이지의 태그에 콘텐츠 컨트롤을 한 개만 있어야 합니다.

ASP.NET 페이지에 `Administration` 폴더 관리 권한이 있는 사용자 용 으로만 사용 됩니다. 관리자 역할에 시스템에 추가한는 <a id="_msoanchor_2"> </a> [ *만들기 및 역할 관리* ](../roles/creating-and-managing-roles-vb.md) 자습서;이 역할에 이러한 두 페이지에 대 한 액세스를 제한 합니다. 이를 위해 추가 `Web.config` 파일을 `Administration` 폴더 구성 및 해당 `<authorization>` 관리자 역할의 사용자가 인정 하 고 다른 모든 사용자를 거부 하는 요소입니다.

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample2.xml)]

이 시점에서 프로젝트의 솔루션 탐색기에 스크린 샷을 그림 1에 표시 된 비슷해야 합니다.


[![웹 사이트에 추가 된 4 개의 새 페이지 및 Web.config 파일](building-an-interface-to-select-one-user-account-from-many-vb/_static/image2.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image1.png)

**그림 1**: 4 개의 새 페이지와 `Web.config` 웹 사이트에 추가 된 파일 ([전체 크기 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image3.png))


마지막으로, 사이트 맵 업데이트 (`Web.sitemap`) 항목을 포함 하는 `ManageUsers.aspx` 페이지. 추가 후 다음 XML는 `<siteMapNode>` 역할 자습서에 대 한 추가 했습니다.

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample3.xml)]

업데이트 사이트 맵을 사용 하 여 브라우저를 통해 사이트를 방문 합니다. 그림 2에서 볼 수 있듯이 이제 왼쪽 탐색 관리 자습서에 대 한 항목이 포함 됩니다.


[![사이트 맵 사용자 관리 이라는 노드를 포함 합니다.](building-an-interface-to-select-one-user-account-from-many-vb/_static/image5.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image4.png)

**그림 2**: 사이트 맵 노드 이라는 사용자 관리를 포함 ([전체 크기 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image6.png))


## <a name="step-2-listing-all-user-accounts-in-a-gridview"></a>GridView의 모든 사용자 계정을 나열 하는 2 단계:

이 자습서의 최종 목표는 관리자가 관리할 사용자 계정을 선택할 수 있는 페이징, 필터링 할 표를 만드는 것입니다. 목록으로 시작 해 보겠습니다 *모든* 는 GridView의 사용자입니다. 설치가 완료 되는 필터 및 페이징 인터페이스 및 기능 추가 합니다.

열기는 `ManageUsers.aspx` 페이지에 `Administration` 폴더 설정 된 GridView를 추가 하 고 해당 `ID` 를 `UserAccounts` 잠시 후에 사용자 계정 집합을 사용 하 여 GridView에 바인딩하는 코드를 작성 하는 `Membership` 클래스의 `GetAllUsers` 메서드. 이전 자습서에 설명 된 대로 `GetAllUsers` 메서드가 반환 되는 `MembershipUserCollection` 개체 컬렉션인의 `MembershipUser` 개체입니다. 각 `MembershipUser` 컬렉션에 같은 속성을 포함 `UserName`, `Email`, `IsApproved`등입니다.

GridView에서 원하는 사용자 계정 정보를 표시 하기 위해 설정 GridView의 `AutoGenerateColumns` 속성을 false로 BoundFields에 대 한 추가 `UserName`, `Email`, 및 `Comment` 속성 및에 대 한 CheckBoxFields는 `IsApproved`, `IsLockedOut`, 및 `IsOnline` 속성입니다. 이 구성은 컨트롤의 선언적 태그 또는 필드 대화 상자를 통해 적용할 수 있습니다. 그림 3는 필드를 자동으로 생성 확인란을 선택 했습니다 BoundFields 및 CheckBoxFields 추가 되 고 구성 된 후 대화 상자 필드의 스크린 샷을 보여줍니다.


[![GridView에 3 개의 BoundFields 및 3 개의 CheckBoxFields 추가](building-an-interface-to-select-one-user-account-from-many-vb/_static/image8.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image7.png)

**그림 3**: 세 BoundFields 추가 및 GridView에 3 개의 CheckBoxFields ([전체 크기 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image9.png))


여 GridView를 구성한 후 해당 선언 태그 다음과 유사한를 확인 합니다.

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample4.aspx)]

다음으로, 사용자 계정 GridView에 바인딩하는 코드를 작성 해야 합니다. 라는 메서드를 만듭니다 `BindUserAccounts` 이 작업을 수행 하에서 호출 된 `Page_Load` 이벤트 처리기에 첫 번째 페이지 방문 합니다.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample5.vb)]

브라우저를 통해 페이지를 테스트 하려면 보십시오. 그림 4에서 볼 수 있듯이 `UserAccounts` 시스템에 사용자 이름, 전자 메일 주소 및 모든 사용자에 대 한 다른 적절 한 계정 정보를 나열 하는 GridView입니다.


[![GridView에서 사용자 계정이 표시 되는지](building-an-interface-to-select-one-user-account-from-many-vb/_static/image11.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image10.png)

**그림 4**: GridView에서의 사용자 계정이 나열 되어 ([전체 크기 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image12.png))


## <a name="step-3-filtering-the-results-by-the-first-letter-of-the-username"></a>3 단계: 사용자의 첫 번째 문자로 결과 필터링

현재는 `UserAccounts` GridView 표시 *모든* 사용자 계정입니다. 수백 또는 수천 개의 사용자 계정이 웹 사이트의 경우는 해당 사용자를 신속 하 게 표시 된 계정 줄이려면 수 합니다. 이 페이지에 링크 단추가 필터링을 추가 하 여 수행할 수 있습니다. 27 linkbutton이 있는 페이지에 추가: 알파벳의 각 문자에 대 한 하나의 LinkButton과 제목이 하나 있습니다. 방문자가 모든 LinkButton을 클릭할 경우 GridView 모든 사용자가 표시 됩니다. 특정 문자를 클릭 하는 경우 사용자는 선택한 문자로 시작 하는 사용자에만 표시 됩니다.

첫 번째 작업이 27 LinkButton 컨트롤을 추가 하는 것입니다. 옵션 중 하나를 27 링크 단추가 선언적으로 만드는 것 한 번에 하나씩 있습니다. 와 반복기 컨트롤을 사용 하는 보다 유연한 방식을 `ItemTemplate` LinkButton을 렌더링 하 고 필터링 옵션으로 반복기에 바인딩됩니다는 `String` 배열입니다.

반복기 컨트롤 위의 페이지에 추가 하 여 시작 된 `UserAccounts` GridView입니다. 반복기의 설정 `ID` 속성을 `FilteringUI` 반복기의 템플릿 구성 되도록 해당 `ItemTemplate` LinkButton 렌더링 인 `Text` 및 `CommandName` 속성 현재 배열 요소에 바인딩됩니다. 설명한 것 처럼는 <a id="_msoanchor_3"> </a> [ *사용자에 게 역할 할당* ](../roles/assigning-roles-to-users-vb.md) 자습서,이 사용 하 여 수행할 수는 `Container.DataItem` 구문이 있습니다. 반복기를 사용 하 여 `SeparatorTemplate` 각 링크 사이의 세로 선을 표시 하려면.

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample6.aspx)]

원하는 필터링 옵션으로이 반복기를 채우려면 라는 메서드를 만듭니다 `BindFilteringUI`합니다. 이 메서드를 호출 하는 `Page_Load` 이벤트 처리기에 첫 번째 페이지를 로드 합니다.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample7.vb)]

요소로 필터링 옵션을 지정 하는이 메서드는 `String` 배열 `filterOptions` 반복기가 인 LinkButton을 렌더링 하는 데는 배열의 각 요소에 대 한 해당 `Text` 및 `CommandName` 배열 값에 할당 된 속성 요소입니다.

그림 5는 `ManageUsers.aspx` 브라우저를 통해 볼 때 페이지입니다.


[![반복기 27 필터링 링크 단추가 나열](building-an-interface-to-select-one-user-account-from-many-vb/_static/image14.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image13.png)

**그림 5**: The 반복기 나열 27 필터링 링크 단추가 ([전체 크기 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image15.png))


> [!NOTE]
> 사용자 이름의 모든 문자, 숫자 및 문장 부호를 포함 하 여 시작할 수 있습니다. 이러한 계정은 볼 수 있도록 관리자가 모든 LinkButton 옵션을 사용 해야 합니다. 또는 숫자로 시작 하는 모든 사용자 계정 반환할 LinkButton을 추가할 수 있습니다. I이 그대로 실행으로 판독기에 대 한 합니다.


포스트백 필터링 링크 단추가 중 하나를 클릭 하 고는 반복기를 발생 시킵니다 `ItemCommand` 이벤트를 아직 이유임 때문에 눈금에서 변경 되지 않은 결과 필터링 하려면 코드를 작성 합니다. `Membership` 클래스를 포함 한 [ `FindUsersByName` 메서드](https://technet.microsoft.com/library/system.web.security.membership.findusersbyname.aspx) 했는데 사용자 지정된 된 검색 패턴과 일치 하는 해당 사용자 계정을 반환 하는 합니다. 이 메서드 인 사용자 이름으로 지정 된 문자로 시작 하는 해당 사용자 계정 검색을 사용할 수는 `CommandName` 클릭 된 필터링 된 LinkButton의 합니다.

업데이트 하 여 시작는 `ManageUser.aspx` 라는 속성이 포함 되도록 페이지의 코드 숨김 클래스 `UsernameToMatch` 이 속성이 게시할 사용자 이름 필터 문자열을 유지 합니다.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample8.vb)]

`UsernameToMatch` 속성에 할당 된 해당 값이 저장 된 `ViewState` UsernameToMatch 키를 사용 하 여 컬렉션입니다. 이 속성의이 값을 읽을 때 확인 하는 값에 있는 경우는 `ViewState` 컬렉션, 그렇지 않으면 해당 기본값은 빈 문자열을 반환 합니다. `UsernameToMatch` 속성에서 속성에 모든 변경 내용은 게시할 보관 되도록 뷰 상태 값을 유지 하는 즉, 일반적인 패턴을 보여 줍니다. 이 패턴에 대 한 자세한 내용은 읽기 [이해 ASP.NET 뷰 상태](https://msdn.microsoftn-us/library/ms972976.aspx)합니다.

다음을 업데이트 하는 `BindUserAccounts` 메서드를 대신 호출 `Membership.GetAllUsers`, 호출 `Membership.FindUsersByName`의 값에 전달 하는 `UsernameToMatch` SQL 와일드 카드 문자를 추가 하는 속성 %입니다.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample9.vb)]

A 문자로 시작 했는데 사용자는 해당 사용자가 표시 하려면 설정는 `UsernameToMatch` 속성 A 다음 호출 `BindUserAccounts` 이에 대 한 호출 결과로 `Membership.FindUsersByName("A%")`, 반환하려면1.마찬가지로,로시작했는데사용자모든사용자를반환합니다는*모든* 사용자를 할당 하는 빈 문자열은 `UsernameToMatch` 속성 있도록는 `BindUserAccounts` 메서드를 호출 합니다 `Membership.FindUsersByName("%")`없어지고 모든 사용자 계정을 반환 합니다.

반복기에 대 한 이벤트 처리기를 만들고 `ItemCommand` 이벤트입니다. 이 이벤트는 linkbutton이 있는 필터 중 하나를 클릭 합니다. 클릭 한 LinkButton 전달 `CommandName` 통해 값는 `RepeaterCommandEventArgs` 개체입니다. 적절 한 값을 할당 해야는 `UsernameToMatch` 속성과 호출은 `BindUserAccounts` 메서드. 경우는 `CommandName` 은 All 이며, 빈 문자열을 할당 `UsernameToMatch` 모든 사용자 계정이 표시 되도록 합니다. 그렇지 않은 경우, 할당 된 `CommandName` 값을`UsernameToMatch`

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample10.vb)]

이 코드 위치에서와 필터링 기능을 테스트 합니다. 해당 페이지를 방문 먼저 모든 사용자 계정이 표시 됩니다 (그림 5를 다시 참조). A LinkButton 클릭 하면 포스트백을 발생 하 고 A로 시작 하는 사용자 계정만 표시 결과 필터링 합니다.


[![필터링 링크 단추가 사용 하 여 해당 사용자는 특정 문자로 시작 했는데 사용자를 표시 하려면](building-an-interface-to-select-one-user-account-from-many-vb/_static/image17.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image16.png)

**그림 6**: 필터링 링크 단추가 사용 하 여 해당 사용자가 있는 사용자 이름 문자로 시작 확실히 표시할 ([전체 크기 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image18.png))


## <a name="step-4-updating-the-gridview-to-use-paging"></a>페이징을 사용 하 여 GridView를 업데이트 하는 4 단계:

그림 5와 6에 표시 된 GridView에서 반환 된 레코드를 모두 나열 된 `FindUsersByName` 메서드. 수백 또는 수천 개의 사용자 계정이 있는 경우 (의 경우 처럼 모든 LinkButton을 클릭할 때 또는 페이지를 처음 방문할 때)의 모든 계정 볼 때 정보 과부하 발생할 수 있습니다. 사용자 계정을 관리 하기 쉽게 표시 하려면 한 번에 사용자 계정을 10 개까지 표시 하는 GridView 구성 합니다.

GridView 컨트롤에서는 두 가지 유형의 페이징을 제공합니다.

- **기본 페이징** -구현 하기 쉽고 유지 하지만 비효율적입니다. 간단히 말해서에서는 기본 GridView 페이징와 *모든* 데이터 소스에서 레코드입니다. 다음만 페이지를 표시할 적절 한 레코드입니다.
- **사용자 지정 페이징** -을 구현 하려면 더 많은 작업이 필요 하지만 데이터를 페이징 하는 사용자 지정 소스를 정확 하 게 표시 하는 레코드 집합이 반환 하기 때문에 기본 페이징 보다 더 효율적입니다.

기본 및 사용자 지정 페이징의 성능 차이 수천 개 레코드를 페이징할 때는 매우 길 수 있습니다. 작성 하기 때문에 있다고 가정 하 고이 인터페이스 수백 또는 수천 개의 사용자 계정이 될 수 있습니다, 그리고 사용자 지정 페이징을 사용 합니다.

> [!NOTE]
> 참조에 대 한 사용자 지정 페이징을 구현 작업과 관련 된 문제 뿐만 아니라 기본 및 사용자 지정 페이징 사이의 차이점에 보다 철저 한 토론을 [효율적으로 통해 큰 크기의 데이터를 페이징](https://asp.net/learn/data-access/tutorial-25-vb.aspx)합니다. 기본 및 사용자 지정 페이징의 성능 차이의 분석을 참조 하십시오. [SQL Server 2005와 함께 ASP.NET에서 사용자 지정 페이징](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)합니다.


사용자 지정 페이징을 구현 하려면 먼저 정확한 GridView에서 표시 하는 레코드 하위 집합을 검색 하는 기준인 메커니즘이 필요 합니다. 다행 스럽게도 하는 `Membership` 클래스의 `FindUsersByName` 메서드 페이지 인덱스 및 페이지 크기를 지정할 수 있도록 하는 오버 로드를 있으며 레코드의 해당 범위에 속하는 사용자 계정만 반환 합니다.

특히,이 오버 로드에는 다음 서명이: [ `FindUsersByName(usernameToMatch, pageIndex, pageSize, totalRecords)` ](https://msdn.microsoft.com/library/fa5st8b2.aspx)합니다.

*pageIndex* 반환 됩니다; 사용자 계정 페이지를 지정 하는 매개 변수 *pageSize* 페이지당 표시할 레코드를 나타냅니다. *totalRecords* 매개 변수는 한 `ByRef` 사용자 저장소에 전체 사용자 계정 수를 반환 하는 매개 변수입니다.

> [!NOTE]
> 반환한 데이터 `FindUsersByName` username; 별로 정렬 된 정렬 조건을 사용자 지정할 수 없습니다.


GridView는 사용자 지정 페이징 있지만 ObjectDataSource 컨트롤에 바인딩된 경우 하도록 구성할 수 있습니다. 사용자 지정 페이징을 구현 하려면 ObjectDataSource 컨트롤에 대 한 두 가지 방법이 필요: 시작 행 인덱스 및 표시할 레코드의 최대 수에 전달 되는 하나에 걸친; 범위에 포함 하는 레코드의 정확한 하위 집합을 반환 하 고 와 레코드의 총 수를 반환 하는 메서드를 통해 호출이 전달 합니다. `FindUsersByName` 페이지 인덱스 및 페이지 크기를 허용 하 고 통해 레코드의 총 수를 반환 하는 오버 로드는 `ByRef` 매개 변수입니다. 따라서 여기는 인터페이스 일치 하지가 않습니다.

옵션 중 하나는 ObjectDataSource를 요구 하 고 내부적으로 호출 하는 인터페이스를 노출 하는 프록시 클래스를 만드는 것은 `FindUsersByName` 메서드. 또 다른 옵션-및에서는이 문서에 대 한 하나-고유한 페이징 인터페이스를 만들고 GridView의 기본 제공 페이징 인터페이스 대신 사용 하는 것입니다.

### <a name="creating-a-first-previous-next-last-paging-interface"></a>첫 번째, 만들기, 이전 페이징 인터페이스 마지막 다음으로,

첫 번째, Previous, 다음, 마지막 링크 단추가와 페이징 인터페이스를 제작 해 보겠습니다. 첫 번째 LinkButton 클릭 하면 이전은 그 이전 페이지로 반환 하는 반면 사용자 데이터의 첫 번째 페이지를 이동 합니다. 마찬가지로, 다음 및 마지막 됩니다 사용자 다음 및 마지막 페이지에 각각 이동 합니다. 아래에 네 개의 LinkButton 컨트롤이 추가 `UserAccounts` GridView입니다.

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample11.aspx)]

다음으로 각 LinkButton의에 대 한 이벤트 처리기를 만들고 `Click` 이벤트입니다.

그림 7에는 Visual Web Developer 디자인 뷰를 통해 볼 때 4 개의 링크 단추가 나와 있습니다.


[![다음으로, 첫 번째, 이전, 추가 및 GridView 아래에 링크 단추가 마지막](building-an-interface-to-select-one-user-account-from-many-vb/_static/image20.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image19.png)

**그림 7**: 첫 번째 추가, Previous, 다음을 및 GridView 아래에 있는 마지막 링크 단추가 ([전체 크기 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image21.png))


### <a name="keeping-track-of-the-current-page-index"></a>현재 페이지 인덱스는 추적

사용자를 처음으로 방문는 `ManageUsers.aspx` 해야 하는지 또는 페이지 필터링 중 하나는 단추, GridView의 데이터의 첫 번째 페이지를 표시 하려고 합니다. 그러나 사용자가 탐색 링크 단추가 중 하나를 클릭 하면 해야 페이지 인덱스를 업데이트 합니다. 페이지 인덱스 및 한 페이지에 표시할 레코드 수를 유지 하려면 다음 두 속성 페이지의 코드 숨김 클래스를 추가 합니다.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample12.vb)]

와 같은 `UsernameToMatch` 속성에는 `PageIndex` 속성이 뷰 상태에 해당 값을 유지 합니다. 읽기 전용 `PageSize` 속성이 10는 하드 코드 된 값을 반환 합니다. 동일한 패턴을 사용 하도록이 속성을 업데이트 하려면 관심 있는 판독기를 초대 `PageIndex`, 다음를 확장 하는 `ManageUsers.aspx` 페이지는 페이지를 방문 하는 사용자 당 표시할 수 사용자 계정 페이지를 지정할 수 있도록 합니다.

### <a name="retrieving-just-the-current-pages-records-updating-the-page-index-and-enabling-and-disabling-the-paging-interface-linkbuttons"></a>현재 페이지의 레코드만 검색, 페이지 인덱스를 업데이트 하 고 활성화 및 페이징 인터페이스 링크 단추가 비활성화

현재 위치에서 페이징 인터페이스와 및 `PageIndex` 및 `PageSize` 속성 추가 업데이트할 준비가 `BindUserAccounts` 메서드를 사용 하 여 적절 한 `FindUsersByName` 오버 로드 합니다. 또한이 메서드를 사용 하도록 설정 하거나 표시 되 고 페이지에 따라 페이징 인터페이스를 사용 하지 않도록를 포함 해야 합니다. 데이터의 첫 번째 페이지를 볼 때 첫 번째 및 이전 링크를 해제 해야 합니다. 마지막 페이지를 볼 때 다음 하 고 마지막 해제 되어야 합니다.

`BindUserAccounts` 메서드를 다음 코드로 업데이트합니다.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample13.vb)]

통해 호출이 전달 하는 레코드의 총 수의 마지막 매개 변수에 의해 결정 됩니다는 `FindUsersByName` 메서드. 사용자 계정의 지정된 된 페이지를 반환한 후 4 개의 링크 단추가 중 하나를 사용, 데이터의 첫 번째 또는 마지막 페이지를 보고 하는지 여부에 따라 합니다.

4 개의 링크 단추가에 대 한 코드를 작성 하는 마지막 단계 `Click` 이벤트 처리기입니다. 이러한 이벤트 처리기를 업데이트 해야 합니다.는 `PageIndex` 속성을 다음에 대 한 호출을 통해 GridView에 데이터를 다시 바인딩해야 `BindUserAccounts` 처음, 이전 및 다음 이벤트 처리기는 매우 간단 합니다. 그러나 `Click` 마지막 LinkButton에 대 한 이벤트 처리기 좀 더 복잡 하므로 마지막 페이지 인덱스를 확인 하기 위해 표시 되는 레코드 수를 결정 해야 합니다.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample14.vb)]

그림 8과 9 작업에 사용자 지정 페이징 인터페이스를 표시합니다. 그림 8 나와 `ManageUsers.aspx` 모든 사용자 계정에 대 한 데이터의 첫 번째 페이지를 볼 때 페이지입니다. Note 13 계정의 유일한 10 표시 됩니다. 업데이트 다시 게시 하면 다음 또는 마지막 링크를 클릭 하 여 `PageIndex` 1, 및 눈금에 계정을 사용자의 두 번째 페이지에 바인딩합니다 (그림 9 참조).


[![첫 번째 10 사용자 계정이 표시 됩니다.](building-an-interface-to-select-one-user-account-from-many-vb/_static/image23.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image22.png)

**그림 8**:의 첫 번째 10 사용자 계정이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image24.png))


[![사용자 계정의 두 번째 페이지를 다음 링크를 클릭 하면 표시 됩니다.](building-an-interface-to-select-one-user-account-from-many-vb/_static/image26.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image25.png)

**그림 9**: 다음 링크를 클릭 하 고 두 번째 페이지의 사용자 계정이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image27.png))


## <a name="summary"></a>요약

관리자는 계정 목록에서 사용자를 선택 해야 합니다. 이전 자습서에서 보이는 것 처럼 사용자 수가 가장으로 채워진 드롭다운 목록을 사용 하 여 있지만이 방법은 잘 확장 되지 않습니다. 보다 더 효율적이이 자습서에서 살펴본:는 필터링 가능한 인터페이스는 페이지 된 GridView에 해당 결과가 표시 됩니다. 이 사용자 인터페이스를 사용 관리자 수 빠르고 효율적으로 찾아 수천 간에 사용자 계정 하나를 선택 합니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [SQL Server 2005와 함께 ASP.NET에서 사용자 지정 페이징](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)
- [많은 양의 데이터를 효율적으로 페이징](https://asp.net/learn/data-access/tutorial-25-vb.aspx)
- [자신의 웹 사이트 관리 도구를 롤링합니다.](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)

### <a name="about-the-author"></a>작성자 정보

여러 ASP/ASP.NET 책의 작성자 및 4GuysFromRolla.com의 창립자 Scott Mitchell의 근무 기간이 Microsoft 웹 기술을 1998 이후입니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은  *[Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*합니다. Scott에 도달할 수 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 또는에서 그의 블로그 통해 [http://ScottOnWriting.NET](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Alicja Maziarz 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩

>[!div class="step-by-step"]
[이전](unlocking-and-approving-user-accounts-cs.md)
[다음](recovering-and-changing-passwords-vb.md)
