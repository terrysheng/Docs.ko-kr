---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
title: "ASP.NET MVC 3 (VB) 소개 | Microsoft Docs"
author: Rick-Anderson
description: "이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: a1b3d789-93b4-487f-b90d-80c9c9b4f8fa
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: f0717e8d635818322be8b3242efe756a20351340
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="intro-to-aspnet-mvc-3-vb"></a>ASP.NET MVC 3 (VB) 소개
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉 Microsoft Visual Studio의 무료 버전을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명 합니다. 시작 하기 전에 아래에 나열 된 필수 구성 요소가 설치 되어 있는지 확인 합니다. 다음 링크를 클릭 하 여 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소 설치: [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.
> 
> 이 항목에 수반 VB.NET 소스 코드를 사용 하 여 Visual Web Developer 프로젝트 ´ ù. [VB.NET 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. 원하는 경우 C#으로 전환 된 [C# 버전](../cs/intro-to-aspnet-mvc-3.md) 이 자습서의 합니다.


이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉 Microsoft Visual Studio의 무료 버전을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명 합니다. 시작 하기 전에 아래에 나열 된 필수 구성 요소가 설치 되어 있는지 확인 합니다. 다음 링크를 클릭 하 여 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.

- [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)

Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소 설치: [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.

이 항목에 수반 VB 소스 코드를 사용 하 여 Visual Web Developer 프로젝트 ´ ù. [여기에 VB 버전을 다운로드](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=14824)합니다. CSharp를 선호 하는 경우 전환의 [CSharp 버전](../cs/intro-to-aspnet-mvc-3.md) 이 자습서의 합니다.

## <a name="what-youll-build"></a>만들 것인지

만들기, 편집 및 나열 하는 데이터베이스에서 영화를 지 원하는 간단한 영화 목록 응용 프로그램을 구현 합니다. 다음은 빌드합니다.이 응용 프로그램의 두 가지 스크린샷입니다. 데이터베이스에서 영화 목록을 표시 하는 페이지에 포함 됩니다.

[![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image2.png)](intro-to-aspnet-mvc-3/_static/image1.png)

도 응용 프로그램 추가, 편집 및 개별 파일에 대 한 참조 정보 뿐만 아니라 영화, 삭제할 수 있습니다. 모든 데이터 입력 시나리오에는 데이터베이스에 저장 된 데이터가 올바른지 확인 하도록 유효성 검사를 포함 됩니다.

[![CreateFormSo](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)

## <a name="skills-youll-learn"></a>기술을 알아봅니다

학습할 다음과 같습니다.

- 새 ASP.NET MVC 프로젝트를 만드는 방법
- Entity Framework 코드 중심을 사용 하 여 새 데이터베이스를 만드는 방법
- 컨트롤러와 뷰 ASP.NET MVC를 만드는 방법
- 검색 한 데이터를 표시 하는 방법
- 데이터를 편집 하 고 데이터 유효성 검사를 사용 하는 방법

## <a name="getting-started"></a>시작

Visual Web Developer 2010 Express (줄여서 "VWD")를 실행 하 여 시작 하 고 선택 **새 프로젝트** 에서 **시작** 페이지.

Visual Web Developer IDE 또는 통합된 개발 환경입니다. Microsoft Word를 사용 하 여 문서를 작성 하는 것 처럼 응용 프로그램을 만드는 있는 IDE를 사용 합니다. Visual Web Developer를 사용할 수 있는 다양 한 옵션을 보여 주는: 위쪽 도구 모음이입니다. IDE에서 작업을 수행 하는 다른 방법은 제공 하는 메뉴가 있습니다. (선택 하는 대신 예를 들어 **새 프로젝트** 에서 **시작** 페이지 메뉴를 사용 하 고 선택할 수 **파일** &gt; **새프로젝트**.)

[![](intro-to-aspnet-mvc-3/_static/image6.png)](intro-to-aspnet-mvc-3/_static/image5.png)

## <a name="creating-your-first-application"></a>응용 프로그램 처음 만들기

프로그래밍 언어와 선택 하는 Visual Basic 또는 Visual C#을 사용 하 여 응용 프로그램을 만들 수 있습니다. 이 자습서에서는 Visual Basic의 왼쪽에서 선택 하 고 선택 **ASP.NET MVC 3 웹 응용 프로그램**합니다. "MvcMovie" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.

![1NewMVCproj_sm](intro-to-aspnet-mvc-3/_static/image7.png)

에 **새 ASP.NET MVC 3 프로젝트** 대화 상자에서 **인터넷 응용 프로그램**합니다. 둡니다 **Razor** 를 기본 뷰 엔진입니다.

![1InternetAppRazor_SM](intro-to-aspnet-mvc-3/_static/image8.png)

**확인**을 클릭합니다. Visual Web Developer 방금 만든 ASP.NET MVC 프로젝트에 대 한 기본 서식 파일을 사용 해야 하므로 응용 프로그램 현재 아무것도 수행 하지 않고! 간단한 "Hello World!"입니다. 프로젝트의 응용 프로그램을 시작 하는 것이 좋습니다.

[![](intro-to-aspnet-mvc-3/_static/image10.png)](intro-to-aspnet-mvc-3/_static/image9.png)

**디버그** 메뉴에서 **디버깅 시작**을 선택합니다.

![](intro-to-aspnet-mvc-3/_static/image11.png)

F 5를 눌러 디버깅을 시작 하려면 바로 가기 키 임을 확인 합니다.

F 5를 눌러 Visual Web Developer 웹 개발 서버를 시작 하 고 웹 응용 프로그램을 실행 하면 됩니다. 그런 다음 VWD는 브라우저를 시작 하 고 응용 프로그램의 홈 페이지를 엽니다. 브라우저의 주소 표시줄을 `localhost` 와 하지 것 같은 `example.com`합니다. 때문 `localhost` 항상 방금 빌드한 응용 프로그램을 실행 중인이 예제의 자신의 로컬 컴퓨터를 가리킵니다. VWD 웹 프로젝트를 실행 하면 임의 포트를 프로젝트에 사용 됩니다. 아래 그림에서는 임의의 포트 번호가 43246입니다. 다른 포트 번호를 사용 하면 프로젝트.

![](intro-to-aspnet-mvc-3/_static/image12.png)

즉시 이러한 기본 템플릿은 하면 두 개의 페이지를 방문 하 고 기본 로그인 페이지를 제공 합니다. 이 응용 프로그램의 작동 방식을 변경 하 고 프로세스에서 ASP.NET MVC에 대해 약간 배우 살펴보겠습니다. 브라우저를 닫고 일부 코드를 변경 해보겠습니다.

>[!div class="step-by-step"]
[다음](adding-a-controller.md)
