---
title: "ASP.NET Core에 대 한 응답 압축 미들웨어"
author: guardrex
description: "응답 압축 및 ASP.NET Core 응용 프로그램에서 응답 압축 미들웨어를 사용 하는 방법에 알아봅니다."
ms.author: riande
manager: wpickett
ms.date: 08/20/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: performance/response-compression
ms.openlocfilehash: 9270287b62f91ddb81d6a347dd583e1cbb32f3c3
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="response-compression-middleware-for-aspnet-core"></a><span data-ttu-id="463ea-103">ASP.NET Core에 대 한 응답 압축 미들웨어</span><span class="sxs-lookup"><span data-stu-id="463ea-103">Response Compression Middleware for ASP.NET Core</span></span>

<span data-ttu-id="463ea-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="463ea-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="463ea-105">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/response-compression/samples)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="463ea-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/response-compression/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="463ea-106">네트워크 대역폭은 제한 된 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-106">Network bandwidth is a limited resource.</span></span> <span data-ttu-id="463ea-107">일반적으로 응답의 크기를 줄이면 응용 프로그램의 응답성 종종 크게 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-107">Reducing the size of the response usually increases the responsiveness of an app, often dramatically.</span></span> <span data-ttu-id="463ea-108">페이로드 크기를 줄이기 위해 가지 방법은 응용 프로그램의 응답을 압축 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-108">One way to reduce payload sizes is to compress an app's responses.</span></span>

## <a name="when-to-use-response-compression-middleware"></a><span data-ttu-id="463ea-109">응답 압축 미들웨어를 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="463ea-109">When to use Response Compression Middleware</span></span>
<span data-ttu-id="463ea-110">IIS, Apache 또는 Nginx 응답 서버 기반 압축 기술을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-110">Use server-based response compression technologies in IIS, Apache, or Nginx.</span></span> <span data-ttu-id="463ea-111">미들웨어의 성능을 때문일 수와 일치 하지 않습니다 서버 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-111">The performance of the middleware probably won't match that of the server modules.</span></span> <span data-ttu-id="463ea-112">[HTTP.sys 서버의](xref:fundamentals/servers/httpsys) 및 [Kestrel](xref:fundamentals/servers/kestrel) 현재 기본 제공 압축 지원을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-112">[HTTP.sys server](xref:fundamentals/servers/httpsys) and [Kestrel](xref:fundamentals/servers/kestrel) don't currently offer built-in compression support.</span></span>

<span data-ttu-id="463ea-113">했으면 응답 압축 미들웨어를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-113">Use Response Compression Middleware when you're:</span></span>

* <span data-ttu-id="463ea-114">다음과 같은 서버 기반 압축 기술을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-114">Unable to use the following server-based compression technologies:</span></span>
  * [<span data-ttu-id="463ea-115">IIS 동적 압축이 모듈</span><span class="sxs-lookup"><span data-stu-id="463ea-115">IIS Dynamic Compression module</span></span>](https://www.iis.net/overview/reliability/dynamiccachingandcompression)
  * [<span data-ttu-id="463ea-116">Apache mod_deflate 모듈</span><span class="sxs-lookup"><span data-stu-id="463ea-116">Apache mod_deflate module</span></span>](http://httpd.apache.org/docs/current/mod/mod_deflate.html)
  * [<span data-ttu-id="463ea-117">Nginx 압축 및 압축 풀기</span><span class="sxs-lookup"><span data-stu-id="463ea-117">Nginx Compression and Decompression</span></span>](https://www.nginx.com/resources/admin-guide/compression-and-decompression/)
* <span data-ttu-id="463ea-118">직접 호스팅:</span><span class="sxs-lookup"><span data-stu-id="463ea-118">Hosting directly on:</span></span>
  * <span data-ttu-id="463ea-119">[HTTP.sys 서버의](xref:fundamentals/servers/httpsys) (이전의 [WebListener](xref:fundamentals/servers/weblistener))</span><span class="sxs-lookup"><span data-stu-id="463ea-119">[HTTP.sys server](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener))</span></span>
  * [<span data-ttu-id="463ea-120">Kestrel</span><span class="sxs-lookup"><span data-stu-id="463ea-120">Kestrel</span></span>](xref:fundamentals/servers/kestrel)

## <a name="response-compression"></a><span data-ttu-id="463ea-121">응답 압축</span><span class="sxs-lookup"><span data-stu-id="463ea-121">Response compression</span></span>
<span data-ttu-id="463ea-122">일반적으로 압축 되지 않음 응답에서 응답 압축 이점을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-122">Usually, any response not natively compressed can benefit from response compression.</span></span> <span data-ttu-id="463ea-123">일반적으로 압축 되지 않음 응답에 포함: CSS, JavaScript, HTML, XML 및 JSON입니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-123">Responses not natively compressed typically include: CSS, JavaScript, HTML, XML, and JSON.</span></span> <span data-ttu-id="463ea-124">PNG 파일 등의 기본적으로 압축 된 자산을 압축 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-124">You shouldn't compress natively compressed assets, such as PNG files.</span></span> <span data-ttu-id="463ea-125">기본적으로 압축 된 응답을 압축 하려고 하면 압축을 처리 하는 데 걸린 시간으로 작은 추가 크기와 전송 시간 감소가 늘린다 가능성이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-125">If you attempt to further compress a natively compressed response, any small additional reduction in size and transmission time will likely be overshadowed by the time it took to process the compression.</span></span> <span data-ttu-id="463ea-126">(파일의 콘텐츠 및 압축의 효율성)에 따라 약 150-1000 바이트 보다 작은 파일을 압축 안 함.</span><span class="sxs-lookup"><span data-stu-id="463ea-126">Don't compress files smaller than about 150-1000 bytes (depending on the file's content and the efficiency of compression).</span></span> <span data-ttu-id="463ea-127">작은 파일을 압축 하는 오버 헤드는 압축 되지 않은 파일 보다 큰 압축된 된 파일을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-127">The overhead of compressing small files may produce a compressed file larger than the uncompressed file.</span></span>

<span data-ttu-id="463ea-128">클라이언트 전송 하 여 해당 기능의 서버를 알려야 클라이언트가 압축 된 콘텐츠를 처리할 수 있는 경우는 `Accept-Encoding` 헤더를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-128">When a client can process compressed content, the client must inform the server of its capabilities by sending the `Accept-Encoding` header with the request.</span></span> <span data-ttu-id="463ea-129">에 정보를 포함 해야 하는 서버 압축 된 콘텐츠를 보내는 `Content-Encoding` 헤더에 압축 된 응답 인코딩 되는 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-129">When a server sends compressed content, it must include information in the `Content-Encoding` header on how the compressed response is encoded.</span></span> <span data-ttu-id="463ea-130">미들웨어에서 지 원하는 콘텐츠 인코딩 명칭은 다음 표에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-130">Content encoding designations supported by the middleware are shown in the following table.</span></span>

| <span data-ttu-id="463ea-131">`Accept-Encoding`헤더 값</span><span class="sxs-lookup"><span data-stu-id="463ea-131">`Accept-Encoding` header values</span></span> | <span data-ttu-id="463ea-132">지원 되는 미들웨어</span><span class="sxs-lookup"><span data-stu-id="463ea-132">Middleware Supported</span></span> | <span data-ttu-id="463ea-133">설명</span><span class="sxs-lookup"><span data-stu-id="463ea-133">Description</span></span>                                                 |
| :-----------------------------: | :------------------: | ----------------------------------------------------------- |
| `br`                            | <span data-ttu-id="463ea-134">아니요</span><span class="sxs-lookup"><span data-stu-id="463ea-134">No</span></span>                   | <span data-ttu-id="463ea-135">Brotli 압축 된 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="463ea-135">Brotli Compressed Data Format</span></span>                               |
| `compress`                      | <span data-ttu-id="463ea-136">아니요</span><span class="sxs-lookup"><span data-stu-id="463ea-136">No</span></span>                   | <span data-ttu-id="463ea-137">UNIX "압축" 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="463ea-137">UNIX "compress" data format</span></span>                                 |
| `deflate`                       | <span data-ttu-id="463ea-138">아니요</span><span class="sxs-lookup"><span data-stu-id="463ea-138">No</span></span>                   | <span data-ttu-id="463ea-139">"deflate" 내부 "zlib" 데이터 형식 압축 된 데이터</span><span class="sxs-lookup"><span data-stu-id="463ea-139">"deflate" compressed data inside the "zlib" data format</span></span>     |
| `exi`                           | <span data-ttu-id="463ea-140">아니요</span><span class="sxs-lookup"><span data-stu-id="463ea-140">No</span></span>                   | <span data-ttu-id="463ea-141">W3C 효율적인 XML 교환</span><span class="sxs-lookup"><span data-stu-id="463ea-141">W3C Efficient XML Interchange</span></span>                               |
| `gzip`                          | <span data-ttu-id="463ea-142">예 (기본값)</span><span class="sxs-lookup"><span data-stu-id="463ea-142">Yes (default)</span></span>        | <span data-ttu-id="463ea-143">gzip 파일 형식</span><span class="sxs-lookup"><span data-stu-id="463ea-143">gzip file format</span></span>                                            |
| `identity`                      | <span data-ttu-id="463ea-144">예</span><span class="sxs-lookup"><span data-stu-id="463ea-144">Yes</span></span>                  | <span data-ttu-id="463ea-145">"인코딩 없이" 식별자: 응답을 인코딩할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-145">"No encoding" identifier: The response must not be encoded.</span></span> |
| `pack200-gzip`                  | <span data-ttu-id="463ea-146">아니요</span><span class="sxs-lookup"><span data-stu-id="463ea-146">No</span></span>                   | <span data-ttu-id="463ea-147">네트워크 전송 형식 Java 아카이브에</span><span class="sxs-lookup"><span data-stu-id="463ea-147">Network Transfer Format for Java Archives</span></span>                   |
| `*`                             | <span data-ttu-id="463ea-148">예</span><span class="sxs-lookup"><span data-stu-id="463ea-148">Yes</span></span>                  | <span data-ttu-id="463ea-149">명시적으로 요청 되지 않는 인코딩이 사용 가능한 모든 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="463ea-149">Any available content encoding not explicitly requested</span></span>     |

<span data-ttu-id="463ea-150">자세한 내용은 참조는 [IANA 공식 콘텐츠 코딩 목록](http://www.iana.org/assignments/http-parameters/http-parameters.xml#http-content-coding-registry)합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-150">For more information, see the [IANA Official Content Coding List](http://www.iana.org/assignments/http-parameters/http-parameters.xml#http-content-coding-registry).</span></span>

<span data-ttu-id="463ea-151">미들웨어를 사용 하면 사용자 지정에 대 한 추가 압축 공급자 추가할 `Accept-Encoding` 헤더 값입니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-151">The middleware allows you to add additional compression providers for custom `Accept-Encoding` header values.</span></span> <span data-ttu-id="463ea-152">자세한 내용은 참조 [사용자 지정 공급자](#custom-providers) 아래 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-152">For more information, see [Custom Providers](#custom-providers) below.</span></span>

<span data-ttu-id="463ea-153">미들웨어는 품질 값에 응답할 수 (qvalue, `q`) 클라이언트에서 압축 체계의 우선 순위를 보낼 때 가중치입니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-153">The middleware is capable of reacting to quality value (qvalue, `q`) weighting when sent by the client to prioritize compression schemes.</span></span> <span data-ttu-id="463ea-154">자세한 내용은 참조 [RFC 7231: 허용 인코딩](https://tools.ietf.org/html/rfc7231#section-5.3.4)합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-154">For more information, see [RFC 7231: Accept-Encoding](https://tools.ietf.org/html/rfc7231#section-5.3.4).</span></span>

<span data-ttu-id="463ea-155">압축 알고리즘 압축 속도 압축의 효율성 간의 균형을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-155">Compression algorithms are subject to a tradeoff between compression speed and the effectiveness of the compression.</span></span> <span data-ttu-id="463ea-156">*효율성* 이 컨텍스트에서 출력의 크기는 뒤에 참조 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-156">*Effectiveness* in this context refers to the size of the output after compression.</span></span> <span data-ttu-id="463ea-157">가장 작은 크기는 대부분에 의해 이루어집니다 *최적의* 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-157">The smallest size is achieved by the most *optimal* compression.</span></span>

<span data-ttu-id="463ea-158">요청에 관련 된 헤더, 캐싱, 송수신 압축 된 콘텐츠는 다음 표에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-158">The headers involved in requesting, sending, caching, and receiving compressed content are described in the table below.</span></span>

| <span data-ttu-id="463ea-159">Header</span><span class="sxs-lookup"><span data-stu-id="463ea-159">Header</span></span>             | <span data-ttu-id="463ea-160">역할</span><span class="sxs-lookup"><span data-stu-id="463ea-160">Role</span></span> |
| ------------------ | ---- |
| `Accept-Encoding`  | <span data-ttu-id="463ea-161">인코딩 구성을 허용 되는 클라이언트에 콘텐츠를 나타내기 위해 서버에 클라이언트에서 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-161">Sent from the client to the server to indicate the content encoding schemes acceptable to the client.</span></span> |
| `Content-Encoding` | <span data-ttu-id="463ea-162">페이로드의 콘텐츠 인코딩을 나타내는 클라이언트에 서버에서 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-162">Sent from the server to the client to indicate the encoding of the content in the payload.</span></span> |
| `Content-Length`   | <span data-ttu-id="463ea-163">압축이 발생할 때의 `Content-Length` 응답 압축 되는 경우는 본문 콘텐츠가 변경 이후 헤더를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-163">When compression occurs, the `Content-Length` header is removed, since the body content changes when the response is compressed.</span></span> |
| `Content-MD5`      | <span data-ttu-id="463ea-164">압축이 발생할 때의 `Content-MD5` 해시는 더 이상 유효 하 고 본문 내용이 변경 되었습니다. 헤더를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-164">When compression occurs, the `Content-MD5` header is removed, since the body content has changed and the hash is no longer valid.</span></span> |
| `Content-Type`     | <span data-ttu-id="463ea-165">콘텐츠의 MIME 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-165">Specifies the MIME type of the content.</span></span> <span data-ttu-id="463ea-166">모든 응답을 지정 해야 해당 `Content-Type`합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-166">Every response should specify its `Content-Type`.</span></span> <span data-ttu-id="463ea-167">미들웨어의 응답을 압축할 수를 확인 하려면이 값을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-167">The middleware checks this value to determine if the response should be compressed.</span></span> <span data-ttu-id="463ea-168">집합을 지정 하는 미들웨어 [기본 MIME 형식을](#mime-types) 인코딩할 수 있지만 MIME 형식을 추가 하거나 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-168">The middleware specifies a set of [default MIME types](#mime-types) that it can encode, but you can replace or add MIME types.</span></span> |
| `Vary`             | <span data-ttu-id="463ea-169">값을 사용 하 여 서버에서 전송 하는 경우 `Accept-Encoding` 클라이언트와 프록시에는 `Vary` 헤더는 클라이언트 또는 캐시 해야 하는 프록시를 나타냅니다 (다)의 값을 기반으로 응답은 `Accept-Encoding` 요청 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-169">When sent by the server with a value of `Accept-Encoding` to clients and proxies, the `Vary` header indicates to the client or proxy that it should cache (vary) responses based on the value of the `Accept-Encoding` header of the request.</span></span> <span data-ttu-id="463ea-170">콘텐츠를 반환 결과 `Vary: Accept-Encoding` 헤더는 모두 압축 및 압축 되지 않은 응답이 별도로 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-170">The result of returning content with the `Vary: Accept-Encoding` header is that both compressed and uncompressed responses are cached separately.</span></span> |

<span data-ttu-id="463ea-171">사용 하 여 응답 압축 미들웨어의 기능을 탐색할 수 있습니다는 [샘플 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/response-compression/samples)합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-171">You can explore the features of the Response Compression Middleware with the [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/response-compression/samples).</span></span> <span data-ttu-id="463ea-172">이 샘플에서는 다음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-172">The sample illustrates:</span></span>
* <span data-ttu-id="463ea-173">Gzip 및 사용자 지정 압축 공급자를 사용 하 여 앱 응답의 압축입니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-173">The compression of app responses using gzip and custom compression providers.</span></span>
* <span data-ttu-id="463ea-174">압축에 대 한 MIME 형식의 기본 목록에 MIME 형식을 추가 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="463ea-174">How to add a MIME type to the default list of MIME types for compression.</span></span>

## <a name="package"></a><span data-ttu-id="463ea-175">패키지</span><span class="sxs-lookup"><span data-stu-id="463ea-175">Package</span></span>
<span data-ttu-id="463ea-176">미들웨어를 프로젝트에 포함 하려면 추가에 대 한 참조는 [ `Microsoft.AspNetCore.ResponseCompression` ](https://www.nuget.org/packages/Microsoft.AspNetCore.ResponseCompression/) 패키지 하거나 사용 하 여는 [ `Microsoft.AspNetCore.All` ](https://www.nuget.org/packages/Microsoft.AspNetCore.All/) 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-176">To include the middleware in your project, add a reference to the [`Microsoft.AspNetCore.ResponseCompression`](https://www.nuget.org/packages/Microsoft.AspNetCore.ResponseCompression/) package or use the [`Microsoft.AspNetCore.All`](https://www.nuget.org/packages/Microsoft.AspNetCore.All/) package.</span></span> <span data-ttu-id="463ea-177">이 기능은 이상 ASP.NET Core 1.1을 대상으로 하는 응용 프로그램에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-177">This feature is available for apps that target ASP.NET Core 1.1 or later.</span></span>

## <a name="configuration"></a><span data-ttu-id="463ea-178">구성</span><span class="sxs-lookup"><span data-stu-id="463ea-178">Configuration</span></span>
<span data-ttu-id="463ea-179">다음 코드를 사용 하 여 응답 압축 미들웨어를 사용 하도록 설정 하는 방법을 보여 줍니다는 기본 gzip 압축을 함께 사용 하 고 기본 MIME 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-179">The following code shows how to enable the Response Compression Middleware with the with the default gzip compression and for default MIME types.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="463ea-180">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="463ea-180">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](response-compression/samples/2.x/StartupBasic.cs?name=snippet1&highlight=4,8)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="463ea-181">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="463ea-181">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](response-compression/samples/1.x/StartupBasic.cs?name=snippet1&highlight=3,8)]

---

> [!NOTE]
> <span data-ttu-id="463ea-182">와 같은 도구를 사용 하 여 [Fiddler](http://www.telerik.com/fiddler), [Firebug](http://getfirebug.com/), 또는 [우체부](https://www.getpostman.com/) 설정 하는 `Accept-Encoding` 요청 헤더 및 응답 헤더, 크기 및 본문을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-182">Use a tool like [Fiddler](http://www.telerik.com/fiddler), [Firebug](http://getfirebug.com/), or [Postman](https://www.getpostman.com/) to set the `Accept-Encoding` request header and study the response headers, size, and body.</span></span>

<span data-ttu-id="463ea-183">요청 하지 않고 샘플 응용 프로그램을 제출는 `Accept-Encoding` 헤더 응답을 압축 하지 않을 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-183">Submit a request to the sample app without the `Accept-Encoding` header and observe that the response is uncompressed.</span></span> <span data-ttu-id="463ea-184">`Content-Encoding` 및 `Vary` 헤더 응답에는 표시 되지 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-184">The `Content-Encoding` and `Vary` headers aren't present on the response.</span></span>

![Fiddler 창 Accept-encoding 헤더 없이 요청의 결과 표시 합니다.](response-compression/_static/request-uncompressed.png)

<span data-ttu-id="463ea-187">요청을 사용한 샘플 앱을 제출는 `Accept-Encoding: gzip` 헤더 응답 압축을 관찰 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-187">Submit a request to the sample app with the `Accept-Encoding: gzip` header and observe that the response is compressed.</span></span> <span data-ttu-id="463ea-188">`Content-Encoding` 및 `Vary` 헤더가 응답에 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-188">The `Content-Encoding` and `Vary` headers are present on the response.</span></span>

![Accept-encoding 헤더로 요청의 결과 및 gzip의 값을 보여 주는 fiddler 창입니다.](response-compression/_static/request-compressed.png)

## <a name="providers"></a><span data-ttu-id="463ea-192">공급자</span><span class="sxs-lookup"><span data-stu-id="463ea-192">Providers</span></span>
### <a name="gzipcompressionprovider"></a><span data-ttu-id="463ea-193">GzipCompressionProvider</span><span class="sxs-lookup"><span data-stu-id="463ea-193">GzipCompressionProvider</span></span>
<span data-ttu-id="463ea-194">사용 하 여 `GzipCompressionProvider` gzip으로 응답을 압축 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-194">Use the `GzipCompressionProvider` to compress responses with gzip.</span></span> <span data-ttu-id="463ea-195">지정 하지 않으면 기본 압축 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-195">This is the default compression provider if none are specified.</span></span> <span data-ttu-id="463ea-196">압축을 수준으로 설정할 수 있습니다는 `GzipCompressionProviderOptions`합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-196">You can set the compression level with the `GzipCompressionProviderOptions`.</span></span> 

<span data-ttu-id="463ea-197">Gzip 압축 공급자 기본적으로 가장 빠른 압축 수준 (`CompressionLevel.Fastest`), 가장 효율적인 압축을 생성 하지 수입니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-197">The gzip compression provider defaults to the fastest compression level (`CompressionLevel.Fastest`), which might not produce the most efficient compression.</span></span> <span data-ttu-id="463ea-198">가장 효율적인 압축을 사용할 경우 최적의 압축에 대 한 미들웨어를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-198">If the most efficient compression is desired, you can configure the middleware for optimal compression.</span></span>

| <span data-ttu-id="463ea-199">압축 수준</span><span class="sxs-lookup"><span data-stu-id="463ea-199">Compression Level</span></span>                | <span data-ttu-id="463ea-200">설명</span><span class="sxs-lookup"><span data-stu-id="463ea-200">Description</span></span>                                                                                                   |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| `CompressionLevel.Fastest`       | <span data-ttu-id="463ea-201">결과 출력은 최적으로 압축 되지 않은 경우에 압축을 가능한 한 빨리 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-201">Compression should complete as quickly as possible, even if the resulting output is not optimally compressed.</span></span> |
| `CompressionLevel.NoCompression` | <span data-ttu-id="463ea-202">압축 하지 않고 수행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-202">No compression should be performed.</span></span>                                                                           |
| `CompressionLevel.Optimal`       | <span data-ttu-id="463ea-203">응답 최적으로 압축 된 압축을 완료 하는 데 시간이 더에 사용 하는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-203">Responses should be optimally compressed, even if the compression takes more time to complete.</span></span>                |


# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="463ea-204">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="463ea-204">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](response-compression/samples/2.x/Program.cs?name=snippet1&highlight=3,8-11)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="463ea-205">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="463ea-205">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](response-compression/samples/1.x/Startup.cs?name=snippet2&highlight=5,10-13)]

---

## <a name="mime-types"></a><span data-ttu-id="463ea-206">MIME 형식</span><span class="sxs-lookup"><span data-stu-id="463ea-206">MIME types</span></span>
<span data-ttu-id="463ea-207">미들웨어 압축에 대 한 MIME 형식의 기본 집합을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-207">The middleware specifies a default set of MIME types for compression:</span></span>
* `text/plain`
* `text/css`
* `application/javascript`
* `text/html`
* `application/xml`
* `text/xml`
* `application/json`
* `text/json`

<span data-ttu-id="463ea-208">대체 하거나 응답 압축 미들웨어 옵션으로 MIME 형식을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-208">You can replace or append MIME types with the Response Compression Middleware options.</span></span> <span data-ttu-id="463ea-209">해당 와일드 카드 MIME 참고와 같은 형식은 `text/*` 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-209">Note that wildcard MIME types, such as `text/*` aren't supported.</span></span> <span data-ttu-id="463ea-210">샘플 응용 프로그램에 대 한 MIME 형식을 추가 `image/svg+xml` 압축 하 고 ASP.NET Core 배너 이미지를 사용 하 고 (*banner.svg*).</span><span class="sxs-lookup"><span data-stu-id="463ea-210">The sample app adds a MIME type for `image/svg+xml` and compresses and serves the ASP.NET Core banner image (*banner.svg*).</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="463ea-211">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="463ea-211">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](response-compression/samples/2.x/Program.cs?name=snippet1&highlight=5)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="463ea-212">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="463ea-212">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](response-compression/samples/1.x/Startup.cs?name=snippet2&highlight=7)]

---

### <a name="custom-providers"></a><span data-ttu-id="463ea-213">사용자 지정 공급자</span><span class="sxs-lookup"><span data-stu-id="463ea-213">Custom providers</span></span>
<span data-ttu-id="463ea-214">사용자 지정 압축 구현으로 만들 수 있습니다 `ICompressionProvider`합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-214">You can create custom compression implementations with `ICompressionProvider`.</span></span> <span data-ttu-id="463ea-215">`EncodingName` 인코딩이 콘텐츠를 나타내는 `ICompressionProvider` 을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-215">The `EncodingName` represents the content encoding that this `ICompressionProvider` produces.</span></span> <span data-ttu-id="463ea-216">에 지정 된 목록을 기반으로 하는 공급자를 선택 하 여이 정보를 사용 하는 미들웨어는 `Accept-Encoding` 요청 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-216">The middleware uses this information to choose the provider based on the list specified in the `Accept-Encoding` header of the request.</span></span>

<span data-ttu-id="463ea-217">클라이언트에서 요청을 제출 샘플 응용 프로그램을 사용 하 여 `Accept-Encoding: mycustomcompression` 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-217">Using the sample app, the client submits a request with the `Accept-Encoding: mycustomcompression` header.</span></span> <span data-ttu-id="463ea-218">미들웨어 사용자 지정 압축 구현을 사용 하 고 있는 응답을 반환는 `Content-Encoding: mycustomcompression` 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-218">The middleware uses the custom compression implementation and returns the response with a `Content-Encoding: mycustomcompression` header.</span></span> <span data-ttu-id="463ea-219">클라이언트에서 실행 되도록 사용자 지정 압축 구현에 대 한 순서에서 사용자 지정 인코딩 압축을 풀 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-219">The client must be able to decompress the custom encoding in order for a custom compression implementation to work.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="463ea-220">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="463ea-220">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](response-compression/samples/2.x/Program.cs?name=snippet1&highlight=4)]

[!code-csharp[Main](response-compression/samples/2.x/CustomCompressionProvider.cs?name=snippet1)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="463ea-221">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="463ea-221">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](response-compression/samples/1.x/Startup.cs?name=snippet2&highlight=6)]

[!code-csharp[Main](response-compression/samples/1.x/CustomCompressionProvider.cs?name=snippet1)]

---

<span data-ttu-id="463ea-222">요청을 사용한 샘플 앱을 제출는 `Accept-Encoding: mycustomcompression` 헤더 응답 헤더를 관찰 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-222">Submit a request to the sample app with the `Accept-Encoding: mycustomcompression` header and observe the response headers.</span></span> <span data-ttu-id="463ea-223">`Vary` 및 `Content-Encoding` 헤더가 응답에 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-223">The `Vary` and `Content-Encoding` headers are present on the response.</span></span> <span data-ttu-id="463ea-224">(표시 되지 않음) 하는 응답 본문은 샘플에서 압축 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-224">The response body (not shown) isn't compressed by the sample.</span></span> <span data-ttu-id="463ea-225">압축 구현 하지 않으므로 `CustomCompressionProvider` 샘플의 클래스.</span><span class="sxs-lookup"><span data-stu-id="463ea-225">There isn't a compression implementation in the `CustomCompressionProvider` class of the sample.</span></span> <span data-ttu-id="463ea-226">그러나 보여 압축 알고리즘을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-226">However, the sample shows where you would implement such a compression algorithm.</span></span>

![Accept-encoding 헤더로 요청의 결과 및 mycustomcompression의 값을 보여 주는 fiddler 창입니다.](response-compression/_static/request-custom-compression.png)

## <a name="compression-with-secure-protocol"></a><span data-ttu-id="463ea-229">보안 프로토콜에 대 한 압축</span><span class="sxs-lookup"><span data-stu-id="463ea-229">Compression with secure protocol</span></span>
<span data-ttu-id="463ea-230">보안 연결을 통해 압축 된 응답으로 제어할 수 있습니다는 `EnableForHttps` 옵션을 기본적으로 비활성화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-230">Compressed responses over secure connections can be controlled with the `EnableForHttps` option, which is disabled by default.</span></span> <span data-ttu-id="463ea-231">와 같은 보안 문제를 일으킬 수 동적으로 생성 된 페이지와 압축을 사용 하 여 [범죄](https://wikipedia.org/wiki/CRIME_(security_exploit)) 및 [위반](https://wikipedia.org/wiki/BREACH_(security_exploit)) 공격입니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-231">Using compression with dynamically generated pages can lead to security problems such as the [CRIME](https://wikipedia.org/wiki/CRIME_(security_exploit)) and [BREACH](https://wikipedia.org/wiki/BREACH_(security_exploit)) attacks.</span></span>

## <a name="adding-the-vary-header"></a><span data-ttu-id="463ea-232">Vary 헤더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-232">Adding the Vary header</span></span>
<span data-ttu-id="463ea-233">경우에 따라 응답을 압축 된 `Accept-Encoding` 헤더로, 잠재적으로 여러 개의 압축 된 버전의 응답 및 압축 되지 않은 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-233">When compressing responses based on the `Accept-Encoding` header, there are potentially multiple compressed versions of the response and an uncompressed version.</span></span> <span data-ttu-id="463ea-234">여러 버전 존재 하 고 저장 해야 캐시 클라이언트와 프록시 캐시 하도록 지시 하려면는 `Vary` 헤더와 함께 추가 됩니다 한 `Accept-Encoding` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-234">In order to instruct client and proxy caches that multiple versions exist and should be stored, the `Vary` header is added with an `Accept-Encoding` value.</span></span> <span data-ttu-id="463ea-235">ASP.NET Core에서 1.x 추가 `Vary` 헤더를 응답은 수동으로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-235">In ASP.NET Core 1.x, adding the `Vary` header to the response is accomplished manually.</span></span> <span data-ttu-id="463ea-236">ASP.NET Core에서 2.x 미들웨어 추가 `Vary` 헤더 응답 압축 되어 있을 때 자동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-236">In ASP.NET Core 2.x, the middleware adds the `Vary` header automatically when the response is compressed.</span></span>

<span data-ttu-id="463ea-237">**ASP.NET Core 1.x만**</span><span class="sxs-lookup"><span data-stu-id="463ea-237">**ASP.NET Core 1.x only**</span></span>

[!code-csharp[Main](response-compression/samples/1.x/Startup.cs?name=snippet1)]

## <a name="middleware-issue-when-behind-an-nginx-reverse-proxy"></a><span data-ttu-id="463ea-238">Nginx 역방향 프록시 뒤에 있을 때는 미들웨어 문제</span><span class="sxs-lookup"><span data-stu-id="463ea-238">Middleware issue when behind an Nginx reverse proxy</span></span>
<span data-ttu-id="463ea-239">요청에서 Nginx, 프록시 되 고 `Accept-Encoding` 헤더를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-239">When a request is proxied by Nginx, the `Accept-Encoding` header is removed.</span></span> <span data-ttu-id="463ea-240">이렇게 하면 미들웨어를에서 응답을 압축지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-240">This prevents the middleware from compressing the response.</span></span> <span data-ttu-id="463ea-241">자세한 내용은 참조 [NGINX: 압축 및 압축 풀기](https://www.nginx.com/resources/admin-guide/compression-and-decompression/)합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-241">For more information, see [NGINX: Compression and Decompression](https://www.nginx.com/resources/admin-guide/compression-and-decompression/).</span></span> <span data-ttu-id="463ea-242">이 문제를 추적 하 여 [Nginx (BasicMiddleware #123)에 대 한 통과 압축 파악](https://github.com/aspnet/BasicMiddleware/issues/123)합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-242">This issue is tracked by [Figure out pass-through compression for Nginx (BasicMiddleware #123)](https://github.com/aspnet/BasicMiddleware/issues/123).</span></span>

## <a name="working-with-iis-dynamic-compression"></a><span data-ttu-id="463ea-243">IIS 동적 압축이 사용</span><span class="sxs-lookup"><span data-stu-id="463ea-243">Working with IIS dynamic compression</span></span>
<span data-ttu-id="463ea-244">활성 IIS 동적 압축이 모듈을 응용 프로그램에 대해 사용 하지 않도록 설정 하려는 서버 수준에서 구성 하는 경우 그렇게 할 수 있습니다에 대 한 추가 된 프로그램 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-244">If you have an active IIS Dynamic Compression Module configured at the server level that you would like to disable for an app, you can do so with an addition to your *web.config* file.</span></span> <span data-ttu-id="463ea-245">자세한 내용은 참조 [비활성화 IIS 모듈](xref:host-and-deploy/iis/modules#disabling-iis-modules)합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-245">For more information, see [Disabling IIS modules](xref:host-and-deploy/iis/modules#disabling-iis-modules).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="463ea-246">문제 해결</span><span class="sxs-lookup"><span data-stu-id="463ea-246">Troubleshooting</span></span>
<span data-ttu-id="463ea-247">와 같은 도구를 사용 하 여 [Fiddler](http://www.telerik.com/fiddler), [Firebug](http://getfirebug.com/), 또는 [우체부](https://www.getpostman.com/)를 설정할 수 있도록는 `Accept-Encoding` 요청 헤더 및 응답 헤더, 크기 및 본문을 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-247">Use a tool like [Fiddler](http://www.telerik.com/fiddler), [Firebug](http://getfirebug.com/), or [Postman](https://www.getpostman.com/), which allow you to set the `Accept-Encoding` request header and study the response headers, size, and body.</span></span> <span data-ttu-id="463ea-248">응답 압축 미들웨어 다음 조건을 충족 하는 응답을 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-248">The Response Compression Middleware compresses responses that meet the following conditions:</span></span>
* <span data-ttu-id="463ea-249">`Accept-Encoding` 헤더가 값이 있으면 `gzip`, `*`를 설정 하는 사용자 지정 압축 공급자와 일치 하는 사용자 지정 인코딩 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-249">The `Accept-Encoding` header is present with a value of `gzip`, `*`, or custom encoding that matches a custom compression provider that you've established.</span></span> <span data-ttu-id="463ea-250">값 되지 않아야 `identity` 품질 값이 있는 (qvalue, `q`) 0 (영)을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-250">The value must not be `identity` or have a quality value (qvalue, `q`) setting of 0 (zero).</span></span>
* <span data-ttu-id="463ea-251">MIME 형식 (`Content-Type`) 설정 해야 하며에 구성 된 MIME 형식과 일치 해야 합니다는 `ResponseCompressionOptions`합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-251">The MIME type (`Content-Type`) must be set and must match a MIME type configured on the `ResponseCompressionOptions`.</span></span>
* <span data-ttu-id="463ea-252">요청을 포함 하지 않아야는 `Content-Range` 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-252">The request must not include the `Content-Range` header.</span></span>
* <span data-ttu-id="463ea-253">요청 응답 압축 미들웨어 옵션에서 보안 프로토콜 (https)를 구성 하지 않으면 안전 하지 않은 프로토콜 (http)를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="463ea-253">The request must use insecure protocol (http), unless secure protocol (https) is configured in the Response Compression Middleware options.</span></span> <span data-ttu-id="463ea-254">*위험을 유의 [위에서 설명한](#compression-with-secure-protocol) 보안 콘텐츠 압축을 사용 하도록 설정할 때.*</span><span class="sxs-lookup"><span data-stu-id="463ea-254">*Note the danger [described above](#compression-with-secure-protocol) when enabling secure content compression.*</span></span>

## <a name="additional-resources"></a><span data-ttu-id="463ea-255">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="463ea-255">Additional resources</span></span>
* [<span data-ttu-id="463ea-256">응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="463ea-256">Application Startup</span></span>](xref:fundamentals/startup)
* [<span data-ttu-id="463ea-257">미들웨어</span><span class="sxs-lookup"><span data-stu-id="463ea-257">Middleware</span></span>](xref:fundamentals/middleware)
* [<span data-ttu-id="463ea-258">Mozilla Developer Network: 허용 인코딩</span><span class="sxs-lookup"><span data-stu-id="463ea-258">Mozilla Developer Network: Accept-Encoding</span></span>](https://developer.mozilla.org/docs/Web/HTTP/Headers/Accept-Encoding)
* [<span data-ttu-id="463ea-259">RFC 7231 섹션 3.1.2.1: 콘텐츠 구분을 사용</span><span class="sxs-lookup"><span data-stu-id="463ea-259">RFC 7231 Section 3.1.2.1: Content Codings</span></span>](https://tools.ietf.org/html/rfc7231#section-3.1.2.1)
* [<span data-ttu-id="463ea-260">RFC 7230 섹션 4.2.3: Gzip 코딩</span><span class="sxs-lookup"><span data-stu-id="463ea-260">RFC 7230 Section 4.2.3: Gzip Coding</span></span>](https://tools.ietf.org/html/rfc7230#section-4.2.3)
* [<span data-ttu-id="463ea-261">GZIP 파일 형식 사양 버전 4.3</span><span class="sxs-lookup"><span data-stu-id="463ea-261">GZIP file format specification version 4.3</span></span>](http://www.ietf.org/rfc/rfc1952.txt)