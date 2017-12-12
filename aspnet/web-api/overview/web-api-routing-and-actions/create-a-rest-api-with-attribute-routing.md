---
uid: web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
title: "ASP.NET Web API 2의에서 특성 라우팅을 사용 하 여 REST API 만들기 | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/26/2013
ms.topic: article
ms.assetid: 23fc77da-2725-4434-99a0-ff872d96336b
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
msc.type: authoredcontent
ms.openlocfilehash: 9ecc233e595716a167ad800a0a21a6162b051648
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="create-a-rest-api-with-attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="70bca-102">ASP.NET Web API 2에서에서의 라우팅 특성으로 REST API 만들기</span><span class="sxs-lookup"><span data-stu-id="70bca-102">Create a REST API with Attribute Routing in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="70bca-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="70bca-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="70bca-104">Web API 2는 새로운 형식을 지 원하는 라우팅 이라고 *특성 라우팅을*합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-104">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="70bca-105">특성 라우팅을의 일반적인 개요를 참조 하십시오. [특성 Web API 2에서의 라우팅](attribute-routing-in-web-api-2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-105">For a general overview of attribute routing, see [Attribute Routing in Web API 2](attribute-routing-in-web-api-2.md).</span></span> <span data-ttu-id="70bca-106">이 자습서에서는 있습니다 특성 라우팅을 만드는 데 사용할 책의 컬렉션에 대 한 REST API입니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-106">In this tutorial, you will use attribute routing to create a REST API for a collection of books.</span></span> <span data-ttu-id="70bca-107">API에는 다음 작업이 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-107">The API will support the following actions:</span></span>

| <span data-ttu-id="70bca-108">작업</span><span class="sxs-lookup"><span data-stu-id="70bca-108">Action</span></span> | <span data-ttu-id="70bca-109">예제 URI</span><span class="sxs-lookup"><span data-stu-id="70bca-109">Example URI</span></span> |
| --- | --- |
| <span data-ttu-id="70bca-110">모든 책 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-110">Get a list of all books.</span></span> | <span data-ttu-id="70bca-111">/ api/설명서</span><span class="sxs-lookup"><span data-stu-id="70bca-111">/api/books</span></span> |
| <span data-ttu-id="70bca-112">책 id 가져오기</span><span class="sxs-lookup"><span data-stu-id="70bca-112">Get a book by ID.</span></span> | <span data-ttu-id="70bca-113">/api/books/1</span><span class="sxs-lookup"><span data-stu-id="70bca-113">/api/books/1</span></span> |
| <span data-ttu-id="70bca-114">책의 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-114">Get the details of a book.</span></span> | <span data-ttu-id="70bca-115">/api/books/1/details</span><span class="sxs-lookup"><span data-stu-id="70bca-115">/api/books/1/details</span></span> |
| <span data-ttu-id="70bca-116">장르별로 책의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-116">Get a list of books by genre.</span></span> | <span data-ttu-id="70bca-117">/api/books/fantasy</span><span class="sxs-lookup"><span data-stu-id="70bca-117">/api/books/fantasy</span></span> |
| <span data-ttu-id="70bca-118">게시 날짜 책의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-118">Get a list of books by publication date.</span></span> | <span data-ttu-id="70bca-119">/api/books/date/2013-02-16 /api/books/date/2013/02/16 (대체 폼)</span><span class="sxs-lookup"><span data-stu-id="70bca-119">/api/books/date/2013-02-16 /api/books/date/2013/02/16 (alternate form)</span></span> |
| <span data-ttu-id="70bca-120">특정 작성자가 발행 한 책 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-120">Get a list of books by a particular author.</span></span> | <span data-ttu-id="70bca-121">/api/authors/1/books</span><span class="sxs-lookup"><span data-stu-id="70bca-121">/api/authors/1/books</span></span> |

<span data-ttu-id="70bca-122">모든 메서드는 읽기 전용 (HTTP GET 요청 수)입니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-122">All methods are read-only (HTTP GET requests).</span></span>

<span data-ttu-id="70bca-123">데이터 계층에 대 한 Entity Framework를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-123">For the data layer, we'll use Entity Framework.</span></span> <span data-ttu-id="70bca-124">책 레코드는 다음 필드가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-124">Book records will have the following fields:</span></span>

- <span data-ttu-id="70bca-125">ID</span><span class="sxs-lookup"><span data-stu-id="70bca-125">ID</span></span>
- <span data-ttu-id="70bca-126">제목</span><span class="sxs-lookup"><span data-stu-id="70bca-126">Title</span></span>
- <span data-ttu-id="70bca-127">장르</span><span class="sxs-lookup"><span data-stu-id="70bca-127">Genre</span></span>
- <span data-ttu-id="70bca-128">게시 날짜</span><span class="sxs-lookup"><span data-stu-id="70bca-128">Publication date</span></span>
- <span data-ttu-id="70bca-129">가격</span><span class="sxs-lookup"><span data-stu-id="70bca-129">Price</span></span>
- <span data-ttu-id="70bca-130">설명</span><span class="sxs-lookup"><span data-stu-id="70bca-130">Description</span></span>
- <span data-ttu-id="70bca-131">AuthorID (Authors 테이블에 외래 키)</span><span class="sxs-lookup"><span data-stu-id="70bca-131">AuthorID (foreign key to an Authors table)</span></span>

<span data-ttu-id="70bca-132">그러나 대부분의 요청에 대 한 API (title, author 및 장르)이이 데이터의 하위 집합을 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-132">For most requests, however, the API will return a subset of this data (title, author, and genre).</span></span> <span data-ttu-id="70bca-133">요청을 가져오지 전체 기록을 클라이언트 `/api/books/{id}/details`합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-133">To get the complete record, the client requests `/api/books/{id}/details`.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70bca-134">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="70bca-134">Prerequisites</span></span>

<span data-ttu-id="70bca-135">[Visual Studio 2017](https://www.visualstudio.com/vs/) Community, Professional 또는 Enterprise edition.</span><span class="sxs-lookup"><span data-stu-id="70bca-135">[Visual Studio 2017](https://www.visualstudio.com/vs/) Community, Professional or Enterprise edition.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="70bca-136">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="70bca-136">Create the Visual Studio Project</span></span>

<span data-ttu-id="70bca-137">Visual Studio를 실행 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-137">Start by running Visual Studio.</span></span> <span data-ttu-id="70bca-138">**파일** 메뉴 선택 **새로** 선택한 후 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-138">From the **File** menu, select **New** and then select **Project**.</span></span>

<span data-ttu-id="70bca-139">에 **템플릿** 창 선택 **설치 된 템플릿** 확장는 **Visual C#** 노드.</span><span class="sxs-lookup"><span data-stu-id="70bca-139">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="70bca-140">아래 **Visual C#**선택, **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-140">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="70bca-141">프로젝트 템플릿 목록에서 선택 **ASP.NET MVC 4 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-141">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="70bca-142">프로젝트 이름을 &quot;BooksAPI&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-142">Name the project &quot;BooksAPI&quot;.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image1.png)

<span data-ttu-id="70bca-143">에 **새 ASP.NET 프로젝트** 대화 상자에서는 **빈** 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-143">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="70bca-144">"폴더를 추가 및에 대 한 참조를 핵심" 아래에서 선택 된 **웹 API** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-144">Under "Add folders and core references for", select the **Web API** checkbox.</span></span> <span data-ttu-id="70bca-145">클릭 **프로젝트 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-145">Click **Create Project**.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image2.png)

<span data-ttu-id="70bca-146">이 웹 API 기능에 대해 구성 된 기본 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-146">This creates a skeleton project that is configured for Web API functionality.</span></span>

### <a name="domain-models"></a><span data-ttu-id="70bca-147">도메인 모델</span><span class="sxs-lookup"><span data-stu-id="70bca-147">Domain Models</span></span>

<span data-ttu-id="70bca-148">다음으로 도메인 모델에 대 한 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-148">Next, add classes for domain models.</span></span> <span data-ttu-id="70bca-149">솔루션 탐색기에서 모델 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-149">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="70bca-150">선택 **추가**을 선택한 후 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-150">Select **Add**, then select **Class**.</span></span> <span data-ttu-id="70bca-151">클래스 이름을 `Author`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-151">Name the class `Author`.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image3.png)

<span data-ttu-id="70bca-152">Author.cs에 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-152">Replace the code in Author.cs with the following:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample1.cs)]

<span data-ttu-id="70bca-153">이제 라는 다른 클래스를 추가할 `Book`합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-153">Now add another class named `Book`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample2.cs)]

### <a name="add-a-web-api-controller"></a><span data-ttu-id="70bca-154">웹 API 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="70bca-154">Add a Web API Controller</span></span>

<span data-ttu-id="70bca-155">이 단계에서는 데이터 계층으로 Entity Framework를 사용 하는 Web API 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-155">In this step, we'll add a Web API controller that uses Entity Framework as the data layer.</span></span>

<span data-ttu-id="70bca-156">Ctrl+Shift+B를 눌러 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-156">Press CTRL+SHIFT+B to build the project.</span></span> <span data-ttu-id="70bca-157">Entity Framework 리플렉션을 사용 하 여 컴파일된 어셈블리는 데이터베이스 스키마를 만들 필요는 모델의 속성을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-157">Entity Framework uses reflection to discover the properties of the models, so it requires a compiled assembly to create the database schema.</span></span>

<span data-ttu-id="70bca-158">솔루션 탐색기에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-158">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="70bca-159">선택 **추가**을 선택한 후 **컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-159">Select **Add**, then select **Controller**.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image4.png)

<span data-ttu-id="70bca-160">에 **추가 스 캐 폴드** 대화 상자에서 "Web API 2 Entity Framework를 사용 하 여 읽기/쓰기 동작이 포함 된 컨트롤러입니다."</span><span class="sxs-lookup"><span data-stu-id="70bca-160">In the **Add Scaffold** dialog, select "Web API 2 Controller with read/write actions, using Entity Framework."</span></span>

[![](create-a-rest-api-with-attribute-routing/_static/image6.png)](create-a-rest-api-with-attribute-routing/_static/image5.png)

<span data-ttu-id="70bca-161">에 **컨트롤러 추가** 대화 상자에서에 대 한 **컨트롤러 이름**, 입력 &quot;BooksController&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-161">In the **Add Controller** dialog, for **Controller name**, enter &quot;BooksController&quot;.</span></span> <span data-ttu-id="70bca-162">선택 된 &quot;비동기 컨트롤러 동작을 사용 하 여&quot; 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-162">Select the &quot;Use async controller actions&quot; checkbox.</span></span> <span data-ttu-id="70bca-163">에 대 한 **모델 클래스**선택, &quot;책&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-163">For **Model class**, select &quot;Book&quot;.</span></span> <span data-ttu-id="70bca-164">(표시 되지 않으면는 `Book` 드롭다운에 나열 된 클래스, 프로젝트가 빌드 되었는지 확인 합니다.) "+" 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-164">(If you don't see the `Book` class listed in the dropdown, make sure that you built the project.) Then click the "+" button.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image7.png)

<span data-ttu-id="70bca-165">클릭 **추가** 에 **새 데이터 컨텍스트에** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="70bca-165">Click **Add** in the **New Data Context** dialog.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image8.png)

<span data-ttu-id="70bca-166">클릭 **추가** 에 **컨트롤러 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="70bca-166">Click **Add** in the **Add Controller** dialog.</span></span> <span data-ttu-id="70bca-167">라는 클래스를 추가 하는 스 캐 폴딩을 `BooksController` 정의 하는 API 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-167">The scaffolding adds a class named `BooksController` that defines the API controller.</span></span> <span data-ttu-id="70bca-168">라는 클래스도 추가 `BooksAPIContext` 데이터 컨텍스트 Entity Framework에 대 한 정의 Models 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-168">It also adds a class named `BooksAPIContext` in the Models folder, which defines the data context for Entity Framework.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image9.png)

### <a name="seed-the-database"></a><span data-ttu-id="70bca-169">데이터베이스를 시드하십시오</span><span class="sxs-lookup"><span data-stu-id="70bca-169">Seed the Database</span></span>

<span data-ttu-id="70bca-170">도구 메뉴에서 선택 **라이브러리 패키지 관리자**를 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-170">From the Tools menu, select **Library Package Manager**, and then select **Package Manager Console**.</span></span>

<span data-ttu-id="70bca-171">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-171">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample3.ps1)]

<span data-ttu-id="70bca-172">이 명령은 Migrations 폴더를 만들고 Configuration.cs 라는 새 코드 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-172">This command creates a Migrations folder and adds a new code file named Configuration.cs.</span></span> <span data-ttu-id="70bca-173">이 파일을 열고 다음 코드를 추가 하는 `Configuration.Seed` 메서드.</span><span class="sxs-lookup"><span data-stu-id="70bca-173">Open this file and add the following code to the `Configuration.Seed` method.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample4.cs)]

<span data-ttu-id="70bca-174">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-174">In the Package Manager Console window, type the following commands.</span></span>

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample5.ps1)]

<span data-ttu-id="70bca-175">이 명령은 로컬 데이터베이스를 만들고 데이터베이스를 채우는 시드 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-175">These commands create a local database and invoke the Seed method to populate the database.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image10.png)

## <a name="add-dto-classes"></a><span data-ttu-id="70bca-176">DTO 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="70bca-176">Add DTO Classes</span></span>

<span data-ttu-id="70bca-177">이제 응용 프로그램을 실행 하 고 /api/books/1에 GET 요청을 보내고 응답 다음과 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-177">If you run the application now and send a GET request to /api/books/1, the response looks similar to the following.</span></span> <span data-ttu-id="70bca-178">(읽기 쉽도록 들여쓰기 추가 했습니다.)</span><span class="sxs-lookup"><span data-stu-id="70bca-178">(I added indentation for readability.)</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample6.json)]

<span data-ttu-id="70bca-179">대신,이 요청을 필드의 하위 집합을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-179">Instead, I want this request to return a subset of the fields.</span></span> <span data-ttu-id="70bca-180">만든 ID 대신 작성자의 이름을 반환 하도록 하겠습니다 또한</span><span class="sxs-lookup"><span data-stu-id="70bca-180">Also, I want it to return the author's name, rather than the author ID.</span></span> <span data-ttu-id="70bca-181">이를 위해 반환 하는 컨트롤러 메서드가 수정 합니다는 *데이터 전송 개체* DTO ()는 EF 모델 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-181">To accomplish this, we'll modify the controller methods to return a *data transfer object* (DTO) instead of the EF model.</span></span> <span data-ttu-id="70bca-182">한 DTO는만 데이터를 전송 하도록 설계 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-182">A DTO is an object that is designed only to carry data.</span></span>

<span data-ttu-id="70bca-183">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** | **새 폴더**합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-183">In Solution Explorer, right-click the project and select **Add** | **New Folder**.</span></span> <span data-ttu-id="70bca-184">폴더 이름을 &quot;Dto&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-184">Name the folder &quot;DTOs&quot;.</span></span> <span data-ttu-id="70bca-185">라는 클래스를 추가 `BookDto` Dto 폴더로 다음 정의 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-185">Add a class named `BookDto` to the DTOs folder, with the following definition:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample7.cs)]

<span data-ttu-id="70bca-186">라는 다른 클래스를 추가 `BookDetailDto`합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-186">Add another class named `BookDetailDto`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample8.cs)]

<span data-ttu-id="70bca-187">다음을 업데이트 하는 `BooksController` 반환 하기 `BookDto` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="70bca-187">Next, update the `BooksController` class to return `BookDto` instances.</span></span> <span data-ttu-id="70bca-188">에서는 [Queryable.Select](https://msdn.microsoft.com/en-us/library/system.linq.queryable.select.aspx) 메서드를 프로젝트 `Book` 인스턴스 `BookDto` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="70bca-188">We'll use the [Queryable.Select](https://msdn.microsoft.com/en-us/library/system.linq.queryable.select.aspx) method to project `Book` instances to `BookDto` instances.</span></span> <span data-ttu-id="70bca-189">컨트롤러 클래스에 대 한 업데이트 된 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-189">Here is the updated code for the controller class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample9.cs)]

> [!NOTE]
> <span data-ttu-id="70bca-190">삭제는 `PutBook`, `PostBook`, 및 `DeleteBook` 메서드가이 자습서에 대 한 필요 없는 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-190">I deleted the `PutBook`, `PostBook`, and `DeleteBook` methods, because they aren't needed for this tutorial.</span></span>


<span data-ttu-id="70bca-191">이제 응용 프로그램을 실행 하 고을 /api/books/1 요청할 경우 응답 본문은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-191">Now if you run the application and request /api/books/1, the response body should look like this:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample10.json)]

## <a name="add-route-attributes"></a><span data-ttu-id="70bca-192">경로 특성 추가</span><span class="sxs-lookup"><span data-stu-id="70bca-192">Add Route Attributes</span></span>

<span data-ttu-id="70bca-193">다음으로 특성 라우팅을 사용 하는 컨트롤러도 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-193">Next, we'll convert the controller to use attribute routing.</span></span> <span data-ttu-id="70bca-194">먼저 추가 하는 **RoutePrefix** 컨트롤러 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-194">First, add a **RoutePrefix** attribute to the controller.</span></span> <span data-ttu-id="70bca-195">이 특성이이 컨트롤러에 모든 메서드에 대 한 초기 URI 세그먼트를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-195">This attribute defines the initial URI segments for all methods on this controller.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample11.cs?highlight=1)]

<span data-ttu-id="70bca-196">그런 다음 추가 **[경로]** 컨트롤러 작업에 특성을 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-196">Then add **[Route]** attributes to the controller actions, as follows:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample12.cs?highlight=1,7)]

<span data-ttu-id="70bca-197">각 컨트롤러 메서드에 대 한 경로 템플릿을 접두사와 문자열에 지정 된 된 **경로** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-197">The route template for each controller method is the prefix plus the string specified in the **Route** attribute.</span></span> <span data-ttu-id="70bca-198">에 대 한는 `GetBook` 매개 변수가 있는 문자열을 포함 하는 메서드를 경로 템플릿에 &quot;{id: int}&quot;, URI 세그먼트는 정수 값을 포함 하는 경우와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-198">For the `GetBook` method, the route template includes the parameterized string &quot;{id:int}&quot;, which matches if the URI segment contains an integer value.</span></span>

| <span data-ttu-id="70bca-199">메서드</span><span class="sxs-lookup"><span data-stu-id="70bca-199">Method</span></span> | <span data-ttu-id="70bca-200">경로 템플릿</span><span class="sxs-lookup"><span data-stu-id="70bca-200">Route Template</span></span> | <span data-ttu-id="70bca-201">예제 URI</span><span class="sxs-lookup"><span data-stu-id="70bca-201">Example URI</span></span> |
| --- | --- | --- |
| `GetBooks` | <span data-ttu-id="70bca-202">"api/books"</span><span class="sxs-lookup"><span data-stu-id="70bca-202">"api/books"</span></span> | `http://localhost/api/books` |
| `GetBook` | <span data-ttu-id="70bca-203">"api/설명서 / {id: int}"</span><span class="sxs-lookup"><span data-stu-id="70bca-203">"api/books/{id:int}"</span></span> | `http://localhost/api/books/5` |

## <a name="get-book-details"></a><span data-ttu-id="70bca-204">책 세부 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="70bca-204">Get Book Details</span></span>

<span data-ttu-id="70bca-205">클라이언트에 GET 요청을 보내 책 세부 정보를 얻으려면 `/api/books/{id}/details`여기서 *{id}* 책의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-205">To get book details, the client will send a GET request to `/api/books/{id}/details`, where *{id}* is the ID of the book.</span></span>

<span data-ttu-id="70bca-206">다음 메서드를 `BooksController` 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-206">Add the following method to the `BooksController` class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample13.cs)]

<span data-ttu-id="70bca-207">요청 하는 경우 `/api/books/1/details`, 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-207">If you request `/api/books/1/details`, the response looks like this:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample14.json)]

## <a name="get-books-by-genre"></a><span data-ttu-id="70bca-208">Genre가 발행 한 책 가져오기</span><span class="sxs-lookup"><span data-stu-id="70bca-208">Get Books By Genre</span></span>

<span data-ttu-id="70bca-209">책의 목록이 특정 장르를 가져오려면 클라이언트에 GET 요청을 보내 `/api/books/genre`여기서 *장르* 장르의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-209">To get a list of books in a specific genre, the client will send a GET request to `/api/books/genre`, where *genre* is the name of the genre.</span></span> <span data-ttu-id="70bca-210">`/get/books/fantasy` 등을 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-210">(For example, `/get/books/fantasy`.)</span></span>

<span data-ttu-id="70bca-211">다음 메서드를 추가 `BooksController`합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-211">Add the following method to `BooksController`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample15.cs)]

<span data-ttu-id="70bca-212">여기 URI 템플릿에서 {장르} 매개 변수를 포함 하는 경로 정의 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-212">Here we are defining a route that contains a {genre} parameter in the URI template.</span></span> <span data-ttu-id="70bca-213">웹 API는 이러한 두 Uri를 구분 하 고 다양 한 방법을 라우팅합니다 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-213">Notice that Web API is able to distinguish these two URIs and route them to different methods:</span></span>

`/api/books/1`

`/api/books/fantasy`

<span data-ttu-id="70bca-214">때문는 `GetBook` 메서드에 "id" 세그먼트는 정수 값 이어야 하는 제약 조건이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-214">That's because the `GetBook` method includes a constraint that the "id" segment must be an integer value:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample16.cs?highlight=1)]

<span data-ttu-id="70bca-215">/Api/books/fantasy 요청 하는 경우 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-215">If you request /api/books/fantasy, the response looks like this:</span></span>

`[ { "Title": "Midnight Rain", "Author": "Ralls, Kim", "Genre": "Fantasy" }, { "Title": "Maeve Ascendant", "Author": "Corets, Eva", "Genre": "Fantasy" }, { "Title": "The Sundered Grail", "Author": "Corets, Eva", "Genre": "Fantasy" } ]`

## <a name="get-books-by-author"></a><span data-ttu-id="70bca-216">작성자가 발행 한 책 가져오기</span><span class="sxs-lookup"><span data-stu-id="70bca-216">Get Books By Author</span></span>

<span data-ttu-id="70bca-217">클라이언트에 GET 요청을 보내 특정 만든에 대 한 한 책의 목록이 가져오려는 `/api/authors/id/books`여기서 *id* 작성자의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-217">To get a list of a books for a particular author, the client will send a GET request to `/api/authors/id/books`, where *id* is the ID of the author.</span></span>

<span data-ttu-id="70bca-218">다음 메서드를 추가 `BooksController`합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-218">Add the following method to `BooksController`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample17.cs)]

<span data-ttu-id="70bca-219">이 예제는 흥미 로우 하기 때문에 &quot;설명서&quot; 는 처리의 자식 리소스 &quot;작성자&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-219">This example is interesting because &quot;books&quot; is treated a child resource of &quot;authors&quot;.</span></span> <span data-ttu-id="70bca-220">이 패턴은 RESTful Api에서 매우 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-220">This pattern is quite common in RESTful APIs.</span></span>

<span data-ttu-id="70bca-221">경로 접두사를 재정의 하는 경로 템플릿에서 물결표 (~)는 **RoutePrefix** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-221">The tilde (~) in the route template overrides the route prefix in the **RoutePrefix** attribute.</span></span>

## <a name="get-books-by-publication-date"></a><span data-ttu-id="70bca-222">게시 날짜 설명서 가져오기</span><span class="sxs-lookup"><span data-stu-id="70bca-222">Get Books By Publication Date</span></span>

<span data-ttu-id="70bca-223">책의 목록이 게시 날짜 여을 가져오려면 클라이언트에 GET 요청을 보내 `/api/books/date/yyyy-mm-dd`여기서 *yyyy-월-일* 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-223">To get a list of books by publication date, the client will send a GET request to `/api/books/date/yyyy-mm-dd`, where *yyyy-mm-dd* is the date.</span></span>

<span data-ttu-id="70bca-224">이 작업을 수행 하는 한 가지 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-224">Here is one way to do this:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample18.cs)]

<span data-ttu-id="70bca-225">`{pubdate:datetime}` 매개 변수가 일치 하도록 제한 되는 **DateTime** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-225">The `{pubdate:datetime}` parameter is constrained to match a **DateTime** value.</span></span> <span data-ttu-id="70bca-226">이 방법이 작동 하지만 예상 보다 더 실제로 허용.</span><span class="sxs-lookup"><span data-stu-id="70bca-226">This works, but it's actually more permissive than we'd like.</span></span> <span data-ttu-id="70bca-227">예를 들어 이러한 Uri 경로 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-227">For example, these URIs will also match the route:</span></span>

`/api/books/date/Thu, 01 May 2008`

`/api/books/date/2000-12-16T00:00:00`

<span data-ttu-id="70bca-228">잘못 된 이러한 Uri를 허용 하는 일은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-228">There's nothing wrong with allowing these URIs.</span></span> <span data-ttu-id="70bca-229">그러나 경로 템플릿을 정규식 제약 조건을 추가 하 여 경로 특정 형식으로 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-229">However, you can restrict the route to a particular format by adding a regular-expression constraint to the route template:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample19.cs?highlight=1)]

<span data-ttu-id="70bca-230">이제 날짜만 형태로 &quot;yyyy-월-일&quot; 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-230">Now only dates in the form &quot;yyyy-mm-dd&quot; will match.</span></span> <span data-ttu-id="70bca-231">이제 실제 날짜 유효성을 검사 하는 regex를 사용 하지 않는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-231">Notice that we don't use the regex to validate that we got a real date.</span></span> <span data-ttu-id="70bca-232">웹 API에 URI 세그먼트를 변환 하려고 할 때 처리 되는 한 **DateTime** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="70bca-232">That is handled when Web API tries to convert the URI segment into a **DateTime** instance.</span></span> <span data-ttu-id="70bca-233">잘못 된 날짜와 같은 ' 2012-47-99' 변환 될 실패 하 고 클라이언트에는 404 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-233">An invalid date such as '2012-47-99' will fail to be converted, and the client will get a 404 error.</span></span>

<span data-ttu-id="70bca-234">슬래시로 구분 기호를 지원할 수도 있습니다 (`/api/books/date/yyyy/mm/dd`) 다른 추가 하 여 **[경로]** 다른 정규식 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-234">You can also support a slash separator (`/api/books/date/yyyy/mm/dd`) by adding another **[Route]** attribute with a different regex.</span></span>

[!code-html[Main](create-a-rest-api-with-attribute-routing/samples/sample20.html)]

<span data-ttu-id="70bca-235">미세 하지만 중요 한 세부 여기 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-235">There is a subtle but important detail here.</span></span> <span data-ttu-id="70bca-236">두 번째 경로 템플릿을 와일드 카드 문자 (\*) {pubdate} 매개 변수의 시작 부분에:</span><span class="sxs-lookup"><span data-stu-id="70bca-236">The second route template has a wildcard character (\*) at the start of the {pubdate} parameter:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample21.json)]

<span data-ttu-id="70bca-237">이렇게 하면 라우팅 엔진 {pubdate}에 URI의 나머지와 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-237">This tells the routing engine that {pubdate} should match the rest of the URI.</span></span> <span data-ttu-id="70bca-238">템플릿 매개 변수는 기본적으로 단일 URI 세그먼트와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-238">By default, a template parameter matches a single URI segment.</span></span> <span data-ttu-id="70bca-239">이 경우 여러 개의 URI 세그먼트에 걸쳐 {pubdate} 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-239">In this case, we want {pubdate} to span several URI segments:</span></span>

`/api/books/date/2013/06/17`

## <a name="controller-code"></a><span data-ttu-id="70bca-240">컨트롤러 코드</span><span class="sxs-lookup"><span data-stu-id="70bca-240">Controller Code</span></span>

<span data-ttu-id="70bca-241">BooksController 클래스에 대 한 전체 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-241">Here is the complete code for the BooksController class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample22.cs)]

## <a name="summary"></a><span data-ttu-id="70bca-242">요약</span><span class="sxs-lookup"><span data-stu-id="70bca-242">Summary</span></span>

<span data-ttu-id="70bca-243">특성 라우팅을 제공 보다 많은 제어 및 유연성 API에 대 한 Uri를 디자인 합니다.</span><span class="sxs-lookup"><span data-stu-id="70bca-243">Attribute routing gives you more control and greater flexibility when designing the URIs for your API.</span></span>