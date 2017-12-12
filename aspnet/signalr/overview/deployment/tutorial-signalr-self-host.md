---
uid: signalr/overview/deployment/tutorial-signalr-self-host
title: "자습서: 자체 호스트 하 SignalR | Microsoft Docs"
author: pfletcher
description: "이 자습서에는 자체 호스팅된 SignalR 2 서버를 만드는 방법과 JavaScript 클라이언트와 연결 하는 방법을 보여 줍니다. V 자습서에 사용 된 소프트웨어 버전 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: 400db427-27af-4f2f-abf0-5486d5e024b5
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/deployment/tutorial-signalr-self-host
msc.type: authoredcontent
ms.openlocfilehash: 997756ff8d48e41da981491d6154f3107ec7a051
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="tutorial-signalr-self-host"></a><span data-ttu-id="8f661-104">자습서: SignalR 자체 호스트</span><span class="sxs-lookup"><span data-stu-id="8f661-104">Tutorial: SignalR Self-Host</span></span>
====================
<span data-ttu-id="8f661-105">으로 [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="8f661-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[<span data-ttu-id="8f661-106">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/SignalR-Self-Host-Sample-6da0f383)

> <span data-ttu-id="8f661-107">이 자습서에는 자체 호스팅된 SignalR 2 서버를 만드는 방법과 JavaScript 클라이언트와 연결 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-107">This tutorial shows how to create a self-hosted SignalR 2 server, and how to connect to it with a JavaScript client.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="8f661-108">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="8f661-108">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="8f661-109">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="8f661-109">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="8f661-110">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="8f661-110">.NET 4.5</span></span>
> - <span data-ttu-id="8f661-111">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="8f661-111">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a><span data-ttu-id="8f661-112">이 자습서와 함께 Visual Studio 2012를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="8f661-112">Using Visual Studio 2012 with this tutorial</span></span>
> 
> 
> <span data-ttu-id="8f661-113">이 자습서와 함께 Visual Studio 2012를 사용 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-113">To use Visual Studio 2012 with this tutorial, do the following:</span></span>
> 
> - <span data-ttu-id="8f661-114">업데이트 프로그램 [패키지 관리자](http://docs.nuget.org/docs/start-here/installing-nuget) 를 최신 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-114">Update your [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) to the latest version.</span></span>
> - <span data-ttu-id="8f661-115">설치는 [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-115">Install the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> - <span data-ttu-id="8f661-116">웹 플랫폼 설치 관리자에서 검색 하 고 설치 **ASP.NET 및 Visual Studio 2012 용 웹 도구 2013.1**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-116">In the Web Platform Installer, search for and install **ASP.NET and Web Tools 2013.1 for Visual Studio 2012**.</span></span> <span data-ttu-id="8f661-117">SignalR 클래스에 대 한 Visual Studio 템플릿을와 같은 설치 **허브**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-117">This will install Visual Studio templates for SignalR classes such as **Hub**.</span></span>
> - <span data-ttu-id="8f661-118">일부 서식 파일 (와 같은 **OWIN 시작 클래스**)은 사용할 수 없습니다; 이러한 경우에 대 한 클래스 파일을 대신 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-118">Some templates (such as **OWIN Startup Class**) will not be available; for these, use a Class file instead.</span></span>
> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="8f661-119">질문이 나 의견이</span><span class="sxs-lookup"><span data-stu-id="8f661-119">Questions and comments</span></span>
> 
> <span data-ttu-id="8f661-120">이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="8f661-120">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="8f661-121">자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-121">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="overview"></a><span data-ttu-id="8f661-122">개요</span><span class="sxs-lookup"><span data-stu-id="8f661-122">Overview</span></span>

<span data-ttu-id="8f661-123">SignalR 서버는 일반적으로 IIS에서 ASP.NET 응용 프로그램에서 호스트 하지만 자체 호스팅 수도 있습니다 (예: 콘솔 응용 프로그램 또는 Windows 서비스)를 자체 호스팅하는 라이브러리를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-123">A SignalR server is usually hosted in an ASP.NET application in IIS, but it can also be self-hosted (such as in a console application or Windows service) using the self-host library.</span></span> <span data-ttu-id="8f661-124">모든 SignalR 2 마찬가지로이 라이브러리는 OWIN 기반 ([.NET에 대 한 Open Web Interface](http://owin.org)).</span><span class="sxs-lookup"><span data-stu-id="8f661-124">This library, like all of SignalR 2, is built on OWIN ([Open Web Interface for .NET](http://owin.org)).</span></span> <span data-ttu-id="8f661-125">OWIN은.NET 웹 서버와 웹 응용 프로그램 간의 추상화를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-125">OWIN defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="8f661-126">OWIN은 OWIN를 자체 IIS 외부의 사용자가 소유한 프로세스에는 웹 응용 프로그램을 호스트 하기에 이상적인는 서버에서 웹 응용 프로그램을 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-126">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>

<span data-ttu-id="8f661-127">IIS에서 호스팅하지 이유는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-127">Reasons for not hosting in IIS include:</span></span>

- <span data-ttu-id="8f661-128">IIS이 환경 사용할 수 없거나 에이전트 설치가 바람직하지 IIS 없이 기존 서버 팜에 등입니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-128">Environments where IIS is not available or desirable, such as an existing server farm without IIS.</span></span>
- <span data-ttu-id="8f661-129">IIS의 성능 오버 헤드를 방지할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-129">The performance overhead of IIS needs to be avoided.</span></span>
- <span data-ttu-id="8f661-130">SignalR 기능은 Windows 서비스, Azure 작업자 역할 또는 다른 프로세스에서 실행 되는 기존 응용 프로그램에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-130">SignalR functionality is to be added to an exising application that runs in a Windows Service, Azure worker role, or other process.</span></span>

<span data-ttu-id="8f661-131">성능상의 이유로 자체 호스트 솔루션을 개발 되 고, 경우 것이 좋습니다도 테스트의 성능 효과 확인할 때 IIS에서 호스트 응용 프로그램을입니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-131">If a solution is being developed as self-host for performance reasons, it's recommended to also test the application hosted in IIS to determine the performance benefit.</span></span>

<span data-ttu-id="8f661-132">이 자습서에는 다음 섹션이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-132">This tutorial contains the following sections:</span></span>

- [<span data-ttu-id="8f661-133">서버 만들기</span><span class="sxs-lookup"><span data-stu-id="8f661-133">Creating the server</span></span>](#server)
- [<span data-ttu-id="8f661-134">JavaScript 클라이언트와 서버에 액세스</span><span class="sxs-lookup"><span data-stu-id="8f661-134">Accessing the server with a JavaScript client</span></span>](#js)

<a id="server"></a>

## <a name="creating-the-server"></a><span data-ttu-id="8f661-135">서버 만들기</span><span class="sxs-lookup"><span data-stu-id="8f661-135">Creating the server</span></span>

<span data-ttu-id="8f661-136">이 자습서에서는 콘솔 응용 프로그램에서 호스팅되는 서버를 만들어야 하지만 모든 종류의 Windows 서비스, Azure 작업자 역할 등의 프로세스에서 서버를 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-136">In this tutorial, you'll create a server that's hosted in a console application, but the server can be hosted in any sort of process, such as a Windows service or Azure worker role.</span></span> <span data-ttu-id="8f661-137">Windows 서비스에서 SignalR 서버 호스팅에 대 한 샘플 코드를 보려면 [Windows 서비스에서 Self-Hosting SignalR](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-137">For sample code for hosting a SignalR server in a Windows Service, see [Self-Hosting SignalR in a Windows Service](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3).</span></span>

1. <span data-ttu-id="8f661-138">관리자 권한으로 Visual Studio 2013을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-138">Open Visual Studio 2013 with administrator privileges.</span></span> <span data-ttu-id="8f661-139">선택 **파일**, **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-139">Select **File**, **New Project**.</span></span> <span data-ttu-id="8f661-140">선택 **Windows** 아래는 **Visual C#** 에서 노드는 **템플릿** 창과 선택은 **콘솔 응용 프로그램** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="8f661-140">Select **Windows** under the **Visual C#** node in the **Templates** pane, and select the **Console Application** template.</span></span> <span data-ttu-id="8f661-141">새 프로젝트 "SignalRSelfHost" 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-141">Name the new project "SignalRSelfHost" and click **OK**.</span></span>

    ![](tutorial-signalr-self-host/_static/image1.png)
2. <span data-ttu-id="8f661-142">선택 하 여 라이브러리 패키지 관리자 콘솔을 열고 **도구**, **라이브러리 패키지 관리자**, **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-142">Open the library package manager console by selecting **Tools**, **Library Package Manager**, **Package Manager Console**.</span></span>
3. <span data-ttu-id="8f661-143">패키지 관리자 콘솔에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-143">In the package manager console, enter the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample1.ps1)]

    <span data-ttu-id="8f661-144">이 명령은 SignalR 2 Self-Host 라이브러리 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-144">This command adds the SignalR 2 Self-Host libraries to the project.</span></span>
4. <span data-ttu-id="8f661-145">패키지 관리자 콘솔에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-145">In the package manager console, enter the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample2.ps1)]

    <span data-ttu-id="8f661-146">이 명령은 Microsoft.Owin.Cors 라이브러리 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-146">This command adds the Microsoft.Owin.Cors library to the project.</span></span> <span data-ttu-id="8f661-147">이 라이브러리는 SignalR 및 서로 다른 도메인에 웹 페이지 클라이언트 호스팅하는 응용 프로그램에 필요한 도메인 간 지원을 위해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-147">This library will be used for cross-domain support, which is required for applications that host SignalR and a web page client in different domains.</span></span> <span data-ttu-id="8f661-148">이후 SignalR 서버와 다른 포트에서 웹 클라이언트 호스팅해서 합니다, 즉, 해당 도메인 간 이러한 구성 요소 간의 통신에 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-148">Since you'll be hosting the SignalR server and the web client on different ports, this means that cross-domain must be enabled for communication between these components.</span></span>
5. <span data-ttu-id="8f661-149">Program.cs의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-149">Replace the contents of Program.cs with the following code.</span></span>

    [!code-csharp[Main](tutorial-signalr-self-host/samples/sample3.cs)]

    <span data-ttu-id="8f661-150">위의 코드는 세 가지 클래스가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-150">The above code includes three classes:</span></span>

    - <span data-ttu-id="8f661-151">**프로그램**를 포함 하 여는 **Main** 메서드 주 실행 경로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-151">**Program**, including the **Main** method defining the primary path of execution.</span></span> <span data-ttu-id="8f661-152">이 방법에서는 웹 응용 프로그램 형식의 **시작** 지정된 된 URL에 따라 시작 됩니다 (`http://localhost:8080`).</span><span class="sxs-lookup"><span data-stu-id="8f661-152">In this method, a web application of type **Startup** is started at the specified URL (`http://localhost:8080`).</span></span> <span data-ttu-id="8f661-153">끝점에 보안에 필요한 경우에 SSL은 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-153">If security is required on the endpoint, SSL can be implemented.</span></span> <span data-ttu-id="8f661-154">참조 [하는 방법: SSL 인증서로 포트 구성](https://msdn.microsoft.com/en-us/library/ms733791.aspx) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-154">See [How to: Configure a Port with an SSL Certificate](https://msdn.microsoft.com/en-us/library/ms733791.aspx) for more information.</span></span>
    - <span data-ttu-id="8f661-155">**시작**, SignalR 서버에 대 한 구성을 포함 하는 클래스 (이 자습서에서는 유일한 구성 하는 데 `UseCors`)에 대 한 호출은 `MapSignalR`, 모든 허브 개체에 대 한 경로 프로젝트에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-155">**Startup**, the class containing the configuration for the SignalR server (the only configuration this tutorial uses is the call to `UseCors`), and the call to `MapSignalR`, which creates routes for any Hub objects in the project.</span></span>
    - <span data-ttu-id="8f661-156">**MyHub**, 응용 프로그램이 클라이언트에 제공 하는 SignalR 허브 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-156">**MyHub**, the SignalR Hub class that the application will provide to clients.</span></span> <span data-ttu-id="8f661-157">이 클래스에는 단일 메서드가 **보낼**, 메시지를 브로드캐스팅하려면 연결 된 다른 모든 클라이언트에 클라이언트에서 호출할 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-157">This class has a single method, **Send**, that clients will call to broadcast a message to all other connected clients.</span></span>
6. <span data-ttu-id="8f661-158">응용 프로그램을 컴파일하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-158">Compile and run the application.</span></span> <span data-ttu-id="8f661-159">서버가 실행 되는 주소를 콘솔 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-159">The address that the server is running should show in a console window.</span></span>

    ![](tutorial-signalr-self-host/_static/image2.png)
7. <span data-ttu-id="8f661-160">예외와 함께 실행이 실패 하면 `System.Reflection.TargetInvocationException was unhandled`, 관리자 권한으로 Visual Studio를 다시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-160">If execution fails with the exception `System.Reflection.TargetInvocationException was unhandled`, you will need to restart Visual Studio with administrator privileges.</span></span>
8. <span data-ttu-id="8f661-161">다음 섹션으로 진행 하기 전에 응용 프로그램을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-161">Stop the application before proceeding to the next section.</span></span>

<a id="js"></a>

## <a name="accessing-the-server-with-a-javascript-client"></a><span data-ttu-id="8f661-162">JavaScript 클라이언트와 서버에 액세스</span><span class="sxs-lookup"><span data-stu-id="8f661-162">Accessing the server with a JavaScript client</span></span>

<span data-ttu-id="8f661-163">이 섹션에서는에서 같은 JavaScript 클라이언트는 [시작 자습서](../getting-started/tutorial-getting-started-with-signalr.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-163">In this section, you'll use the same JavaScript client from the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="8f661-164">클라이언트에 허브 URL을 명시적으로 정의 하는 한 가지 수정을 칠할만 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-164">We'll only make one modification to the client, which is to explicitly define the hub URL.</span></span> <span data-ttu-id="8f661-165">자체 호스팅된 응용 프로그램 서버 되지 않을 수도 있습니다 반드시 (역방향 프록시 및 부하 분산 장치)로 인해 연결 URL과 동일한 주소에서 하므로 URL 요구를 명시적으로 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-165">With a self-hosted application, the server may not necessarily be at the same address as the connection URL (due to reverse proxies and load balancers), so the URL needs to be defined explicitly.</span></span>

1. <span data-ttu-id="8f661-166">**솔루션 탐색기**솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 **추가**, **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-166">In **Solution Explorer**, right-click on the solution and select **Add**, **New Project**.</span></span> <span data-ttu-id="8f661-167">선택 된 **웹** 노드를 선택한는 **ASP.NET 웹 응용 프로그램** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="8f661-167">Select the **Web** node, and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="8f661-168">"JavascriptClient" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-168">Name the project "JavascriptClient" and click **OK**.</span></span>

    ![](tutorial-signalr-self-host/_static/image3.png)
2. <span data-ttu-id="8f661-169">선택 된 **빈** 템플릿과 나머지 옵션이 선택 되지 않은 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-169">Select the **Empty** template, and leave the remaining options unselected.</span></span> <span data-ttu-id="8f661-170">선택 **프로젝트 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-170">Select **Create Project**.</span></span>

    ![](tutorial-signalr-self-host/_static/image4.png)
3. <span data-ttu-id="8f661-171">패키지 관리자 콘솔에서에서 "JavascriptClient" 프로젝트를 선택는 **기본 프로젝트** 드롭 다운 하 고 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-171">In the package manager console, select the "JavascriptClient" project in the **Default project** drop-down, and execute the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample4.ps1)]

    <span data-ttu-id="8f661-172">이 명령은 클라이언트에 넣어야 SignalR 및 JQuery 라이브러리를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-172">This command installs the SignalR and JQuery libraries that you'll need in the client.</span></span>
4. <span data-ttu-id="8f661-173">선택한 서버 프로젝트를 마우스 오른쪽 단추로 클릭 **추가**, **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-173">Right-click on your project and select **Add**, **New Item**.</span></span> <span data-ttu-id="8f661-174">선택 된 **웹** 노드와 HTML 페이지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-174">Select the **Web** node, and select HTML Page.</span></span> <span data-ttu-id="8f661-175">페이지 이름을 **Default.html**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-175">Name the page **Default.html**.</span></span>

    ![](tutorial-signalr-self-host/_static/image5.png)
5. <span data-ttu-id="8f661-176">새 HTML 페이지의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-176">Replace the contents of the new HTML page with the following code.</span></span> <span data-ttu-id="8f661-177">스크립트 참조 다음에 프로젝트의 Scripts 폴더에서 스크립트와 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-177">Verify that the script references here match the scripts in the Scripts folder of the project.</span></span>

    [!code-html[Main](tutorial-signalr-self-host/samples/sample5.html?highlight=31-32)]

    <span data-ttu-id="8f661-178">다음 코드 (위의 코드 샘플에 강조 표시) (뿐 아니라 SignalR 베타 버전 2로 코드를 업그레이드) Getting 과장 된 자습서에 사용 된 클라이언트에 대 한 추가입니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-178">The following code (highlighted in the code sample above) is the addition that you've made to the client used in the Getting Stared tutorial (in addition to upgrading the code to SignalR version 2 beta).</span></span> <span data-ttu-id="8f661-179">이 줄의 코드는 기본 연결 URL SignalR에 대 한 서버에 명시적으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-179">This line of code explicitly sets the base connection URL for SignalR on the server.</span></span>

    [!code-javascript[Main](tutorial-signalr-self-host/samples/sample6.js)]
6. <span data-ttu-id="8f661-180">솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 **시작 프로젝트 설정 중...** . 선택 된 **여러 개의 시작 프로젝트** 라디오 단추를 하 고 두 프로젝트의 설정 **동작** 를 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-180">Right-click on the solution, and select **Set Startup Projects...**. Select the **Multiple startup projects** radio button, and set both projects' **Action** to **Start**.</span></span>

    ![](tutorial-signalr-self-host/_static/image6.png)
7. <span data-ttu-id="8f661-181">"Default.html"를 마우스 오른쪽 단추로 클릭 하 고 선택 **시작 페이지로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-181">Right-click on "Default.html" and select **Set As Start Page**.</span></span>
8. <span data-ttu-id="8f661-182">응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-182">Run the application.</span></span> <span data-ttu-id="8f661-183">서버 및 페이지 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-183">The server and page will launch.</span></span> <span data-ttu-id="8f661-184">웹 페이지를 다시 로드 해야 할 수 있습니다 (또는 선택 **계속** 디버거에서) 서버를 시작 하기 전에 페이지를 로드 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="8f661-184">You may need to reload the web page (or select **Continue** in the debugger) if the page loads before the server is started.</span></span>
9. <span data-ttu-id="8f661-185">브라우저에서 메시지가 표시 되 면 사용자 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-185">In the browser, provide a username when prompted.</span></span> <span data-ttu-id="8f661-186">다른 브라우저 탭 또는 창에는 페이지의 URL을 복사 하 고 다른 사용자 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-186">Copy the page's URL into another browser tab or window and provide a different username.</span></span> <span data-ttu-id="8f661-187">시작 자습서에서와 같이 다른 브라우저 창에서 메시지를 보낼 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f661-187">You will be able to send messages from one browser pane to the other, as in the Getting Started tutorial.</span></span>