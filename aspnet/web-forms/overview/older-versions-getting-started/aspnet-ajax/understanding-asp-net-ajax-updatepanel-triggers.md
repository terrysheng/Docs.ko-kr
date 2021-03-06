---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-updatepanel-triggers
title: "ASP.NET AJAX UpdatePanel 트리거 이해 | Microsoft Docs"
author: scottcate
description: "Visual Studio에서 태그 편집기에서 작업, 변경 될 수 있습니다 (IntelliSense)에서 UpdatePanel 컨트롤의 두 개의 자식 요소입니다. Wh 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/12/2008
ms.topic: article
ms.assetid: faab8503-2984-48a9-8a40-7728461abc50
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-updatepanel-triggers
msc.type: authoredcontent
ms.openlocfilehash: 1338ef0763d9bfab451bc30cafa39f715200153d
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="understanding-aspnet-ajax-updatepanel-triggers"></a>ASP.NET AJAX UpdatePanel 트리거 이해
====================
으로 [Scott 인증서](https://github.com/scottcate)

[PDF 다운로드](http://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial02_Triggers_cs.pdf)

> Visual Studio에서 태그 편집기에서 작업, 변경 될 수 있습니다 (IntelliSense)에서 UpdatePanel 컨트롤의 두 개의 자식 요소입니다. 그 중 하나는 페이지 (또는 사용자 정의 컨트롤의 하나를 사용 하는 경우)에서 컨트롤을 지정 하는 트리거 요소에는 요소가 있는 UpdatePanel 컨트롤의 부분 렌더링을 트리거할입니다.


## <a name="introduction"></a>소개

Microsoft의 ASP.NET 기술을 개체 지향 및 이벤트 기반 프로그래밍 모델을 가져오며 컴파일된 코드의 장점을 함께 결합 합니다. 그러나 피어 채널의 서버 쪽 처리 모델에는 Microsoft ASP.NET 3.5 AJAX 확장에 포함 된 새로운 기능으로 처리할 수 있으며이 중 대다수가 기술에 내재 된 몇 가지 단점이 있습니다. 이러한 확장 페이지의 부분 렌더링을 포함 하 여 전체 페이지 새로 고침 (프로 파일링 API는 ASP.NET 포함), 클라이언트 스크립트 및 광범위 한 클라이언트 쪽 API를 통해 웹 서비스에 액세스 하는 기능을 요구 하지 않고 새로운 많은 리치 클라이언트 기능을 사용 하도록 설정 다양 한 ASP.NET 서버측 컨트롤 집합에 표시 된 컨트롤 스키마를 반영 하도록 설계 되었습니다.

이 백서는 ASP.NET AJAX의 XML 트리거 기능 검사 `UpdatePanel` 구성 요소입니다. XML 트리거 특정 UpdatePanel 컨트롤에 대 한 부분 렌더링을 일으킬 수 있는 구성 요소에 대해 세분화 된 제어를 제공 합니다.

이 백서는 Beta 2 버전의.NET Framework 3.5 및 Visual Studio 2008을 기반으로 합니다. ASP.NET AJAX 확장에 이전에 ASP.NET 2.0을 목표로 추가 기능 어셈블리는.NET Framework 기본 클래스 라이브러리에 통합 되었습니다. 이 백서는 또한 하지 Visual Web Developer Express, Visual Studio 2008을 사용 하는 (코드 샘플에 관계 없이 완전히 호환 됩니다. 하지만 Visual Studio의 사용자 인터페이스에 따라 연습을 제공 합니다 가정 개발 환경)입니다.

## <a name="triggers"></a>*트리거*

기본적으로의 지정 된 UpdatePanel에 대 한 트리거가 포함 된 TextBox 컨트롤 (예)에서 포스트백을 호출 하는 모든 자식 컨트롤을 자동으로 포함 자신의 `AutoPostBack` 속성이로 설정 **true**합니다. 그러나 트리거 포함할 수도 있습니다 태그;을 사용 하 여 이 작업 내에서 수행 되는 `<triggers>` UpdatePanel 컨트롤 선언의 섹션. 트리거를 통해 액세스할 수 있지만 `Triggers` 컬렉션 속성을 것이 좋습니다 (예를 들어, 컨트롤을 사용할 수 없는 경우 디자인 타임에) 실행 시간에 대 한 모든 부분 렌더링 트리거를 등록 하면 사용 하 여는 `RegisterAsyncPostBackControl(Control)` 의 메서드는 ScriptManager 내 페이지에 대 한 개체는 `Page_Load` 이벤트입니다. 페이지는 상태 비저장 서버 이므로 다시 등록 해야 이러한 컨트롤 만들어질 때마다 저장.

자동 자식 트리거 포함도 비활성화할 수 있습니다 (있도록 자식 만드는 컨트롤을 포스트백 자동으로 부분 렌더링을 트리거하지 않음)을 설정 하 여는 `ChildrenAsTriggers` 속성을 **false**합니다. 이렇게 하면 있도록 개발자는 옵트인 발생할 수 있는 모든 이벤트를 처리 하는 것이 아니라 이벤트에 응답 하려면 어떤 특정 컨트롤을 할당할 때 가장 높은 유연성 페이지 렌더링을 호출할 수 있으며 권장 됩니다.

UpdatePanel 컨트롤 중첩 된 경우는 UpdateMode로 설정 되어 있는지 확인 **조건부**, UpdatePanel 자식 트리거되는 있지만 부모 하지 않은 경우, 다음의 자식 UpdatePanel이 새로 고쳐집니다. 그러나 부모 UpdatePanel을 새로 고칠 경우 다음 자식 UpdatePanel 됩니다도 새로 고칠 수입니다.

## <a name="the-lttriggersgt-element"></a>*&lt;트리거&gt; 요소*

Visual Studio에서 태그 편집기에서 작업, 변경 될 수 있습니다 (IntelliSense)에서 두 개의 자식 요소에 `UpdatePanel` 제어 합니다. 가장 일반적인 원인과 요소는는 `<ContentTemplate>` 기본적으로 콘텐츠를 통해 업데이트 패널이 소유한를 캡슐화 하는 요소 (부분 렌더링 म 사용 콘텐츠). 다른 요소는는 `<Triggers>` 페이지 (또는 사용자 정의 컨트롤의 하나를 사용 하는 경우)에 있는 컨트롤을 지정 하는 요소는 UpdatePanel 컨트롤의 부분 렌더링을 트리거할 하는 &lt;트리거&gt; 요소가 상주 하 합니다.

`<Triggers>` 요소 개수에 관계 없이 각 두 개의 자식 노드가 포함 될 수 있습니다: `<asp:AsyncPostBackTrigger>` 및 `<asp:PostBackTrigger>`합니다. 모두 두 개의 특성 `ControlID` 및 `EventName`, 고 캡슐화의 현재 단위 내에서 컨트롤을 지정할 수 있습니다 (예를 들어, 웹 사용자 정의 컨트롤 내에서 UpdatePanel 컨트롤 있으면 하지 않아야에 컨트롤을 참조 하려면 페이지는 사용자 정의 컨트롤을 저장할)입니다.

`<asp:AsyncPostBackTrigger>` 것의 자식으로 존재 하는 컨트롤의 모든 이벤트를 대상으로 지정할 수 있다는 점에서 요소는 특히 유용 *모든* 캡슐화는이 트리거는 자식 UpdatePanel 뿐 아니라 단위에서 UpdatePanel 컨트롤 . 따라서 부분 페이지 업데이트를 트리거하기 모든 컨트롤을 만들 수 있습니다.

마찬가지로,는 `<asp:PostBackTrigger>` 트리거 부분 페이지 렌더링 하지만 서버에 대 한 전체 왕복을 요구 하는 요소를 사용할 수 있습니다. 컨트롤 그렇지 않은 경우 일반적으로 트리거할 부분 페이지 렌더링 될 때 전체 페이지 렌더링을 강제로 실행 하려면이 트리거 요소를 사용할 수도 있습니다 (경우에 예를 들어, 한 `Button` 컨트롤에 있는 `<ContentTemplate>` UpdatePanel 컨트롤의 요소). 다시, PostBackTrigger 요소 캡슐화의 현재 단위로 UpdatePanel 컨트롤의 자식 컨트롤을 지정할 수 있습니다.

## <a name="lttriggersgt-element-reference"></a>*&lt;트리거&gt; 요소 참조*

*태그의 하위 항목:*

| **태그** | **설명** |
| --- | --- |
| &lt;asp: AsyncPostBackTrigger&gt; | 컨트롤 및 부분 페이지 업데이트를이 트리거 참조가 포함 되어 있는 UpdatePanel을 발생 시키는 이벤트를 지정 합니다. |
| &lt;asp: PostBackTrigger&gt; | 컨트롤 및 전체 페이지 업데이트가 (전체 페이지 새로 고침)를 발생 시키는 이벤트를 지정 합니다. 이 태그는 컨트롤의 부분 렌더링 트리거할지 그렇지 않은 경우 전체 새로 고침을 강제로 사용할 수 있습니다. |

## <a name="walkthrough-cross-updatepanel-triggers"></a>*연습: 간 UpdatePanel 트리거*

1. 부분 렌더링을 사용 하도록 설정 하는 ScriptManager 개체와 새 ASP.NET 페이지를 만듭니다. -첫 번째 범위에서이 페이지에 두 개의 적어지므로 추가 Label (레이블 1) 컨트롤과 단추 컨트롤 2 개 (Button1 및 Button2)를 포함 합니다. Button1이 필드를 모두 업데이트 하려면 클릭 하 고 Button2 줄 또는이 업데이트 하려면 클릭이 표시 되어야 합니다. 두 번째 updatepanel에서 Label 컨트롤 (Label2)만 포함 하지만 해당 ForeColor 속성을 식별 하는 기본 클래스로 설정 합니다.
2. 두 UpdatePanel 태그 UpdateMode 속성 설정 **조건부**합니다.

**Default.aspx에 대 한 목록 1: 태그:** 

[!code-aspx[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample1.aspx)]

1. Button1에 대 한 Click 이벤트 처리기에 Label1.Text 및 Label2.Text 클래스로 설정 시간 종속적 (예: DateTime.Now.ToLongTimeString()) 합니다. Button2에 대 한 Click 이벤트 처리기에 대 한만 Label1.Text 시간 종속적 값으로 설정 합니다.

**목록 2 코드 숨김 default.aspx.cs에서 (잘립니다).:** 

[!code-csharp[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample2.cs)]

1. F5 키를 눌러 작성 하 고 프로젝트를 실행 합니다. 모두 패널에 업데이트를 클릭 하면 두 레이블 변경은 텍스트 그러나 업데이트가 패널을 클릭할 때만 Label1 업데이트 합니다.


[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image2.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image1.png)

([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-updatepanel-triggers/_static/image3.png))


## <a name="under-the-hood"></a>*기본적인 이해*

이 예제에서는 방금 구성한를 활용 하 ASP.NET AJAX 수행 하는 및 우리의 UpdatePanel 간 패널 트리거 작동 하는 방법을 참조를 수행할 수 있습니다. 이렇게 하려면 오른쪽으로 생성 된 페이지의 HTML, 소스, FireBug-라는 Mozilla Firefox 확장으로 작업 하 AJAX 포스트백 수 쉽게 알아봅니다. 또한 Lutz Roeder 여.NET Reflector 도구를 사용 합니다. 이러한 도구는 무료로 사용할 수 있는 온라인, 있고 인터넷 검색 하 여 확인할 수 있습니다.

페이지 소스 코드에 대 한 검사를 보여 줍니다 거의 특이; UpdatePanel 컨트롤으로 렌더링 됩니다 `<div>` 컨테이너 및에서는 제공 된 스크립트 리소스 내용 볼 수에서 `<asp:ScriptManager>`합니다. 내부 AJAX 클라이언트 스크립트 라이브러리에 있는 PageRequestManager 몇 가지 새로운 AJAX 특정 호출도 있습니다. 렌더링 된 한 두 개의 UpdatePanel 컨테이너-보면 마지막으로, `<input>` 두 개의 단추 `<asp:Label>` 로 컨트롤 렌더링 `<span>` 컨테이너입니다. (FireBug에 DOM 트리를 검사 하는 경우 확인할 수 있습니다는 레이블이 표시 되는 콘텐츠의 나오지 않습니다 것을 나타내기 위해 흐리게 표시 됩니다).

Updatepanel이 단추를 클릭 상위 UpdatePanel 현재 서버 시간으로 업데이트 됩니다. FireBug에서 요청을 검사할 수 있도록 콘솔 탭을 선택 합니다. POST 요청 매개 변수를 먼저 없는지 확인 합니다.


[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image5.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image4.png)

([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-updatepanel-triggers/_static/image6.png))


UpdatePanel에 게 표시 되므로 서버 쪽 AJAX 코드 ScriptManager1 매개 변수를 통해 컨트롤 트리 발생 정확 하 게 참고: `Button1` 의 `UpdatePanel1` 제어 합니다. 이제 모두 패널 업데이트 단추를 클릭 합니다. 그런 다음 응답을 검사 하 보면 파이프로 구분 된 일련의 변수는 문자열;에 설정 상위 UpdatePanel을 보면 특히 `UpdatePanel1`, 해당 HTML 브라우저에 보내지는 전체에 있습니다. UpdatePanel의 html이 원래 HTML 콘텐츠를 통해 새 내용으로 대체 하는 AJAX 클라이언트 스크립트 라이브러리는 `.innerHTML` 속성 있으므로 서버는 HTML로 서버에서 변경 된 내용이 보냅니다.

이제, 모두 패널 업데이트 단추를 클릭 하 고 서버에서 결과 확인 합니다. 결과 매우 유사-적어지므로 두 서버에서 새 HTML을 수신 합니다. 이전 콜백와 마찬가지로 추가 페이지 상태 전송 됩니다.

볼 수 있듯이, 특별 한 코드가 없는 사용 하 여 AJAX 포스트백을 수행 하 때문에, AJAX 클라이언트 스크립트 라이브러리는 코드를 추가 하지 않고 폼 다시 게시를 가로챌 수 있습니다. 폼 자동으로 제출 하지 않는-ASP.NET 폼 유효성 검사 및 이미 상태에 대 한 코드를 주로 낼 수 자동 스크립트 리소스 포함 PostBackOptions 클래스를 자동으로 삽입 되도록 자동으로 서버 컨트롤 JavaScript 사용 및 ClientScriptManager 클래스입니다.

예를 들어; CheckBox 컨트롤 .NET Reflector 클래스 디스어셈블리를 검사 합니다. 이렇게 하려면 System.Web 어셈블리, 열려 있는지 확인 하 고 탐색 하는 `System.Web.UI.WebControls.CheckBox` 열기 클래스는 `RenderInputTag` 메서드. 확인 하는 조건부 찾습니다는 `AutoPostBack` 속성:


[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image8.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image7.png)

([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-updatepanel-triggers/_static/image9.png))


자동 다시 게시에서 사용 되는 경우는 `CheckBox` 결과 (true 인지 AutoPostBack 속성)를 통해 제어 `<input>` 에서 스크립트를 처리 하는 ASP.NET 이벤트와 태그를 렌더링 하므로 해당 `onclick` 특성입니다. 폼의 제출, 그런 다음 인터 셉 션 주요 변경 내용 수 있는 정확 하지 않은 문자열 대체를 사용 하 여 발생할 수 있는 잠재적인 모든 작동에 ASP.NET AJAX nonintrusively, 페이지에 삽입할 수 있습니다. 또한이 통해 *모든* UpdatePanel 컨테이너 내에서 해당 사용을 지원 하도록 추가 코드 없이 ASP.NET AJAX의 기능을 활용 하 여 사용자 지정 ASP.NET 컨트롤입니다.

`<triggers>` PageRequestManager 호출에서 초기화 되는 값에 해당 하는 기능 \_updateControls (참고는 ASP.NET AJAX 클라이언트 스크립트 라이브러리는 사용 하 여 규칙에 따라 해당 메서드, 이벤트 및 시작 하는 필드 이름 밑줄로 내부로 표시 된, 및 사용 되지 않는 라이브러리 자체 외부에서 사용). 제어 하는 AJAX 포스트백을 발생 하는 데 사용 됩니다 관찰할 수 있습니다.

예를 들어는 적어지므로 외부 한 컨트롤을 완전히 상태로 유지 하 고는 UpdatePanel 내에서 하나를 그대로 두고 페이지로 추가 두 개의 추가 컨트롤이 해 보겠습니다. 위쪽 UpdatePanel 내에서 CheckBox 컨트롤을 추가 하 고 목록 내에서 정의 된 색의 번호로 DropDownList를 삭제 합니다. 새 태그는 다음과 같습니다.

**새 마크업 코드 3:**

[!code-aspx[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample3.aspx)]

그리고 새 코드 숨김 여기:

**목록 4: 코드 숨김**

[!code-csharp[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample4.cs)]

이 페이지의 기본 개념은 드롭 다운 목록 중 두 번째 레이블을 표시 하기 위해 세 가지 색을 선택, 확인란 굵은 글꼴는에서 레이블이 날짜와 시간을 표시 하는 여부를 확인 하는입니다. 확인란 AJAX 업데이트, 발생 하지 않습니다 되지만 UpdatePanel 내 상주 하지는 경우에 드롭 다운 목록 되어서는 안 됩니다.


[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image11.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image10.png)

([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-updatepanel-triggers/_static/image12.png))


위의 화면에 표시 되 면 가장 최근 단추 클릭 수를 마우스 오른쪽 단추로 업데이트가 패널이 아래 시간 상위 시간에 관계 없이 항목을 업데이트 했습니다. 날짜를도 전환할 번의 클릭 사이의 날짜 아래쪽 레이블에 표시 됩니다. 마지막 관심 아래쪽 레이블의 색을입니다: 컨트롤 상태는 중요 한에서 설명 하는 레이블 텍스트를 보다 더 최근에 업데이트 된 및 사용자 AJAX 다시 게시를 통해 유지 되어야 합니다. *그러나*, 시간이 업데이트 되지 않았습니다. 시간 된의 지 속성을 통해 자동으로 다시 채워지지는 \_ \_컨트롤이 서버에 다시 렌더링 되는 경우 ASP.NET 런타임에 의해 해석 되 고 페이지의 VIEWSTATE 필드입니다. ASP.NET AJAX 서버 코드는 메서드는 컨트롤 상태; 변경 하는 인식 하지 않으므로 뷰 상태에서 단순히 다시 채웁니다 하 고 적합 한 이벤트를 실행 합니다.

그러나 그 지적, 있는지가 I 초기화 페이지 내에서 시간\_Load 이벤트 시간은는 증가 되기 올바르게 합니다. 따라서 개발자가 적절 한 코드는 적절 한 이벤트 처리기 중 실행 되 고 있는 주의 하 고 해야 페이지의 사용을 방지\_컨트롤 이벤트 처리기는 것이 적절 한 때를 로드 합니다.

## <a name="summary"></a>요약

ASP.NET AJAX Extensions UpdatePanel 컨트롤 용도가 넓은 함수로, 이며 다양 한 방법 업데이트할 수 만드는 컨트롤 이벤트를 식별 하는 데 활용할 수 있습니다. 해당 컨트롤은 자식 컨트롤에 의해 자동으로 업데이트 되 고 지원 하지만 페이지에 컨트롤 이벤트에 응답할 수 있습니다.

서버 처리 부하에 대 한 가능성을 줄이기 위해는 것이 좋습니다는 `ChildrenAsTriggers` UpdatePanel의 속성 설정할 `false`, 하며, 이벤트에 참여할-대신에 기본적으로 포함 해야 합니다. 또한 불필요 한 모든 이벤트를를 일으키는 유효성 검사 및 입력 필드에 변경 내용을 포함 하 여 잠재적으로 원치 효과 않습니다. 이러한 유형의 버그를 격리 하기 위해 페이지를 사용자에 게 투명 하 게 업데이트 원인이 아닐 즉각적으로 드러나지 따라서 하기 때문에 어려울 수 있습니다.

ASP.NET AJAX 폼의 내부 작동 방식을 검토 하 여 인터 셉 션 모델을 게시, ASP.NET에서 이미 제공 되는 프레임 워크 사용 되기 때문에 확인할 수 있었습니다. 이 과정에서 클래스는 최대 호환성 동일한 프레임 워크를 사용 하 여 디자인 된 컨트롤을 유지 하며 페이지 용으로 작성 된 JavaScript에 최소가 개입 합니다.

## <a name="bio"></a>약력

Rob Paveza Terralever의 수석.NET 응용 프로그램 개발자는 ([www.terralever.com](http://www.terralever.com)), 템피 소재, AZ.에 선행 대화형 마케팅 회사 에 연결할 수 그 [ robpaveza@gmail.com ](mailto:robpaveza@gmail.com), 그의 블로그에 있는 것 [http://geekswithblogs.net/robp/](http://geekswithblogs.net/robp/)합니다.

Scott 인증서의 근무 기간이 Microsoft 웹 기술을 1997 년부터 이며 myKB.com 부서장 ([www.myKB.com](http://www.myKB.com)) ASP.NET 작성 i 여기서 기반 응용 프로그램 기술 자료 소프트웨어 솔루션에 집중 합니다. Scott에 전자 메일을 통해 연결할 수 [ scott.cate@myKB.com ](mailto:scott.cate@myKB.com) 또는에서 그의 블로그 [ScottCate.com](http://ScottCate.com)

>[!div class="step-by-step"]
[이전](understanding-partial-page-updates-with-asp-net-ajax.md)
[다음](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
