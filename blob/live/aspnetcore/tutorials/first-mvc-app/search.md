---
title: "검색 추가"
author: rick-anderson
description: "간단한 ASP.NET Core MVC 앱에 검색을 추가하는 방법을 보여 줍니다."
keywords: ASP.NET Core,
ms.author: riande
manager: wpickett
ms.date: 03/07/2017
ms.topic: get-started-article
ms.assetid: d69e5529-8ef6-4628-855d-200206d962b9
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/first-mvc-app/search
ms.openlocfilehash: f811cd0063404872b0e993a99e8a92cc354064ce
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
[!INCLUDE[adding-model](../../includes/mvc-intro/search1.md)]

<span data-ttu-id="3b9f9-104">**rename** 명령을 사용하여 `searchString` 매개 변수의 이름을 `id`로 신속하게 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b9f9-104">You can quickly rename the `searchString` parameter to `id` with the **rename** command.</span></span> <span data-ttu-id="3b9f9-105">`searchString` **> Rename**을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b9f9-105">Right click on `searchString` **> Rename**.</span></span>

![바로 가기 메뉴](search/_static/rename.png)

<span data-ttu-id="3b9f9-107">이름 바꾸기 대상이 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b9f9-107">The rename targets are highlighted.</span></span>

![인덱스 ActionResult 메서드 전체에서 강조 표시된 변수를 보여 주는 코드 편집기](search/_static/rename2.png)

<span data-ttu-id="3b9f9-109">매개 변수를 `id`로, `searchString`의 모든 항목을 `id`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3b9f9-109">Change the parameter to `id` and all occurrences of `searchString` change to `id`.</span></span>

![변수를 보여 주는 코드 편집기는 id로 변경되었습니다.](search/_static/rename3.png)

[!INCLUDE[adding-model](../../includes/mvc-intro/search2.md)]

<span data-ttu-id="3b9f9-111">intelliSense에서 변경 내용 업데이트를 돕는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3b9f9-111">Notice how intelliSense helps us update the markup.</span></span>

![양식 요소에 대해 특성 목록에서 선택한 메서드가 있는 Intellisense 바로 가기 메뉴](search/_static/int_m.png)

![메서드 특성 목록에서 선택한 값이 있는 Intellisense 바로 가기 메뉴](search/_static/int_get.png)

<span data-ttu-id="3b9f9-114">`<form>` 태그에서 눈에 띄는 글꼴을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3b9f9-114">Notice the distinctive font in the `<form>` tag.</span></span> <span data-ttu-id="3b9f9-115">눈에 띄는 해당 글꼴은 [태그 도우미](../../mvc/views/tag-helpers/intro.md)에서 지원되는 태그를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3b9f9-115">That distinctive font indicates the tag is supported by [Tag Helpers](../../mvc/views/tag-helpers/intro.md).</span></span>

![자주색 텍스트가 있는 양식 태그](search/_static/th_font.png)

[!INCLUDE[adding-model](../../includes/mvc-intro/search3.md)]

>[!div class="step-by-step"]
<span data-ttu-id="3b9f9-117">[이전](controller-methods-views.md)
[다음](new-field.md)</span><span class="sxs-lookup"><span data-stu-id="3b9f9-117">[Previous](controller-methods-views.md)
[Next](new-field.md)</span></span>  