---
title: "ASP.NET Core에서 HTTP.sys 웹 서버 구현"
author: tdykstra
description: "Windows의 ASP.NET Core에 대한 웹 서버인 HTTP.sys에 대해 알아봅니다. HTTP.sys 커널 모드 드라이버를 기반으로 한 HTTP.sys는 IIS 없이 인터넷에 대한 직접 연결에 사용될 수 있는 Kestrel에 대한 대안입니다."
manager: wpickett
ms.author: tdykstra
ms.custom: mvc
ms.date: 03/13/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/servers/httpsys
ms.openlocfilehash: d7ae6c070c7eecfd714086e15f32eff96c0943d9
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="httpsys-web-server-implementation-in-aspnet-core"></a>ASP.NET Core에서 HTTP.sys 웹 서버 구현

작성자: [Tom Dykstra](https://github.com/tdykstra), [Chris Ross](https://github.com/Tratcher), [Luke Latham](https://github.com/guardrex)

> [!NOTE]
> 이 주제는 ASP.NET Core 2.0 이상에 적용됩니다. 이전 버전의 ASP.NET Core에서 HTTP.sys는 [WebListener](xref:fundamentals/servers/weblistener)라고 합니다.

[HTTP.sys](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture#hypertext-transfer-protocol-stack-httpsys)는 Windows에서만 실행되는 [ASP.NET Core에 대한 웹 서버](xref:fundamentals/servers/index)입니다. HTTP.sys는 [Kestrel](xref:fundamentals/servers/kestrel)에 대한 대안이며 Kestel이 제공하지 않는 일부 기능을 제공합니다.

> [!IMPORTANT]
> HTTP.sys는 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)과 호환되지 않으므로 IIS 또는 IIS Express와 함께 사용될 수 없습니다.

HTTP.sys는 다음과 같은 기능을 지원합니다.

* [Windows 인증](xref:security/authentication/windowsauth)
* 포트 공유
* SNI를 사용하는 HTTPS
* TLS를 통한 HTTP/2(Windows 10 이상)
* 직접 파일 전송
* 응답 캐싱
* WebSockets(Windows 8 이상)

지원되는 Windows 버전:

* Windows 7 이상
* Windows Server 2008 R2 이상

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/httpsys/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="when-to-use-httpsys"></a>HTTP.sys를 사용하는 경우

HTTP.sys는 다음과 같은 배포에 유용합니다.

* IIS를 사용하지 않고 인터넷에 서버를 직접 노출해야 하는 경우

  ![HTTP.sys는 인터넷과 직접 통신합니다.](httpsys/_static/httpsys-to-internet.png)

* 내부 배포에는 [Windows 인증](xref:security/authentication/windowsauth)처럼 Kestrel에서 사용할 수 없는 기능이 필요합니다.

  ![HTTP.sys는 내부 네트워크와 직접 통신합니다.](httpsys/_static/httpsys-to-internal.png)

HTTP.sys는 많은 유형의 공격으로부터 보호하고 모든 기능을 갖춘 웹 서버의 견고성, 보안 및 확장성을 제공하는 완성도 높은 기술입니다. IIS 자체는 HTTP.sys 위에 HTTP 수신기로 실행됩니다. 

## <a name="how-to-use-httpsys"></a>HTTP.sys 사용 방법

### <a name="configure-the-aspnet-core-app-to-use-httpsys"></a>HTTP.sys를 사용하도록 ASP.NET Core 앱 구성

1. [Microsoft.AspNetCore.All 메타패키지](xref:fundamentals/metapackage)([nuget.org](https://www.nuget.org/packages/Microsoft.AspNetCore.All/))(ASP.NET Core 2.0 이상)를 사용할 경우 프로젝트 파일의 패키지 참조가 필요하지 않습니다. `Microsoft.AspNetCore.All` 메타패키지를 사용하지 않는 경우 [Microsoft.AspNetCore.Server.HttpSys](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.HttpSys/)에 패키지 참조를 추가합니다.

1. 웹 호스트를 빌드할 때 [UseHttpSys](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderhttpsysextensions.usehttpsys) 확장 메서드를 호출하여 필요한 [HTTP.sys 옵션](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions)을 지정합니다.

   [!code-csharp[](httpsys/sample/Program.cs?name=snippet1&highlight=4-12)]

   추가 HTTP.sys 구성은 [레지스트리 설정](https://support.microsoft.com/kb/820129)을 통해 처리됩니다.

   **HTTP.sys 옵션**

   | 속성 | 설명 | 기본 |
   | -------- | ----------- | :-----: |
   | [AllowSynchronousIO](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.allowsynchronousio) | `HttpContext.Request.Body` 및 `HttpContext.Response.Body`에 대해 동기 입력/출력이 허용되는지 여부를 제어합니다. | `true` |
   | [Authentication.AllowAnonymous](/dotnet/api/microsoft.aspnetcore.server.httpsys.authenticationmanager.allowanonymous) | 익명 요청을 허용합니다. | `true` |
   | [Authentication.Schemes](/dotnet/api/microsoft.aspnetcore.server.httpsys.authenticationmanager.schemes) | 허용되는 인증 체계를 지정합니다. 수신기를 삭제하기 전에 언제든지 수정할 수 있습니다. 값은 [AuthenticationSchemes 열거형](/dotnet/api/microsoft.aspnetcore.server.httpsys.authenticationschemes): `Basic`, `Kerberos`, `Negotiate`, `None`, `NTLM`에서 제공됩니다. | `None` |
   | [EnableResponseCaching](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.enableresponsecaching) | 적합한 헤더가 있는 응답에 대해 [커널 모드](/windows-hardware/drivers/gettingstarted/user-mode-and-kernel-mode) 캐싱을 시도합니다. 응답에 `Set-Cookie`, `Vary` 또는 `Pragma` 헤더가 포함될 수 없습니다. `public` 및 `shared-max-age` 또는 `max-age` 값인 `Cache-Control` 헤더나 `Expires` 헤더가 포함되어야 합니다. | `true` |
   | [MaxAccepts](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.maxaccepts) | 최대 동시 승인 수입니다. | 5 &times; [Environment.<br>ProcessorCount](/dotnet/api/system.environment.processorcount) |
   | [MaxConnections](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.maxconnections) | 허용되는 최대 동시 연결 수입니다. 무한의 경우 `-1`을 사용합니다. 레지스트리의 시스템 수준 설정을 사용하려면 `null`을 사용합니다. | `null`<br>(제한 없음) |
   | [MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.maxrequestbodysize) | <a href="#maxrequestbodysize">MaxRequestBodySize</a> 섹션을 참조하세요. | 30000000바이트<br>(~28.6MB) |
   | [RequestQueueLimit](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.requestqueuelimit) | 큐에 대기할 수 있는 최대 요청 수입니다. | 1000 |
   | [ThrowWriteExceptions](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.throwwriteexceptions) | 클라이언트 연결 해제로 인해 실패한 응답 본문 쓰기가 예외를 throw하거나 정상적으로 완료되어야 하는지 여부를 나타납니다. | `false`<br>(정상적으로 완료) |
   | [Timeouts](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts) | 레지스트리에 구성될 수도 있는 HTTP.sys [TimeoutManager](/dotnet/api/microsoft.aspnetcore.server.httpsys.timeoutmanager) 구성을 표시합니다. API 링크를 따라 기본값을 포함하여 각 설정에 대해 자세히 알아보세요.<ul><li>[Timeouts.DrainEntityBody](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.drainentitybody) &ndash; HTTP 서버 API가 지속적 연결에서 엔터티 본문을 비우는 데 허용되는 시간입니다.</li><li>[Timeouts.EntityBody](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.entitybody) &ndash; 요청 엔터티가 도착하는 데 허용되는 시간입니다.</li><li>[Timeouts.HeaderWait](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.headerwait) &ndash; HTTP 서버 API가 요청 헤더를 구문 분석하는 데 허용되는 시간입니다.</li><li>[Timeouts.IdleConnection](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.idleconnection) &ndash; 유휴 연결에 허용되는 시간입니다.</li><li>[Timeouts.MinSendBytesPerSecond](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.minsendbytespersecond) &ndash; 응답에 대한 최소 전송 속도입니다.</li><li>[Timeouts.RequestQueue](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.timeouts.requestqueue) &ndash; 앱이 선택하기 전에 요청이 요청 큐에 남아 있는 데 허용되는 시간입니다.</li></ul> |  |
   | [UrlPrefixes](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.urlprefixes) | [UrlPrefixCollection](/dotnet/api/microsoft.aspnetcore.server.httpsys.urlprefixcollection)을 지정하여 HTTP.sys를 등록합니다. 컬렉션에 접두사를 추가하는 데 사용되는 [UrlPrefixCollection.Add](/dotnet/api/microsoft.aspnetcore.server.httpsys.urlprefixcollection.add)가 가장 유용합니다. 이러한 API는 수신기를 삭제하기 전에 언제든지 수정할 수 있습니다. |  |

   <a name="maxrequestbodysize"></a>
   **MaxRequestBodySize**

   요청 본문에 대해 허용되는 최대 크기(바이트)입니다. `null`로 설정하면 최대 요청 본문 크기는 무제한입니다. 항상 무제한인 업그레이드된 연결에는 이 제한이 영향을 미치지 않습니다.

   단일 `IActionResult`에 대해 ASP.NET Core MVC 앱에서 제한을 재정의할 때는 작업 메서드에서 [RequestSizeLimitAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requestsizelimitattribute) 특성을 사용하는 방법이 좋습니다.
   
   ```csharp
   [RequestSizeLimit(100000000)]
   public IActionResult MyActionMethod()
   ```

   앱에서 요청을 읽기 시작한 후 요청에 대한 제한을 구성하려고 하면 예외가 throw됩니다. `IsReadOnly` 속성을 사용하여 `MaxRequestBodySize` 속성이 제한을 구성하기에 너무 늦은, 읽기 전용 상태인지를 나타낼 수 있습니다.

   앱에서 요청별로 [MaxRequestBodySize](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.maxrequestbodysize)를 재정의해야 하는 경우 [IHttpMaxRequestBodySizeFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttpmaxrequestbodysizefeature)를 사용합니다.

   [!code-csharp[](httpsys/sample/Startup.cs?name=snippet1&highlight=6-7)]

1. Visual Studio를 사용하는 경우 앱이 IIS 또는 IIS Express를 실행하도록 구성되지 않았는지 확인합니다.

   Visual Studio에서 기본 실행 프로필은 IIS Express용입니다. 프로젝트를 콘솔 앱으로 실행하려면 다음 스크린샷에 표시된 것처럼 선택한 프로필을 수동으로 변경합니다.

   ![콘솔 앱 프로필 선택](httpsys/_static/vs-choose-profile.png)

### <a name="configure-windows-server"></a>Windows Server 구성

1. 앱이 [프레임워크 종속 배포](/dotnet/core/deploying/#framework-dependent-deployments-fdd)인 경우 .NET Core, .NET Framework 또는 둘 다(앱이 NET Framework를 대상으로 하는 .NET Core 앱인 경우)를 설치합니다.

   * **.NET Core** &ndash; 앱에 .NET Core가 필요한 경우 [.NET 다운로드](https://www.microsoft.com/net/download/windows)에서 .NET Core 설치 관리자를 가져와 실행합니다.
   * **.NET Framework** &ndash; 앱에 .NET Framework가 필요한 경우 [.NET Framework: 설치 가이드](/dotnet/framework/install/)를 참조하여 설치 지침을 확인합니다. 필수 .NET Framework를 설치합니다. 최신 .NET Framework의 설치 관리자는 [.NET 다운로드](https://www.microsoft.com/net/download/windows)에서 찾을 수 있습니다.

1. 앱에 대한 URL 및 포트를 구성합니다.

   기본적으로 ASP.NET Core는 `http://localhost:5000`으로 바인딩합니다. URL 접두사 및 포트를 구성하려면 다음을 사용하는 옵션이 포함됩니다.

   * [UseUrls](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useurls)
   * `urls` 명령줄 인수
   * `ASPNETCORE_URLS`환경 변수
   * [UrlPrefixes](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.urlprefixes)

   다음 코드 예제에서는 [UrlPrefixes](/dotnet/api/microsoft.aspnetcore.server.httpsys.httpsysoptions.urlprefixes)를 사용하는 방법을 보여줍니다.

   [!code-csharp[](httpsys/sample/Program.cs?name=snippet1&highlight=11)]

   `UrlPrefixes`의 장점은 형식이 잘못된 접두사에 대해 오류 메시지가 즉시 생성된다는 점입니다.

   `UrlPrefixes`의 설정은 `UseUrls`/`urls`/`ASPNETCORE_URLS` 설정을 재정의합니다. 따라서 `UseUrls`, `urls` 및 `ASPNETCORE_URLS` 환경 변수의 장점은 Kestrel과 HTTP.sys 간을 쉽게 전환할 수 있다는 점입니다. `UseUrls`, `urls` 및 `ASPNETCORE_URLS`에 대한 자세한 내용은 [호스팅](xref:fundamentals/hosting)을 참조하세요.

   HTTP.sys는 [HTTP Server API UrlPrefix 문자열 형식](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)을 사용합니다.

   > [!WARNING]
   > 최상위 와일드카드 바인딩(`http://*:80/` 및 `http://+:80`)을 사용하지 **않아야** 합니다. 최상위 와일드카드 바인딩은 보안 취약점에 앱을 노출시킬 수 있습니다. 강력한 와일드카드와 약한 와일드카드 모두에 적용됩니다. 와일드카드보다는 명시적 호스트 이름을 사용합니다. 전체 부모 도메인을 제어하는 경우 하위 도메인 와일드카드 바인딩(예: `*.mysub.com`)에는 이러한 보안 위험이 없습니다(취약한 `*.com`과 반대임). 자세한 내용은 [rfc7230 섹션-5.4](https://tools.ietf.org/html/rfc7230#section-5.4)를 참조하세요.

1. URL 접두사를 미리 등록하여 HTTP.sys에 대해 바인딩하고 x.509 인증서를 설정합니다.

   URL 접두사가 Windows에 미리 등록되어 있지 않은 경우 관리자 권한으로 앱을 실행합니다. 1024보다 큰 포트 번호로 HTTP(HTTPS 아님)를 사용하여 localhost에 바인딩하는 경우에만 관리자 권한이 필요하지 않습니다.

   1. HTTP.sys 구성에 대한 기본 제공 도구는 *netsh.exe*입니다. *netsh.exe*는 URL 접두사를 예약하고 X.509 인증서를 할당하는 데 사용됩니다. 도구를 사용하려면 관리자 권한이 필요합니다.

      다음 예제에서는 포트 80 및 443에 대해 URL 접두사를 예약하는 명령을 보여줍니다.

      ```console
      netsh http add urlacl url=http://+:80/ user=Users
      netsh http add urlacl url=https://+:443/ user=Users
      ```

      다음 예제에서는 X.509 인증서를 할당하는 방법을 보여줍니다.

      ```console
      netsh http add sslcert ipport=0.0.0.0:443 certhash=MyCertHash_Here appid={00000000-0000-0000-0000-000000000000}"
      ```

      *netsh.exe*에 대한 참조 문서입니다.

      * [HTTP(Hypertext Transfer Protocol)에 대한 Netsh 명령](https://technet.microsoft.com/library/cc725882.aspx)
      * [UrlPrefix 문자열](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)

   1. 필요한 경우, 자체 서명 X.509 인증서를 생성합니다.

     [!INCLUDE[How to make an X.509 cert](../../includes/make-x509-cert.md)]

1. 방화벽 포트를 열어 HTTP.sys에 도달하는 트래픽을 허용합니다. *netsh.exe* 또는 [PowerShell cmdlet](https://technet.microsoft.com/library/jj554906)을 사용합니다.

## <a name="additional-resources"></a>추가 자료

* [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)(HTTP 서버 API)
* [aspnet/HttpSysServer GitHub 리포지토리(소스 코드)](https://github.com/aspnet/HttpSysServer/)
* [호스팅](xref:fundamentals/hosting)
