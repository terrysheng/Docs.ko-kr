---
title: "ASP.NET Core에서 razor 페이지 경로 및 응용 프로그램 규칙 기능"
author: guardrex
description: "경로 및 응용 프로그램 모델 공급자 규칙 기능 하는 방법을 제어 페이지 라우팅, 검색 및 처리를 검색 합니다."
ms.author: riande
manager: wpickett
ms.date: 10/23/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/razor-pages/razor-pages-convention-features
ms.openlocfilehash: 69475ca9abd4e732dc704ad6a8a2fffe219984f7
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="razor-pages-route-and-app-convention-features-in-aspnet-core"></a><span data-ttu-id="07679-103">ASP.NET Core에서 razor 페이지 경로 및 응용 프로그램 규칙 기능</span><span class="sxs-lookup"><span data-stu-id="07679-103">Razor Pages route and app convention features in ASP.NET Core</span></span>

<span data-ttu-id="07679-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="07679-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="07679-105">라우팅 페이지, 검색 및 Razor 페이지 응용 프로그램에서 처리를 제어 하려면 페이지 경로 및 응용 프로그램 모델 공급자 규칙 기능을 사용 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="07679-105">Learn how to use page route and app model provider convention features to control page routing, discovery, and processing in Razor Pages apps.</span></span> <span data-ttu-id="07679-106">개별 페이지에 대 한 사용자 지정 페이지 경로 구성 해야 할 때 사용 하 여 페이지에 대 한 라우팅을 구성는 [AddPageRoute 규칙](#configure-a-page-route) 이 항목의 뒷부분에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-106">When you need to configure custom page routes for individual pages, configure routing to pages with the [AddPageRoute convention](#configure-a-page-route) described later in this topic.</span></span>

<span data-ttu-id="07679-107">사용 하 여는 [샘플 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/razor-pages-convention-features/sample) ([다운로드 하는 방법을](xref:tutorials/index#how-to-download-a-sample))이이 항목에서 설명 하는 기능을 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07679-107">Use the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/razor-pages-convention-features/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample)) to explore the features described in this topic.</span></span>

| <span data-ttu-id="07679-108">기능</span><span class="sxs-lookup"><span data-stu-id="07679-108">Features</span></span> | <span data-ttu-id="07679-109">샘플을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07679-109">The sample demonstrates ...</span></span> |
| -------- | --------------------------- |
| [<span data-ttu-id="07679-110">경로 및 응용 프로그램에 해당 하는 모델의 규칙</span><span class="sxs-lookup"><span data-stu-id="07679-110">Route and app model conventions</span></span>](#add-route-and-app-model-conventions)<br><br><span data-ttu-id="07679-111">Conventions.Add</span><span class="sxs-lookup"><span data-stu-id="07679-111">Conventions.Add</span></span><ul><li><span data-ttu-id="07679-112">IPageRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="07679-112">IPageRouteModelConvention</span></span></li><li><span data-ttu-id="07679-113">IPageApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="07679-113">IPageApplicationModelConvention</span></span></li></ul> | <span data-ttu-id="07679-114">경로 템플릿 및 헤더는 응용 프로그램의 페이지에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-114">Adding a route template and header to an app's pages.</span></span> |
| [<span data-ttu-id="07679-115">경로 동작 규칙 페이지</span><span class="sxs-lookup"><span data-stu-id="07679-115">Page route action conventions</span></span>](#page-route-action-conventions)<ul><li><span data-ttu-id="07679-116">AddFolderRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="07679-116">AddFolderRouteModelConvention</span></span></li><li><span data-ttu-id="07679-117">AddPageRouteModelConvention</span><span class="sxs-lookup"><span data-stu-id="07679-117">AddPageRouteModelConvention</span></span></li><li><span data-ttu-id="07679-118">AddPageRoute</span><span class="sxs-lookup"><span data-stu-id="07679-118">AddPageRoute</span></span></li></ul> | <span data-ttu-id="07679-119">폴더에 있는 페이지를 한 페이지를 경로 템플릿을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-119">Adding a route template to pages in a folder and to a single page.</span></span> |
| [<span data-ttu-id="07679-120">페이지 모델 작업 규칙</span><span class="sxs-lookup"><span data-stu-id="07679-120">Page model action conventions</span></span>](#page-model-action-conventions)<ul><li><span data-ttu-id="07679-121">AddFolderApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="07679-121">AddFolderApplicationModelConvention</span></span></li><li><span data-ttu-id="07679-122">AddPageApplicationModelConvention</span><span class="sxs-lookup"><span data-stu-id="07679-122">AddPageApplicationModelConvention</span></span></li><li><span data-ttu-id="07679-123">ConfigureFilter (필터 클래스, 람다 식 또는 필터 팩터리)</span><span class="sxs-lookup"><span data-stu-id="07679-123">ConfigureFilter (filter class, lambda expression, or filter factory)</span></span></li></ul> | <span data-ttu-id="07679-124">단일 페이지에 헤더를 추가 및 구성 폴더의 페이지에 헤더를 추가는 [필터 공장](xref:mvc/controllers/filters#ifilterfactory) 는 응용 프로그램의 페이지에 헤더를 추가 하려면.</span><span class="sxs-lookup"><span data-stu-id="07679-124">Adding a header to pages in a folder, adding a header to a single page, and configuring a [filter factory](xref:mvc/controllers/filters#ifilterfactory) to add a header to an app's pages.</span></span> |
| [<span data-ttu-id="07679-125">기본 페이지 응용 프로그램 모델 공급자</span><span class="sxs-lookup"><span data-stu-id="07679-125">Default page app model provider</span></span>](#replace-the-default-page-app-model-provider) | <span data-ttu-id="07679-126">처리기 이름 지정에 대 한 규칙을 변경 하려면 기본 페이지 모델 공급자를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-126">Replacing the default page model provider to change the conventions for handler naming.</span></span> |

## <a name="add-route-and-app-model-conventions"></a><span data-ttu-id="07679-127">경로 및 응용 프로그램 모델 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="07679-127">Add route and app model conventions</span></span>

<span data-ttu-id="07679-128">에 대 한 대리자를 추가 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) Razor 페이지에 적용 되는 경로 및 응용 프로그램 모델 규칙을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-128">Add a delegate for [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) to add route and app model conventions that apply to Razor Pages.</span></span>

<span data-ttu-id="07679-129">**모든 페이지에 경로 모델 규칙 추가**</span><span class="sxs-lookup"><span data-stu-id="07679-129">**Add a route model convention to all pages**</span></span>

<span data-ttu-id="07679-130">사용 하 여 [규칙](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) 만들고 추가 하는 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) 의 컬렉션에 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 경로 및 페이지 모델 동안 적용 되는 인스턴스 구문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-130">Use [Conventions](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) to create and add an [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) to the collection of [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) instances that are applied during route and page model construction.</span></span>

<span data-ttu-id="07679-131">샘플 응용 프로그램 추가 `{globalTemplate?}` 의 모든 앱에서 페이지 경로 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="07679-131">The sample app adds a `{globalTemplate?}` route template to all of the pages in the app:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Conventions/GlobalTemplatePageRouteModelConvention.cs?name=snippet1)]

> [!NOTE]
> <span data-ttu-id="07679-132">`Order` 속성에 대 한는 `AttributeRouteModel` 로 설정 된 `0` (영)입니다.</span><span class="sxs-lookup"><span data-stu-id="07679-132">The `Order` property for the `AttributeRouteModel` is set to `0` (zero).</span></span> <span data-ttu-id="07679-133">이렇게 하면이 서식 파일은 단일 경로 값을 제공 하는 경우 첫 번째 경로 데이터 값 위치에 대 한 우선 순위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-133">This ensures that this template is given priority for the first route data value position when a single route value is provided.</span></span> <span data-ttu-id="07679-134">이 샘플의 추가 예를 들어는 `{aboutTemplate?}` 항목의 뒷부분에 나오는 경로 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="07679-134">For example, the sample adds an `{aboutTemplate?}` route template later in the topic.</span></span> <span data-ttu-id="07679-135">`{aboutTemplate?}` 템플릿이 제공 됩니다는 `Order` 의 `1`합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-135">The `{aboutTemplate?}` template is given an `Order` of `1`.</span></span> <span data-ttu-id="07679-136">정보 페이지에서 요청 될 경우 `/About/RouteDataValue`, "RouteDataValue"에 로드 된 `RouteData.Values["globalTemplate"]` (`Order = 0`) 및 not `RouteData.Values["aboutTemplate"]` (`Order = 1`) 설정으로 인해는 `Order` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="07679-136">When the About page is requested at `/About/RouteDataValue`, "RouteDataValue" is loaded into `RouteData.Values["globalTemplate"]` (`Order = 0`) and not `RouteData.Values["aboutTemplate"]` (`Order = 1`) due to setting the `Order` property.</span></span>

<span data-ttu-id="07679-137">*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="07679-137">*Startup.cs*:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet1)]

<span data-ttu-id="07679-138">요청에 대 한 페이지 샘플의 `localhost:5000/About/GlobalRouteValue` 하 고 결과 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-138">Request the sample's About page at `localhost:5000/About/GlobalRouteValue` and inspect the result:</span></span>

![정보 페이지 GlobalRouteValue의 경로 세그먼트와 요청 됩니다.](razor-pages-convention-features/_static/about-page-global-template.png)

<span data-ttu-id="07679-141">**모든 페이지에 응용 프로그램 모델 규칙 추가**</span><span class="sxs-lookup"><span data-stu-id="07679-141">**Add an app model convention to all pages**</span></span>

<span data-ttu-id="07679-142">사용 하 여 [규칙](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) 만들고 추가 하는 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) 의 컬렉션에 [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) 경로 및 페이지 동안 적용 되는 인스턴스 모델 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-142">Use [Conventions](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.razorpagesoptions.conventions) to create and add an [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) to the collection of [IPageConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageconvention) instances that are applied during route and page model construction.</span></span>

<span data-ttu-id="07679-143">샘플 응용 프로그램에 포함 되어이 및 다른 규칙 항목의 뒷부분에 나오는 보여 주기 위해는 `AddHeaderAttribute` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="07679-143">To demonstrate this and other conventions later in the topic, the sample app includes an `AddHeaderAttribute` class.</span></span> <span data-ttu-id="07679-144">클래스 생성자가 허용 된 `name` 문자열 및 `values` 문자열 배열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-144">The class constructor accepts a `name` string and a `values` string array.</span></span> <span data-ttu-id="07679-145">이러한 값에 사용 되는 `OnResultExecuting` 응답 헤더를 설정 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="07679-145">These values are used in its `OnResultExecuting` method to set a response header.</span></span> <span data-ttu-id="07679-146">전체 클래스에 표시 되는 [모델 작업 규칙 페이지](#page-model-action-conventions) 항목의 뒷부분에 나오는 섹션.</span><span class="sxs-lookup"><span data-stu-id="07679-146">The full class is shown in the [Page model action conventions](#page-model-action-conventions) section later in the topic.</span></span>

<span data-ttu-id="07679-147">샘플 앱에서는 `AddHeaderAttribute` 머리글을 추가 하려면 클래스 `GlobalHeader`, 모든 앱에서 페이지에:</span><span class="sxs-lookup"><span data-stu-id="07679-147">The sample app uses the `AddHeaderAttribute` class to add a header, `GlobalHeader`, to all of the pages in the app:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Conventions/GlobalHeaderPageApplicationModelConvention.cs?name=snippet1)]

<span data-ttu-id="07679-148">*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="07679-148">*Startup.cs*:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet2)]

<span data-ttu-id="07679-149">요청에 대 한 페이지 샘플의 `localhost:5000/About` 결과를 보려면 헤더를 검사 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07679-149">Request the sample's About page at `localhost:5000/About` and inspect the headers to view the result:</span></span>

![정보 페이지의 응답 헤더는 GlobalHeader 추가 된 것을 표시 합니다.](razor-pages-convention-features/_static/about-page-global-header.png)

## <a name="page-route-action-conventions"></a><span data-ttu-id="07679-151">경로 동작 규칙 페이지</span><span class="sxs-lookup"><span data-stu-id="07679-151">Page route action conventions</span></span>

<span data-ttu-id="07679-152">파생 되는 기본 경로 모델 공급자 [IPageRouteModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelprovider) 페이지 경로 구성 하기 위한 확장 지점을 제공 하도록 설계 된 규칙을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-152">The default route model provider that derives from [IPageRouteModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelprovider) invokes conventions which are designed to provide extensibility points for configuring page routes.</span></span>

<span data-ttu-id="07679-153">**폴더 경로 모델 규칙**</span><span class="sxs-lookup"><span data-stu-id="07679-153">**Folder route model convention**</span></span>

<span data-ttu-id="07679-154">사용 하 여 [AddFolderRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderroutemodelconvention) 만들고 추가 하는 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) 에 작업을 호출 하는 [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) 아래 페이지의 모든는 지정 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="07679-154">Use [AddFolderRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderroutemodelconvention) to create and add an [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) that invokes an action on the [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) for all of the pages under the specified folder.</span></span>

<span data-ttu-id="07679-155">샘플 앱에서는 `AddFolderRouteModelConvention` 추가 하는 `{otherPagesTemplate?}` 경로 템플릿을의 페이지에는 *OtherPages* 폴더:</span><span class="sxs-lookup"><span data-stu-id="07679-155">The sample app uses `AddFolderRouteModelConvention` to add an `{otherPagesTemplate?}` route template to the pages in the *OtherPages* folder:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet3)]

> [!NOTE]
> <span data-ttu-id="07679-156">`Order` 속성에 대 한는 `AttributeRouteModel` 로 설정 된 `1`합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-156">The `Order` property for the `AttributeRouteModel` is set to `1`.</span></span> <span data-ttu-id="07679-157">이렇게 하면에 대 한 템플릿 `{globalTemplate?}` (이 항목의 앞부분에 나오는 설정) 하면 단일 경로 값을 제공 하는 경우 첫 번째 경로 데이터 값 위치에 대 한 우선 순위가 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07679-157">This ensures that the template for `{globalTemplate?}` (set earlier in the topic) is given priority for the first route data value position when a single route value is provided.</span></span> <span data-ttu-id="07679-158">페이지 1 페이지를 요청 하는 경우 `/OtherPages/Page1/RouteDataValue`, "RouteDataValue"에 로드 된 `RouteData.Values["globalTemplate"]` (`Order = 0`) 및 not `RouteData.Values["otherPagesTemplate"]` (`Order = 1`) 설정으로 인해는 `Order` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="07679-158">If the Page1 page is requested at `/OtherPages/Page1/RouteDataValue`, "RouteDataValue" is loaded into `RouteData.Values["globalTemplate"]` (`Order = 0`) and not `RouteData.Values["otherPagesTemplate"]` (`Order = 1`) due to setting the `Order` property.</span></span>

<span data-ttu-id="07679-159">요청에서 샘플의 1 페이지 페이지 `localhost:5000/OtherPages/Page1/GlobalRouteValue/OtherPagesRouteValue` 하 고 결과 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-159">Request the sample's Page1 page at `localhost:5000/OtherPages/Page1/GlobalRouteValue/OtherPagesRouteValue` and inspect the result:</span></span>

![OtherPages 폴더에 대 한 1 페이지 GlobalRouteValue 및 OtherPagesRouteValue 경로 세그먼트와 요청 됩니다.](razor-pages-convention-features/_static/otherpages-page1-global-and-otherpages-templates.png)

<span data-ttu-id="07679-162">**페이지 경로 모델 규칙**</span><span class="sxs-lookup"><span data-stu-id="07679-162">**Page route model convention**</span></span>

<span data-ttu-id="07679-163">사용 하 여 [AddPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageroutemodelconvention) 만들고 추가 하는 [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) 에 작업을 호출 하는 [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) 지정 된 페이지에 대 한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="07679-163">Use [AddPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageroutemodelconvention) to create and add an [IPageRouteModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageroutemodelconvention) that invokes an action on the [PageRouteModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageroutemodel) for the page with the specified name.</span></span>

<span data-ttu-id="07679-164">샘플 앱에서는 `AddPageRouteModelConvention` 추가 하는 `{aboutTemplate?}` 경로 템플릿을 정보 페이지에:</span><span class="sxs-lookup"><span data-stu-id="07679-164">The sample app uses `AddPageRouteModelConvention` to add an `{aboutTemplate?}` route template to the About page:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet4)]

> [!NOTE]
> <span data-ttu-id="07679-165">`Order` 속성에 대 한는 `AttributeRouteModel` 로 설정 된 `1`합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-165">The `Order` property for the `AttributeRouteModel` is set to `1`.</span></span> <span data-ttu-id="07679-166">이렇게 하면에 대 한 템플릿 `{globalTemplate?}` (이 항목의 앞부분에 나오는 설정) 하면 단일 경로 값을 제공 하는 경우 첫 번째 경로 데이터 값 위치에 대 한 우선 순위가 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07679-166">This ensures that the template for `{globalTemplate?}` (set earlier in the topic) is given priority for the first route data value position when a single route value is provided.</span></span> <span data-ttu-id="07679-167">정보 페이지에서 요청 된 경우 `/About/RouteDataValue`, "RouteDataValue"에 로드 된 `RouteData.Values["globalTemplate"]` (`Order = 0`) 및 not `RouteData.Values["aboutTemplate"]` (`Order = 1`) 설정으로 인해는 `Order` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="07679-167">If the About page is requested at `/About/RouteDataValue`, "RouteDataValue" is loaded into `RouteData.Values["globalTemplate"]` (`Order = 0`) and not `RouteData.Values["aboutTemplate"]` (`Order = 1`) due to setting the `Order` property.</span></span>

<span data-ttu-id="07679-168">요청에 대 한 페이지 샘플의 `localhost:5000/About/GlobalRouteValue/AboutRouteValue` 하 고 결과 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-168">Request the sample's About page at `localhost:5000/About/GlobalRouteValue/AboutRouteValue` and inspect the result:</span></span>

![페이지에 대 한 요청 된 경로 세그먼트와 GlobalRouteValue 및 AboutRouteValue 합니다.](razor-pages-convention-features/_static/about-page-global-and-about-templates.png)

## <a name="configure-a-page-route"></a><span data-ttu-id="07679-171">페이지 경로 구성</span><span class="sxs-lookup"><span data-stu-id="07679-171">Configure a page route</span></span>

<span data-ttu-id="07679-172">사용 하 여 [AddPageRoute](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.addpageroute) 지정된 페이지 경로에 페이지에 대 한 경로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-172">Use [AddPageRoute](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.addpageroute) to configure a route to a page at the specified page path.</span></span> <span data-ttu-id="07679-173">페이지에 생성 된 링크에 지정 된 경로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-173">Generated links to the page use your specified route.</span></span> <span data-ttu-id="07679-174">`AddPageRoute`사용 하 여 `AddPageRouteModelConvention` 경로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-174">`AddPageRoute` uses `AddPageRouteModelConvention` to establish the route.</span></span>

<span data-ttu-id="07679-175">샘플 응용 프로그램에 대 한 경로 만듭니다. `/TheContactPage` 에 대 한 *Contact.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="07679-175">The sample app creates a route to `/TheContactPage` for *Contact.cshtml*:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet5)]

<span data-ttu-id="07679-176">연락처 페이지에도 액세스할 수 `/Contact` 의 기본 경로 통해.</span><span class="sxs-lookup"><span data-stu-id="07679-176">The Contact page can also be reached at `/Contact` via its default route.</span></span>

<span data-ttu-id="07679-177">연락처 페이지에 샘플 응용 프로그램의 사용자 지정 경로 선택 사항에 대 한 허용 `text` 경로 세그먼트 (`{text?}`).</span><span class="sxs-lookup"><span data-stu-id="07679-177">The sample app's custom route to the Contact page allows for an optional `text` route segment (`{text?}`).</span></span> <span data-ttu-id="07679-178">이 선택적 세그먼트에는 페이지에도 포함 되어 해당 `@page` 방문자에 있는 페이지에 액세스 하는 경우 지시문의 `/Contact` 경로:</span><span class="sxs-lookup"><span data-stu-id="07679-178">The page also includes this optional segment in its `@page` directive in case the visitor accesses the page at its `/Contact` route:</span></span>

[!code-cshtml[Main](razor-pages-convention-features/sample/Pages/Contact.cshtml?highlight=1)]

<span data-ttu-id="07679-179">URL에 대해 생성 하는 **연락처** 업데이트 된 경로 반영 하는 렌더링 된 페이지의 링크:</span><span class="sxs-lookup"><span data-stu-id="07679-179">Note that the URL generated for the **Contact** link in the rendered page reflects the updated route:</span></span>

![탐색 모음에서 샘플 응용 프로그램에 게 문의 링크](razor-pages-convention-features/_static/contact-link.png)

![Href로 설정 되어 있는지 나타냅니다 렌더링 된 html에서 연락처 링크 검사 ' / TheContactPage'](razor-pages-convention-features/_static/contact-link-source.png)

<span data-ttu-id="07679-182">페이지를 방문 하면 연락처 하나에 해당 일반 경로 `/Contact`, 또는 사용자 지정 경로 `/TheContactPage`합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-182">Visit the Contact page at either its ordinary route, `/Contact`, or the custom route, `/TheContactPage`.</span></span> <span data-ttu-id="07679-183">추가로 제공 하는 경우 `text` 경로 세그먼트의 페이지에 표시는 HTML로 인코딩된 세그먼트를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-183">If you supply an additional `text` route segment, the page shows the HTML-encoded segment that you provide:</span></span>

![제공 된 옵션 'text' 경로 세그먼트 'TextValue' url에서의 edge 브라우저 예제입니다.](razor-pages-convention-features/_static/route-segment-with-custom-route.png)

## <a name="page-model-action-conventions"></a><span data-ttu-id="07679-186">페이지 모델 작업 규칙</span><span class="sxs-lookup"><span data-stu-id="07679-186">Page model action conventions</span></span>

<span data-ttu-id="07679-187">구현 하는 기본 페이지 모델 공급자 [IPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelprovider) 페이지 모델을 구성 하기 위한 확장 지점을 제공 하도록 설계 된 규칙을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-187">The default page model provider that implements [IPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelprovider) invokes conventions which are designed to provide extensibility points for configuring page models.</span></span> <span data-ttu-id="07679-188">이러한 규칙은 빌드 및 페이지 검색 및 처리 기능을 수정 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-188">These conventions are useful when building and modifying page discovery and processing features.</span></span>

<span data-ttu-id="07679-189">샘플 응용 프로그램에 대 한이 섹션의 예제를 사용 하 여는 `AddHeaderAttribute` 클래스 즉는 [ResultFilterAttribute](/dotnet/api/microsoft.aspnetcore.mvc.filters.resultfilterattribute), 응답 헤더를 적용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-189">For the examples in this section, the sample app uses an `AddHeaderAttribute` class, which is a [ResultFilterAttribute](/dotnet/api/microsoft.aspnetcore.mvc.filters.resultfilterattribute), that applies a response header:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Filters/AddHeader.cs?name=snippet1)]

<span data-ttu-id="07679-190">규칙을 사용 하는 샘플 및 단일 페이지 폴더에 있는 페이지의 모든 특성을 적용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07679-190">Using conventions, the sample demonstrates how to apply the attribute to all of the pages in a folder and to a single page.</span></span>

<span data-ttu-id="07679-191">**응용 프로그램 모델 규칙 폴더**</span><span class="sxs-lookup"><span data-stu-id="07679-191">**Folder app model convention**</span></span>

<span data-ttu-id="07679-192">사용 하 여 [AddFolderApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderapplicationmodelconvention) 만들고 추가 하는 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) 에 작업을 호출 하는 [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) 에 대 한 인스턴스 지정된 된 폴더 아래에 있는 모든 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="07679-192">Use [AddFolderApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addfolderapplicationmodelconvention) to create and add an [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) that invokes an action on [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) instances for all pages under the specified folder.</span></span>

<span data-ttu-id="07679-193">이 샘플의 사용법을 보여줍니다 `AddFolderApplicationModelConvention` 헤더를 추가 하 여 `OtherPagesHeader`, 내부 페이지에는 *OtherPages* 응용 프로그램의 폴더:</span><span class="sxs-lookup"><span data-stu-id="07679-193">The sample demonstrates the use of `AddFolderApplicationModelConvention` by adding a header, `OtherPagesHeader`, to the pages inside the *OtherPages* folder of the app:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet6)]

<span data-ttu-id="07679-194">요청에서 샘플의 1 페이지 페이지 `localhost:5000/OtherPages/Page1` 결과를 보려면 헤더를 검사 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07679-194">Request the sample's Page1 page at `localhost:5000/OtherPages/Page1` and inspect the headers to view the result:</span></span>

![페이지 OtherPages/1 페이지의 응답 헤더는 OtherPagesHeader 추가 된 것을 표시 합니다.](razor-pages-convention-features/_static/page1-otherpages-header.png)

<span data-ttu-id="07679-196">**응용 프로그램 모델 규칙 페이지**</span><span class="sxs-lookup"><span data-stu-id="07679-196">**Page app model convention**</span></span>

<span data-ttu-id="07679-197">사용 하 여 [AddPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageapplicationmodelconvention) 만들고 추가 하는 [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) 에 작업을 호출 하는 [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) 페이지 speciifed 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="07679-197">Use [AddPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageconventioncollection.addpageapplicationmodelconvention) to create and add an [IPageApplicationModelConvention](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.ipageapplicationmodelconvention) that invokes an action on the [PageApplicationModel](/dotnet/api/microsoft.aspnetcore.mvc.applicationmodels.pageapplicationmodel) for the page with the speciifed name.</span></span>

<span data-ttu-id="07679-198">이 샘플의 사용법을 보여줍니다 `AddPageApplicationModelConvention` 헤더를 추가 하 여 `AboutHeader`, 정보 페이지에:</span><span class="sxs-lookup"><span data-stu-id="07679-198">The sample demonstrates the use of `AddPageApplicationModelConvention` by adding a header, `AboutHeader`, to the About page:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet7)]

<span data-ttu-id="07679-199">요청에 대 한 페이지 샘플의 `localhost:5000/About` 결과를 보려면 헤더를 검사 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07679-199">Request the sample's About page at `localhost:5000/About` and inspect the headers to view the result:</span></span>

![정보 페이지의 응답 헤더는 AboutHeader 추가 된 것을 표시 합니다.](razor-pages-convention-features/_static/about-page-about-header.png)

<span data-ttu-id="07679-201">**필터 구성**</span><span class="sxs-lookup"><span data-stu-id="07679-201">**Configure a filter**</span></span>

<span data-ttu-id="07679-202">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter) 적용할 지정된 된 필터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-202">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter) configures the specified filter to apply.</span></span> <span data-ttu-id="07679-203">필터 클래스를 구현할 수 있지만 샘플 응용 프로그램에 백그라운드는 필터를 반환 하는 팩터리로 구현 되는 람다 식에 필터를 구현 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07679-203">You can implement a filter class, but the sample app shows how to implement a filter in a lambda expression, which is implemented behind-the-scenes as a factory that returns a filter:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet8)]

<span data-ttu-id="07679-204">페이지 응용 프로그램 모델에서 페이지 2 페이지를 가리키는 세그먼트에 대 한 상대 경로 확인을 위해 사용 된 *OtherPages* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="07679-204">The page app model is used to check the relative path for segments that lead to the Page2 page in the *OtherPages* folder.</span></span> <span data-ttu-id="07679-205">조건을 통과 하는 경우에 헤더가 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07679-205">If the condition passes, a header is added.</span></span> <span data-ttu-id="07679-206">그렇지 않은 경우, `EmptyFilter` 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07679-206">If not, the `EmptyFilter` is applied.</span></span>

<span data-ttu-id="07679-207">`EmptyFilter`이 [작업 필터](xref:mvc/controllers/filters#action-filters)합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-207">`EmptyFilter` is an [Action filter](xref:mvc/controllers/filters#action-filters).</span></span> <span data-ttu-id="07679-208">Razor 페이지에서 작업 필터를 무시 하므로 `EmptyFilter` 아니요 ops 경로 포함 하지 않는 경우 의도 한 대로 `OtherPages/Page2`합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-208">Since Action filters are ignored by Razor Pages, the `EmptyFilter` no-ops as intended if the path doesn't contain `OtherPages/Page2`.</span></span>

<span data-ttu-id="07679-209">요청에서 샘플의 2 페이지 페이지 `localhost:5000/OtherPages/Page2` 결과를 보려면 헤더를 검사 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07679-209">Request the sample's Page2 page at `localhost:5000/OtherPages/Page2` and inspect the headers to view the result:</span></span>

![OtherPagesPage2Header 2 페이지에 대 한 응답에 추가 됩니다.](razor-pages-convention-features/_static/page2-filter-header.png)

<span data-ttu-id="07679-211">**필터 팩터리 구성**</span><span class="sxs-lookup"><span data-stu-id="07679-211">**Configure a filter factory**</span></span>

<span data-ttu-id="07679-212">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter?view=aspnetcore-2.0#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_ConfigureFilter_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_Func_Microsoft_AspNetCore_Mvc_ApplicationModels_PageApplicationModel_Microsoft_AspNetCore_Mvc_Filters_IFilterMetadata__) 적용 하려면 지정 된 팩터리 구성 [필터](xref:mvc/controllers/filters) 모든 Razor 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07679-212">[ConfigureFilter](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.configurefilter?view=aspnetcore-2.0#Microsoft_Extensions_DependencyInjection_PageConventionCollectionExtensions_ConfigureFilter_Microsoft_AspNetCore_Mvc_ApplicationModels_PageConventionCollection_System_Func_Microsoft_AspNetCore_Mvc_ApplicationModels_PageApplicationModel_Microsoft_AspNetCore_Mvc_Filters_IFilterMetadata__) configures the specified factory to apply [filters](xref:mvc/controllers/filters) to all Razor Pages.</span></span>

<span data-ttu-id="07679-213">사용 하는 예제를 제공 하는 샘플 응용 프로그램을 [필터 공장](xref:mvc/controllers/filters#ifilterfactory) 헤더를 추가 하 여 `FilterFactoryHeader`, 응용 프로그램의 페이지에 두 값이 포함:</span><span class="sxs-lookup"><span data-stu-id="07679-213">The sample app provides an example of using a [filter factory](xref:mvc/controllers/filters#ifilterfactory) by adding a header, `FilterFactoryHeader`, with two values to the app's pages:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet9)]

<span data-ttu-id="07679-214">*AddHeaderWithFactory.cs*:</span><span class="sxs-lookup"><span data-stu-id="07679-214">*AddHeaderWithFactory.cs*:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Factories/AddHeaderWithFactory.cs?name=snippet1)]

<span data-ttu-id="07679-215">요청에 대 한 페이지 샘플의 `localhost:5000/About` 결과를 보려면 헤더를 검사 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07679-215">Request the sample's About page at `localhost:5000/About` and inspect the headers to view the result:</span></span>

![응답 헤더 정보 페이지의 두 개의 FilterFactoryHeader 헤더 추가 된 것을 표시 합니다.](razor-pages-convention-features/_static/about-page-filter-factory-header.png)

## <a name="replace-the-default-page-app-model-provider"></a><span data-ttu-id="07679-217">기본 페이지 응용 프로그램 모델 공급자를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-217">Replace the default page app model provider</span></span>

<span data-ttu-id="07679-218">Razor 페이지를 사용 하 여는 `IPageApplicationModelProvider` 를 만들려면 인터페이스는 [DefaultPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider)합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-218">Razor Pages uses the `IPageApplicationModelProvider` interface to create a [DefaultPageApplicationModelProvider](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider).</span></span> <span data-ttu-id="07679-219">처리기 검색 및 처리에 대 한 직접 구현 논리를 제공 하는 기본 모델 공급자에서 상속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07679-219">You can inherit from the default model provider to provide your own implementation logic for handler discovery and processing.</span></span> <span data-ttu-id="07679-220">기본 구현 ([참조 소스](https://github.com/aspnet/Mvc/blob/rel/2.0.1/src/Microsoft.AspNetCore.Mvc.RazorPages/Internal/DefaultPageApplicationModelProvider.cs))에 대 한 규칙을 설정 *명명 되지 않은* 및 *라는* 아래 설명 하는 처리기 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-220">The default implementation ([reference source](https://github.com/aspnet/Mvc/blob/rel/2.0.1/src/Microsoft.AspNetCore.Mvc.RazorPages/Internal/DefaultPageApplicationModelProvider.cs)) establishes conventions for *unnamed* and *named* handler naming, which is described below.</span></span>

<span data-ttu-id="07679-221">**기본 명명 되지 않은 처리기 메서드**</span><span class="sxs-lookup"><span data-stu-id="07679-221">**Default unnamed handler methods**</span></span>

<span data-ttu-id="07679-222">HTTP 동사 ("명명 되지 않은" 처리기 메서드)에 대 한 처리기 메서드는 규칙을 따릅니다: `On<HTTP verb>[Async]` (추가 `Async` 은 선택적 이지만 비동기 메서드에 대 한 권장).</span><span class="sxs-lookup"><span data-stu-id="07679-222">Handler methods for HTTP verbs ("unnamed" handler methods) follow a convention: `On<HTTP verb>[Async]` (appending `Async` is optional but recommended for async methods).</span></span>

| <span data-ttu-id="07679-223">명명 되지 않은 처리기 메서드</span><span class="sxs-lookup"><span data-stu-id="07679-223">Unnamed handler method</span></span>     | <span data-ttu-id="07679-224">작업</span><span class="sxs-lookup"><span data-stu-id="07679-224">Operation</span></span>                      |
| -------------------------- | ------------------------------ |
| `OnGet`/`OnGetAsync`       | <span data-ttu-id="07679-225">페이지 상태를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-225">Initialize the page state.</span></span>     |
| `OnPost`/`OnPostAsync`     | <span data-ttu-id="07679-226">POST 요청을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-226">Handle POST requests.</span></span>          |
| `OnDelete`/`OnDeleteAsync` | <span data-ttu-id="07679-227">삭제 요청 수 &#8224; 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-227">Handle DELETE requests&#8224;.</span></span> |
| `OnPut`/`OnPutAsync`       | <span data-ttu-id="07679-228">PUT 요청을 &#8224; 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-228">Handle PUT requests&#8224;.</span></span>    |
| `OnPatch`/`OnPatchAsync`   | <span data-ttu-id="07679-229">PATCH 요청 &#8224; 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-229">Handle PATCH requests&#8224;.</span></span>  |

<span data-ttu-id="07679-230">&#8224; 페이지에 대 한 API 호출에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-230">&#8224;Used for making API calls to the page.</span></span>

<span data-ttu-id="07679-231">**기본 명명 된 처리기 메서드**</span><span class="sxs-lookup"><span data-stu-id="07679-231">**Default named handler methods**</span></span>

<span data-ttu-id="07679-232">("이름" 처리기 메서드)는 개발자가 제공 하는 처리기 메서드는 비슷한 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="07679-232">Handler methods provided by the developer ("named" handler methods) follow a similar convention.</span></span> <span data-ttu-id="07679-233">HTTP 동사 또는 HTTP 동사 뒤 처리기 이름은 표시 및 `Async`: `On<HTTP verb><handler name>[Async]` (추가 `Async` 은 선택적 이지만 비동기 메서드에 대 한 권장).</span><span class="sxs-lookup"><span data-stu-id="07679-233">The handler name appears after the HTTP verb or between the HTTP verb and `Async`: `On<HTTP verb><handler name>[Async]` (appending `Async` is optional but recommended for async methods).</span></span> <span data-ttu-id="07679-234">예를 들어 메시지를 처리 하는 메서드는 아래 표에 표시 된 명명 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07679-234">For example, methods that process messages might take the naming shown in the table below.</span></span>

| <span data-ttu-id="07679-235">라는 처리기 메서드 예제</span><span class="sxs-lookup"><span data-stu-id="07679-235">Example named handler method</span></span>             | <span data-ttu-id="07679-236">예제 작업</span><span class="sxs-lookup"><span data-stu-id="07679-236">Example operation</span></span>        |
| ---------------------------------------- | ------------------------ |
| `OnGetMessage`/`OnGetMessageAsync`       | <span data-ttu-id="07679-237">메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="07679-237">Obtain a message.</span></span>        |
| `OnPostMessage`/`OnPostMessageAsync`     | <span data-ttu-id="07679-238">메시지를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-238">POST a message.</span></span>          |
| `OnDeleteMessage`/`OnDeleteMessageAsync` | <span data-ttu-id="07679-239">메시지 #8224; 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-239">DELETE a message&#8224;.</span></span> |
| `OnPutMessage`/`OnPutMessageAsync`       | <span data-ttu-id="07679-240">메시지 &#8224; 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="07679-240">PUT a message&#8224;.</span></span>    |
| `OnPatchMessage`/`OnPatchMessageAsync`   | <span data-ttu-id="07679-241">메시지 &#8224; PATCH 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-241">PATCH a message&#8224;.</span></span>  |

<span data-ttu-id="07679-242">&#8224; 페이지에 대 한 API 호출에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-242">&#8224;Used for making API calls to the page.</span></span>

<span data-ttu-id="07679-243">**처리기 메서드 이름을 사용자 지정**</span><span class="sxs-lookup"><span data-stu-id="07679-243">**Customize handler method names**</span></span>

<span data-ttu-id="07679-244">명명 되지 않은 및 명명 된 처리기 메서드가 이름을 지정 하는 방식을 변경 하려는 경우를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-244">Assume that you prefer to change the way unnamed and named handler methods are named.</span></span> <span data-ttu-id="07679-245">대체 이름 지정 체계 메서드 이름이 "On"으로 시작 되지 않는 HTTP 동사를 확인 하려면 첫 번째 단어 세그먼트를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="07679-245">An alternative naming scheme is to avoid starting the method names with "On" and use the first word segment to determine the HTTP verb.</span></span> <span data-ttu-id="07679-246">다른 변경을 수행할 수 있습니다 삭제에 대 한 동사를 변환, 예: PUT, 및 POST를 패치 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-246">You can make other changes, such as converting the verbs for DELETE, PUT, and PATCH to POST.</span></span> <span data-ttu-id="07679-247">구성표를 다음 표에 표시 된 메서드 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-247">Such a scheme provides the method names shown in the following table.</span></span>

| <span data-ttu-id="07679-248">처리기 메서드</span><span class="sxs-lookup"><span data-stu-id="07679-248">Handler method</span></span>                       | <span data-ttu-id="07679-249">작업</span><span class="sxs-lookup"><span data-stu-id="07679-249">Operation</span></span>                      |
| ------------------------------------ | ------------------------------ |
| `Get`                                | <span data-ttu-id="07679-250">페이지 상태를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-250">Initialize the page state.</span></span>     |
| `Post`/`PostAsync`                   | <span data-ttu-id="07679-251">POST 요청을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-251">Handle POST requests.</span></span>          |
| `Delete`/`DeleteAsync`               | <span data-ttu-id="07679-252">삭제 요청 수 &#8224; 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-252">Handle DELETE requests&#8224;.</span></span> |
| `Put`/`PutAsync`                     | <span data-ttu-id="07679-253">PUT 요청을 &#8224; 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-253">Handle PUT requests&#8224;.</span></span>    |
| `Patch`/`PatchAsync`                 | <span data-ttu-id="07679-254">PATCH 요청 &#8224; 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-254">Handle PATCH requests&#8224;.</span></span>  |
| `GetMessage`                         | <span data-ttu-id="07679-255">메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="07679-255">Obtain a message.</span></span>              |
| `PostMessage`/`PostMessageAsync`     | <span data-ttu-id="07679-256">메시지를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-256">POST a message.</span></span>                |
| `DeleteMessage`/`DeleteMessageAsync` | <span data-ttu-id="07679-257">삭제할 메시지를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-257">POST a message to delete.</span></span>      |
| `PutMessage`/`PutMessageAsync`       | <span data-ttu-id="07679-258">배치에 메시지를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-258">POST a message to put.</span></span>         |
| `PatchMessage`/`PatchMessageAsync`   | <span data-ttu-id="07679-259">패치에 메시지를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-259">POST a message to patch.</span></span>       |

<span data-ttu-id="07679-260">&#8224; 페이지에 대 한 API 호출에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-260">&#8224;Used for making API calls to the page.</span></span>

<span data-ttu-id="07679-261">이 체계를 설정 하려면에서 상속 하는 `DefaultPageApplicationModelProvider` 클래스 및 재정의 [CreateHandlerModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider.createhandlermodel) 확인 하기 위한 사용자 지정 논리를 제공 하는 메서드 [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) 처리기 이름은 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-261">To establish this scheme, inherit from the `DefaultPageApplicationModelProvider` class and override the [CreateHandlerModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.internal.defaultpageapplicationmodelprovider.createhandlermodel) method to supply custom logic for resolving [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) handler names.</span></span> <span data-ttu-id="07679-262">샘플 앱 표시이 작업을 수행 하는 방법의 `CustomPageApplicationModelProvider` 클래스:</span><span class="sxs-lookup"><span data-stu-id="07679-262">The sample app shows you how this is done in its `CustomPageApplicationModelProvider` class:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/CustomPageApplicationModelProvider.cs?name=snippet1&highlight=1-2,45-46,64-68,78-85,87,92,106)]

<span data-ttu-id="07679-263">클래스의 장점:</span><span class="sxs-lookup"><span data-stu-id="07679-263">Highlights of the class include:</span></span>

* <span data-ttu-id="07679-264">클래스에서 상속 `DefaultPageApplicationModelProvider`합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-264">The class inherits from `DefaultPageApplicationModelProvider`.</span></span>
* <span data-ttu-id="07679-265">`TryParseHandlerMethod` 처리 하는 HTTP 동사를 결정 하는 처리기 (`httpMethod`) 및 명명 된 처리기 이름 (`handlerName`)를 만들 때는 `PageHandlerModel`합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-265">The `TryParseHandlerMethod` processes a handler to determine the HTTP verb (`httpMethod`) and named handler name (`handlerName`) when creating the `PageHandlerModel`.</span></span>
  * <span data-ttu-id="07679-266">`Async` 있는 경우, 후 위 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07679-266">An `Async` postfix is ignored, if present.</span></span>
  * <span data-ttu-id="07679-267">대/소문자 구분 메서드 이름에서 HTTP 동사를 구문 분석 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07679-267">Casing is used to parse the HTTP verb from the method name.</span></span>
  * <span data-ttu-id="07679-268">때 메서드 이름 (없이 `Async`)는 HTTP 동사 이름 같음, 처리기가 없는 명명 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-268">When the method name (without `Async`) is equal to the HTTP verb name, there's no named handler.</span></span> <span data-ttu-id="07679-269">`handlerName` 로 설정 된 `null`, 그리고 메서드 이름이 `Get`, `Post`, `Delete`, `Put`, 또는 `Patch`합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-269">The `handlerName` is set to `null`, and the method name is `Get`, `Post`, `Delete`, `Put`, or `Patch`.</span></span>
  * <span data-ttu-id="07679-270">때 메서드 이름 (없이 `Async`) HTTP 동사 이름 보다 긴 명명 된 처리기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07679-270">When the method name (without `Async`) is longer than the HTTP verb name, there's a named handler.</span></span> <span data-ttu-id="07679-271">`handlerName`는 `<method name (less 'Async', if present)>`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="07679-271">The `handlerName` is set to `<method name (less 'Async', if present)>`.</span></span> <span data-ttu-id="07679-272">예를 들어 "GetMessage" 및 "GetMessageAsync" 모두 "GetMessage"의 처리기 이름을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-272">For example, both "GetMessage" and "GetMessageAsync" yield a handler name of "GetMessage".</span></span>
  * <span data-ttu-id="07679-273">DELETE, PUT, 및 PATCH HTTP 동사는 POST로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07679-273">DELETE, PUT, and PATCH HTTP verbs are converted to POST.</span></span>

<span data-ttu-id="07679-274">등록 된 `CustomPageApplicationModelProvider` 에 `Startup` 클래스:</span><span class="sxs-lookup"><span data-stu-id="07679-274">Register the `CustomPageApplicationModelProvider` in the `Startup` class:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Startup.cs?name=snippet10)]

<span data-ttu-id="07679-275">코드 숨김 파일 *Index.cshtml.cs* 페이지 응용 프로그램에 대 한 일반 처리기 메서드 명명 규칙은 변경 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07679-275">The code-behind file *Index.cshtml.cs* shows how the ordinary handler method naming conventions are changed for pages in the app.</span></span> <span data-ttu-id="07679-276">"에서" 접두사 명명 Razor 페이지를 사용 하는 일반적인 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07679-276">The ordinary "On" prefix naming used with Razor Pages is removed.</span></span> <span data-ttu-id="07679-277">페이지 상태를 초기화 하는 메서드는 이제 이름이 `Get`합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-277">The method that initializes the page state is now named `Get`.</span></span> <span data-ttu-id="07679-278">여러 페이지에 대 한 코드 숨김 파일을 열 경우 응용 프로그램 전체에서 사용 하는이 규칙을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07679-278">You can see this convention used throughout the app if you open any code-behind file for any of the pages.</span></span>

<span data-ttu-id="07679-279">다른 메서드는 각각 처리를 설명 하는 HTTP 동사와 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-279">Each of the other methods start with the HTTP verb that describes its processing.</span></span> <span data-ttu-id="07679-280">로 시작 하는 두 가지 방법 `Delete` DELETE HTTP 동사 하지만의 논리로 정상적으로 처리 됩니다 `TryParseHandlerMethod` 명시적으로 모두 처리기에 대 한 동사 POST로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-280">The two methods that start with `Delete` would normally be treated as DELETE HTTP verbs, but the logic in `TryParseHandlerMethod` explicitly sets the verb to POST for both handlers.</span></span>

<span data-ttu-id="07679-281">`Async` 는 선택 사항 간의 `DeleteAllMessages` 및 `DeleteMessageAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-281">Note that `Async` is optional between `DeleteAllMessages` and `DeleteMessageAsync`.</span></span> <span data-ttu-id="07679-282">비동기 메서드 모두 하지만 사용 하도록 선택할 수는 `Async` 여부를 후 위; 수행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="07679-282">They're both asynchronous methods, but you can choose to use the `Async` postfix or not; we recommend that you do.</span></span> <span data-ttu-id="07679-283">`DeleteAllMessages`설명을 위해 여기에이 있지만 이러한 메서드의 이름을 지정 하는 것이 좋습니다 `DeleteAllMessagesAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-283">`DeleteAllMessages` is used here for demonstration purposes, but we recommend that you name such a method `DeleteAllMessagesAsync`.</span></span> <span data-ttu-id="07679-284">처리에 영향을 주지 샘플의 구현 하지만 사용 하는 `Async` 비동기 메서드로 된다는 사실에 입각 호출 후 위 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-284">It doesn't affect the processing of the sample's implementation, but using the `Async` postfix calls out the fact that it's an asynchronous method.</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Pages/Index.cshtml.cs?name=snippet1&highlight=1,6,16,29)]

<span data-ttu-id="07679-285">에 제공 된 처리기 이름을 확인 *Index.cshtml* 일치는 `DeleteAllMessages` 및 `DeleteMessageAsync` 처리기 메서드:</span><span class="sxs-lookup"><span data-stu-id="07679-285">Note the handler names provided in *Index.cshtml* match the `DeleteAllMessages` and `DeleteMessageAsync` handler methods:</span></span>

[!code-cshtml[Main](razor-pages-convention-features/sample/Pages/Index.cshtml?range=29-60&highlight=7-8,24-25)]

<span data-ttu-id="07679-286">`Async`처리기 메서드 이름에 `DeleteMessageAsync` 는 축소 하 여 포함 된 `TryParseHandlerMethod` 처리기 메서드를 POST 요청의 일치에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-286">`Async` in the handler method name `DeleteMessageAsync` is factored out by the `TryParseHandlerMethod` for handler matching of POST request to method.</span></span> <span data-ttu-id="07679-287">`asp-page-handler` 이름 `DeleteMessage` 처리기 메서드에 일치 `DeleteMessageAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-287">The `asp-page-handler` name of `DeleteMessage` is matched to the handler method `DeleteMessageAsync`.</span></span>

## <a name="mvc-filters-and-the-page-filter-ipagefilter"></a><span data-ttu-id="07679-288">MVC 필터 및 페이지 필터 (IPageFilter)</span><span class="sxs-lookup"><span data-stu-id="07679-288">MVC Filters and the Page filter (IPageFilter)</span></span>

<span data-ttu-id="07679-289">MVC [작업 필터](xref:mvc/controllers/filters#action-filters) Razor 페이지 처리기 메서드를 사용 하므로 Razor 페이지에서 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07679-289">MVC [Action filters](xref:mvc/controllers/filters#action-filters) are ignored by Razor Pages, since Razor Pages use handler methods.</span></span> <span data-ttu-id="07679-290">다른 유형의 MVC 필터는 사용할 수 있습니다 사용할 수 있는: [권한 부여](xref:mvc/controllers/filters#authorization-filters), [예외](xref:mvc/controllers/filters#exception-filters), [리소스](xref:mvc/controllers/filters#resource-filters), 및 [결과](xref:mvc/controllers/filters#result-filters)합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-290">Other types of MVC filters are available for you to use: [Authorization](xref:mvc/controllers/filters#authorization-filters), [Exception](xref:mvc/controllers/filters#exception-filters), [Resource](xref:mvc/controllers/filters#resource-filters), and [Result](xref:mvc/controllers/filters#result-filters).</span></span> <span data-ttu-id="07679-291">자세한 내용은 참조는 [필터](xref:mvc/controllers/filters) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="07679-291">For more information, see the [Filters](xref:mvc/controllers/filters) topic.</span></span>

<span data-ttu-id="07679-292">페이지 필터 ([IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter)) Razor 페이지에 적용 되는 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="07679-292">The Page filter ([IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter)) is a filter that applies to Razor Pages.</span></span> <span data-ttu-id="07679-293">주변 페이지 처리기 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-293">It surrounds the execution of a page handler method.</span></span> <span data-ttu-id="07679-294">처리기 메서드 실행 페이지의 단계에서 사용자 지정 코드를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07679-294">It allows you to process custom code at stages of page handler method execution.</span></span> <span data-ttu-id="07679-295">샘플 응용 프로그램의 한 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="07679-295">Here's an example from the sample app:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Filters/ReplaceRouteValueFilterAttribute.cs?name=snippet1)]

<span data-ttu-id="07679-296">이 필터에 대 한 검사는 `globalTemplate` "ReplacementValue"에서 "TriggerValue" 및 교체의 값을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-296">This filter checks for a `globalTemplate` route value of "TriggerValue" and swaps in "ReplacementValue".</span></span>

<span data-ttu-id="07679-297">`ReplaceRouteValueFilter` 특성에 직접 적용할 수 있습니다는 `PageModel` 코드 숨김에서:</span><span class="sxs-lookup"><span data-stu-id="07679-297">The `ReplaceRouteValueFilter` attribute can be applied directly to a `PageModel` in code-behind:</span></span>

[!code-csharp[Main](razor-pages-convention-features/sample/Pages/OtherPages/Page3.cshtml.cs?range=10-12&highlight=1)]

<span data-ttu-id="07679-298">에 있는 샘플 응용 프로그램에서 요청 Page3 페이지 `localhost:5000/OtherPages/Page3/TriggerValue`합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-298">Request the Page3 page from the sample app with at `localhost:5000/OtherPages/Page3/TriggerValue`.</span></span> <span data-ttu-id="07679-299">필터는 경로 값을 대체 하는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="07679-299">Notice how the filter replaces the route value:</span></span>

![경로 값을 ReplacementValue 바꿀 필터에서 TriggerValue 경로 세그먼트 결과로 OtherPages/Page3를 요청 합니다.](razor-pages-convention-features/_static/otherpages-page3-filter-replacement-value.png)

## <a name="see-also"></a><span data-ttu-id="07679-301">참고 항목</span><span class="sxs-lookup"><span data-stu-id="07679-301">See also</span></span>

* [<span data-ttu-id="07679-302">Razor 페이지 권한 부여 규칙</span><span class="sxs-lookup"><span data-stu-id="07679-302">Razor Pages authorization conventions</span></span>](xref:security/authorization/razor-pages-authorization)