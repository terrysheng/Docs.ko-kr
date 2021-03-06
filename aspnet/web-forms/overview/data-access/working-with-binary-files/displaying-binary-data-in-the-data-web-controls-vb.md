---
uid: web-forms/overview/data-access/working-with-binary-files/displaying-binary-data-in-the-data-web-controls-vb
title: "(VB)를 제어 하는 데이터 웹에 이진 데이터를 표시 | Microsoft Docs"
author: rick-anderson
description: "이 자습서에서는 이진 데이터를 이미지 파일의 표시 및 f '다운로드' 링크를 제공을 포함 하 여 웹 페이지를 표시 하는 옵션 표시 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/27/2007
ms.topic: article
ms.assetid: 9201656a-e1c2-4020-824b-18fb632d2925
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/displaying-binary-data-in-the-data-web-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: df79748bf5734ffcb9eb81ca089aeded0e63bdc5
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="displaying-binary-data-in-the-data-web-controls-vb"></a>웹 컨트롤 (VB) 데이터에서에서 이진 데이터 표시
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_55_VB.exe) 또는 [PDF 다운로드](displaying-binary-data-in-the-data-web-controls-vb/_static/datatutorial55vb1.pdf)

> 이 자습서에서는 이진 데이터를 이미지 파일의 표시 및 PDF 파일에 대 한 '다운로드' 링크를 제공을 포함 하 여 웹 페이지를 표시 하는 옵션 표시 합니다.


## <a name="introduction"></a>소개

이전 자습서에서는 이진 데이터는 응용 프로그램 s 기본 데이터 모델 연결에 대 한 두 가지 기법을 탐색 하 고 브라우저에서 웹 서버의 파일 시스템에 파일을 업로드할 파일 업로드 컨트롤을 사용 합니다. 에서는 데이터 모델을 통해 업로드 된 이진 데이터를 연결 하는 방법을 알아보려면 아직 했습니다. 즉, 파일 업로드 되 고 파일 시스템에 저장 된 후 적절 한 데이터베이스 레코드에는 파일의 경로를 저장 합니다. 데이터베이스에서 직접에서 데이터가 저장 되는 경우 업로드 된 이진 데이터 필요한 파일 시스템에 저장할 수 없습니다 있지만 데이터베이스에 삽입 해야 합니다.

데이터 모델이 있는 데이터 연결 살펴보기 전에 먼저 최종 사용자에 게 이진 데이터를 제공 하는 방법에 대해 s를 사용 하지만 있습니다. 텍스트 데이터를 제공 하는 것은 간단 하지만 이진 데이터가 표시 되는 방법을? 종속, 물론, 이진 데이터의 형식에 있습니다. 이미지에 대 한 म 경우가 많습니다; 이미지를 표시 하려면 Pdf, Microsoft Word 문서, ZIP 파일 및 다른 종류의 이진 데이터를 다운로드 링크를 제공 하는 것이 좋습니다.

데이터를 사용 하 여 연결 된 텍스트 데이터와 함께 이진 데이터를 표시 하는 방법을 살펴볼이 자습서에서는 웹 GridView 및 DetailsView와 같은 제어 합니다. 다음 자습서에서는 데이터베이스에 업로드 된 파일 연결에 살펴보겠습니다.

## <a name="step-1-providingbrochurepathvalues"></a>1 단계: 제공`BrochurePath`값

`Picture` 열에는 `Categories` 다양 한 범주 이미지에 대 한 이진 데이터가 이미 포함 되어 있습니다. 특히,는 `Picture` 각 레코드에 대 한 열 매끄럽지, 낮은 품질, 16 색 비트맵 이미지의 이진 콘텐츠를 보유 합니다. 각 항목 이미지는 172 픽셀 너비와 120 픽셀 높이 약 11 (kb)를 사용 합니다. 더 많은 어떤 s에 이진 콘텐츠는 `Picture` 78 바이트를 포함 하는 열 [OLE](http://en.wikipedia.org/wiki/Object_Linking_and_Embedding) 이미지를 표시 하기 전에 제거 해야 하는 헤더입니다. 이 헤더 정보는 Microsoft Access에서 Northwind 데이터베이스에 해당 루트가 때문에 존재 합니다. Access에서 이진 데이터는이 헤더에 tacks OLE 개체 데이터 형식을 사용 하 여 저장 됩니다. 지금은 그림을 표시 하기 위해 이러한 고품질 이미지의 헤더를 제거 하는 방법을 살펴보겠습니다. 이후 자습서에서 s 범주를 업데이트 하기 위한 인터페이스 빌드합니다 `Picture` 열 OLE 헤더 불필요 한 OLE 머리글 없이 해당 JPG 이미지를 사용 하는 이러한 비트맵 이미지를 바꿉니다.

이전 자습서에서 파일 업로드 컨트롤을 사용 하는 방법에 대해 살펴보았습니다. 따라서 계속 추가 하는 브로슈어 파일에서 웹 서버의 파일 시스템에 있습니다. 하지만 이렇게 업데이트 하지 않습니다는 `BrochurePath` 열에는 `Categories` 테이블입니다. 다음 자습서에서는이 수행 하는 방법을 보겠습니다 하지만 지금은 직접이 열에 대 한 값을 제공 해야 합니다.

이 s 자습서 다운로드에 7 개 PDF 브로슈어 파일에서 찾을 수 있습니다는 `~/Brochures` 폴더, Seafood 제외 하 고 범주를 각각에 대해 각각 하나씩 있습니다. I 의도적으로 모든 레코드는 관련 이진 데이터가 시나리오를 처리 하는 방법을 보여 주기 위해 Seafood 브로슈어 추가 생략 되었습니다. 업데이트 하려면는 `Categories` 값이 테이블을 마우스 오른쪽 단추로 클릭는 `Categories` 노드 서버 탐색기에서 테이블 데이터 표시를 선택 합니다. 그런 다음 브로슈어 파일 그림 1 에서처럼를 면에 있는 각 범주에 대 한 가상 경로 입력 합니다. 둡니다 Seafood 범주에 대 한 없습니다 브로슈어 이므로 해당 `BrochurePath` s 열 값으로 `NULL`합니다.


[![범주 테이블의 BrochurePath 열에 대 한 값을 직접 입력](displaying-binary-data-in-the-data-web-controls-vb/_static/image1.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image1.png)

**그림 1**:에 대 한 값을 수동으로 입력 된 `Categories` 테이블 s `BrochurePath` 열 ([전체 크기 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-vb/_static/image2.png))


## <a name="step-2-providing-a-download-link-for-the-brochures-in-a-gridview"></a>GridView에 브로슈어에 대 한 다운로드 링크를 제공 하는 2 단계:

와 `BrochurePath` 에 제공 된 값은 `Categories` 테이블 준비 된 범주의 브로슈어 다운로드 링크와 함께 각 범주를 나열 하는 GridView를 만들려고 했습니다. 4 단계에서에서도 s 범주 이미지를 표시 하려면이 GridView 확장할 것입니다.

GridView의 디자이너 도구 상자에서 끌어 시작는 `DisplayOrDownloadData.aspx` 페이지에 `BinaryData` 폴더입니다. GridView s 설정 `ID` 를 `Categories` GridView s 스마트 태그를 통해 새 데이터 원본에 연결 하려면 선택 합니다. 특히, 라는 ObjectDataSource 바인딩할 `CategoriesDataSource` 사용 하 여 데이터를 검색 하는 `CategoriesBLL` 개체의 `GetCategories()` 메서드.


[![CategoriesDataSource 라는 새 ObjectDataSource 만들기](displaying-binary-data-in-the-data-web-controls-vb/_static/image2.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image3.png)

**그림 2**: 명명 된 새 ObjectDataSource 만드는 `CategoriesDataSource` ([전체 크기 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-vb/_static/image4.png))


[![ObjectDataSource CategoriesBLL 클래스를 사용 하도록 구성](displaying-binary-data-in-the-data-web-controls-vb/_static/image3.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image5.png)

**그림 3**: 구성에 사용 하 여 ObjectDataSource는 `CategoriesBLL` 클래스 ([전체 크기 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-vb/_static/image6.png))


[![GetCategories() 메서드를 사용 하 여 범주 목록을 검색합니다](displaying-binary-data-in-the-data-web-controls-vb/_static/image4.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image7.png)

**그림 4**: 사용 하면 검색 목록의 범주는 `GetCategories()` 메서드 ([전체 크기 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-vb/_static/image8.png))


데이터 소스 구성 마법사를 완료 한 후 Visual Studio는 자동으로 추가 하려면 BoundField는 `Categories` GridView에 대 한는 `CategoryID`, `CategoryName`, `Description`, `NumberOfProducts`, 및 `BrochurePath` `DataColumn` s입니다. 계속 해 서 제거는 `NumberOfProducts` 이후 BoundField는 `GetCategories()` 방법을의 쿼리는이 정보를 검색 하지 않습니다. 제거는 `CategoryID` BoundField 및 이름 바꾸기는 `CategoryName` 및 `BrochurePath` BoundFields `HeaderText` 속성 범주 및 브로슈어를 각각. 다음과 같이 변경한 후 GridView 및 ObjectDataSource s 선언적 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample1.aspx)]

이 페이지는 브라우저를 통해 (그림 5 참조). 8 개 범주를 각각 나열 됩니다. 7 가지 범주와 `BrochurePath` 값는 `BrochurePath` 해당 BoundField에 표시 된 값입니다. Seafood 있는 `NULL` 값을 해당 `BrochurePath`, 빈 셀을 표시 합니다.


[![각 범주가의 이름, 설명 및 BrochurePath 값 목록](displaying-binary-data-in-the-data-web-controls-vb/_static/image5.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image9.png)

**그림 5**: 각 범주의 이름, 설명 및 `BrochurePath` 나열 된 값 ([전체 크기 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-vb/_static/image10.png))


텍스트를 표시 하는 대신는 `BrochurePath` 브로슈어에 대 한 링크를 만들려면 원하는 열입니다. 이를 위해 제거는 `BrochurePath` BoundField는 HyperLinkField 바꿉니다. 새 HyperLinkField s 설정 `HeaderText` 속성 면, 해당 `Text` 보기 면 속성 및 해당 `DataNavigateUrlFields` 속성을 `BrochurePath`합니다.


![HyperLinkField BrochurePath에 대 한 추가](displaying-binary-data-in-the-data-web-controls-vb/_static/image6.gif)

**그림 6**:에 대 한 HyperLinkField 추가`BrochurePath`


그림 7 볼 수 있듯이 GridView에 링크 열을 추가 합니다이. 보기 브로슈어 링크를 클릭 하면 브라우저에서 직접 PDF를 표시 하거나 사용자 PDF reader가 설치 되어 있는지 여부에 따라 파일을 다운로드 하 고 s 브라우저 설정 메시지를 표시 합니다.


[![범주의 브로슈어 보기 브로슈어 링크를 클릭 하 여 볼 수 있습니다.](displaying-binary-data-in-the-data-web-controls-vb/_static/image7.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image11.png)

**그림 7**: 보기 브로슈어 링크를 클릭 하 여 A 범주의 브로슈어 볼 수 있습니다 ([전체 크기 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-vb/_static/image12.png))


[![S 브로슈어 PDF의 범주 표시](displaying-binary-data-in-the-data-web-controls-vb/_static/image8.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image13.png)

**그림 8**: 브로슈어 PDF 표시 되는 다음 범주 s ([전체 크기 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-vb/_static/image14.png))


## <a name="hiding-the-view-brochure-text-for-categories-without-a-brochure"></a>브로슈어 없이 범주에 대 한 보기 브로슈어 텍스트 숨기기

그림 7에서 볼 수 있듯이 `BrochurePath` HyperLinkField 표시 해당 `Text` 여부에 관계 없이 모든 레코드에 대 한 속성 값 (보기 브로슈어) 여기서 s는 비-`NULL` 값 `BrochurePath`합니다. 물론, 경우 `BrochurePath` 은 `NULL`, 링크 텍스트,으로 표시 됩니다 경우 Seafood 범주와 마찬가지로 (그림 7 다시 참조). 보기 브로슈어 텍스트를 표시 하는 대신 좋을 것 없이 해당 범주에 `BrochurePath` 값이 같은 아니요 브로슈어 사용할 수 있는 몇 가지 대체 텍스트를 표시 합니다.

이 문제를 제공 하기 위해를 TemplateField 내용이 기반으로 적절 한 출력을 내보내는 페이지 메서드를 호출을 통해 생성 되는 데 사용 해야는 `BrochurePath` 값입니다. 먼저 살펴본이 기법을 서식 지정에 [GridView 컨트롤에 사용 하 여 TemplateFields](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) 자습서입니다.

선택 하 여는 HyperLinkField를 TemplateField로 설정 된 `BrochurePath` HyperLinkField 클릭 한 다음에서 변환이이 필드를 TemplateField로 열 편집 대화 상자에서 연결 합니다.


![HyperLinkField를 TemplateField로 변환](displaying-binary-data-in-the-data-web-controls-vb/_static/image9.gif)

**그림 9**:는 HyperLinkField를 TemplateField로 변환


와 TemplateField 만들어집니다는 `ItemTemplate` 하이퍼링크 웹을 포함 하는 컨트롤 `NavigateUrl` 속성이 바인딩되는 `BrochurePath` 값입니다. 이 태그는 메서드를 호출 하 여 대체 `GenerateBrochureLink`값에서 전달 `BrochurePath`:


[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample2.aspx)]

다음으로 만듭니다는 `Protected` 메서드는 asp.net에서 페이지 라는 s 코드 숨김 클래스 `GenerateBrochureLink` 반환 하는 `String` 고 수락 하는 `Object` 입력된 매개 변수로 합니다.


[!code-vb[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample3.vb)]

이 메서드를 확인 하는 경우 전달에서 `Object` 값은 데이터베이스 `NULL` 및 그렇다면 범주에는 브로슈어 부족을 나타내는 메시지를 반환 합니다. 그렇지 않은 경우는 `BrochurePath` 값을 해당 하이퍼링크에 표시 되 합니다. 되는 경우는 `BrochurePath` 값은 s에 전달 된 표시는 [ `ResolveUrl(url)` 메서드](https://msdn.microsoft.com/library/system.web.ui.control.resolveurl.aspx)합니다. 이 메서드는 전달 기능을 확인 *url*, 대체는 `~` 문자 적절 한 가상 경로 사용 합니다. 예를 들어, 응용 프로그램에서 시작 하는 경우 `/Tutorial55`, `ResolveUrl("~/Brochures/Meats.pdf")` 돌아갑니다 `/Tutorial55/Brochures/Meat.pdf`합니다.

그림 10 이러한 변경 내용을 적용 한 후 페이지를 보여줍니다. Seafood 범주의 `BrochurePath` 필드 이제 아니요 브로슈어 사용할 수 있는 텍스트에 표시 됩니다.


[![이러한 범주 없이 정도 브로슈어에 대 한 텍스트 아니요 브로슈어 사용할 표시 됩니다.](displaying-binary-data-in-the-data-web-controls-vb/_static/image10.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image15.png)

**그림 10**: The 텍스트 아니요 브로슈어 사용할 수 있는 범주 없이 정도 브로슈어에 대해 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-vb/_static/image16.png))


## <a name="step-3-adding-a-web-page-to-display-a-category-s-picture"></a>3 단계: 범주의 그림을 표시 하는 웹 페이지 추가

사용자는 ASP.NET 페이지를 방문 페이지의 HTML ASP.NET을 받습니다. 받은 HTML은 단순히 텍스트 및 이진 데이터가 포함 되지 않습니다. 이미지, 사운드 파일 등, Macromedia Flash 응용 프로그램, 포함 된 Windows Media Player 비디오, 추가 이진 데이터, 웹 서버에서 별도 리소스로 존재 합니다. HTML이이 파일에 대 한 참조를 포함 되어 있지만 파일의 실제 내용이 포함 되지 않습니다.

예를 들어 HTML에서에서는 `<img>` 요소와 그림을 참조를 사용 하는 `src` 같이 이미지 파일을 가리키는 특성:


[!code-html[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample4.html)]

브라우저가이 HTML을 받으면 다른 요청을 브라우저에 표시 한 다음 이미지 파일의 이진 콘텐츠를 검색 하는 웹 서버를 만듭니다. 이진 데이터에 동일한 개념을 적용합니다. 2 단계에서에서 브로슈어 페이지의 HTML 태그의 일부로 브라우저에 전송 되지 않았습니다. 대신, 렌더링 된 HTML 제공 된 하이퍼링크를 클릭 하면 PDF 문서를 직접 요청 하도록 브라우저에 발생 합니다.

를 표시 하거나 사용자가 데이터베이스 내에 상주 하는 이진 데이터를 다운로드 하도록 허용 하려면 데이터를 반환 하는 별도 웹 페이지 생성 해야 합니다. 샘플 응용 프로그램에서는 거기 s 이진 데이터 필드를 하나만 데이터베이스 범주의 그림에 직접 저장 합니다. 따라서 페이지 필요는 호출할 때 특정 범주에 대 한 이미지 데이터를 반환 합니다.

새 ASP.NET 페이지를 추가 `BinaryData` 라는 폴더 `DisplayCategoryPicture.aspx`합니다. 이렇게 할 경우 마스터 페이지 선택 확인란을 선택 합니다. 이 페이지에서는 `CategoryID` querystring과 해당 범주의 s 이진 데이터를 반환 값 `Picture` 열입니다. 이 페이지는 이진 데이터와 겉을 반환 하므로 HTML 섹션의 모든 태그는 필요 하지 않습니다. 따라서 소스 탭 하단 왼쪽된 모서리 쪽에서 클릭 하 고 모두를 제외 하 고 페이지의 태그 제거는 `<%@ Page %>` 지시문입니다. 즉, `DisplayCategoryPicture.aspx` s 선언 태그는 한 줄으로 구성 되어야 합니다.


[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample5.aspx)]

표시 되 면는 `MasterPageFile` 특성에 `<%@ Page %>` 지시문을 제거 합니다.

페이지의 코드 숨김 클래스에 다음 코드를 추가 `Page_Load` 이벤트 처리기.


[!code-vb[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample6.vb)]

이 코드에 대 한 읽기에서 시작 하는 `CategoryID` querystring 값을 변수에 라는 `categoryID`합니다. 에 대 한 호출을 통해 그림 데이터를 검색 하는 다음으로 `CategoriesBLL` s 클래스 `GetCategoryWithBinaryDataByCategoryID(categoryID)` 메서드. 이 데이터를 사용 하 여 클라이언트에 반환 되는 `Response.BinaryWrite(data)` 메서드 전에이 메서드가 호출 되는 `Picture` 열 값의 OLE 머리글을 제거 해야 합니다. 만들어 이렇게는 `Byte` 라는 배열을 `strippedImageData` 정확 하 게 78 보유 하는 기능을 보다 작은 문자는 `Picture` 열. [ `Array.Copy` 메서드](https://msdn.microsoft.com/library/z50k9bft.aspx) 에서 데이터를 복사 하는 데 사용 `category.Picture` 를 통해 78 위치에서 시작 `strippedImageData`합니다.

`Response.ContentType` 속성 지정는 [MIME 형식을](http://en.wikipedia.org/wiki/MIME) 브라우저에 렌더링 하는 방법을 알 수 있도록 반환 되는 콘텐츠의 합니다. 이후는 `Categories` 테이블의 `Picture` 열이 비트맵 이미지, 비트맵 MIME 형식 사용은 여기 (이미지/bmp). MIME 형식을 생략 하면 대부분의 브라우저는 여전히 이미지 올바르게 표시할 이미지 파일 s 이진 데이터의 내용에 따라 형식을 유추할 수 있습니다. 그러나 해당 MIME을 포함 하는 것이 좋습니다 s 가능한 경우 입력 합니다. 참조는 [Internet Assigned Numbers Authority 웹 사이트](http://www.iana.org/) 의 전체 목록을 보려면 [MIME 미디어 형식](http://www.iana.org/assignments/media-types/)합니다.

만든이 페이지와 특정 범주의의 그림을 볼 수 있습니다 방문 하 여 `DisplayCategoryPicture.aspx?CategoryID=categoryID`합니다. 그림 11에서 볼 수 있는 음료 범주의 그림에 나와 `DisplayCategoryPicture.aspx?CategoryID=1`합니다.


[![음료 범주의 그림이 표시 됩니다](displaying-binary-data-in-the-data-web-controls-vb/_static/image11.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image17.png)

**그림 11**: The 음료 범주의 그림이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-vb/_static/image18.png))


If, 방문할 때 `DisplayCategoryPicture.aspx?CategoryID=categoryID`을 'System.Byte ' 형식으로 ' System.DBNull' 종류의 개체를 캐스팅할 수 없습니다 읽을 수 있는 예외가 발생이 일으킬 수 있는 두 가지입니다. 첫째, 고 `Categories` 테이블 s `Picture` 열은 허용 `NULL` 값입니다. 그러나 `DisplayCategoryPicture.aspx` 페이지에서이 있는 비-가정`NULL` 있는 값을 값입니다. `Picture` 의 속성은 `CategoriesDataTable` 으로 설정한 경우에 직접 액세스할 수 없는 `NULL` 값입니다. 허용 하려는 경우 `NULL` 에 대 한 값은 `Picture` 열 d 포함 하려면 다음과 같은 조건:


[!code-vb[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample7.vb)]

위의 코드에서는 일부 이미지 라는 파일을 한다는 문제가 s `NoPictureAvailable.gif` 에 `Images` 그림 없이 해당 범주에 대 한 표시 하려면 폴더입니다.

경우에이 예외를 발생 수는 `CategoriesTableAdapter` s `GetCategoryWithBinaryDataByCategoryID` s 메서드에 `SELECT` 문이 임시 SQL 문이 사용 중이 고 적 TableAdapter s에 대 한 마법사를 다시 실행 하는 경우에 발생할 수 있음 주 쿼리의 열 목록으로 다시 되돌렸습니다. 주 쿼리입니다. 확인 되도록 `GetCategoryWithBinaryDataByCategoryID` s 메서드에 `SELECT` 문을 아직 포함 되어는 `Picture` 열입니다.

> [!NOTE]
> 될 때마다는 `DisplayCategoryPicture.aspx` 가 방문 하면 데이터베이스를 액세스 하 고 지정 된 범주의 그림 데이터가 반환 됩니다. 그러나 범주의 그림 않았음을 t 달라졌는지 때까지 사용자가 표시 마지막 작업입니다. 에 대 한 HTTP를 사용 하면 다행히 *조건부 가져옵니다*합니다. 조건부 GET HTTP 요청을 하는 클라이언트와 함께 보냅니다는 [ `If-Modified-Since` HTTP 헤더](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html) 날짜와 클라이언트는 웹 서버에서이 리소스를 마지막으로 검색 하는 시간을 제공 하는 합니다. 웹 서버를 선택할 수 이후 날짜를 지정 하는이 콘텐츠가 변경 되지 않은 경우는 [수정 되지 않음 상태 코드 (304)](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) 다시 보내는 중 요청 된 리소스의 콘텐츠를 취소 하 고 있습니다. 즉,이 기술이에서는 웹 서버 클라이언트에서 마지막 액세스 이후 수정 되지 않은 경우 리소스에 대 한 콘텐츠를 전송 하지 않아도 됩니다.


그러나이 동작을 구현 하려면 추가 하는 사용 하려면는 `PictureLastModified` 열을는 `Categories` 캡처할 때 테이블은 `Picture` 열 확인 하기 위한 코드 뿐만 아니라 마지막으로 업데이트 된는 `If-Modified-Since` 헤더입니다. 대 한 자세한 내용은 `If-Modified-Since` 머리글과 조건부 GET 워크플로에서 참조 [RSS 해커에 대 한 HTTP 조건부 GET](http://fishbowl.pastiche.org/2002/10/21/http_conditional_get_for_rss_hackers) 및 [A 자세히 살펴보고 ASP.NET 페이지에서 HTTP 요청을 수행](http://aspnet.4guysfromrolla.com/articles/122204-1.aspx)합니다.

## <a name="step-4-displaying-the-category-pictures-in-a-gridview"></a>4 단계:는 GridView에 범주 그림을 나타내려면

사용 하 여 표시할 수 특정 범주의의 그림을 표시 하는 웹 페이지를 만들었으므로 이제 해당는 [이미지 웹 컨트롤](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/standard/image.aspx) 또는 HTML `<img>` 요소를 가리키는 `DisplayCategoryPicture.aspx?CategoryID=categoryID`합니다. 이미지 URL 데이터베이스 데이터에 의해 결정 되는 GridView 또는 DetailsView의 이미지 필드를 사용 하 여 표시할 수 있습니다. ImageField 포함 `DataImageUrlField` 및 `DataImageUrlFormatString` HyperLinkField s 처럼 작동 하는 속성 `DataNavigateUrlFields` 및 `DataNavigateUrlFormatString` 속성입니다.

S를 확장 하 고 `Categories` GridView에 `DisplayOrDownloadData.aspx` 각 범주의 그림을 표시 하는 이미지 필드를 추가 하 여 합니다. 단순히는 이미지 필드를 추가 하 고 설정의 `DataImageUrlField` 및 `DataImageUrlFormatString` 속성을 `CategoryID` 및 `DisplayCategoryPicture.aspx?CategoryID={0}`각각. 이 렌더링 하는 GridView 열을 만듭니다는 `<img>` 요소 인 `src` 특성 참조 `DisplayCategoryPicture.aspx?CategoryID={0}`{0}의 GridView 행으로 바뀌는, `CategoryID` 값입니다.


![GridView에는 이미지 필드를 추가 합니다.](displaying-binary-data-in-the-data-web-controls-vb/_static/image12.gif)

**그림 12**: GridView에는 이미지 필드를 추가 합니다.


Soothe 처럼 GridView s 선언적 구문은 이미지 필드를 추가한 후 다음:


[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample8.aspx)]

브라우저를 통해이 페이지를 보려면 잠시 시간. Note 각 레코드의 범주에 대 한 그림을 이제 포함 됩니다.


[![각 행에 대 한 범주의 그림이 표시 됩니다.](displaying-binary-data-in-the-data-web-controls-vb/_static/image13.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image19.png)

**그림 13**: The 범주 s 각 행에 대해 그림이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-vb/_static/image20.png))


## <a name="summary"></a>요약

이 자습서에서는 이진 데이터를 표시 하는 방법을 검사 했습니다. 데이터 표시 되는 방식을 데이터의 형식에 따라 달라 집니다. PDF 브로슈어 파일에 대 한 혜택을 제공 해 사용자 보기 브로슈어 링크를 클릭 하면 PDF 파일에 직접 사용자 걸렸습니다. 범주의 내용을 검색 하 고 데이터베이스에서 이진 데이터를 반환 하는 페이지를 처음 만들 म을 다음 해당 페이지를 사용 하는 GridView에 각 범주의 그림을 표시 합니다.

해당 म 것은 사용 이제 했습니다 준비 된 삽입, 업데이트 및 삭제 된 이진 데이터는 데이터베이스에 대해 수행 하는 방법을 검사할에서는 이진 데이터를 표시 하는 방법을 알아보았습니다. 다음 자습서는 해당 데이터베이스 레코드와 업로드 된 파일을 연결 하는 방법을 살펴보겠습니다. 그 후 자습서, 연결 된 해당 레코드가 제거 될 때 이진 데이터를 삭제 하는 방법 뿐만 아니라 기존 이진 데이터를 업데이트 하는 방법을 살펴보겠습니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Teresa 머피 및 Dave Gardner 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](uploading-files-vb.md)
[다음](including-a-file-upload-option-when-adding-a-new-record-vb.md)
