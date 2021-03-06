---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: "컨트롤러와 뷰를 사용 하 여 목록/세부 정보 UI 구현할 | Microsoft Docs"
author: microsoft
description: "4 단계에는 데이터 목록/세부 정보 탐색 환경을 제공 하기 위해 모델의 이점을 활용 하는 응용 프로그램에는 컨트롤러를 추가 하는 방법을 보여 줍니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 2f9148a2d419863229e2c5a2a0c98984001fcee5
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a>컨트롤러와 뷰를 사용 하 여 목록/세부 정보 UI를 구현 하려면
====================
여 [Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이 무료의 4 단계 ["업그레이드 되었으며 수정" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 하는 워크 쓰루는 작고 빌드만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.
> 
> 4 단계에는 컨트롤러 업그레이드 되었으며 수정 사이트에서 dinners에 대 한 데이터 목록/세부 정보 탐색 환경을 제공 하기 위해 모델의 이점을 활용 하는 응용 프로그램에 추가 하는 방법을 보여 줍니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행한 것이 좋습니다는 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-step-4-controllers-and-views"></a>업그레이드 되었으며 수정 4 단계: 컨트롤러와 뷰

기존 웹 프레임 워크 (클래식 ASP, PHP, ASP.NET Web Forms, 등), 들어오는 Url은 일반적으로 디스크 파일에 매핑됩니다. 예: URL에 대 한 요청 같은 "/ Products.aspx" 또는 "/ Products.php" "Products.aspx" 또는 "Products.php" 파일에서 처리 될 수 있습니다.

웹 기반 MVC 프레임 워크를 약간 다른 방식으로 서버 코드에 Url을 매핑합니다. 파일에 들어오는 Url 매핑, 대신 대신 Url에 매핑되는지 클래스에 대 한 메서드. 이러한 클래스는 "컨트롤러" 라고 하 고 사용자 입력을 처리 하는 들어오는 HTTP 요청을 처리 해야 하는, 검색 및 데이터를 저장 및 보내기에 대 한 응답을 결정 하는 클라이언트에 다시 (HTML을 표시, 파일을 다운로드, 다른 리디렉션 URL 등)입니다.

업그레이드 되었으며 수정 응용 프로그램에 대 한를 기본 모델을 구축 했으므로, 이제는 사이트에서 Dinners에 대 한 데이터 목록/세부 정보 탐색 환경을 제공 하기 위해의 이점을 활용 하는 응용 프로그램에 컨트롤러를 추가 하려면 다음 단계가 됩니다.

### <a name="adding-a-dinnerscontroller-controller"></a>DinnersController 컨트롤러 추가

이 웹 프로젝트 내에서 "컨트롤러" 폴더를 마우스 오른쪽 단추로 클릭 하 여 시작 알아보고 선택 하겠습니다는 **추가-&gt;컨트롤러** 메뉴 명령 (또한이 명령을 실행할 수 있습니다이 Ctrl-M, Ctrl + C를 입력 하 여):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

그러면 "컨트롤러 추가" 대화 상자를 표시 됩니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

새 컨트롤러 "DinnersController" 이름을 알아보고 "추가" 단추를 클릭 하겠습니다. Visual Studio는 우리의 \Controllers 디렉터리 아래에 있는 DinnersController.cs 파일을 추가 합니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

코드 편집기 내에서 새 DinnersController 클래스를도 열립니다.

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a>Index () 및 Details() 작업 메서드를 DinnersController 클래스에 추가합니다.

응용 프로그램을 사용 하 여 예정 된 dinners 목록을 찾아보고 항목에 대 한 특정 세부 정보를 보려면 목록에서 모든 Dinner 클릭할 수 있도록 하는 방문자를 사용 하려고 합니다. 응용 프로그램에서 다음 Url을 게시 하 여 수행 합니다.

| **URL** | **용도** |
| --- | --- |
| */Dinners/* | 예정 된 dinners는 HTML 목록 표시 |
| */Dinners/세부 정보 / [id]* | 데이터베이스에 dinner DinnerID 일치시킬지 URL – 내에 포함 하는 "id" 매개 변수가 나타내는 특정 저녁에 대 한 세부 정보를 표시 합니다. 예를 들어: /Dinners/Details/2 해당 DinnerID 값이 2 저녁에 대 한 세부 정보와 함께 HTML 페이지를 표시 합니다. |

아래와 같은 DinnersController 클래스에 두 개의 공용 "작업 방법"을 추가 하 여 이러한 Url의 초기 구현 발표 합니다.

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

다음 업그레이드 되었으며 수정 응용 프로그램을 실행 알아보고 브라우저를 사용 하 여 호출할 하겠습니다. 에 입력 하는 *"/" (Dinners/* URL 하면 우리의 *index ()* 메서드 실행 시를 송신할 다시 다음 응답:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

에 입력 하는 *"/ 2/세부 정보/Dinners"* URL 하면 우리의 *Details()* 메서드를 실행 하 고 다음 응답을 다시 보냅니다:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

하는지에 대해-어떻게 ASP.NET MVC 것을 아시나요 DinnersController 클래스를 만들고 이러한 메서드를 호출 하 시겠습니까? 하겠습니다를 이해 하려면 라우팅의 작동 원리에 빠르게 확인 합니다.

### <a name="understanding-aspnet-mvc-routing"></a>이해 ASP.NET MVC 라우팅

ASP.NET MVC 컨트롤러 클래스에 Url 매핑하는 방식을 제어 시 유연성을 많이 제공 하는 강력한 URL 라우팅 엔진을 포함 합니다. ASP.NET MVC 컨트롤러 클래스를 만드는 메서드를 호출할 수 있을 뿐만 아니라 다른 변수 수 수 자동으로 URL 쿼리 문자열에서 구문 분석 하 고 있는 방법 매개 변수로 메서드에 전달 된 구성할를 선택 하는 방법를 완전히 사용자 지정할 수 있도록 인수입니다. 완전히 SEO (검색 엔진 최적화)에 대 한 사이트 최적화 뿐만 아니라 응용 프로그램에서 원하는 모든 URL의 구조를 게시할 수 있는 유연성을 제공 합니다.

새 ASP.NET MVC 프로젝트는 기본적으로 미리 구성 된 이미 등록 URL 라우팅 규칙 집합이 함께 제공 됩니다. 이렇게 하면 쉽게 시작 응용 프로그램에 아무 것도 명시적으로 구성할 필요 없이 수 있습니다. 기본 라우팅 규칙 등록 – 우리는 프로젝트의 루트에 있는 "Global.asax" 파일을 두 번 클릭 하 여 열 수 있는 프로젝트의 "Application" 클래스 내에서 찾을 수 있습니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

이 클래스의 "RegisterRoutes" 메서드 내에서 기본 ASP.NET MVC 라우팅 규칙을 등록 합니다.

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

"경로입니다. MapRoute() "위의 메서드 호출을 컨트롤러 클래스 URL 형식을 사용 하 여 들어오는 Url을 매핑하는 기본 라우팅 규칙을 등록:" / {controller} / {action} / {id} "– 여기서"컨트롤러 "는 인스턴스화할 컨트롤러 클래스의 이름을"action"의 이름인는 한 "id"를 호출 하는 공용 메서드는 메서드에 대 한 인수로 전달할 수 있는 URL 내에 포함 하는 선택적 매개 변수입니다. "MapRoute()" 메서드 호출에 전달 된 세 번째 매개 변수는 URL에 존재 하지 않는 컨트롤러/작업/id 값에 사용할 기본 값의 집합 (컨트롤러 동작 = "Home", "Index", Id = = "").

다음은 이러한 기본값을 사용 하 여 Url의 다양 한 방법을 보여 주는 테이블 매핑된 "*/ {컨트롤러} / {action} / {id}"*경로 규칙:

| **URL** | **컨트롤러 클래스** | **동작 메서드** | **전달 된 매개 변수** |
| --- | --- | --- | --- |
| */ Dinners/세부 정보/2* | DinnersController | Details(id) | id = 2 |
| */ Dinners/편집/5* | DinnersController | Edit(id) | id = 5 |
| */ Dinners/만들기* | DinnersController | Create) | N/A |
| */ Dinners* | DinnersController | Index) | N/A |
| */ 홈* | HomeController | Index) | N/A |
| */* | HomeController | Index) | N/A |

기본 값을 표시 하는 마지막 3 개의 행 (컨트롤러 = 가정, 작업 = 인덱스, Id = "") 사용 하 고 합니다. "Index" 메서드 하나를 지정 하지 않으면 기본 동작 이름으로 등록 되므로 "/ Dinners" 및 "/ 홈" Url 원인 index () 동작 메서드를 해당 컨트롤러 클래스에서 호출 합니다. 지정 하지 않고 "홈" 컨트롤러가 기본 컨트롤러로 등록 된, 하기 때문에 "/" URL HomeController 만들어야 하 고 index () 동작 메서드를 호출할 수 발생 합니다.

이러한 기본 URL 라우팅 규칙, 마음에 들지 않으면 좋은 소식 쉽게 변경-바로 위의 RegisterRoutes 메서드 내에서 편집할 수 있다는 점입니다. 이 업그레이드 되었으며 수정 응용 프로그램에 대 한 하지만 기본 URL 라우팅 규칙을 변경 하려면 않겠습니다 – 대신 있습니다 사용할 것으로-됩니다.

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a>우리의 DinnersController에서 DinnerRepository를 사용 하 여

보겠습니다 DinnersController의 현재 구현은 이제 대체 index () 및 Details() 동작 메서드를 예제의 모델을 사용 하는 구현 합니다.

동작을 구현 하려면 앞서 작성 DinnerRepository 클래스를 사용 합니다. 에서는 "NerdDinner.Models" 네임 스페이스를 참조 하는 "using" 문을 추가 하 여 시작 하 고 DinnerController 클래스에 필드로 취급 DinnerRepository의 인스턴스를 선언 합니다.

나중에이 장의에서는 합니다 "종속성 주입"의 개념을 소개 하 고 우리의 DinnerRepository의 인스턴스를 방금 만들겠습니다 이제 테스트 – 하지만 권한에 대 한 또 다른 방법은 더 나은 단위 수 있도록 DinnerRepository에 대 한 참조를 가져오려면이 컨트롤러에 대 한 표시 아래와 같은 인라인 합니다.

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

이제 검색 된 데이터 모델 개체를 사용 하 여 HTML 응답을 생성할 준비가 되었습니다.

### <a name="using-views-with-our-controller"></a>이 컨트롤러와 뷰를 사용 하 여

조합 HTML을 사용 하 여이 작업 메서드 내에서 코드를 작성할 수 있지만 *Response.Write()* 클라이언트로 다시 전송할는 접근 방식을 통제 하기 힘들어집니다 매우 신속 하 게 도우미 메서드입니다. 훨씬 더 나은 방법은 응용 프로그램 및 우리의 DinnersController 작업 메서드 내부의 데이터 논리를 수행 하 고 그런 다음 HTML 표현을 출력 하는 일을 담당 하는 별도 "보기" 서식 파일에 대 한 HTML 응답을 렌더링 하는 데 필요한 데이터에 대 한 합니다. 잠시 후에 볼 수 있겠지만, "view" 템플릿은 일반적으로 포함 된 렌더링 코드와 HTML 태그를 포함 하는 텍스트 파일입니다.

우리의 뷰 렌더링에서 트 컨트롤러 논리를 분리는 몇 가지 큰 이점을 제공 합니다. 특히 응용 프로그램 코드와 UI 서식을/렌더링 코드 사이의 명확한 "문제의 분리" 적용 수 있습니다. 이렇게 하면 훨씬 쉽게 격리에 대 한 단위 테스트 응용 프로그램 논리를 UI 렌더링 논리에서. 예제에서는 쉽게 나중에 응용 프로그램 코드를 변경 하지 않고도 UI 렌더링 서식 파일을 수정할 수 있습니다. 및 개발자와 디자이너가 프로젝트에 함께 공동 작업을 쉽게 만들 수 것입니다.

DinnersController 클래스 뷰 템플릿을 사용 하 여 반환 형식이 "void" 대신 "ActionResult"의 반환 형식을 갖도록 하는 것과 두 개의 작업 메서드 메서드 시그니처를 변경 하 여 HTML UI 응답 반송 한다고 나타내는 업데이트할 수 있습니다. 그런 다음를 호출할 수 있습니다는 *View()* 다시 반환 하는 컨트롤러 기본 클래스에서 도우미 메서드에 다음과 유사한 "ViewResult" 개체:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

시그니처는 *View()* 위에 사용 하 여 도우미 메서드는 아래 같습니다:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

첫 번째 매개 변수는 *View()* 도우미 메서드는 HTML 응답을 렌더링 하는 데 원하는 보기 템플릿 파일의 이름입니다. 두 번째 템플릿 보기 HTML 응답을 렌더링 하는 데 필요한 데이터를 포함 하는 모델 개체입니다.

우리 index () 작업 메서드 내에서 호출 된 *View()* 도우미 메서드와 dinners "Index" 뷰 템플릿을 사용 하는 HTML 목록이 렌더링 하려고 한다는 것을 나타내는입니다. 전달 템플릿 보기 Dinner에서 목록을 생성 하는 개체 시퀀스의:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

우리의 Details() 작업 메서드 내에서 URL 내에서 제공 하는 id를 사용 하 여 Dinner 개체를 검색 하려고 합니다. 유효한 Dinner 이라고 발견 되는 *View()* 도우미 메서드를 "Details" 뷰 템플릿을 사용 하 여 검색 된 Dinner 개체를 렌더링 하도록 지정 했습니다. म 렌더링 Dinner "NotFound" 뷰 템플릿을 사용 하 여 존재 하지 유용한 오류 메시지가 잘못 된 dinner 요청 된 경우 (및 오버 로드 된 버전의는 *View()* 템플릿 이름 원활한 도우미 메서드 ):

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

이제 템플릿 보기 "NotFound", "Details" 및 "인덱스"를 구현 해 보겠습니다.

### <a name="implementing-the-notfound-view-template"></a>템플릿 "NotFound" 보기를 구현합니다.

요청 된 dinner를 찾을 수 없습니다 되었음을 나타내는 오류 메시지가 표시 하는 "NotFound" 보기 템플릿 – 구현부터 시작 합니다.

म 합니다 컨트롤러 작업 메서드 내에서 텍스트 커서를 배치 하 여 새 보기 템플릿을 만들 다음 마우스 오른쪽 단추로 클릭 하 고 "추가" 메뉴 명령을 선택 (Ctrl-M, Ctrl + V를 입력 하 여이 명령은 또한 실행 수):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

이 옵션은 아래와 같은 "뷰 추가" 대화 상자를 표시 합니다. 대화 상자에서 만들 뷰 이름을 미리 채워집니다 기본적으로 일치 하는 동작 메서드의 이름을 커서 시점의 대화 상자에 (이 경우 "Details") 시작 되었습니다. "NotFound" 서식 파일을 먼저 구현 하고자 하기 때문에이 뷰 이름을 재정의 알아보고 "NotFound" 대신 되도록 설정 하겠습니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

"추가" 단추를 클릭 Visual Studio 내에 만들 새 템플릿 "NotFound.aspx" 보기에는 "\Views\Dinners" 디렉터리 (생성 된 디렉터리는 존재 하지 않는 경우):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

또한이 새 "NotFound.aspx" 보기 서식 파일을 코드 편집기에는 것이 열립니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

기본적으로 템플릿 보기는 두 개의 "콘텐츠 영역" 내용 및 코드를 추가할 수 있습니다. 첫 번째 "제목" HTML 페이지의 다시 전송를 사용자 지정할 수 있습니다. 두 번째 다시 전송 HTML 페이지의 "기본 콘텐츠"를 사용자 지정할 수 있습니다.

템플릿 우리의 "NotFound" 보기를 구현 하려면 몇 가지 기본 콘텐츠를 추가 합니다.

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

에서는 다음 직접 시도해 볼 수 브라우저 내에서. 보겠습니다 이렇게 하려면 요청에서 *"/ 9999/Dinners/세부 정보"* URL입니다. 현재 데이터베이스에 존재 하지 않는 하 우리의 "NotFound" 보기 템플릿을 렌더링 하지 우리의 DinnersController.Details() 동작 메서드가 dinner 참조 됩니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

한 가지 위의 스크린샷에 나와 있는 알 수입니다이 기본 보기 템플릿 html을 화면에 기본 콘텐츠를 둘러싸는 bunch를 상속 했습니다. 사이트에서 모든 보기에 대해 일관 된 레이아웃을 적용할 수 있도록 해 주는 "마스터 페이지" 템플릿을 사용 하 여는 우리의 보기 템플릿을 때문입니다. 마스터 페이지이 자습서의 뒷부분에 나오는 부분에 더 많은 작동 방식에 대해 설명 합니다.

### <a name="implementing-the-details-view-template"></a>템플릿 "Details" 보기를 구현합니다.

단일 Dinner 모델에 대 한 HTML을 생성 하는 "Details" 뷰 템플릿에 – 이제 구현 해 보겠습니다.

म 합니다 우리의 텍스트 커서 Details 작업 메서드 내에서이 작업을 수행 하 고 마우스 오른쪽 단추로 클릭 하 고 "추가" 메뉴 명령을 선택 (또는 Ctrl-M, Ctrl + V를 눌러):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

이 "뷰 추가" 대화 상자를 표시 합니다. 기본 뷰 이름 ("정보") 하 게 유지 합니다. 도 대화 상자에서 "강력한 형식의 뷰 만들기" 확인란을 선택 하 고 보기에는 컨트롤러에서 전달 하는 모델 유형에의 이름 (combobox 드롭다운을 사용 하 여) 선택 합니다. 이 보기에 대해 Dinner 개체를 전달 (이 형식에 대 한 정규화 된 이름이: "NerdDinner.Models.Dinner"):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

여기서 "빈 보기"를 만들려면 선택한, 이전 서식 파일과 달리이 시간에 자동으로 선택 됩니다 "스 캐 폴드" "Details" 템플릿을 사용 하 여 보기. 위의 대화 상자에서 "콘텐츠 보기" 드롭다운을 변경 하 여 다음과 같이 나타낼 수 있습니다.

"스 캐 폴딩" Dinner 개체를 전달 하는 것에 따라 세부 정보 보기 템플릿 우리의의 구현이 초기에 생성 됩니다. 이 보기 템플릿 구현에 신속 하 게 시작 하는 쉬운 방법을 제공 합니다.

"추가" 단추를 클릭 Visual Studio 내에 만들 새 "Details.aspx" 보기 템플릿 파일을 수행해 줍니다 우리의 "\Views\Dinners" 디렉터리:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

또한이 새 "Details.aspx" 보기 서식 파일을 코드 편집기에서 열립니다. 저녁 모델을 기반으로 세부 정보 보기의 초기 스 캐 폴드 구현을 포함 합니다. 스 캐 폴딩 엔진.NET 리플렉션을 사용 하 여, 전달 된 클래스에 노출 된 공용 속성을 보고 하 고 찾은 각 형식에 따라 적절 한 콘텐츠를 추가 합니다.

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

요청할 수는 *"/ 1/세부 정보/Dinners"* URL을 브라우저에서이 "details" 스 캐 폴드 구현 어떻게 나타나는지 확인 합니다. 이 URL을 사용 하 여 우리가 처음 만들 때 수동으로 데이터베이스에 추가한 dinners 중 하나가 표시 됩니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

이 us 실행 되 고 신속 하 게 가져오고 우리의 Details.aspx 뷰가의 초기 구현을 제공 합니다. 그런 다음 이동 하 고 우리의 만족도 UI를 사용자 지정 하도록 조정할 수 있습니다 했습니다.

더욱 긴밀 하 게 Details.aspx 서식 파일에서 살펴볼 때는 것에 정적 HTML 포함으로 렌더링 코드를 삽입 소요 됩니다. &lt;% %&gt; 코드 너 템플릿 보기에서 렌더링할 때 코드를 실행 하 고 &lt;% = %&gt; 코드 너 그 안에 포함 된 코드를 실행 하 고 다음 서식 파일의 출력 스트림에 결과 렌더링 합니다.

"모델" 강력한 형식의 속성을 사용 하 여 컨트롤러에서 전달 된 "Dinner" 모델 개체에 액세스 하는 뷰 내에서 코드를 작성할 수 있습니다. Visual Studio 측정할 전체 코드 intellisense 편집기 내에서이 "Model" 속성에 액세스할 때:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

우리의 마지막 세부 정보 보기 템플릿에 대 한 소스 아래 모양이 되도록 몇 가지 변경을 만들어 보겠습니다.

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

액세스할 때의 *"/ 1/세부 정보/Dinners"* URL 다시 하므로 이제 다음과 유사한 렌더링 합니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a>템플릿 "Index" 보기를 구현합니다.

생성 하는 예정 된 Dinners 목록이 "Index" 보기 템플릿 – 이제 구현 해 보겠습니다. 이 인덱스 작업 메서드 내에서 텍스트 커서를 놓은 다음 마우스 오른쪽 단추로 합니다 म 클릭 하 고 "추가" 메뉴 명령을 선택 (또는 Ctrl-M, Ctrl + V를 눌러) 할 일입니다.

"뷰 추가" 대화 상자 내에서 "Index" 라는 보기 템플릿을 유지 알아보고 "강력한 형식의 뷰 만들기" 확인란을 선택 하겠습니다. 이 시간에서는 자동으로 "List" 보기 서식 파일을 생성 하 고 "NerdDinner.Models.Dinner" 모델 형식으로 뷰에 전달 선택를 선택 합니다 (있는 스 캐 폴딩 하는 것으로 가정 하는 뷰 추가 대화 상자의 하면 "목록" 생성 나타낸 것 때문에 전달 Dinner 개체 시퀀스의 컨트롤러에서 뷰로):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

"추가" 단추를 클릭 Visual Studio는을 수행해 줍니다 새 "Index.aspx" 보기 템플릿 파일을 우리의 "\Views\Dinners" 디렉터리 내에서 만듭니다. 것은 "스 캐 폴드" 내 뷰에 전달 Dinners의 HTML 테이블 목록은를 제공 하는 초기 구현 합니다.

된 액세스 권한 및 응용 프로그램을 실행할 때의 *"/" (Dinners/* 같이 URL dinners 목록의 렌더링 합니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

위의 테이블 솔루션 목록 Dinner 나열 마주보는 소비자에 대해 원하는 대로 매우이 Dinner 데이터 –의 표 형식 레이아웃에 있습니다. Index.aspx 뷰 템플릿을 업데이트 하 고 더 적은 열 데이터를 나열 하 고 사용 하도록 수정 수는 &lt;ul&gt; 아래 코드를 사용 하 여 테이블 대신이 렌더링 하는 요소:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

부문의 각 dinner 반복 것으로 위의 foreach 문 내에서 "var" 키워드를 사용 했습니다. C# 3.0에 잘 하는 것 이라는 dinner 개체가 런타임에 바인딩된 임을 의미 "var"를 사용 하 여 생각할 수 있습니다. 대신 컴파일러가 "Model" 강력한 형식의 속성에 대해 형식 유추를 사용 하 고 있는지 의미 (가 형식의 "a b l e&lt;Dinner&gt;") 및 로컬 "dinner" 변수 얻을 수 있는 전체 즉 Dinner 유형 –으로 컴파일 intellisense 및 컴파일 시간에 대 한 코드 블록 내에서 확인 하는 중:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

새로 고침을 누릅니다 우리는 */Dinners* 아래 우리의 업데이트 된 보기 이제 다음과 같은 브라우저에서 URL:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

이 더 나은 – 찾고 하지만 아직 완전히 준비 되지 않았습니다. 수행할 마지막 단계는 최종 사용자가 목록에서 개별 Dinners를 클릭 하 고에 대 한 세부 정보를 볼 수 있도록 합니다. 이 우리의 DinnersController 세부 정보 동작 메서드에 연결 되는 HTML 하이퍼링크 요소를 렌더링 하 여 구현 합니다.

두 가지 방법 중 하나에 인덱스, 뷰 내의이 하이퍼링크를 생성할 수 있습니다. 첫 번째는 HTML을 수동으로 만드는 &lt;는&gt; 포함에서는 아래와 같은 요소 &lt;% %&gt; 내에서 차단 된 &lt;는&gt; HTML 요소:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

프로그래밍 방식으로 HTML을 만들기를 지 원하는 ASP.NET MVC에서 기본 제공 "Html.ActionLink()" 도우미 메서드를 활용 하는 다른 방법은 사용할 수는 &lt;는&gt; 에 다른 동작 메서드에 연결 하는 요소는 컨트롤러:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

Html.ActionLink() 도우미 메서드를 사용 하는 첫 번째 매개 변수가 표시할 링크 텍스트입니다 (이 경우 제목 dinner의)에서 두 번째 매개 변수는 컨트롤러 동작 이름 (이 예제의 Details 메서드)에 대 한 링크를 생성 하려고 하 고 세 번째 매개 변수는 집합 작업 (속성 이름/값을 가진 익명 형식으로 구현 됨)로 전달할 매개 변수입니다. 이 경우 여기서 지정 하는, 연결 하 고 ASP.NET MVC에서 규칙 기본 URL 라우팅 이므로 dinner의 "id" 매개 변수 "{Controller} / {Action} / {id}" Html.ActionLink() 도우미 메서드는 다음과 같은 출력을 생성 합니다.

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

우리의 Index.aspx 보기에 대 한 Html.ActionLink() 도우미 메서드 접근 방식을 사용 알아보고 각 dinner 적절 한 세부 정보 URL에 목록 링크에 있는 하겠습니다.

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

및 도달할 때 이제는 */Dinners* dinner 목록 아래 다음과 같은 URL:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

목록에서 Dinners 중 하나를 클릭 하는 경우 항목에 대 한 자세한 내용을 보려면 이동할 합니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a>명명 규칙 기반 및 \Views 디렉터리 구조

기본적으로 ASP.NET MVC 응용 프로그램 템플릿 보기를 확인할 때 구조 이름 지정 규칙 기반 디렉터리를 사용 합니다. 개발자를 정규화 위치 경로 컨트롤러 클래스 내에서 뷰를 참조할 때 필요가 없도록 있습니다. 기본적으로 ASP.NET MVC 뷰 템플릿 파일 내에서 찾습니다는 * \Views\[ControllerName]\* 응용 프로그램 아래 디렉터리입니다.

예를 들어 지금까지 작업 템플릿 세 가지 보기를 명시적으로 참조 DinnersController 클래스 –: "Index", "Details" 및 "NotFound"입니다. ASP.NET MVC에서는 기본적으로 찾습니다. 내에서 이러한 보기는 *\Views\Dinners* 우리의 응용 프로그램 루트 디렉터리 아래에 있는 디렉터리:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

어떻게 없어 위에 현재 프로젝트 내에서 세 가지 컨트롤러 클래스 (DinnersController, HomeController 및 AccountController-마지막 두 프로젝트를 만들 때 기본적으로 추가 된), 세 가지 하위 디렉터리 (마다 하나씩 되며 컨트롤러) \Views 디렉터리 내에서.

홈 및 계정 컨트롤러에서 참조 하는 뷰에 해당에서 보기 템플릿을 자동으로 해결 됩니다 *\Views\Home* 및 *\Views\Account* 디렉터리입니다. *\Views\Shared* 하위 디렉터리를 다시 사용 되는 응용 프로그램 내의 여러 컨트롤러에서 템플릿 보기를 저장 하는 방법을 제공 합니다. 먼저 내에서 확인 ASP.NET MVC 템플릿 보기를 확인 하려고 시도 하는 경우는 *\Views\[컨트롤러]* 특정 디렉터리 템플릿 보기를 찾을 수 없는 경우 발생 표시 됩니다 내에서 *\Views\ 공유* 디렉터리입니다.

개별 보기 템플릿 이름 지정에 관한, 권장된 지침은 보기 템플릿 렌더링를 일으킨 작업 메서드와 동일한 이름을 공유 하는 것입니다. 예를 들어 우리의 "Index" 위에 동작 메서드가 뷰 결과 렌더링 하 "Index" 보기를 사용 및 "Details 라는" 작업 메서드 "Details" 보기를 사용 하 여 결과 렌더링 하는 합니다. 따라서 쉽게 각 작업과 연결 된 것은 신속 하 게 확인할 수 있습니다.

개발자가 명시적으로 템플릿 보기에는 컨트롤러에서 호출 되는 동작 메서드가와 동일한 이름을 보기 템플릿 이름을 지정할 필요가 없습니다. 대신 방금에 전달할 수는 모델 개체 "View()" 도우미 메서드 (하지 않고 뷰 이름 지정) 및 ASP.NET MVC를 사용 하 여 자동으로 유추 됩니다는 *\Views\[ControllerName]\[ActionName]* 렌더링 하는 디스크에 템플릿 보기.

따라서 약간, 컨트롤러 코드를 정리 하 고 코드에서 두 번 이름 중복을 피하기 위해 수 있습니다.

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

위의 코드는 좋은 Dinner 등록/정보를 구현 하는 데 필요한 모든 사이트에 대 한 환경입니다.

#### <a name="next-step"></a>다음 단계

검색 환경 구축 멋진 Dinner를 했습니다.

CRUD (만들기, 읽기, 업데이트, 삭제) 데이터를 편집할 수 있도록 지원 이제 하도록 하겠습니다.

>[!div class="step-by-step"]
[이전](build-a-model-with-business-rule-validations.md)
[다음](provide-crud-create-read-update-delete-data-form-entry-support.md)
