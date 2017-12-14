---
uid: mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb
title: "ASP.NET MVC (VB) 15 분 내에 동영상 데이터베이스 응용 프로그램을 만들 | Microsoft Docs"
author: StephenWalther
description: "Stephen Walther 전체 데이터베이스 기반의 ASP.NET MVC 응용 프로그램의 시작 끝나기를 작성 합니다. 이 자습서는 새로운 t 있는 사용자에 게 충분히 소개 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: e4ba9786-734c-4eb3-91bb-089793325d0d
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb
msc.type: authoredcontent
ms.openlocfilehash: 4dbb3804bbb0ccb80506a592f1efb585c5748c2f
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="create-a-movie-database-application-in-15-minutes-with-aspnet-mvc-vb"></a><span data-ttu-id="5113f-104">ASP.NET mvc (VB) 15 분 내에 동영상 데이터베이스 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="5113f-104">Create a Movie Database Application in 15 Minutes with ASP.NET MVC (VB)</span></span>
====================
<span data-ttu-id="5113f-105">으로 [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="5113f-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="5113f-106">코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="5113f-106">Download Code</span></span>](http://download.microsoft.com/download/7/2/8/728F8794-E59A-4D18-9A56-7AD2DB05BD9D/MovieApp_VB.zip)

> <span data-ttu-id="5113f-107">Stephen Walther 전체 데이터베이스 기반의 ASP.NET MVC 응용 프로그램의 시작 끝나기를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-107">Stephen Walther builds an entire database-driven ASP.NET MVC application from start to finish.</span></span> <span data-ttu-id="5113f-108">이 자습서는 ASP.NET MVC 응용 프로그램을 구축 하는 프로세스를 짐작할 배우려는 하 고는 ASP.NET MVC 프레임 워크를 처음 사용에 대 한 훌륭한 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-108">This tutorial is a great introduction for people who are new to the ASP.NET MVC Framework and who want to get a sense of the process of building an ASP.NET MVC application.</span></span>


<span data-ttu-id="5113f-109">이 자습서의 목적은 "어떤 것과 같습니다"의 의미를 제공 하는 ASP.NET MVC 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-109">The purpose of this tutorial is to give you a sense of "what it is like" to build an ASP.NET MVC application.</span></span> <span data-ttu-id="5113f-110">이 자습서에는 전체 ASP.NET MVC 응용 프로그램 작성 시작에서 완료 하는 데 통해 blast 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-110">In this tutorial, I blast through building an entire ASP.NET MVC application from start to finish.</span></span> <span data-ttu-id="5113f-111">I 간단한 데이터베이스 기반 응용 프로그램 목록, 만들기, 하는 방법을 편집 데이터베이스 레코드를 보여 주는 빌드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-111">I show you how to build a simple database-driven application that illustrates how you can list, create, and edit database records.</span></span>

<span data-ttu-id="5113f-112">응용 프로그램을 구축 하는 프로세스를 간소화 하기 위해 Visual Studio 2008의 스 캐 폴딩 기능을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-112">To simplify the process of building our application, we'll take advantage of the scaffolding features of Visual Studio 2008.</span></span> <span data-ttu-id="5113f-113">초기 코드 및이 컨트롤러, 모델 및 보기에 대 한 콘텐츠를 생성 하는 Visual Studio를 알려드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-113">We'll let Visual Studio generate the initial code and content for our controllers, models, and views.</span></span>

<span data-ttu-id="5113f-114">Active Server Pages 또는 ASP.NET으로 작업 하는 경우 다음 찾아야 ASP.NET MVC 친숙 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-114">If you have worked with Active Server Pages or ASP.NET, then you should find ASP.NET MVC very familiar.</span></span> <span data-ttu-id="5113f-115">ASP.NET MVC 뷰는 Active Server Pages 응용 프로그램의 페이지과 매우 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-115">ASP.NET MVC views are very much like the pages in an Active Server Pages application.</span></span> <span data-ttu-id="5113f-116">와 기존의 ASP.NET Web Forms 응용 프로그램과 마찬가지로 ASP.NET MVC를 제공은 다양 한 언어 및.NET framework에서 제공 하는 클래스에 대 한 전체 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-116">And, just like a traditional ASP.NET Web Forms application, ASP.NET MVC provides you with full access to the rich set of languages and classes provided by the .NET framework.</span></span>

<span data-ttu-id="5113f-117">좋겠습니다는이 자습서를 알려는 방법에 대 ASP.NET MVC 응용 프로그램을 작성 하는 환경을 유사한 및 다른 Active Server Pages 또는 ASP.NET Web Forms 응용 프로그램을 작성 하는 환경을 보다 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-117">My hope is that this tutorial will give you a sense of how the experience of building an ASP.NET MVC application is both similar and different than the experience of building an Active Server Pages or ASP.NET Web Forms application.</span></span>

## <a name="overview-of-the-movie-database-application"></a><span data-ttu-id="5113f-118">영화 데이터베이스 응용 프로그램의 개요</span><span class="sxs-lookup"><span data-stu-id="5113f-118">Overview of the Movie Database Application</span></span>

<span data-ttu-id="5113f-119">이러한 목표를 간단 하 게 하므로 매우 간단한 영화 데이터베이스 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-119">Because our goal is to keep things simple, we'll build a very simple Movie Database application.</span></span> <span data-ttu-id="5113f-120">영화 데이터베이스 응용 프로그램에서 세 가지를 수행 하는 것을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-120">Our simple Movie Database application will allow us to do three things:</span></span>

1. <span data-ttu-id="5113f-121">영화 데이터베이스 레코드 집합 나열</span><span class="sxs-lookup"><span data-stu-id="5113f-121">List a set of movie database records</span></span>
2. <span data-ttu-id="5113f-122">새 동영상 데이터베이스 레코드를 만듭니다</span><span class="sxs-lookup"><span data-stu-id="5113f-122">Create a new movie database record</span></span>
3. <span data-ttu-id="5113f-123">기존 영화 데이터베이스 레코드를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-123">Edit an existing movie database record</span></span>

<span data-ttu-id="5113f-124">다시, 간단 하 게 유지 하고자 하기 때문에 응용 프로그램을 빌드하는 데 필요한 ASP.NET MVC 프레임 워크의 기능의 최소 수의 장점은 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-124">Again, because we want to keep things simple, we'll take advantage of the minimum number of features of the ASP.NET MVC framework needed to build our application.</span></span> <span data-ttu-id="5113f-125">예를 들어 우리 않습니다 활용 기반 개발 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-125">For example, we won't be taking advantage of Test-Driven Development.</span></span>

<span data-ttu-id="5113f-126">응용 프로그램을 만들려면 각 다음 단계를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-126">In order to create our application, we need to complete each of the following steps:</span></span>

1. <span data-ttu-id="5113f-127">ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="5113f-127">Create the ASP.NET MVC Web Application Project</span></span>
2. <span data-ttu-id="5113f-128">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="5113f-128">Create the database</span></span>
3. <span data-ttu-id="5113f-129">데이터베이스 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="5113f-129">Create the database model</span></span>
4. <span data-ttu-id="5113f-130">ASP.NET MVC 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="5113f-130">Create the ASP.NET MVC controller</span></span>
5. <span data-ttu-id="5113f-131">ASP.NET MVC 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="5113f-131">Create the ASP.NET MVC views</span></span>

## <a name="preliminaries"></a><span data-ttu-id="5113f-132">준비 단계</span><span class="sxs-lookup"><span data-stu-id="5113f-132">Preliminaries</span></span>

<span data-ttu-id="5113f-133">Visual Studio 2008 또는 Visual Web Developer 2008 Express는 ASP.NET MVC 응용 프로그램을 빌드하는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-133">You'll need either Visual Studio 2008 or Visual Web Developer 2008 Express to build an ASP.NET MVC application.</span></span> <span data-ttu-id="5113f-134">ASP.NET MVC 프레임 워크를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-134">You also need to download the ASP.NET MVC framework.</span></span>

<span data-ttu-id="5113f-135">Visual Studio 2008를 소유 하지 않는 경우 Visual Studio 2008의 90 일 평가판이 웹이 사이트에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-135">If you don't own Visual Studio 2008, then you can download a 90 day trial version of Visual Studio 2008 from this website:</span></span>

[<span data-ttu-id="5113f-136">https://msdn.microsoft.com/en-us/vs2008/products/cc268305.aspx</span><span class="sxs-lookup"><span data-stu-id="5113f-136">https://msdn.microsoft.com/en-us/vs2008/products/cc268305.aspx</span></span>](https://msdn.microsoft.com/en-us/vs2008/products/cc268305.aspx)

<span data-ttu-id="5113f-137">또는 만들 수 있습니다 ASP.NET MVC 응용 프로그램 Visual Web Developer Express 2008을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-137">Alternatively, you can create ASP.NET MVC applications with Visual Web Developer Express 2008.</span></span> <span data-ttu-id="5113f-138">Visual Web Developer Express를 사용 하려는 경우 서비스 팩 1을 갖고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-138">If you decide to use Visual Web Developer Express then you must have Service Pack 1 installed.</span></span> <span data-ttu-id="5113f-139">Visual Web Developer 2008 Express 서비스 팩 1이 웹 사이트에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-139">You can download Visual Web Developer 2008 Express with Service Pack 1 from this website:</span></span>

[<span data-ttu-id="5113f-140">https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;4a83-b309-53b7b77edf78&displaylang = en</span><span class="sxs-lookup"><span data-stu-id="5113f-140">https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en</span></span>](https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en)

<span data-ttu-id="5113f-141">Visual Studio 2008 또는 Visual Web Developer 2008을 설치한 후 ASP.NET MVC 프레임 워크를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-141">After you install either Visual Studio 2008 or Visual Web Developer 2008, you need to install the ASP.NET MVC framework.</span></span> <span data-ttu-id="5113f-142">다음 웹 사이트에서 ASP.NET MVC 프레임 워크를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-142">You can download the ASP.NET MVC framework from the following website:</span></span>

[<span data-ttu-id="5113f-143">https://www.asp.net/mvc/</span><span class="sxs-lookup"><span data-stu-id="5113f-143">https://www.asp.net/mvc/</span></span>](../../../index.md)

> [!NOTE] 
> 
> <span data-ttu-id="5113f-144">ASP.NET 프레임 워크 및 ASP.NET MVC 프레임 워크를 개별적으로 다운로드 하는 대신 웹 플랫폼 설치 관리자를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-144">Instead of downloading the ASP.NET framework and the ASP.NET MVC framework individually, you can take advantage of the Web Platform Installer.</span></span> <span data-ttu-id="5113f-145">웹 플랫폼 설치 관리자는 설치 된 응용 프로그램을 쉽게 관리할 수 있도록 하는 응용 프로그램은 사용자의 컴퓨터:</span><span class="sxs-lookup"><span data-stu-id="5113f-145">The Web Platform Installer is an application that enables you to easily manage the installed applications are your computer:</span></span>
> 
> [<span data-ttu-id="5113f-146">https://www.microsoft.com/web/gallery/Install.aspx</span><span class="sxs-lookup"><span data-stu-id="5113f-146">https://www.microsoft.com/web/gallery/Install.aspx</span></span>](https://www.microsoft.com/web/gallery/Install.aspx)


## <a name="creating-an-aspnet-mvc-web-application-project"></a><span data-ttu-id="5113f-147">ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="5113f-147">Creating an ASP.NET MVC Web Application Project</span></span>

<span data-ttu-id="5113f-148">Visual Studio 2008에서 새 ASP.NET MVC 웹 응용 프로그램 프로젝트를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-148">Let's start by creating a new ASP.NET MVC Web Application project in Visual Studio 2008.</span></span> <span data-ttu-id="5113f-149">메뉴 옵션을 선택 **파일, 새 프로젝트** 그림 1의 새 프로젝트 대화 상자를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-149">Select the menu option **File, New Project** and you will see the New Project dialog box in Figure 1.</span></span> <span data-ttu-id="5113f-150">프로그래밍 언어와 Visual Basic을 선택 하 고 ASP.NET MVC 웹 응용 프로그램 프로젝트 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-150">Select Visual Basic as the programming language and select the ASP.NET MVC Web Application project template.</span></span> <span data-ttu-id="5113f-151">프로젝트 이름을 MovieApp를 지정 하 고 확인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-151">Give your project the name MovieApp and click the OK button.</span></span>


<span data-ttu-id="5113f-152">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5113f-152">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.png)</span></span>

<span data-ttu-id="5113f-153">**그림 01**:의 새 프로젝트 대화 상자 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="5113f-153">**Figure 01**: The New Project dialog box ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.png))</span></span>


<span data-ttu-id="5113f-154">새 프로젝트 대화 상자 맨 위에 있는 드롭다운 목록에서.NET Framework 3.5를 선택 하거나 ASP.NET MVC 웹 응용 프로그램 프로젝트 템플릿이 나타나지 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-154">Make sure that you select .NET Framework 3.5 from the dropdown list at the top of the New Project dialog or the ASP.NET MVC Web Application project template won't appear.</span></span>


<span data-ttu-id="5113f-155">새 MVC 웹 응용 프로그램 프로젝트를 만들 때마다 Visual Studio 별도 단위 테스트 프로젝트를 만들 것인지 묻는 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-155">Whenever you create a new MVC Web Application project, Visual Studio prompts you to create a separate unit test project.</span></span> <span data-ttu-id="5113f-156">그림 2에 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-156">The dialog in Figure 2 appears.</span></span> <span data-ttu-id="5113f-157">이어서 우리가 않습니다 수 만들고 테스트가이 자습서에서는 시간 제약 조건으로 인해 (예,이 대 한 약간 어느 정도 느끼는 해야) 선택은 **아니요** 옵션는 **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-157">Because we won't be creating tests in this tutorial because of time constraints (and, yes, we should feel a little guilty about this) select the **No** option and click the **OK** button.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5113f-158">Visual Web Developer에서 테스트 프로젝트를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-158">Visual Web Developer does not support test projects.</span></span>


<span data-ttu-id="5113f-159">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="5113f-159">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.png)</span></span>

<span data-ttu-id="5113f-160">**그림 02**: The 단위 테스트 프로젝트 만들기 대화 상자 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="5113f-160">**Figure 02**: The Create Unit Test Project dialog ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.png))</span></span>


<span data-ttu-id="5113f-161">ASP.NET MVC 응용 프로그램에 표준 집합이 폴더: 모델, 뷰 및 컨트롤러 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-161">An ASP.NET MVC application has a standard set of folders: a Models, Views, and Controllers folder.</span></span> <span data-ttu-id="5113f-162">솔루션 탐색기 창에서 폴더의이 표준 집합을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-162">You can see this standard set of folders in the Solution Explorer window.</span></span> <span data-ttu-id="5113f-163">영화 데이터베이스 응용 프로그램을 작성 하기 위해 각 모델, 뷰 및 컨트롤러 폴더에 파일을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-163">We'll need to add files to each of the Models, Views, and Controllers folders in order to build our Movie Database application.</span></span>

<span data-ttu-id="5113f-164">Visual Studio와 함께 새 MVC 응용 프로그램을 만들 때에 샘플 응용 프로그램을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-164">When you create a new MVC application with Visual Studio, you get a sample application.</span></span> <span data-ttu-id="5113f-165">처음부터 다시 시작 하려는 것 이므로이 샘플 응용 프로그램에 대 한 콘텐츠를 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-165">Because we want to start from scratch, we need to delete the content for this sample application.</span></span> <span data-ttu-id="5113f-166">다음 파일 및 폴더를 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-166">You need to delete the following file and the following folder:</span></span>

- <span data-ttu-id="5113f-167">Controllers\HomeController.vb</span><span class="sxs-lookup"><span data-stu-id="5113f-167">Controllers\HomeController.vb</span></span>
- <span data-ttu-id="5113f-168">Views\Home</span><span class="sxs-lookup"><span data-stu-id="5113f-168">Views\Home</span></span>

## <a name="creating-the-database"></a><span data-ttu-id="5113f-169">데이터베이스를 만드는 중</span><span class="sxs-lookup"><span data-stu-id="5113f-169">Creating the Database</span></span>

<span data-ttu-id="5113f-170">영화 데이터베이스 레코드를 보관할 데이터베이스를 만들려는 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-170">We need to create a database to hold our movie database records.</span></span> <span data-ttu-id="5113f-171">다행히도 Visual Studio 라는 SQL Server Express는 무료 데이터베이스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-171">Luckily, Visual Studio includes a free database named SQL Server Express.</span></span> <span data-ttu-id="5113f-172">데이터베이스를 만들려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-172">Follow these steps to create the database:</span></span>

1. <span data-ttu-id="5113f-173">응용 프로그램을 마우스 오른쪽 단추로 클릭\_메뉴 옵션을 선택 하는 솔루션 탐색기 창에서 데이터 폴더 **추가, 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-173">Right-click the App\_Data folder in the Solution Explorer window and select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="5113f-174">선택 된 **데이터** 범주를 선택은 **SQL Server 데이터베이스** 서식 파일 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="5113f-174">Select the **Data** category and select the **SQL Server Database** template (see Figure 3).</span></span>
3. <span data-ttu-id="5113f-175">새 사용자 데이터베이스 이름을 *MoviesDB.mdf* 클릭는 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-175">Name your new database *MoviesDB.mdf* and click the **Add** button.</span></span>

<span data-ttu-id="5113f-176">앱에 있는 MoviesDB.mdf 파일을 두 번 클릭 하 여 데이터베이스에 연결할 수 데이터베이스를 만든 후\_데이터 폴더.</span><span class="sxs-lookup"><span data-stu-id="5113f-176">After you create your database, you can connect to the database by double-clicking the MoviesDB.mdf file located in the App\_Data folder.</span></span> <span data-ttu-id="5113f-177">MoviesDB.mdf 파일을 두 번 클릭 하면 서버 탐색기 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-177">Double-clicking the MoviesDB.mdf file opens the Server Explorer window.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5113f-178">서버 탐색기 창이 Visual Web Developer의 경우 데이터베이스 탐색기 창이 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-178">The Server Explorer window is named the Database Explorer window in the case of Visual Web Developer.</span></span>


<span data-ttu-id="5113f-179">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="5113f-179">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.png)</span></span>

<span data-ttu-id="5113f-180">**그림 03**: Microsoft SQL Server 데이터베이스 만들기 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="5113f-180">**Figure 03**: Creating a Microsoft SQL Server Database ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.png))</span></span>


<span data-ttu-id="5113f-181">다음으로 새 데이터베이스 테이블을 만들 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-181">Next, we need to create a new database table.</span></span> <span data-ttu-id="5113f-182">서버 탐색기 창 내에서 테이블 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **새 테이블 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-182">From within the Sever Explorer window, right-click the Tables folder and select the menu option **Add New Table**.</span></span> <span data-ttu-id="5113f-183">이 메뉴 옵션을 선택 하면 데이터베이스 테이블 디자이너를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-183">Selecting this menu option opens the database table designer.</span></span> <span data-ttu-id="5113f-184">다음 데이터베이스 열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-184">Create the following database columns:</span></span>

<a id="0.2_table01"></a>


| <span data-ttu-id="5113f-185">**열 이름**</span><span class="sxs-lookup"><span data-stu-id="5113f-185">**Column Name**</span></span> | <span data-ttu-id="5113f-186">**데이터 형식**</span><span class="sxs-lookup"><span data-stu-id="5113f-186">**Data Type**</span></span> | <span data-ttu-id="5113f-187">**Null 허용**</span><span class="sxs-lookup"><span data-stu-id="5113f-187">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5113f-188">ID</span><span class="sxs-lookup"><span data-stu-id="5113f-188">Id</span></span> | <span data-ttu-id="5113f-189">Int</span><span class="sxs-lookup"><span data-stu-id="5113f-189">Int</span></span> | <span data-ttu-id="5113f-190">False</span><span class="sxs-lookup"><span data-stu-id="5113f-190">False</span></span> |
| <span data-ttu-id="5113f-191">제목</span><span class="sxs-lookup"><span data-stu-id="5113f-191">Title</span></span> | <span data-ttu-id="5113f-192">Nvarchar (100)</span><span class="sxs-lookup"><span data-stu-id="5113f-192">Nvarchar(100)</span></span> | <span data-ttu-id="5113f-193">False</span><span class="sxs-lookup"><span data-stu-id="5113f-193">False</span></span> |
| <span data-ttu-id="5113f-194">감독</span><span class="sxs-lookup"><span data-stu-id="5113f-194">Director</span></span> | <span data-ttu-id="5113f-195">Nvarchar (100)</span><span class="sxs-lookup"><span data-stu-id="5113f-195">Nvarchar(100)</span></span> | <span data-ttu-id="5113f-196">False</span><span class="sxs-lookup"><span data-stu-id="5113f-196">False</span></span> |
| <span data-ttu-id="5113f-197">DateReleased</span><span class="sxs-lookup"><span data-stu-id="5113f-197">DateReleased</span></span> | <span data-ttu-id="5113f-198">DateTime</span><span class="sxs-lookup"><span data-stu-id="5113f-198">DateTime</span></span> | <span data-ttu-id="5113f-199">False</span><span class="sxs-lookup"><span data-stu-id="5113f-199">False</span></span> |


<span data-ttu-id="5113f-200">첫 번째 열, Id 열에 두 특수 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-200">The first column, the Id column, has two special properties.</span></span> <span data-ttu-id="5113f-201">먼저, Id 열 기본 키 열으로 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-201">First, you need to mark the Id column as the primary key column.</span></span> <span data-ttu-id="5113f-202">Id 열을 선택한 다음 클릭는 **기본 키 설정** 단추 (이 키를 처럼 생긴 아이콘).</span><span class="sxs-lookup"><span data-stu-id="5113f-202">After selecting the Id column, click the **Set Primary Key** button (it is the icon that looks like a key).</span></span> <span data-ttu-id="5113f-203">둘째, Id 열을 Id 열으로 표시 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-203">Second, you need to mark the Id column as an Identity column.</span></span> <span data-ttu-id="5113f-204">열 속성 창에서 Id 사양 섹션까지 아래로 스크롤한 다음 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-204">In the Column Properties window, scroll down to the Identity Specification section and expand it.</span></span> <span data-ttu-id="5113f-205">변경 된 **Id** 속성 값을 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-205">Change the **Is Identity** property to the value **Yes**.</span></span> <span data-ttu-id="5113f-206">작업을 완료 하는 경우 테이블 그림 4와 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-206">When you are finished, the table should look like Figure 4.</span></span>


<span data-ttu-id="5113f-207">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="5113f-207">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.png)</span></span>

<span data-ttu-id="5113f-208">**그림 04**: The 영화 데이터베이스 테이블 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="5113f-208">**Figure 04**: The Movies database table ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.png))</span></span>


<span data-ttu-id="5113f-209">새 테이블을 저장 하는 최종 단계가입니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-209">The final step is to save the new table.</span></span> <span data-ttu-id="5113f-210">저장 단추 (플로피 아이콘)를 클릭 하 고 새 테이블 이름을 영화를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-210">Click the Save button (the icon of the floppy) and give the new table the name Movies.</span></span>

<span data-ttu-id="5113f-211">테이블 생성을 완료 한 후 테이블에 일부 영화 레코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-211">After you finish creating the table, add some movie records to the table.</span></span> <span data-ttu-id="5113f-212">서버 탐색기 창에 동영상 테이블을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **테이블 데이터 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-212">Right-click the Movies table in the Server Explorer window and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="5113f-213">(그림 5 참조) 하 여 좋아하는 영화 목록을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-213">Enter a list of your favorite movies (see Figure 5).</span></span>


<span data-ttu-id="5113f-214">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="5113f-214">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.png)</span></span>

<span data-ttu-id="5113f-215">**그림 05**: 영화 레코드 입력 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="5113f-215">**Figure 05**: Entering movie records ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.png))</span></span>


## <a name="creating-the-model"></a><span data-ttu-id="5113f-216">모델 만들기</span><span class="sxs-lookup"><span data-stu-id="5113f-216">Creating the Model</span></span>

<span data-ttu-id="5113f-217">다음 데이터베이스를 표현 하는 클래스 집합을 만들 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-217">We next need to create a set of classes to represent our database.</span></span> <span data-ttu-id="5113f-218">데이터베이스 모델을 만드는 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-218">We need to create a database model.</span></span> <span data-ttu-id="5113f-219">예제의 데이터베이스 모델에 대 한 클래스를 자동으로 생성 하기 위해 Microsoft 엔터티 프레임 워크의 장점은 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-219">We'll take advantage of the Microsoft Entity Framework to generate the classes for our database model automatically.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5113f-220">ASP.NET MVC 프레임 워크는 Microsoft Entity Framework 연결 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-220">The ASP.NET MVC framework is not tied to the Microsoft Entity Framework.</span></span> <span data-ttu-id="5113f-221">다양 한 개체 관계형 매핑을 사용 하 여 데이터베이스에 모델 클래스를 만들 수 있습니다 (또는 / M) 도구 LINQ to SQL, subsonic은 이러한 방식을, 및 NHibernate를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-221">You can create your database model classes by taking advantage of a variety of Object Relational Mapping (OR/M) tools including LINQ to SQL, Subsonic, and NHibernate.</span></span>


<span data-ttu-id="5113f-222">엔터티 데이터 모델 마법사를 시작 하려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-222">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="5113f-223">솔루션 탐색기 창 및 메뉴 옵션 선택 모델 폴더를 마우스 오른쪽 단추로 클릭 **추가, 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-223">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="5113f-224">선택 된 **데이터** 범주를 선택은 **ADO.NET 엔터티 데이터 모델** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="5113f-224">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="5113f-225">데이터 모델 이름을 *MoviesDBModel.edmx* 클릭는 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-225">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="5113f-226">추가 단추를 클릭 한 후에 엔터티 데이터 모델 마법사 나타납니다 (그림 6 참조).</span><span class="sxs-lookup"><span data-stu-id="5113f-226">After you click the Add button, the Entity Data Model Wizard appears (see Figure 6).</span></span> <span data-ttu-id="5113f-227">마법사를 완료 하려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-227">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="5113f-228">에 **모델 콘텐츠 선택** 선택 단계는 **데이터베이스에서 생성** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-228">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="5113f-229">에 **데이터 연결 선택** 단계를 사용 하 여는 *MoviesDB.mdf* 데이터 연결 및 이름 *MoviesDBEntities* 연결 설정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-229">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="5113f-230">클릭는 **다음** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-230">Click the **Next** button.</span></span>
3. <span data-ttu-id="5113f-231">에 **데이터베이스 개체 선택** 단계, 테이블 노드를 확장 하 고, 영화 테이블을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-231">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="5113f-232">네임 스페이스를 입력 *MovieApp.Models* 클릭는 **마침** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-232">Enter the namespace *MovieApp.Models* and click the **Finish** button.</span></span>


<span data-ttu-id="5113f-233">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="5113f-233">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.png)</span></span>

<span data-ttu-id="5113f-234">**그림 06**: 엔터티 데이터 모델 마법사를 사용 하 여 데이터베이스 모델 생성 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="5113f-234">**Figure 06**: Generating a database model with the Entity Data Model Wizard ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.png))</span></span>


<span data-ttu-id="5113f-235">엔터티 데이터 모델 마법사를 완료 한 후 엔터티 데이터 모델 디자이너가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-235">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="5113f-236">디자이너는 영화 데이터베이스 테이블에 표시 됩니다 (그림 7 참조).</span><span class="sxs-lookup"><span data-stu-id="5113f-236">The Designer should display the Movies database table (see Figure 7).</span></span>


<span data-ttu-id="5113f-237">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="5113f-237">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.png)</span></span>

<span data-ttu-id="5113f-238">**그림 07**: The 엔터티 데이터 모델 디자이너 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="5113f-238">**Figure 07**: The Entity Data Model Designer ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.png))</span></span>


<span data-ttu-id="5113f-239">계속 하기 전에 하나의 변경 내용을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-239">We need to make one change before we continue.</span></span> <span data-ttu-id="5113f-240">엔터티 데이터 마법사 영화 데이터베이스 테이블을 나타내는 동영상 이라는 모델 클래스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-240">The Entity Data Wizard generates a model class named Movies that represents the Movies database table.</span></span> <span data-ttu-id="5113f-241">영화 클래스 사용 하 여 특정 영화를 나타내는 합니다, 하므로 되려면 클래스의 이름을 수정 해야 *영화* 대신 *영화* (단 수 아님 복수).</span><span class="sxs-lookup"><span data-stu-id="5113f-241">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="5113f-242">디자이너 화면의 클래스 이름을 두 번 클릭 하 고 동영상에서 영화 클래스의 이름을 변경 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5113f-242">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="5113f-243">이 변경 후 클릭는 **저장** 단추 (플로피 디스크 아이콘)를 영화 클래스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-243">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="creating-the-aspnet-mvc-controller"></a><span data-ttu-id="5113f-244">ASP.NET MVC 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="5113f-244">Creating the ASP.NET MVC Controller</span></span>

<span data-ttu-id="5113f-245">다음 단계는 ASP.NET MVC 컨트롤러를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-245">The next step is to create the ASP.NET MVC controller.</span></span> <span data-ttu-id="5113f-246">컨트롤러는 사용자 간의 ASP.NET MVC 응용 프로그램 상호 작용 하는 방식을 제어 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-246">A controller is responsible for controlling how a user interacts with an ASP.NET MVC application.</span></span>

<span data-ttu-id="5113f-247">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-247">Follow these steps:</span></span>

1. <span data-ttu-id="5113f-248">솔루션 탐색기 창에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **추가, 컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-248">In the Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller**.</span></span>
2. <span data-ttu-id="5113f-249">컨트롤러 추가 대화 상자에 이름을 입력 *HomeController* 하 고 레이블이 확인란 **만들기, 업데이트 및 세부 정보 시나리오에 대 한 작업 메서드를 추가** (그림 8 참조).</span><span class="sxs-lookup"><span data-stu-id="5113f-249">In the Add Controller dialog, enter the name *HomeController* and check the checkbox labeled **Add action methods for Create, Update, and Details scenarios** (see Figure 8).</span></span>
3. <span data-ttu-id="5113f-250">클릭는 **추가** 단추를 프로젝트에 새 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-250">Click the **Add** button to add the new controller to your project.</span></span>

<span data-ttu-id="5113f-251">다음이 단계를 완료 한 후 목록 1의 컨트롤러가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-251">After you complete these steps, the controller in Listing 1 is created.</span></span> <span data-ttu-id="5113f-252">인덱스 세부 정보, 만들기, 명명 된 메서드에 있음 및 편집.</span><span class="sxs-lookup"><span data-stu-id="5113f-252">Notice that it contains methods named Index, Details, Create, and Edit.</span></span> <span data-ttu-id="5113f-253">다음 섹션에서 작동 하도록 이러한 메서드를 얻으려고 하는 데 필요한 코드를 추가 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-253">In the following sections, we'll add the necessary code to get these methods to work.</span></span>


<span data-ttu-id="5113f-254">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="5113f-254">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image15.png)</span></span>

<span data-ttu-id="5113f-255">**그림 08**: 새 ASP.NET MVC 컨트롤러 추가 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="5113f-255">**Figure 08**: Adding a new ASP.NET MVC Controller ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image16.png))</span></span>


<span data-ttu-id="5113f-256">**1 – Controllers\HomeController.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="5113f-256">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample1.vb)]

## <a name="listing-database-records"></a><span data-ttu-id="5113f-257">데이터베이스 레코드 목록</span><span class="sxs-lookup"><span data-stu-id="5113f-257">Listing Database Records</span></span>

<span data-ttu-id="5113f-258">Home 컨트롤러의 index () 메서드는 ASP.NET MVC 응용 프로그램에 대 한 기본 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-258">The Index() method of the Home controller is the default method for an ASP.NET MVC application.</span></span> <span data-ttu-id="5113f-259">ASP.NET MVC 응용 프로그램을 실행 하면 index () 메서드는 첫 번째 컨트롤러 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-259">When you run an ASP.NET MVC application, the Index() method is the first controller method that is called.</span></span>

<span data-ttu-id="5113f-260">영화 데이터베이스 테이블에서 레코드의 목록을 표시 하는 index () 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-260">We'll use the Index() method to display the list of records from the Movies database table.</span></span> <span data-ttu-id="5113f-261">데이터베이스의 이점은 index () 메서드와 함께 영화 데이터베이스 레코드를 검색 하려면 앞에서 만든 모델 클래스 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-261">We'll take advantage of the database model classes that we created earlier to retrieve the movie database records with the Index() method.</span></span>

<span data-ttu-id="5113f-262">라는 새 개인 필드가 포함 되도록 코드 2에서 HomeController 클래스를 수정한 후 I \_db입니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-262">I've modified the HomeController class in Listing 2 so that it contains a new private field named \_db.</span></span> <span data-ttu-id="5113f-263">MoviesDBEntities 클래스는 데이터베이스 모델 나타내며이 클래스는 데이터베이스와 통신을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-263">The MoviesDBEntities class represents our database model and we'll use this class to communicate with our database.</span></span>

<span data-ttu-id="5113f-264">또한 목록 2의 index () 메서드를 수정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-264">I've also modified the Index() method in Listing 2.</span></span> <span data-ttu-id="5113f-265">Index () 메서드 MoviesDBEntities 클래스를 사용 하 여 영화 데이터베이스 테이블에서 모든 동영상 레코드를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-265">The Index() method uses the MoviesDBEntities class to retrieve all of the movie records from the Movies database table.</span></span> <span data-ttu-id="5113f-266">식  *\_db입니다. MovieSet.ToList()* 영화 데이터베이스 테이블에서 모든 동영상 레코드의 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-266">The expression *\_db.MovieSet.ToList()* returns a list of all of the movie records from the Movies database table.</span></span>

<span data-ttu-id="5113f-267">영화 목록이 뷰에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-267">The list of movies is passed to the view.</span></span> <span data-ttu-id="5113f-268">데이터 보기와 보기에 전달 되 View() 메서드에 전달 되는 모든 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-268">Anything that gets passed to the View() method gets passed to the view as view data.</span></span>

<span data-ttu-id="5113f-269">**2 – Controllers/HomeController.vb (수정 된 인덱스 메서드)를 나열 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5113f-269">**Listing 2 – Controllers/HomeController.vb (modified Index method)**</span></span>

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample2.vb)]

<span data-ttu-id="5113f-270">Index () 메서드 라는 인덱스 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-270">The Index() method returns a view named Index.</span></span> <span data-ttu-id="5113f-271">영화 데이터베이스 레코드의 목록을 표시 하려면이 보기를 만드는 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-271">We need to create this view to display the list of movie database records.</span></span> <span data-ttu-id="5113f-272">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-272">Follow these steps:</span></span>


<span data-ttu-id="5113f-273">프로젝트가 빌드되어야 (메뉴 옵션을 선택 **빌드, 솔루션 빌드**) 열기 전에 **뷰 추가** 없는 클래스 또는 대화 상자에 표시 됩니다는 **데이터 클래스 보기** 드롭다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-273">You should build your project (select the menu option **Build, Build Solution**) before opening the **Add View** dialog or no classes will appear in the **View data class** dropdown list.</span></span>


1. <span data-ttu-id="5113f-274">코드 편집기에서 index () 메서드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **뷰 추가** (그림 9 참조).</span><span class="sxs-lookup"><span data-stu-id="5113f-274">Right-click the Index() method in the code editor and select the menu option **Add View** (see Figure 9).</span></span>
2. <span data-ttu-id="5113f-275">뷰 추가 대화 상자에서 레이블이 지정 된 확인란 확인 **강력한 형식의 뷰 만들기** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-275">In the Add View dialog, verify that the checkbox labeled **Create a strongly-typed view** is checked.</span></span>
3. <span data-ttu-id="5113f-276">**콘텐츠를 볼** 드롭다운 목록에서 값을 선택 *목록*합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-276">From the **View content** dropdown list, select the value *List*.</span></span>
4. <span data-ttu-id="5113f-277">**데이터 클래스 보기** 드롭다운 목록에서 값을 선택 *MovieApp.Movie*합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-277">From the **View data class** dropdown list, select the value *MovieApp.Movie*.</span></span>
5. <span data-ttu-id="5113f-278">새 만들려는 추가 단추를 클릭 (그림 10 참조)를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-278">Click the Add button to create the new view (see Figure 10).</span></span>

<span data-ttu-id="5113f-279">다음이 단계를 완료 한 후 Index.aspx 라는 새 뷰로 Views\Home 폴더에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-279">After you complete these steps, a new view named Index.aspx is added to the Views\Home folder.</span></span> <span data-ttu-id="5113f-280">인덱스 보기의 내용은 보기 3에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-280">The contents of the Index view are included in Listing 3.</span></span>


<span data-ttu-id="5113f-281">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="5113f-281">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image17.png)</span></span>

<span data-ttu-id="5113f-282">**그림 09**: 컨트롤러 동작으로 인해 뷰 추가 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="5113f-282">**Figure 09**: Adding a view from a controller action ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image18.png))</span></span>


<span data-ttu-id="5113f-283">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="5113f-283">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image19.png)</span></span>

<span data-ttu-id="5113f-284">**그림 10**: 뷰 추가 대화 상자를 사용 하 여 새 보기 만들기 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="5113f-284">**Figure 10**: Creating a new view with the Add View dialog ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image20.png))</span></span>


[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample3.aspx)]

<span data-ttu-id="5113f-285">인덱스 뷰는 모든 HTML 테이블 내에서 영화 데이터베이스 테이블에서 영화 레코드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-285">The Index view displays all of the movie records from the Movies database table within an HTML table.</span></span> <span data-ttu-id="5113f-286">뷰에 For Each 루프 ViewData.Model 속성으로 표현 되는 각 동영상을 반복 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-286">The view contains a For Each loop that iterates through each movie represented by the ViewData.Model property.</span></span> <span data-ttu-id="5113f-287">그런 다음 F5 키를 클릭 하 여 응용 프로그램을 실행할 그림 11에서 웹 페이지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-287">If you run your application by hitting the F5 key, then you'll see the web page in Figure 11.</span></span>


<span data-ttu-id="5113f-288">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="5113f-288">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image21.png)</span></span>

<span data-ttu-id="5113f-289">**그림 11**: The 인덱스 보기 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image22.png))</span><span class="sxs-lookup"><span data-stu-id="5113f-289">**Figure 11**: The Index view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image22.png))</span></span>


## <a name="creating-new-database-records"></a><span data-ttu-id="5113f-290">새 데이터베이스 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="5113f-290">Creating New Database Records</span></span>

<span data-ttu-id="5113f-291">이전 섹션에서 만든 인덱스 보기에는 새 데이터베이스 레코드를 만들기 위한 링크가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-291">The Index view that we created in the previous section includes a link for creating new database records.</span></span> <span data-ttu-id="5113f-292">계속 해 서 논리를 구현 하 고 새 동영상 데이터베이스 레코드를 만드는 데 필요한 보기를 만드는 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-292">Let's go ahead and implement the logic and create the view necessary for creating new movie database records.</span></span>

<span data-ttu-id="5113f-293">Home 컨트롤러 create ()를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-293">The Home controller contains two methods named Create().</span></span> <span data-ttu-id="5113f-294">첫 번째 create () 메서드 매개 변수가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-294">The first Create() method has no parameters.</span></span> <span data-ttu-id="5113f-295">Create () 메서드의이 오버 로드는 새 동영상 데이터베이스 레코드를 만들기 위한 HTML 폼을 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-295">This overload of the Create() method is used to display the HTML form for creating a new movie database record.</span></span>

<span data-ttu-id="5113f-296">두 번째 create () 메서드가 FormCollection 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-296">The second Create() method has a FormCollection parameter.</span></span> <span data-ttu-id="5113f-297">Create () 메서드의이 오버 로드는 새 동영상을 만들기 위한 HTML 폼이 서버에 게시 될 때 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-297">This overload of the Create() method is called when the HTML form for creating a new movie is posted to the server.</span></span> <span data-ttu-id="5113f-298">이 두 번째 create () 메서드는 메서드가 HTTP Post 작업을 수행 하지 않는 한 호출 하지 못하도록 방지 AcceptVerbs 특성이 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-298">Notice that this second Create() method has an AcceptVerbs attribute that prevents the method from being called unless an HTTP Post operation is performed.</span></span>

<span data-ttu-id="5113f-299">이 두 번째 create () 메서드 목록 4에 업데이트 된 HomeController 클래스에서 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-299">This second Create() method has been modified in the updated HomeController class in Listing 4.</span></span> <span data-ttu-id="5113f-300">새 버전의 create () 메서드 영화 매개 변수를 받아들이고 새 동영상 영화 데이터베이스 테이블에 삽입 하기 위한 논리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-300">The new version of the Create() method accepts a Movie parameter and contains the logic for inserting a new movie into the Movies database table.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5113f-301">바인딩 특성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-301">Notice the Bind attribute.</span></span> <span data-ttu-id="5113f-302">않기 때문에 HTML 양식 으로부터 영화 Id 속성을 업데이트 하려면,이 속성을 명시적으로 제외 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-302">Because we don't want to update the Movie Id property from HTML form, we need to explicitly exclude this property.</span></span>


<span data-ttu-id="5113f-303">**4 – Controllers\HomeController.vb (수정 된 Create 메서드)를 나열 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5113f-303">**Listing 4 – Controllers\HomeController.vb (modified Create method)**</span></span>

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample4.vb)]

<span data-ttu-id="5113f-304">Visual Studio에서는 새 동영상 데이터베이스를 만들기 위한 양식을 만드는 쉽게 (그림 12 참조)를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-304">Visual Studio makes it easy to create the form for creating a new movie database record (see Figure 12).</span></span> <span data-ttu-id="5113f-305">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-305">Follow these steps:</span></span>

1. <span data-ttu-id="5113f-306">코드 편집기에서 create () 메서드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-306">Right-click the Create() method in the code editor and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="5113f-307">레이블이 지정 된 확인란 확인 **강력한 형식의 뷰 만들기** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-307">Verify that the checkbox labeled **Create a strongly-typed view** is checked.</span></span>
3. <span data-ttu-id="5113f-308">**콘텐츠를 볼** 드롭다운 목록에서 값을 선택 *만들기*합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-308">From the **View content** dropdown list, select the value *Create*.</span></span>
4. <span data-ttu-id="5113f-309">**데이터 클래스 보기** 드롭다운 목록에서 값을 선택 *MovieApp.Movie*합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-309">From the **View data class** dropdown list, select the value *MovieApp.Movie*.</span></span>
5. <span data-ttu-id="5113f-310">클릭는 **추가** 단추를 새 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-310">Click the **Add** button to create the new view.</span></span>


<span data-ttu-id="5113f-311">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="5113f-311">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image23.png)</span></span>

<span data-ttu-id="5113f-312">**그림 12**: 만들기 뷰 추가 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="5113f-312">**Figure 12**: Adding the Create view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image24.png))</span></span>


<span data-ttu-id="5113f-313">Visual Studio를 자동으로 목록 5에서 뷰를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-313">Visual Studio generates the view in Listing 5 automatically.</span></span> <span data-ttu-id="5113f-314">이 보기는 각 영화 클래스의 속성에 해당 하는 필드를 포함 하는 HTML 폼을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-314">This view contains an HTML form that includes fields that correspond to each of the properties of the Movie class.</span></span>

<span data-ttu-id="5113f-315">**5-Views\Home\Create.aspx 나열**</span><span class="sxs-lookup"><span data-stu-id="5113f-315">**Listing 5 – Views\Home\Create.aspx**</span></span>

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample5.aspx)]

> [!NOTE] 
> 
> <span data-ttu-id="5113f-316">뷰 추가 대화 상자에서 생성 되는 HTML 형식 Id 양식 필드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-316">The HTML form generated by the Add View dialog generates an Id form field.</span></span> <span data-ttu-id="5113f-317">Id 열이 Id 열 이기 때문에이 양식 필드 필요 하지 않으므로 안전 하 게 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-317">Because the Id column is an Identity column, we don't need this form field and you can safely remove it.</span></span>


<span data-ttu-id="5113f-318">만들기 뷰를 추가한 후에 데이터베이스에 새 동영상 레코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-318">After you add the Create view, you can add new Movie records to the database.</span></span> <span data-ttu-id="5113f-319">F5 키를 눌러 응용 프로그램을 실행 하 고 그림 13에서 양식을 보려면 새로 만들기 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-319">Run your application by pressing the F5 key and click the Create New link to see the form in Figure 13.</span></span> <span data-ttu-id="5113f-320">완료 하 고 양식을 제출 하는 경우 새 동영상 데이터베이스 레코드가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-320">If you complete and submit the form, a new movie database record is created.</span></span>

<span data-ttu-id="5113f-321">공지 폼 유효성 검사를 자동으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-321">Notice that you get form validation automatically.</span></span> <span data-ttu-id="5113f-322">동영상에 대 한 릴리스 날짜를 입력 하는 것을 잊은 하거나을 잘못 된 릴리스 날짜를 입력 하는 경우 폼이 다시 표시 및 릴리스 날짜 필드가 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-322">If you neglect to enter a release date for a movie, or you enter an invalid release date, then the form is redisplayed and the release date field is highlighted.</span></span>


<span data-ttu-id="5113f-323">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="5113f-323">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image25.png)</span></span>

<span data-ttu-id="5113f-324">**그림 13**: 새 동영상 데이터베이스 레코드를 만드는 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image26.png))</span><span class="sxs-lookup"><span data-stu-id="5113f-324">**Figure 13**: Creating a new movie database record ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image26.png))</span></span>


## <a name="editing-existing-database-records"></a><span data-ttu-id="5113f-325">기존 데이터베이스 레코드 편집</span><span class="sxs-lookup"><span data-stu-id="5113f-325">Editing Existing Database Records</span></span>

<span data-ttu-id="5113f-326">이전 섹션을 나열 하 고 새 데이터베이스 레코드를 만들 수 방법을 설명한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-326">In the previous sections, we discussed how you can list and create new database records.</span></span> <span data-ttu-id="5113f-327">이 최종 단원에서는 기존 데이터베이스 레코드를 편집할 수는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-327">In this final section, we discuss how you can edit existing database records.</span></span>

<span data-ttu-id="5113f-328">첫째, 편집 폼을 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-328">First, we need to generate the Edit form.</span></span> <span data-ttu-id="5113f-329">Visual Studio에서 편집 폼에 자동으로 생성 하므로이 단계가 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-329">This step is easy since Visual Studio will generate the Edit form for us automatically.</span></span> <span data-ttu-id="5113f-330">Visual Studio code 편집기에서 HomeController.vb 클래스를 열고이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-330">Open the HomeController.vb class in the Visual Studio code editor and follow these steps:</span></span>

1. <span data-ttu-id="5113f-331">코드 편집기에서 Edit() 메서드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **뷰 추가** (그림 14 참조).</span><span class="sxs-lookup"><span data-stu-id="5113f-331">Right-click the Edit() method in the code editor and select the menu option **Add View** (see Figure 14).</span></span>
2. <span data-ttu-id="5113f-332">확인란 확인 **강력한 형식의 뷰 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-332">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
3. <span data-ttu-id="5113f-333">**콘텐츠를 볼** 드롭다운 목록에서 값을 선택 *편집*합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-333">From the **View content** dropdown list, select the value *Edit*.</span></span>
4. <span data-ttu-id="5113f-334">**데이터 클래스 보기** 드롭다운 목록에서 값을 선택 *MovieApp.Movie*합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-334">From the **View data class** dropdown list, select the value *MovieApp.Movie*.</span></span>
5. <span data-ttu-id="5113f-335">클릭는 **추가** 단추를 새 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-335">Click the **Add** button to create the new view.</span></span>

<span data-ttu-id="5113f-336">Views\Home 폴더에 Edit.aspx 라는 새 뷰를 추가 이러한 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-336">Completing these steps adds a new view named Edit.aspx to the Views\Home folder.</span></span> <span data-ttu-id="5113f-337">이 보기는 HTML 폼 영화 레코드 편집을 위해 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-337">This view contains an HTML form for editing a movie record.</span></span>


<span data-ttu-id="5113f-338">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="5113f-338">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image27.png)</span></span>

<span data-ttu-id="5113f-339">**그림 14**: 편집 뷰 추가 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image28.png))</span><span class="sxs-lookup"><span data-stu-id="5113f-339">**Figure 14**: Adding the Edit view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image28.png))</span></span>


> [!NOTE] 
> 
> <span data-ttu-id="5113f-340">편집 뷰 영화 Id 속성에 해당 하는 HTML 폼 필드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-340">The Edit view contains an HTML form field that corresponds to the Movie Id property.</span></span> <span data-ttu-id="5113f-341">Id 속성의 값을 편집 하는 사람을 않도록 하기 때문에이 양식 필드를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-341">Because you don't want people editing the value of the Id property, you should remove this form field.</span></span>


<span data-ttu-id="5113f-342">마지막으로, Home 컨트롤러 데이터베이스 레코드를 편집을 지원 하도록 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-342">Finally, we need to modify the Home controller so that it supports editing a database record.</span></span> <span data-ttu-id="5113f-343">업데이트 된 HomeController 클래스 목록 6에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-343">The updated HomeController class is contained in Listing 6.</span></span>

<span data-ttu-id="5113f-344">**6-Controllers\HomeController.vb (편집 메서드)를 나열합니다.**</span><span class="sxs-lookup"><span data-stu-id="5113f-344">**Listing 6 – Controllers\HomeController.vb (Edit methods)**</span></span>

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample6.vb)]

<span data-ttu-id="5113f-345">목록 6에서 Edit() 메서드의 두 오버 로드에 추가 논리를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-345">In Listing 6, I've added additional logic to both overloads of the Edit() method.</span></span> <span data-ttu-id="5113f-346">첫 번째 Edit() 메서드는 메서드에 전달 된 Id 매개 변수에 해당 하는 영화 데이터베이스 레코드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-346">The first Edit() method returns the movie database record that corresponds to the Id parameter passed to the method.</span></span> <span data-ttu-id="5113f-347">두 번째 오버 로드는 데이터베이스에서 영화 레코드에 대 한 업데이트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-347">The second overload performs the updates to a movie record in the database.</span></span>

<span data-ttu-id="5113f-348">공지 원래 영화를 검색 하 고 다음 데이터베이스의 기존 영화를 업데이트 하려면 ApplyPropertyChanges()를 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-348">Notice that you must retrieve the original movie, and then call ApplyPropertyChanges(), to update the existing movie in the database.</span></span>

## <a name="summary"></a><span data-ttu-id="5113f-349">요약</span><span class="sxs-lookup"><span data-stu-id="5113f-349">Summary</span></span>

<span data-ttu-id="5113f-350">이 자습서는 ASP.NET MVC 응용 프로그램 작성 경험의 의미를 제공 하는 것 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-350">The purpose of this tutorial was to give you a sense of the experience of building an ASP.NET MVC application.</span></span> <span data-ttu-id="5113f-351">검색 된 ASP.NET MVC 웹 응용 프로그램을 빌드하는 Active Server Pages 또는 ASP.NET 응용 프로그램을 작성 하는 환경을 매우 유사 하는 것이 좋겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-351">I hope that you discovered that building an ASP.NET MVC web application is very similar to the experience of building an Active Server Pages or ASP.NET application.</span></span>

<span data-ttu-id="5113f-352">이 자습서에서는 ASP.NET MVC 프레임 워크의 가장 기본적인 기능만 검사 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-352">In this tutorial, we examined only the most basic features of the ASP.NET MVC framework.</span></span> <span data-ttu-id="5113f-353">이후 자습서에서 우리 심층적으로 알아보기 컨트롤러, 컨트롤러 작업, 보기, 데이터 보기 및 HTML 도우미와 같은 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="5113f-353">In future tutorials, we dive deeper into topics such as controllers, controller actions, views, view data, and HTML helpers.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="5113f-354">이전</span><span class="sxs-lookup"><span data-stu-id="5113f-354">Previous</span></span>](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs.md)