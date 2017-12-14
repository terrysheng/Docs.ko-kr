---
title: "ASP.NET 및 ASP.NET Core 중에서 선택"
author: rick-anderson
description: "ASP.NET 및 ASP.NET Core 중에서 선택하는 방법을 알아보세요."
keywords: "ASP.NET Core, 기본 사항, 개요"
ms.author: riande
manager: wpickett
ms.date: 09/30/2017
ms.topic: article
ms.assetid: f0d17abf-3c69-413e-87fc-30780805e33f
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/choose-between-aspnet-and-aspnetcore
ms.openlocfilehash: 875064bd3437acc4e2a53220e19e86431d8c159b
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
# <a name="choose-between-aspnet-and-aspnet-core"></a><span data-ttu-id="83c24-104">ASP.NET 및 ASP.NET Core 중에서 선택</span><span class="sxs-lookup"><span data-stu-id="83c24-104">Choose between ASP.NET and ASP.NET Core</span></span> 

<span data-ttu-id="83c24-105">만들려는 웹 응용 프로그램에 관계 없이 ASP.NET에는 Windows Server를 대상으로 지정한 엔터프라이즈 웹 응용 프로그램에서 Linux 컨테이너를 대상으로 지정한 작은 마이크로 서비스 및 그 사이의 모든 항목에 대한 솔루션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c24-105">No matter the web application you are creating, ASP.NET has a solution for you: from enterprise web applications targeting Windows Server, to small microservices targeting Linux containers, and everything in between.</span></span>

## <a name="aspnet-core"></a><span data-ttu-id="83c24-106">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="83c24-106">ASP.NET Core</span></span>

<span data-ttu-id="83c24-107">ASP.NET Core는 Windows, macOS 또는 Linux에서 클라우드 기반 최신 웹 응용 프로그램을 빌드하기 위한 오픈 소스 플랫폼 간 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="83c24-107">ASP.NET Core is an open-source, cross-platform framework for building modern, cloud-based web applications on Windows, macOS, or Linux.</span></span>

## <a name="aspnet"></a><span data-ttu-id="83c24-108">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="83c24-108">ASP.NET</span></span>

<span data-ttu-id="83c24-109">ASP.NET은 Windows에서 엔터프라이즈 수준의 서버 기반 웹 응용 프로그램을 만들 때 필요한 모든 서비스를 제공하는 완성도 있는 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="83c24-109">ASP.NET is a mature framework that provides all the services needed to build enterprise-class, server-based web applications on Windows.</span></span>

## <a name="which-one-is-right-for-me"></a><span data-ttu-id="83c24-110">어떤 기능이 내게 적합한가요?</span><span class="sxs-lookup"><span data-stu-id="83c24-110">Which one is right for me?</span></span>

| <span data-ttu-id="83c24-111">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="83c24-111">ASP.NET Core</span></span> | <span data-ttu-id="83c24-112">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="83c24-112">ASP.NET</span></span> |
|---|---|
|<span data-ttu-id="83c24-113">Windows, macOS 또는 Linux용 빌드</span><span class="sxs-lookup"><span data-stu-id="83c24-113">Build for Windows, macOS, or Linux</span></span>|<span data-ttu-id="83c24-114">Windows용 빌드</span><span class="sxs-lookup"><span data-stu-id="83c24-114">Build for Windows</span></span>|
|<span data-ttu-id="83c24-115">[Razor 페이지](xref:mvc/razor-pages/index)는 ASP.NET Core 2.0을 사용하여 웹 UI를 만드는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="83c24-115">[Razor Pages](xref:mvc/razor-pages/index) is the recommended approach to create a Web UI with ASP.NET Core 2.0.</span></span> <span data-ttu-id="83c24-116">또한 [MVC](xref:mvc/overview) 및 [Web API](xref:tutorials/first-web-api)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83c24-116">See also [MVC](xref:mvc/overview) and [Web API](xref:tutorials/first-web-api)</span></span>|<span data-ttu-id="83c24-117">[Web Forms](https://docs.microsoft.com/aspnet/web-forms), [SignalR](https://docs.microsoft.com/aspnet/signalr), [MVC](https://docs.microsoft.com/aspnet/mvc), [Web API](https://docs.microsoft.com/aspnet/web-api/) 또는 [웹 페이지](https://docs.microsoft.com/aspnet/web-pages)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="83c24-117">Use [Web Forms](https://docs.microsoft.com/aspnet/web-forms), [SignalR](https://docs.microsoft.com/aspnet/signalr), [MVC](https://docs.microsoft.com/aspnet/mvc), [Web API](https://docs.microsoft.com/aspnet/web-api/), or [Web Pages](https://docs.microsoft.com/aspnet/web-pages)</span></span>|
|<span data-ttu-id="83c24-118">컴퓨터당 여러 버전</span><span class="sxs-lookup"><span data-stu-id="83c24-118">Multiple versions per machine</span></span>|<span data-ttu-id="83c24-119">컴퓨터당 하나의 버전</span><span class="sxs-lookup"><span data-stu-id="83c24-119">One version per machine</span></span>|
|<span data-ttu-id="83c24-120">C# 또는 F#을 사용하여 Visual Studio, [Mac용 Visual Studio](https://www.visualstudio.com/vs/visual-studio-mac/) 또는 [Visual Studio Code](https://code.visualstudio.com/)에서 개발</span><span class="sxs-lookup"><span data-stu-id="83c24-120">Develop with Visual Studio, [Visual Studio for Mac](https://www.visualstudio.com/vs/visual-studio-mac/), or [Visual Studio Code](https://code.visualstudio.com/) using C# or F#</span></span>|<span data-ttu-id="83c24-121">C#, VB 또는 F#을 사용하여 Visual Studio에서 개발</span><span class="sxs-lookup"><span data-stu-id="83c24-121">Develop with Visual Studio using C#, VB, or F#</span></span>|
|<span data-ttu-id="83c24-122">ASP.NET보다 고성능</span><span class="sxs-lookup"><span data-stu-id="83c24-122">Higher performance than ASP.NET</span></span>|<span data-ttu-id="83c24-123">성능 양호</span><span class="sxs-lookup"><span data-stu-id="83c24-123">Good performance</span></span>|
|[<span data-ttu-id="83c24-124">.NET Framework 또는 .NET Core 런타임 선택</span><span class="sxs-lookup"><span data-stu-id="83c24-124">Choose .NET Framework or .NET Core runtime</span></span>](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server)|<span data-ttu-id="83c24-125">.NET Framework 런타임 사용</span><span class="sxs-lookup"><span data-stu-id="83c24-125">Use .NET Framework runtime</span></span>|

## <a name="aspnet-core-scenarios"></a><span data-ttu-id="83c24-126">ASP.NET Core 시나리오</span><span class="sxs-lookup"><span data-stu-id="83c24-126">ASP.NET Core scenarios</span></span>

<!-- update link to Razor Pages mvc movie series when done -->
* <span data-ttu-id="83c24-127">[Razor 페이지](xref:mvc/razor-pages/index)는 ASP.NET Core 2.0을 사용하여 웹 UI를 만드는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="83c24-127">[Razor Pages](xref:mvc/razor-pages/index) is the recommended approach to create a Web UI with ASP.NET Core 2.0.</span></span>
* [<span data-ttu-id="83c24-128">웹 사이트</span><span class="sxs-lookup"><span data-stu-id="83c24-128">Websites</span></span>](xref:tutorials/first-mvc-app/index)
* [<span data-ttu-id="83c24-129">API</span><span class="sxs-lookup"><span data-stu-id="83c24-129">APIs</span></span>](xref:tutorials/first-web-api)

## <a name="aspnet-scenarios"></a><span data-ttu-id="83c24-130">ASP.NET 시나리오</span><span class="sxs-lookup"><span data-stu-id="83c24-130">ASP.NET scenarios</span></span>

* [<span data-ttu-id="83c24-131">웹 사이트</span><span class="sxs-lookup"><span data-stu-id="83c24-131">Websites</span></span>](https://docs.microsoft.com/aspnet/mvc)
* [<span data-ttu-id="83c24-132">API</span><span class="sxs-lookup"><span data-stu-id="83c24-132">APIs</span></span>](https://docs.microsoft.com/aspnet/web-api)
* [<span data-ttu-id="83c24-133">실시간</span><span class="sxs-lookup"><span data-stu-id="83c24-133">Real-time</span></span>](https://docs.microsoft.com/aspnet/signalr)

## <a name="resources"></a><span data-ttu-id="83c24-134">리소스</span><span class="sxs-lookup"><span data-stu-id="83c24-134">Resources</span></span>

* [<span data-ttu-id="83c24-135">ASP.NET 소개</span><span class="sxs-lookup"><span data-stu-id="83c24-135">Introduction to ASP.NET</span></span>](https://docs.microsoft.com/aspnet/overview)
* [<span data-ttu-id="83c24-136">ASP.NET Core 소개</span><span class="sxs-lookup"><span data-stu-id="83c24-136">Introduction to ASP.NET Core</span></span>](xref:index)