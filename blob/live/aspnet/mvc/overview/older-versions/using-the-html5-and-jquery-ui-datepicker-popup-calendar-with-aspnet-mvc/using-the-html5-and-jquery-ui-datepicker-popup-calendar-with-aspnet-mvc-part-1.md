---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1
title: "ASP.NET MVC-1 부 HTML5 및 jQuery UI Datepicker 팝업 일정 사용 | Microsoft Docs"
author: Rick-Anderson
description: "이 자습서는 기본적인 편집기 템플릿과 표시 템플릿은 ASP.NET MV에서 jQuery UI datepicker 팝업 일정 사용 방법 알려 드리겠습니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/29/2011
ms.topic: article
ms.assetid: c23d27f7-b0cf-44f2-8445-fb69e045c674
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1
msc.type: authoredcontent
ms.openlocfilehash: 9320c8a2aadb3b3c5bd6cd90b59d8a72db384c0c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-1"></a><span data-ttu-id="44a49-103">ASP.NET MVC-1 부 HTML5 및 jQuery UI Datepicker 팝업 일정 사용</span><span class="sxs-lookup"><span data-stu-id="44a49-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 1</span></span>
====================
<span data-ttu-id="44a49-104">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="44a49-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="44a49-105">이 자습서는 기본적인 편집기 템플릿과 표시 템플릿은 ASP.NET MVC 웹 응용 프로그램에서 jQuery UI datepicker 팝업 일정 사용 방법 알려 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>


<span data-ttu-id="44a49-106">이 자습서는 편집기 템플릿, 표시 템플릿 및 jQuery를 사용 하는 방법의 기본 사항은 설명 [UI datepicker 팝업 일정](http://plugins.jquery.com/project/datepicker) ASP.NET MVC 웹 응용 프로그램에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-106">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery [UI datepicker popup calendar](http://plugins.jquery.com/project/datepicker) in an ASP.NET MVC Web application.</span></span> <span data-ttu-id="44a49-107">이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1을 사용할 수 있습니다 (&quot;Visual Web Developer&quot;), Microsoft Visual Studio의 무료 버전 또는 이미 있는 경우에 Visual Studio 2010 s p 1을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-107">For this tutorial, you can use Microsoft Visual Web Developer 2010 Express Service Pack 1 (&quot;Visual Web Developer&quot;), which is a free version of Microsoft Visual Studio, or you can use Visual Studio 2010 SP1 if you already have that.</span></span>

<span data-ttu-id="44a49-108">시작 하기 전에 아래에 나열 된 필수 구성 요소가 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="44a49-109">다음 링크를 클릭 하 여 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="44a49-110">또는 다음 링크를 사용 하 여 필요한 소프트웨어를 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-110">Alternatively, you can individually install the required software using the following links:</span></span>

- [<span data-ttu-id="44a49-111">Visual Studio Web Developer Express SP1 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="44a49-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [<span data-ttu-id="44a49-112">ASP.NET MVC 3 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="44a49-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- <span data-ttu-id="44a49-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)</span><span class="sxs-lookup"><span data-stu-id="44a49-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>

<span data-ttu-id="44a49-114">Visual Studio 2010 대신 Visual Web Developer를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소 설치: [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-114">If you're using Visual Studio 2010 instead of Visual Web Developer, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>

<span data-ttu-id="44a49-115">이 자습서를 마쳤습니다 가정는 [MVC 3으로 시작](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 자습서 또는 ASP.NET MVC 개발 고쳐야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-115">This tutorial assumes you have completed the [Getting Started with MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) tutorial or that you're familiar with ASP.NET MVC development.</span></span> <span data-ttu-id="44a49-116">이 자습서에서 완성 된 프로젝트로 시작는 [MVC 3 시작](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-116">This tutorial starts with the completed project from the [Getting Started with MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) tutorial.</span></span>

<span data-ttu-id="44a49-117">이 자습서에서 C# 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-117">This tutorial shows code in C#.</span></span> <span data-ttu-id="44a49-118">그러나는 [시작 프로젝트](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800) 및 완료 된 프로젝트를 Visual Basic에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-118">However, the [starter project](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800) and completed project are also available in Visual Basic.</span></span>

<span data-ttu-id="44a49-119">C# 및 Visual Basic 소스 코드를 Visual Studio 프로젝트는이 항목에 수반: [다운로드](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800)합니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-119">A Visual Studio project with C# and Visual Basic source code is available to accompany this topic: [Download](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800).</span></span>

### <a name="what-youll-build"></a><span data-ttu-id="44a49-120">만들 것인지</span><span class="sxs-lookup"><span data-stu-id="44a49-120">What You'll Build</span></span>

<span data-ttu-id="44a49-121">서식 파일을 추가 합니다 (특히, 편집 및 템플릿을 표시)에서 만든 단순 영화 목록 응용 프로그램에는 [MVC 3 시작](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-121">You'll add templates (specifically, edit and display templates) to the simple movie-listing application that was created in the [Getting Started with MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) tutorial.</span></span> <span data-ttu-id="44a49-122">또한 추가 합니다는 [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) 팝업 일정 날짜를 입력 하는 간편 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-122">You will also add a [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) popup calendar to simplify the process of entering dates.</span></span> <span data-ttu-id="44a49-123">다음 스크린샷에 표시 jQuery UI datepicker 팝업 일정으로 수정 된 응용 프로그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-123">The following screenshot shows the modified application with the jQuery UI datepicker popup calendar displayed.</span></span>

![완성 된 jQuery](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image1.png)

### <a name="skills-youll-learn"></a><span data-ttu-id="44a49-125">기술을 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="44a49-125">Skills You'll Learn</span></span>

<span data-ttu-id="44a49-126">학습할 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-126">Here's what you'll learn:</span></span>

- <span data-ttu-id="44a49-127">특성을 사용 하는 방법의 [DataAnnotations](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.aspx) 표시 되는 데이터의 형식을 제어 하 고 편집 모드에 있을 때 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-127">How to use attributes from the [DataAnnotations](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.aspx) namespace to control the format of data when it's displayed and when it's in edit mode.</span></span>
- <span data-ttu-id="44a49-128">템플릿을 만드는 방법 (편집 및 템플릿을 표시) 데이터의 서식을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-128">How to create templates (edit and display templates) to control the formatting of data.</span></span>
- <span data-ttu-id="44a49-129">추가 하는 방법의 [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) 날짜 필드를 입력 하는 방법으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-129">How to add the [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) as a way to enter date fields.</span></span>

### <a name="getting-started"></a><span data-ttu-id="44a49-130">시작</span><span class="sxs-lookup"><span data-stu-id="44a49-130">Getting Started</span></span>

<span data-ttu-id="44a49-131">다음 링크를 사용 하 여 시작 프로젝트에서 영화 목록 응용 프로그램을 아직 없는 경우 다운로드할: [다운로드](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800)합니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-131">If you don't already have the movie-listing application from the starter project, download it using the following link: [Download](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800).</span></span> <span data-ttu-id="44a49-132">다음 Windows 탐색기에서 마우스 오른쪽 단추로 클릭는 *MvcMovie.zip* 파일을 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-132">Then in Windows Explorer, right-click the *MvcMovie.zip* file and select **Properties**.</span></span> <span data-ttu-id="44a49-133">에 **MvcMovie.zip 속성** 대화 상자에서 **차단 해제**합니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-133">In the **MvcMovie.zip Properties** dialog box, select **Unblock**.</span></span> <span data-ttu-id="44a49-134">(사용 하려고 할 때 발생 하는 보안 경고가 표시 되지 않도록 차단 해제는 *.zip* 웹에서 다운로드 한 파일입니다.)</span><span class="sxs-lookup"><span data-stu-id="44a49-134">(Unblocking prevents a security warning that occurs when you try to use a *.zip* file that you've downloaded from the web.)</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image2.png)

<span data-ttu-id="44a49-135">마우스 오른쪽 단추로 클릭는 *MvcMovie.zip* 파일을 선택 **압축 풀기** 에 파일 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-135">Right-click the *MvcMovie.zip* file and select **Extract All** to unzip the file.</span></span> <span data-ttu-id="44a49-136">Visual Web Developer 또는 Visual Studio 2010에서 엽니다는 *MvcMovieCS\_TU.sln* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-136">In Visual Web Developer or Visual Studio 2010, open the *MvcMovieCS\_TU.sln* file.</span></span>

<span data-ttu-id="44a49-137">**솔루션 탐색기**, 두 번 클릭은 *Views\Shared\\_Layout.cshtml* 엽니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-137">In **Solution Explorer**, double-click the *Views\Shared\\_Layout.cshtml* to open it.</span></span> <span data-ttu-id="44a49-138">변경 된 `H1` 헤더를 **MVC 만든 동영상 앱** 를 **영화 jQuery**합니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-138">Change the `H1` header from **MVC Movie App** to **Movie jQuery**.</span></span> <span data-ttu-id="44a49-139">CTRL + f 5를 눌러 응용 프로그램을 실행 하 고 클릭 하 고 **홈** 탭을 사용 하는 `Index` 영화 컨트롤러의 메서드.</span><span class="sxs-lookup"><span data-stu-id="44a49-139">Press CTRL+F5 to run the application and click the **Home** tab, which takes you to the `Index` method of the movie controller.</span></span> <span data-ttu-id="44a49-140">응용 프로그램을 사용 하려면 선택은 **편집** 링크 및 **세부 정보** 동영상 중 하나에 대 한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-140">To try out the application, select the **Edit** link and the **Details** link for one of the movies.</span></span> <span data-ttu-id="44a49-141">인덱스에서 값을 편집한 다음에 유의 하 고 세부 정보 보기, 릴리스 날짜 및 가격 원활 하 게 형식이 지정:</span><span class="sxs-lookup"><span data-stu-id="44a49-141">Notice that in the Index, Edit, and Details views, the release date and price are nicely formatted:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image3.png)

<span data-ttu-id="44a49-142">사용 하 여 결과은 날짜 및 가격에 대 한 서식을 [DisplayFormat](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 특성의 속성에는 `Movie` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-142">The formatting for the date and the price is the result of using the [DisplayFormat](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute on properties of the `Movie` class.</span></span>

<span data-ttu-id="44a49-143">열기는 *Movie.cs* 파일을 주석으로 처리는 `DisplayFormat` 특성에 `ReleaseDate` 및 `Price` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-143">Open the *Movie.cs* file and comment out the `DisplayFormat` attribute on the `ReleaseDate` and `Price` properties.</span></span> <span data-ttu-id="44a49-144">그 결과 `Movie` 클래스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-144">The resulting `Movie` class looks like this:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample1.cs)]

<span data-ttu-id="44a49-145">다시 응용 프로그램을 실행 하 고 선택 하려면 CTRL + f 5는 **홈** 동영상 목록을 보려면 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-145">Press CTRL+F5 again to run the application and select the **Home** tab to view the movie list.</span></span> <span data-ttu-id="44a49-146">이 이번 릴리스 날짜에서 날짜 및 시간을 나타내고 price 필드의 통화 기호를 더 이상 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-146">This time the release date shows the date and time, and the price field no longer shows the currency symbol.</span></span> <span data-ttu-id="44a49-147">변경 내용을 `Movie` 클래스 취소 했 듯이, 좋은 서식을 있지만 잠시 후에를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-147">Your change in the `Movie` class has undone the nice formatting that you saw earlier, but you'll fix that in a moment.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image4.png)

### <a name="using-the-dataannotations-datatype-attribute-to-specify-the-data-type"></a><span data-ttu-id="44a49-148">DataAnnotations 데이터 형식 특성을 사용 하 여 데이터 형식을 지정 하려면</span><span class="sxs-lookup"><span data-stu-id="44a49-148">Using the DataAnnotations DataType Attribute to Specify the Data Type</span></span>

<span data-ttu-id="44a49-149">주석 처리를 대체 `DisplayFormat` 특성에 대 한는 `ReleaseDate` 속성을는 [DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatype.aspx) 특성을 사용 하 여는 `Date` 열거형입니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-149">Replace the commented-out `DisplayFormat` attribute for the `ReleaseDate` property with the [DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatype.aspx) attribute, using the `Date` enumeration.</span></span> <span data-ttu-id="44a49-150">대체는 `DisplayFormat` 특성에 대 한는 `Price` 속성을는 [DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatype.aspx) 특성 다시 사용 하 여이 시간은 `Currency` 열거형입니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-150">Replace the `DisplayFormat` attribute for the `Price` property with the [DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatype.aspx) attribute again, this time using the `Currency` enumeration.</span></span> <span data-ttu-id="44a49-151">다음은 완성 된 코드의 모양을입니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-151">This is what the completed code looks like:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample2.cs)]

<span data-ttu-id="44a49-152">응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-152">Run the application.</span></span> <span data-ttu-id="44a49-153">이제 릴리스 날짜 및 가격 속성은 형식이 잘못 (사용 하 여 적절 한 날짜 및 통화 형식).</span><span class="sxs-lookup"><span data-stu-id="44a49-153">Now the release date and the price properties are formatted correctly (that is, using appropriate date and currency formats).</span></span> <span data-ttu-id="44a49-154">[DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatype.aspx) 특성 형식 메타 데이터를 제공 기본 제공 ASP.NET MVC에 대 한 서식 파일 필드를 올바른 형식으로 렌더링 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-154">The [DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatype.aspx) attribute provides type metadata for the built-in ASP.NET MVC templates so that the fields render in the correct format.</span></span> <span data-ttu-id="44a49-155">사용 하는 `DataType` 특성은 사용 하는 것이 좋습니다는 `DisplayFormat` 때문에 코드에서는 원래 특성의 `DataType` 깔끔하고 국제화 등의 목적에 대해 더 융통성이 특성 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-155">Using the `DataType` attribute is preferable to using the `DisplayFormat` attribute that was originally in the code, because the `DataType` attribute makes the model cleaner and more flexible for purposes like internationalization.</span></span>

<span data-ttu-id="44a49-156">다음 섹션의 날짜 필드를 표시할 사용자 지정 서식 파일을 확인 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="44a49-156">In the next section you'll see how to make custom templates to display date fields.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="44a49-157">다음</span><span class="sxs-lookup"><span data-stu-id="44a49-157">Next</span></span>](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)