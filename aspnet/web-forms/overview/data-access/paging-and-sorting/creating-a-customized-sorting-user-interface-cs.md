---
uid: web-forms/overview/data-access/paging-and-sorting/creating-a-customized-sorting-user-interface-cs
title: "사용자 지정 된 정렬의 사용자 인터페이스 (C#) 만들기 | Microsoft Docs"
author: rick-anderson
description: "데이터 정렬의 긴 목록을 표시 하는 경우를 아주 유용할 수 있습니다 행 구분 기호를 도입 하 여 관련된 데이터를 그룹화 합니다. 이 자습서에서는 보겠습니다 cre 하는 방법..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/15/2006
ms.topic: article
ms.assetid: 6f81b633-9d01-4e52-ae4a-2ea6bc109475
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/creating-a-customized-sorting-user-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: dbd2f6c8f1e21529da8a0fbffab212a29f615cc1
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="creating-a-customized-sorting-user-interface-c"></a>사용자 지정 된 정렬의 사용자 인터페이스 (C#) 만들기
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_27_CS.exe) 또는 [PDF 다운로드](creating-a-customized-sorting-user-interface-cs/_static/datatutorial27cs1.pdf)

> 데이터 정렬의 긴 목록을 표시 하는 경우를 아주 유용할 수 있습니다 행 구분 기호를 도입 하 여 관련된 데이터를 그룹화 합니다. 이 자습서는 이러한 정렬 사용자 인터페이스를 만드는 방법을 살펴보겠습니다.


## <a name="introduction"></a>소개

긴 목록을 표시 합니다. 정렬 한 경우 데이터 정렬된 된 열에서 서로 다른 값의 일부만 있는 최종 사용자 할 때 하드를 차이 경계 수행 정확히, where, 구분 합니다. 예를 들어 데이터베이스에 있지만 9 개의 다른 범주 선택 81 제품 들 (8 개의 고유 범주와 `NULL` 옵션). Seafood 범주에 속하는 제품을 검사 하는 데 관심이 인 사용자의 대/소문자를 고려 합니다. 나열 된 페이지에서 *모든* 단일 GridView에 제품, 사용자가 최상의 선택 하나로 그룹화 범주별 결과 정렬 하려면 이라고 판단할 수 모든 함께 Seafood 제품입니다. 범주별으로 정렬 한 후 사용자 다음 해야 목록을 찾아봅니다 Seafood 그룹화 된 제품의 시작 및 종료 위치를 찾고 있습니다. 결과 사전순으로 정렬 하므로는 Seafood 제품 제품 범주 이름 어렵습니다 하지만 여전히 밀접 하 게 검색 하는 눈금에 항목 목록이 필요 합니다.

정렬 된 그룹 간의 경계를 강조 표시 하려면 여러 웹 사이트는 이러한 그룹 사이 구분 기호를 추가 하는 사용자 인터페이스를 사용 합니다. 구분 기호 그림 1에 나와 있는 것 처럼 사용자를 보다 신속 하 게 특정 그룹을 찾 및 해당 경계 식별으로 데이터에 어떤 고유한 그룹 존재를 확인할 수 있습니다.


[![각 범주 그룹은 명확 하 게 식별](creating-a-customized-sorting-user-interface-cs/_static/image2.png)](creating-a-customized-sorting-user-interface-cs/_static/image1.png)

**그림 1**: 각 범주 그룹은 명확 하 게 식별 ([전체 크기 이미지를 보려면 클릭](creating-a-customized-sorting-user-interface-cs/_static/image3.png))


이 자습서는 이러한 정렬 사용자 인터페이스를 만드는 방법을 살펴보겠습니다.

## <a name="step-1-creating-a-standard-sortable-gridview"></a>1 단계: 표준, 정렬 가능한 GridView 만들기

향상 된 정렬 인터페이스를 제공 하 여 GridView를 보강 하는 방법을 살펴 전에 먼저 제품을 나열 하는 표준 정렬 가능한 GridView 만든이 있습니다. 열어 시작는 `CustomSortingUI.aspx` 페이지에 `PagingAndSorting` 폴더입니다. 페이지에는 GridView 추가 설정, 해당 `ID` 속성을 `ProductList`, 새 ObjectDataSource에 바인딩 하세요. ObjectDataSource 사용 하도록 구성 된 `ProductsBLL` s 클래스 `GetProducts()` 레코드를 선택 하기 위한 방법을 합니다.

만 포함 되는 GridView를 다음으로 구성 된 `ProductName`, `CategoryName`, `SupplierName`, 및 `UnitPrice` BoundFields 및 지원 되지 않는 CheckBoxField 합니다. 마지막으로 구성 하는 GridView s 스마트 태그에 정렬 사용 확인란을 선택 하 여 정렬을 지 원하는 데 GridView (또는 설정 하 여 해당 `AllowSorting` 속성을 `true`). 후 이러한 항목을 추가 하 고 `CustomSortingUI.aspx` 페이지 선언 태그는 다음과 같은 표시 됩니다.


[!code-aspx[Main](creating-a-customized-sorting-user-interface-cs/samples/sample1.aspx)]

브라우저에서 지금까지 진행률을 볼 보십시오. 그림 2는 알파벳 순서로 범주별으로 해당 데이터 정렬 될 때 정렬 가능한 GridView를 보여줍니다.


[![정렬 가능한 GridView의 데이터가 범주별으로 정렬 되는](creating-a-customized-sorting-user-interface-cs/_static/image5.png)](creating-a-customized-sorting-user-interface-cs/_static/image4.png)

**그림 2**: 데이터가 정렬 되는 범주별으로 정렬 하는 GridView s ([전체 크기 이미지를 보려면 클릭](creating-a-customized-sorting-user-interface-cs/_static/image6.png))


## <a name="step-2-exploring-techniques-for-adding-the-separator-rows"></a>2 단계: 구분 기호 행을 추가 하기 위한 기술 탐색

일반, 정렬 가능한 GridView 완료 된 모든 작업을 남았습니다 각 고유한 정렬된 그룹 앞 GridView에서 행 구분 기호를 추가할 수 있습니다. 그러나 어떻게 이러한 행에 삽입할 수 있습니다 GridView? 기본적으로, GridView의 행을 반복 하 여 정렬된 된 열에서 값 사이의 차이점을 수행 하는 위치를 확인 및 필요 적절 한 구분 기호 행을 추가 합니다. 있는지 솔루션 어딘가에 GridView s 자연스럽이 문제를 고려할 때는 `RowDataBound` 이벤트 처리기입니다. 설명한 것 처럼는 [데이터 기반 시 사용자 지정 서식](../custom-formatting/custom-formatting-based-upon-data-cs.md) 자습서, s 행 데이터를 기반으로 행 수준 서식을 적용 하는 경우이 이벤트 처리기는 일반적으로 사용 됩니다. 그러나는 `RowDataBound` 이벤트 처리기가 문제를 해결, 행도이 이벤트 처리기에서 프로그래밍 방식으로 GridView에 추가할 수 없습니다. GridView의 `Rows` , 실제로 컬렉션이 읽기 전용입니다.

GridView에 추가 행을 추가 하는 세 가지 옵션이 했습니다.

- GridView에 바인딩되는 실제 데이터에 이러한 메타 데이터 구분 기호 행 추가
- GridView를 데이터에 바인딩된 후 더 추가 `TableRow` 수집을 제어 하는 GridView s에는 인스턴스
- GridView 컨트롤을 확장 하 고 GridView의 구조 생성을 담당 이러한 메서드를 재정의 하는 사용자 지정 서버 컨트롤 만들기

사용자 지정 서버 컨트롤을 만드는 대부분의 웹 페이지 또는 여러 웹 사이트에서이 기능이 필요 했습니다 경우 가장 좋은 방법이 될를 합니다. 그러나 많은 양의 코드 및 GridView s 내부 작업의 세부 수준으로 철저 하 게 탐색 해야 하는데 것입니다. 따라서이 자습서에 대 한 해당 옵션을 고려 하지 됩니다.

다른 두 가지 옵션 추가 구분 기호 행 되는 실제 데이터는 GridView에 바인딩될과 후 GridView의 컨트롤 컬렉션을 조작 해당 했는데도 문제가 있다면 바인딩된-문제를 다르게 공격 토론을 활용 합니다.

## <a name="adding-rows-to-the-data-bound-to-the-gridview"></a>GridView에 바인딩된 데이터에 행을 추가 합니다.

데이터 원본에 GridView 바인딩되면 만듭니다는 `GridViewRow` 데이터 원본에 의해 반환 된 각 레코드에 대 한 합니다. 따라서 데이터 원본에 GridView에 바인딩하기 전에 구분 기호 레코드를 추가 하 여 필요한 구분 기호 행을 삽입 수입니다. 그림 3이이 개념을 보여 줍니다.


![데이터 소스에 행 구분 기호를 추가 하 한 기술](creating-a-customized-sorting-user-interface-cs/_static/image7.png)

**그림 3**: 중 한 가지 방법은 데이터 원본에 행 구분 기호를 추가 해야


특별 한 구분 기호 레코드가; 있기 때문에 따옴표로 용어 구분 기호 레코드를 사용 rec0. 대신, 우리 해야 어떻게 하 든 플래그 데이터 원본에 있는 특정 레코드 일반 데이터 행이 아닌 한 구분 기호로 사용 되입니다. 다시 바인딩에서는 예제는 `ProductsDataTable` 인스턴스는 GridView에 `ProductRows`합니다. म 수 플래그입니다. 레코드 구분 기호 행으로 설정 하 여 해당 `CategoryID` 속성을 `-1` (이후 값 없습니다 t 존재 일반적으로).

이 기술을 활용 하 여 d 해야 다음 단계를 수행 합니다.

1. GridView에 바인딩할 데이터를 프로그래밍 방식으로 검색 (한 `ProductsDataTable` 인스턴스)
2. GridView s에 따라 데이터를 정렬 `SortExpression` 및 `SortDirection` 속성
3. 반복은 `ProductsRows` 에 `ProductsDataTable`차이점 정렬된 된 열에 있는 곳을 찾고,
4. 각 그룹 경계에서 구분 기호 레코드를 삽입 `ProductsRow` 인스턴스 하나에 s DataTable로 `CategoryID` 로 설정 `-1` (또는 레코드 구분 기호 레코드를 표시 되 면 어떤 지정 결정 되었습니다)
5. 행 구분 기호를 삽입 한 후 프로그래밍 방식으로 데이터를 바인딩하는 GridView

다음 5 단계 외에도 d 해야 GridView s에 대 한 이벤트 처리기를 제공 `RowDataBound` 이벤트입니다. 여기에서 d 확인 `DataRow` 구분 했는지 확인 하 고 행을 하나 있는 `CategoryID` 설정은 `-1`합니다. 이 경우 d 아마도 하고자 서식이 또는 셀에 표시 되는 텍스트를 조정 합니다.

또한 GridView s에 대 한 이벤트 처리기를 제공 하는 데 필요한 만큼, 위에 나와 있는 것 보다 좀 더 작업이 필요한 정렬 그룹 경계 삽입이 기술을 사용 하 여 `Sorting` 의 추적 이벤트 및 유지는 `SortExpression` 및 `SortDirection` 값입니다.

## <a name="manipulating-the-gridview-s-control-collection-after-it-s-been-databound"></a>컬렉션 뒤 s 제어 GridView s 조작 된 데이터 바인딩

GridView에 바인딩하기 전에 데이터를 메시징, 대신 구분 기호 행 추가할 수 있는 *후* 데이터가 GridView에 바인딩 되었습니다. 데이터 바인딩 프로세스는 GridView의 컨트롤 계층 구조, 즉 실제로 쌓이는 단순히 `Table` 인스턴스 셀 컬렉션으로 이루어져 있으며 각 행의 컬렉션으로 구성 합니다. GridView의 컨트롤 컬렉션에 포함 되어 특히는 `Table` 개체의 루트에는 `GridViewRow` (에서 파생 되는 `TableRow` 클래스)의 각 레코드에 대 한는 `DataSource` 는 GridView에 바인딩될 및 `TableCell` 각 의개체`GridViewRow` 에서 각 데이터 필드에 대 한 인스턴스는 `DataSource`합니다.

정렬 각 그룹 사이 구분 기호 행을 추가 하려면 만든 후이 컨트롤 계층 구조를 직접 조작할 수 있습니다. 우리는 GridView의 컨트롤 계층 구조를 마지막으로 페이지를 렌더링 하는 시점에 대 한 만들어졌음을 확신할 수 있습니다. 따라서이 방법은 재정의 `Page` s 클래스 `Render` 메서드, 이때 GridView s 최종 컨트롤 계층 구조는 필요한 구분 기호 행을 포함 하도록 업데이트 됩니다. 그림 4에서는이 프로세스를 보여 줍니다.


[![또 다른 방법은 조작 GridView의 컨트롤 계층 구조](creating-a-customized-sorting-user-interface-cs/_static/image9.png)](creating-a-customized-sorting-user-interface-cs/_static/image8.png)

**그림 4**: GridView의 컨트롤 계층 구조를 조작 하는 또 다른 방법은 ([전체 크기 이미지를 보려면 클릭](creating-a-customized-sorting-user-interface-cs/_static/image10.png))


이 자습서에서는이 방법을 통해 정렬 환경을 사용자 지정을 사용 합니다.

> [!NOTE]
> 코드 I에 제공 된 예제 기반 m이이 자습서에서는 제시 [Teemu Keiski](http://aspadvice.com/blogs/joteke/default.aspx) s 블로그 항목- [GridView 정렬 그룹화와 다소 재생할](http://aspadvice.com/blogs/joteke/archive/2006/02/11/15130.aspx)합니다.


## <a name="step-3-adding-the-separator-rows-to-the-gridview-s-control-hierarchy"></a>GridView의 컨트롤 계층 구조에 구분 기호 행을 추가 하는 3 단계:

이 추가 끝에서 페이지 수명 주기의 하지만 실제 GridView c 하기 전에 수행 하고자 하는 행을 추가 하는 구분 기호 GridView의 컨트롤 계층 구조에 해당 컨트롤 계층 구조를 만들고 해당 페이지 방문에 마지막으로 만든 후만 할 것 이므로 HTML로 렌더링 된 제어 계층 구조입니다. 최신 가능한는 것이 작업을 수행할 중요 한 점은 `Page` s 클래스 `Render` 이벤트에 다음 메서드 서명을 사용 하는 코드 숨김 클래스에서 재정의할 수 있습니다.


[!code-csharp[Main](creating-a-customized-sorting-user-interface-cs/samples/sample2.cs)]

경우는 `Page` s 원래 클래스 `Render` 메서드 `base.Render(writer)` 각 페이지에서 컨트롤의 렌더링 되는 태그를 기반으로 해당 제어 계층 구조를 생성 합니다. 따라서를 반드시 호출 두 명이 `base.Render(writer)`페이지가 렌더링 되도록 GridView s를 조작할 म 컨트롤 호출 하기 전에 계층 구조 `base.Render(writer)`전에 GridView의 컨트롤 계층 구조에 추가 된 구분 기호 행 되도록 s 된 렌더링 합니다.

정렬 그룹 헤더를 삽입 하려면 먼저 데이터를 정렬 하는 사용자가 요청을 확인 해야 합니다. 기본적으로 GridView의 내용을 정렬 되지 않습니다 및 헤더를 정렬 하는 모든 그룹을 입력 해야 하는 t 따라서 하지 않는 것입니다.

> [!NOTE]
> GridView 페이지 처음 로드 될 때 특정 열을 기준으로 정렬 하려면 GridView s 호출 `Sort` 메서드에 첫 번째 페이지 방문 (만 후속 포스트백). 이를 위해이 호출에서 추가 된 `Page_Load` 내에서 이벤트 처리기는 `if (!Page.IsPostBack)` 조건부 합니다. 다시 참조는 [페이징 및 보고서 데이터 정렬](paging-and-sorting-report-data-cs.md) 에 대 한 자세한 자습서 정보는 `Sort` 메서드.


데이터 정렬 된 경우 어떤 열을 확인 하 여 다음 작업은으로 데이터를 정렬 하 고 값을 해당 열 s의에서 차이 찾고 있는 행을 검색 합니다. 다음 코드 사용 하면 데이터 정렬 된 기준인 데이터 정렬 된 열을 찾습니다.


[!code-csharp[Main](creating-a-customized-sorting-user-interface-cs/samples/sample3.cs)]

GridView 아직 되도록 정렬, GridView의 `SortExpression` 속성이 설정 되지 것입니다. 따라서만 하고자이 속성에 값이 일부 경우 행을 구분 기호를 추가 합니다. 그렇지 않으면 다음 데이터 정렬 기준이 되는 열의 인덱스를 결정 해야 합니다. GridView s 순환 하 여 이렇게 `Columns` 컬렉션을 갖는 열에 대 한 검색 `SortExpression` 속성 GridView s 값은 `SortExpression` 속성입니다. 열의 인덱스 외에도에서는 또한 잡고는 `HeaderText` 구분 기호 행을 표시할 때 사용 되는 속성입니다.

데이터가 정렬 되는 열의 인덱스에 있는 마지막 단계는 GridView의 행을 열거입니다. 각 행에 대해 이전 행 정렬 s 열 s 값에서의 정렬 된 열의 값이 다른 지 여부를 결정 해야 합니다. 따라서 먼저 새 삽입 하려고 하는 경우 `GridViewRow` 컨트롤 계층 인스턴스. 이 작업은 다음 코드와 함께 수행 됩니다.


[!code-csharp[Main](creating-a-customized-sorting-user-interface-cs/samples/sample4.cs)]

프로그래밍 방식으로 참조 하 여이 코드가 시작 되는 `Table` GridView의 컨트롤 계층의 루트에 개체를 만드는 이라는 문자열 변수 `lastValue`합니다. `lastValue`현재 행 정렬 s 열 값의 이전 행의 값과 비교 하는 데 사용 됩니다. 다음, GridView s `Rows` 컬렉션이 열거 되 고 각 행에 대해 정렬 된 열의 값에 저장 됩니다는 `currentValue` 변수입니다.

> [!NOTE]
> S 셀을 사용 하려면 특정 행의 정렬 열 값을 결정 하려면 `Text` 속성입니다. 이 방법이 편리 BoundFields, 하지만 됩니다 하지 TemplateFields, CheckBoxFields 원하는 대로 작동 등에입니다. 곧 대체 GridView 필드에 대 한 고려 하는 방법을 살펴보겠습니다.


`currentValue` 및 `lastValue` 변수 그런 다음 비교 됩니다. 두 내용이 다르면 컨트롤 계층 구조에 새 구분 기호 행을 추가 해야 합니다. 인덱스를 확인 하 여 이렇게는 `GridViewRow` 에 `Table` 개체 s `Rows` 컬렉션을 새로 만드는 `GridViewRow` 및 `TableCell` 인스턴스, 그리고 다음 추가 `TableCell` 및 `GridViewRow` 에 컨트롤 계층 구조입니다.

구분 기호 s 유일한 행 있는지 참고 `TableCell` 은 GridView의 전체 너비를 확장 되도록 서식이 지정 사용 하 여 포맷 되는 `SortHeaderRowStyle` CSS 클래스 있으며 해당 `Text` 속성 등의 정렬 그룹 모두를 표시 이름 (예: 범주) 및 (예: 음료) 그룹의 값입니다. 마지막으로, `lastValue` 의 값으로 업데이트 됩니다 `currentValue`합니다.

정렬 그룹 머리글 행의 서식을 지정 하는 데 사용 되는 CSS 클래스 `SortHeaderRowStyle` 에 지정 되어야 하는 `Styles.css` 파일입니다. 모든 스타일 설정이 방법을 원하지; 사용 다음 사용 합니다.


[!code-css[Main](creating-a-customized-sorting-user-interface-cs/samples/sample5.css)]

현재 코드로 정렬 인터페이스 추가 정렬 그룹 머리글의 경우 모든 BoundField에서 정렬할 때 (공급 업체에서 정렬할 때 스크린샷을 보여 주는 그림 5 참조). 그러나 다른 모든 필드 형식 (예: CheckBoxField 또는 TemplateField)에서 정렬할 때 정렬 그룹 헤더에 (그림 6 참조)를 찾을 수는 있습니다.


[![BoundFields로 정렬할 때 정렬 그룹 머리글을 포함 하는 정렬 인터페이스](creating-a-customized-sorting-user-interface-cs/_static/image12.png)](creating-a-customized-sorting-user-interface-cs/_static/image11.png)

**그림 5**: The 정렬 인터페이스 포함 정렬 그룹 머리글 때 기준으로 정렬 BoundFields ([전체 크기 이미지를 보려면 클릭](creating-a-customized-sorting-user-interface-cs/_static/image13.png))


[![정렬 그룹 헤더는 누락 된 경우 정렬 된 CheckBoxField](creating-a-customized-sorting-user-interface-cs/_static/image15.png)](creating-a-customized-sorting-user-interface-cs/_static/image14.png)

**그림 6**: The 정렬 그룹 헤더는 누락 된 경우 정렬 된 CheckBoxField ([전체 크기 이미지를 보려면 클릭](creating-a-customized-sorting-user-interface-cs/_static/image16.png))


CheckBoxField에서 정렬할 때 정렬 그룹 머리글이 없는 이유는 코드가 현재만 사용 하므로 `TableCell` s `Text` 속성의 각 행에 대 한 정렬된 된 열 값을 결정 합니다. CheckBoxFields에 대 한는 `TableCell` s `Text` 속성은 빈 문자열에는 대신 값 내에 상주 하는 CheckBox 웹 컨트롤을 통해 사용할 수는 `TableCell` s `Controls` 컬렉션입니다.

BoundFields 이외의 필드 형식을 처리 하려면 코드를 추가 해야 여기서는 `currentValue` 에 있는 확인란의 존재 여부를 확인 하려면 변수가 할당 되는 `TableCell` s `Controls` 컬렉션입니다. 사용 하는 대신 `currentValue = gvr.Cells[sortColumnIndex].Text`,이 코드를 다음과 같이 바꿉니다.


[!code-csharp[Main](creating-a-customized-sorting-user-interface-cs/samples/sample6.cs)]

정렬된 된 열을 검사 하 여이 코드 `TableCell` 현재 행에서 모든 컨트롤 되는지 확인할 수는 `Controls` 컬렉션입니다. 파일이 있고 첫 번째 컨트롤은 CheckBox 하는 경우는 `currentValue` 예 또는 아니요, 확인란 s에 따라 변수가 설정 되어 `Checked` 속성입니다. 값을 가져옵니다,는 `TableCell` s `Text` 속성입니다. 이 논리는 GridView에 있을 수 있는 모든 TemplateFields에 대 한 정렬 처리를 복제할 수 있습니다.

위의 코드를 추가 정렬 그룹 머리글이 있는지 이제 지원 되지 않는 CheckBoxField에서 정렬할 때 (그림 7 참조).


[![정렬 그룹 머리글은 이제 존재 정렬은 CheckBoxField](creating-a-customized-sorting-user-interface-cs/_static/image18.png)](creating-a-customized-sorting-user-interface-cs/_static/image17.png)

**그림 7**: The 정렬 그룹 머리글은 이제 존재 정렬은 CheckBoxField ([전체 크기 이미지를 보려면 클릭](creating-a-customized-sorting-user-interface-cs/_static/image19.png))


> [!NOTE]
> 제품을 설정한 경우 `NULL` 값에 대 한 데이터베이스는 `CategoryID`, `SupplierID`, 또는 `UnitPrice` 필드, 해당 값으로 나타납니다 GridView에서 빈 문자열만 와해당제품에대한구분기호s행내부텍스트를의미합니다.기본적으로`NULL`범주와 같은 값을 읽이 됩니다: (즉, 없어 s 항목 뒤에 이름이 없는: 범주와 함께: 음료). 여기에 표시 된 값을 반환 하는 경우 설정할 수 있습니다는 BoundFields [ `NullDisplayText` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.boundfield.nulldisplaytext.aspx) 텍스트에 표시 하려는 하거나 할당할 때 조건문 Render 메서드에 추가할 수 있습니다는 `currentValue` 구분 기호를 행의 `Text` 속성입니다.


## <a name="summary"></a>요약

GridView 정렬 인터페이스 사용자 지정 하는 여러 기본 제공 옵션이 포함 되지 않습니다. 그러나 약간의 하위 수준 코드를 있는 것 s 추가 사용자 지정 된 인터페이스를 만드는 GridView의 컨트롤 계층 구조를 수정할 수 있습니다. 이 자습서에서는 보다 쉽게 고유한 그룹 및 해당 그룹의 경계를 식별 하는 정렬 가능한 GridView에 대 한 정렬 그룹 구분 기호 행을 추가 하는 방법에 살펴보았습니다. 사용자 지정 된 정렬 인터페이스의 추가 예에 대 한 체크 아웃 [Scott Guthrie](https://weblogs.asp.net/scottgu/) s [몇 가지 ASP.NET 2.0 GridView 정렬 팁과 요령](https://weblogs.asp.net/scottgu/archive/2006/02/11/437995.aspx) 블로그 항목입니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

>[!div class="step-by-step"]
[이전](sorting-custom-paged-data-cs.md)
[다음](paging-and-sorting-report-data-vb.md)
