---
title: "ASP.NET Core에 Id 소개"
author: rick-anderson
description: "ASP.NET Core 응용 프로그램과 함께 Id를 사용 하 여"
ms.author: riande
manager: wpickett
ms.date: 01/02/2018
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authentication/identity
ms.openlocfilehash: 436a5ecfd126c9660591cd55efc1cc52b9493136
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="introduction-to-identity-on-aspnet-core"></a><span data-ttu-id="94386-103">ASP.NET Core에 Id 소개</span><span class="sxs-lookup"><span data-stu-id="94386-103">Introduction to Identity on ASP.NET Core</span></span>

<span data-ttu-id="94386-104">여 [Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra), Jon Galloway [Erik Reitan](https://github.com/Erikre), 및 [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="94386-104">By [Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra), Jon Galloway, [Erik Reitan](https://github.com/Erikre), and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="94386-105">ASP.NET Core Id는 응용 프로그램에 로그인 기능을 추가할 수 있는 멤버 자격 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="94386-105">ASP.NET Core Identity is a membership system which allows you to add login functionality to your application.</span></span> <span data-ttu-id="94386-106">사용자 계정 및 로그인 사용자 이름으로 만들 수 있습니다 및 암호 또는 Facebook, Google, Microsoft 계정, Twitter 또는 다른 사용자와 같은 외부 로그인 공급자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94386-106">Users can create an account and login with a user name and password or they can use an external login provider such as Facebook, Google, Microsoft Account, Twitter or others.</span></span>

<span data-ttu-id="94386-107">ASP.NET Core Id 사용자 이름, 암호 및 프로필 데이터를 저장 하는 SQL Server 데이터베이스를 사용 하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94386-107">You can configure ASP.NET Core Identity to use a SQL Server database to store user names, passwords, and profile data.</span></span> <span data-ttu-id="94386-108">또는 사용자 고유의 영구 저장소 예를 들어 Azure 테이블 저장소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94386-108">Alternatively, you can use your own persistent store, for example, an Azure Table Storage.</span></span> <span data-ttu-id="94386-109">이 문서에는 Visual Studio는 CLI를 사용 하 여 위한 지침이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94386-109">This document contains instructions for Visual Studio and for using the CLI.</span></span>

[<span data-ttu-id="94386-110">보거나 샘플 코드를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-110">View or download the sample code.</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authentication/identity/sample/src/ASPNETCore-IdentityDemoComplete/) [<span data-ttu-id="94386-111">(다운로드 하는 방법)</span><span class="sxs-lookup"><span data-stu-id="94386-111">(How to download)</span></span>](https://docs.microsoft.com/en-us/aspnet/core/tutorials/index#how-to-download-a-sample)

## <a name="overview-of-identity"></a><span data-ttu-id="94386-112">Id의 개요</span><span class="sxs-lookup"><span data-stu-id="94386-112">Overview of Identity</span></span>

<span data-ttu-id="94386-113">이 항목에서는 등록, 로그인 하는 기능을 추가 하려면 ASP.NET Core Id를 사용 하 고 로그 아웃 한 사용자 합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-113">In this topic, you'll learn how to use ASP.NET Core Identity to add functionality to register, log in, and log out a user.</span></span> <span data-ttu-id="94386-114">ASP.NET Core Id를 사용 하 여 앱을 만드는 방법에 대해 더 자세한 내용은이 문서의 끝에 다음 단계 섹션을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="94386-114">For more detailed instructions about creating apps using ASP.NET Core Identity, see the Next Steps section at the end of this article.</span></span>

1.  <span data-ttu-id="94386-115">개별 사용자 계정을 가진 ASP.NET Core 웹 응용 프로그램 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94386-115">Create an ASP.NET Core Web Application project with Individual User Accounts.</span></span>

    # <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="94386-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="94386-116">Visual Studio</span></span>](#tab/visual-studio)

    <span data-ttu-id="94386-117">Visual Studio에서 선택 **파일** > **새로** > **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-117">In Visual Studio, select **File** > **New** > **Project**.</span></span> <span data-ttu-id="94386-118">선택 **ASP.NET Core 웹 응용 프로그램** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-118">Select **ASP.NET Core Web Application** and click **OK**.</span></span>

    ![새 프로젝트 대화 상자](identity/_static/01-new-project.png)

    <span data-ttu-id="94386-120">ASP.NET Core 선택 **웹 응용 프로그램 (모델-뷰-컨트롤러)** ASP.NET에 대 한 핵심 2.x를 선택한 다음 선택 **인증 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-120">Select an ASP.NET Core **Web Application (Model-View-Controller)** for ASP.NET Core 2.x, then select **Change Authentication**.</span></span>

    ![새 프로젝트 대화 상자](identity/_static/02-new-project.png)

    <span data-ttu-id="94386-122">제공 하는 대화 상자가 나타납니다 인증 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-122">A dialog appears offering authentication choices.</span></span> <span data-ttu-id="94386-123">선택 **개별 사용자 계정** 클릭 **확인** 이전 대화 상자로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="94386-123">Select **Individual User Accounts** and click **OK** to return to the previous dialog.</span></span>

    ![새 프로젝트 대화 상자](identity/_static/03-new-project-auth.png)

    <span data-ttu-id="94386-125">선택 하면 **개별 사용자 계정** 모델, Viewmodel, 뷰, 컨트롤러 및 프로젝트 템플릿의 일부로 인증에 필요한 기타 자산을 만들려면 Visual Studio를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-125">Selecting **Individual User Accounts** directs Visual Studio to create Models, ViewModels, Views, Controllers, and other assets required for authentication as part of the project template.</span></span>

    # <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="94386-126">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="94386-126">.NET Core CLI</span></span>](#tab/netcore-cli)

    <span data-ttu-id="94386-127">.NET Core CLI를 사용 하는 경우 사용 하 여 새 프로젝트 만들기 ``dotnet new mvc --auth Individual``합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-127">If using the .NET Core CLI, create the new project using ``dotnet new mvc --auth Individual``.</span></span> <span data-ttu-id="94386-128">이 명령은 Visual Studio 만듭니다 Identity 템플릿 코드와 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94386-128">This command creates a new project with the same Identity template code Visual Studio creates.</span></span>

    <span data-ttu-id="94386-129">만든된 프로젝트에 포함 되어는 `Microsoft.AspNetCore.Identity.EntityFrameworkCore` Id 데이터 및 스키마를 사용 하 여 SQL Server를 유지 하는 패키지 [Entity Framework Core](https://docs.microsoft.com/ef/)합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-129">The created project contains the `Microsoft.AspNetCore.Identity.EntityFrameworkCore` package, which persists the Identity data and schema to SQL Server using [Entity Framework Core](https://docs.microsoft.com/ef/).</span></span>

    ---

2.  <span data-ttu-id="94386-130">Id 서비스를 구성 하 고 미들웨어에서 추가 `Startup`합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-130">Configure Identity services and add middleware in `Startup`.</span></span>

    <span data-ttu-id="94386-131">Id 서비스에서 응용 프로그램에 추가 되는 `ConfigureServices` 에서 메서드는 `Startup` 클래스:</span><span class="sxs-lookup"><span data-stu-id="94386-131">The Identity services are added to the application in the `ConfigureServices` method in the `Startup` class:</span></span>

    # <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="94386-132">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="94386-132">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)
    
    [!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,11-28,30-39)]
    
    <span data-ttu-id="94386-133">이러한 서비스를 통해 응용 프로그램에서 사용할 수 [종속성 주입](xref:fundamentals/dependency-injection)합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-133">These services are made available to the application through [dependency injection](xref:fundamentals/dependency-injection).</span></span>
    
    <span data-ttu-id="94386-134">Identity를 호출 하 여 응용 프로그램에 대해 사용할 `UseAuthentication` 에 `Configure` 메서드.</span><span class="sxs-lookup"><span data-stu-id="94386-134">Identity is enabled for the application by calling `UseAuthentication` in the `Configure` method.</span></span> <span data-ttu-id="94386-135">`UseAuthentication`인증 추가 [미들웨어](xref:fundamentals/middleware) 요청 파이프라인을 합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-135">`UseAuthentication` adds authentication [middleware](xref:fundamentals/middleware) to the request pipeline.</span></span>
    
    [!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configure&highlight=17)]
    
    # <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="94386-136">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="94386-136">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)
    
    [!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,13-34)]
    
    <span data-ttu-id="94386-137">이러한 서비스를 통해 응용 프로그램에서 사용할 수 [종속성 주입](xref:fundamentals/dependency-injection)합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-137">These services are made available to the application through [dependency injection](xref:fundamentals/dependency-injection).</span></span>
    
    <span data-ttu-id="94386-138">Identity를 호출 하 여 응용 프로그램에 대해 사용할 `UseIdentity` 에 `Configure` 메서드.</span><span class="sxs-lookup"><span data-stu-id="94386-138">Identity is enabled for the application by calling `UseIdentity` in the `Configure` method.</span></span> <span data-ttu-id="94386-139">`UseIdentity`쿠키 기반 인증 추가 [미들웨어](xref:fundamentals/middleware) 요청 파이프라인을 합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-139">`UseIdentity` adds cookie-based authentication [middleware](xref:fundamentals/middleware) to the request pipeline.</span></span>
        
    [!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configure&highlight=21)]
    
    ---
     
    <span data-ttu-id="94386-140">프로세스를 응용 프로그램 시작에 대 한 자세한 내용은 참조 [응용 프로그램 시작](xref:fundamentals/startup)합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-140">For more information about the application start up process, see [Application Startup](xref:fundamentals/startup).</span></span>

3.  <span data-ttu-id="94386-141">사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94386-141">Create a user.</span></span>

    <span data-ttu-id="94386-142">응용 프로그램을 시작 하 고을 클릭는 **등록** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-142">Launch the application and then click on the **Register** link.</span></span>

    <span data-ttu-id="94386-143">처음이이 작업을 수행 하는 경우 마이그레이션을 실행 하는 데 필요한 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94386-143">If this is the first time you're performing this action, you may be required to run migrations.</span></span> <span data-ttu-id="94386-144">응용 프로그램 하 라는 메시지가 표시 **적용 마이그레이션**합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-144">The application prompts you to **Apply Migrations**.</span></span> <span data-ttu-id="94386-145">필요한 경우 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="94386-145">Refresh the page if needed.</span></span>
    
    ![마이그레이션 웹 페이지를 적용 합니다.](identity/_static/apply-migrations.png)
    
    <span data-ttu-id="94386-147">또는 영구 데이터베이스 없이 응용 프로그램과 함께 ASP.NET Core Id를 사용 하 여 메모리 내 데이터베이스를 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94386-147">Alternately, you can test using ASP.NET Core Identity with your app without a persistent database by using an in-memory database.</span></span> <span data-ttu-id="94386-148">메모리 내 데이터베이스를 사용 하려면 추가 ``Microsoft.EntityFrameworkCore.InMemory`` 앱 패키지 및 응용 프로그램의 호출을 수정 ``AddDbContext`` 에 ``ConfigureServices`` 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="94386-148">To use an in-memory database, add the ``Microsoft.EntityFrameworkCore.InMemory`` package to your app and modify your app's call to ``AddDbContext`` in ``ConfigureServices`` as follows:</span></span>

    ```csharp
    services.AddDbContext<ApplicationDbContext>(options =>
        options.UseInMemoryDatabase(Guid.NewGuid().ToString()));
    ```
    
    <span data-ttu-id="94386-149">사용자가 클릭할 때는 **등록** 링크는 ``Register`` 에서 동작이 호출 될 ``AccountController``합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-149">When the user clicks the **Register** link, the ``Register`` action is invoked on ``AccountController``.</span></span> <span data-ttu-id="94386-150">``Register`` 동작 호출 하 여 사용자를 만듭니다 `CreateAsync` 에 `_userManager` 개체 (제공 된 ``AccountController`` 종속성 주입 하 여):</span><span class="sxs-lookup"><span data-stu-id="94386-150">The ``Register`` action creates the user by calling `CreateAsync` on the `_userManager` object (provided to ``AccountController`` by dependency injection):</span></span>
 
    [!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_register&highlight=11)]

    <span data-ttu-id="94386-151">에 대 한 호출 사용자가 로그인 된 사용자가 성공적으로 만들어진 경우 ``_signInManager.SignInAsync``합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-151">If the user was created successfully, the user is logged in by the call to ``_signInManager.SignInAsync``.</span></span>

    <span data-ttu-id="94386-152">**참고:** 참조 [계정 확인](xref:security/authentication/accconfirm#prevent-login-at-registration) 등록 시 즉시 로그인을 방지 하는 단계에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-152">**Note:** See [account confirmation](xref:security/authentication/accconfirm#prevent-login-at-registration) for steps to prevent immediate login at registration.</span></span>
 
4.  <span data-ttu-id="94386-153">로그인.</span><span class="sxs-lookup"><span data-stu-id="94386-153">Log in.</span></span>
 
    <span data-ttu-id="94386-154">사용자가 클릭 하 여 로그인 할 수는 **로그인** 사이트의 맨 위에 링크 될 수 있습니다 이동 하 게 될 로그인 페이지에 권한 부여를 요구 하는 사이트의 일부에 액세스 하려는 경우 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-154">Users can sign in by clicking the **Log in** link at the top of the site, or they may be navigated to the Login page if they attempt to access a part of the site that requires authorization.</span></span> <span data-ttu-id="94386-155">사용자가 로그인 페이지에 폼을 제출는 ``AccountController`` ``Login`` 작업을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-155">When the user submits the form on the Login page, the ``AccountController`` ``Login`` action is called.</span></span>

    <span data-ttu-id="94386-156">``Login`` 동작 호출 ``PasswordSignInAsync`` 에 ``_signInManager`` 개체 (제공 된 ``AccountController`` 종속성 주입 하 여).</span><span class="sxs-lookup"><span data-stu-id="94386-156">The ``Login`` action calls ``PasswordSignInAsync`` on the ``_signInManager`` object (provided to ``AccountController`` by dependency injection).</span></span>

    [!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_login&highlight=13-14)]
 
    <span data-ttu-id="94386-157">기본 ``Controller`` 클래스가 노출 한 ``User`` 컨트롤러 메서드에서 액세스할 수 있는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="94386-157">The base ``Controller`` class exposes a ``User`` property that you can access from controller methods.</span></span> <span data-ttu-id="94386-158">예를 들어, 열거할 수 있습니다 `User.Claims` 을 권한 부여 결정을 내립니다.</span><span class="sxs-lookup"><span data-stu-id="94386-158">For instance, you can enumerate `User.Claims` and make authorization decisions.</span></span> <span data-ttu-id="94386-159">자세한 내용은 참조 [권한 부여](xref:security/authorization/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-159">For more information, see [Authorization](xref:security/authorization/index).</span></span>
 
5.  <span data-ttu-id="94386-160">로그 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-160">Log out.</span></span>
 
    <span data-ttu-id="94386-161">클릭 하 고 **로그 아웃** 호출 연결는 `LogOut` 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-161">Clicking the **Log out** link calls the `LogOut` action.</span></span>
 
    [!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo/Controllers/AccountController.cs?name=snippet_logout&highlight=7)]
 
    <span data-ttu-id="94386-162">앞의 코드 호출 위에 `_signInManager.SignOutAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="94386-162">The preceding code above calls the `_signInManager.SignOutAsync` method.</span></span> <span data-ttu-id="94386-163">`SignOutAsync` 메서드 쿠키에 저장 하는 사용자의 클레임을 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="94386-163">The `SignOutAsync` method clears the user's claims stored in a cookie.</span></span>
 
6.  <span data-ttu-id="94386-164">구성입니다.</span><span class="sxs-lookup"><span data-stu-id="94386-164">Configuration.</span></span>

    <span data-ttu-id="94386-165">Id는 응용 프로그램의 시작 클래스에서 재정의할 수 있는 몇 가지 기본 동작에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94386-165">Identity has some default behaviors that you can override in your application's startup class.</span></span> <span data-ttu-id="94386-166">구성 하지 않아도 ``IdentityOptions`` 기본 동작을 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="94386-166">You do not need to configure ``IdentityOptions`` if you are using the default behaviors.</span></span>

    # <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="94386-167">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="94386-167">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)
    
    [!code-csharp[Main](identity/sample/src/ASPNETv2-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=7-9,11-28,30-39)]
    
    # <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="94386-168">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="94386-168">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)
    
    [!code-csharp[Main](identity/sample/src/ASPNET-IdentityDemo/Startup.cs?name=snippet_configureservices&highlight=13-34)]

    ---
    
    <span data-ttu-id="94386-169">Id를 구성 하는 방법에 대 한 자세한 내용은 참조 [구성 Identity](xref:security/authentication/identity-configuration)합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-169">For more information about how to configure Identity, see [Configure Identity](xref:security/authentication/identity-configuration).</span></span>
    
    <span data-ttu-id="94386-170">기본 키의 데이터 형식을 구성할 수 참조 [Id 구성 기본 키 데이터 형식이](xref:security/authentication/identity-primary-key-configuration)합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-170">You also can configure the data type of the primary key, see [Configure Identity primary keys data type](xref:security/authentication/identity-primary-key-configuration).</span></span>
 
7.  <span data-ttu-id="94386-171">데이터베이스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="94386-171">View the database.</span></span>

    <span data-ttu-id="94386-172">앱 (Windows와 Visual Studio 사용자에 대 한 기본값)는 SQL Server 데이터베이스를 사용 하는 경우에 만든 응용 프로그램 데이터베이스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94386-172">If your app is using a SQL Server database (the default on Windows and for Visual Studio users), you can view the database the app created.</span></span> <span data-ttu-id="94386-173">사용할 수 있습니다 **SQL Server Management Studio**합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-173">You can use **SQL Server Management Studio**.</span></span> <span data-ttu-id="94386-174">또는 Visual Studio에서 선택 **보기** > **SQL Server 개체 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-174">Alternatively, from Visual Studio, select **View** > **SQL Server Object Explorer**.</span></span> <span data-ttu-id="94386-175">연결할 **(localdb) \MSSQLLocalDB**합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-175">Connect to **(localdb)\MSSQLLocalDB**.</span></span> <span data-ttu-id="94386-176">일치 하는 이름을 사용 하 여 데이터베이스 **aspnet-<*프로젝트의 이름*>-<*날짜 문자열* >**  표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94386-176">The database with a name matching **aspnet-<*name of your project*>-<*date string*>** is displayed.</span></span>

    ![AspNetUsers 데이터베이스 테이블에 대 한 상황에 맞는 메뉴](identity/_static/04-db.png)
    
    <span data-ttu-id="94386-178">데이터베이스 확장 및 해당 **테이블**를 마우스 오른쪽 단추로 클릭 한 다음는 **dbo입니다. AspNetUsers** 테이블을 선택한 **데이터 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-178">Expand the database and its **Tables**, then right-click the **dbo.AspNetUsers** table and select **View Data**.</span></span>

8. <span data-ttu-id="94386-179">Identity 작동 확인</span><span class="sxs-lookup"><span data-stu-id="94386-179">Verify Identity works</span></span>

    <span data-ttu-id="94386-180">기본 *ASP.NET Core 웹 응용 프로그램* 프로젝트 템플릿이 필요 없이 응용 프로그램에서 모든 작업에 액세스할 수 있도록 로그인에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94386-180">The default *ASP.NET Core Web Application* project template allows users to access any action in the application without having to login.</span></span> <span data-ttu-id="94386-181">ASP.NET Identity 작동 하는지 확인 하려면 추가`[Authorize]` 특성을 `About` 의 작업은 `Home` 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="94386-181">To verify that ASP.NET Identity works, add an`[Authorize]` attribute to the `About` action of the `Home` Controller.</span></span>
 
    ```cs
    [Authorize]
    public IActionResult About()
    {
        ViewData["Message"] = "Your application description page.";
        return View();
    }
    ```
    
    # <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="94386-182">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="94386-182">Visual Studio</span></span>](#tab/visual-studio)

    <span data-ttu-id="94386-183">사용 하 여 프로젝트 실행 **Ctrl** + **F5** 로 이동 하 고는 **에 대 한** 페이지.</span><span class="sxs-lookup"><span data-stu-id="94386-183">Run the project using **Ctrl** + **F5** and navigate to the **About** page.</span></span> <span data-ttu-id="94386-184">인증 된 사용자만 액세스할 수 있습니다는 **에 대 한** 페이지 이제 하므로 ASP.NET에 로그인 하거나 등록 로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="94386-184">Only authenticated users may access the **About** page now, so ASP.NET redirects you to the login page to login or register.</span></span>

    # <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="94386-185">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="94386-185">.NET Core CLI</span></span>](#tab/netcore-cli)

    <span data-ttu-id="94386-186">명령 창을 열고 프로젝트의 루트 디렉터리로 이동 포함 된 디렉터리는 `.csproj` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="94386-186">Open a command window and navigate to the project's root directory containing the `.csproj` file.</span></span> <span data-ttu-id="94386-187">실행 된 `dotnet run` 명령을 앱을 실행 하려면:</span><span class="sxs-lookup"><span data-stu-id="94386-187">Run the `dotnet run` command to run the app:</span></span>

    ```cs
    dotnet run 
    ```

    <span data-ttu-id="94386-188">검색의 출력에 지정 된 URL의 `dotnet run` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="94386-188">Browse the URL specified in the output from the `dotnet run` command.</span></span> <span data-ttu-id="94386-189">URL 가리키는 `localhost` 생성 된 포트 번호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-189">The URL should point to `localhost` with a generated port number.</span></span> <span data-ttu-id="94386-190">탐색 하 고 **에 대 한** 페이지.</span><span class="sxs-lookup"><span data-stu-id="94386-190">Navigate to the **About** page.</span></span> <span data-ttu-id="94386-191">인증 된 사용자만 액세스할 수 있습니다는 **에 대 한** 페이지 이제 하므로 ASP.NET에 로그인 하거나 등록 로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="94386-191">Only authenticated users may access the **About** page now, so ASP.NET redirects you to the login page to login or register.</span></span>

    ---

## <a name="identity-components"></a><span data-ttu-id="94386-192">Identity 구성 요소</span><span class="sxs-lookup"><span data-stu-id="94386-192">Identity Components</span></span>

<span data-ttu-id="94386-193">Id 시스템에 대 한 기본 참조 어셈블리는 `Microsoft.AspNetCore.Identity`합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-193">The primary reference assembly for the Identity system is `Microsoft.AspNetCore.Identity`.</span></span> <span data-ttu-id="94386-194">이 패키지 ASP.NET Core Id에 대 한 인터페이스의 핵심 집합으로 포함 되어 있으며 `Microsoft.AspNetCore.Identity.EntityFrameworkCore`합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-194">This package contains the core set of interfaces for ASP.NET Core Identity, and is included by `Microsoft.AspNetCore.Identity.EntityFrameworkCore`.</span></span>

<span data-ttu-id="94386-195">이러한 종속성 ASP.NET Core 응용 프로그램의 Id 시스템을 사용 하려면 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-195">These dependencies are needed to use the Identity system in ASP.NET Core applications:</span></span>

* <span data-ttu-id="94386-196">`Microsoft.AspNetCore.Identity.EntityFrameworkCore`-Identity Entity Framework Core 사용 시 필요한 형식을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-196">`Microsoft.AspNetCore.Identity.EntityFrameworkCore` - Contains the required types to use Identity with Entity Framework Core.</span></span>

* <span data-ttu-id="94386-197">`Microsoft.EntityFrameworkCore.SqlServer`-Entity Framework Core는 SQL Server와 같은 관계형 데이터베이스에 대 한 Microsoft의 권장 되는 데이터 액세스 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="94386-197">`Microsoft.EntityFrameworkCore.SqlServer` - Entity Framework Core is Microsoft's recommended data access technology for relational databases like SQL Server.</span></span> <span data-ttu-id="94386-198">테스트를 위해 사용할 수 있습니다 `Microsoft.EntityFrameworkCore.InMemory`합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-198">For testing, you can use `Microsoft.EntityFrameworkCore.InMemory`.</span></span>

* <span data-ttu-id="94386-199">`Microsoft.AspNetCore.Authentication.Cookies`-앱이 쿠키 기반 인증을 사용할 수 있도록 하는 미들웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="94386-199">`Microsoft.AspNetCore.Authentication.Cookies` - Middleware that enables an app to use cookie-based authentication.</span></span>

## <a name="migrating-to-aspnet-core-identity"></a><span data-ttu-id="94386-200">ASP.NET Core Id로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="94386-200">Migrating to ASP.NET Core Identity</span></span>

<span data-ttu-id="94386-201">추가 정보 및 기존 본인 마이그레이션하는 방법에 대 한 지침을 참조 저장 [마이그레이션 인증 및 Id](xref:migration/identity)합니다.</span><span class="sxs-lookup"><span data-stu-id="94386-201">For additional information and guidance on migrating your existing Identity store see [Migrating Authentication and Identity](xref:migration/identity).</span></span>

## <a name="next-steps"></a><span data-ttu-id="94386-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="94386-202">Next Steps</span></span>

* [<span data-ttu-id="94386-203">인증 및 ID 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="94386-203">Migrating Authentication and Identity</span></span>](xref:migration/identity)
* [<span data-ttu-id="94386-204">계정 확인 및 암호 복구</span><span class="sxs-lookup"><span data-stu-id="94386-204">Account Confirmation and Password Recovery</span></span>](xref:security/authentication/accconfirm)
* [<span data-ttu-id="94386-205">SMS를 사용한 2단계 인증</span><span class="sxs-lookup"><span data-stu-id="94386-205">Two-factor authentication with SMS</span></span>](xref:security/authentication/2fa)
* [<span data-ttu-id="94386-206">Facebook, Google 및 기타 외부 공급자를 통해 인증 사용</span><span class="sxs-lookup"><span data-stu-id="94386-206">Enabling authentication using Facebook, Google and other external providers</span></span>](xref:security/authentication/social/index)