---
uid: web-forms/overview/data-access/working-with-batched-data/batch-deleting-cs
title: "일괄 처리 삭제 (C#) | Microsoft Docs"
author: rick-anderson
description: "한 번에 여러 데이터베이스 레코드를 삭제 하는 방법을 알아봅니다. 사용자 인터페이스 계층에는 향상 된 GridView에서 만든 이전 tut 시 빌드..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/26/2007
ms.topic: article
ms.assetid: ac6916d0-a5ab-4218-9760-7ba9e72d258c
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-deleting-cs
msc.type: authoredcontent
ms.openlocfilehash: 71c4b323c2604d9e775f75272bb9565505580522
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="batch-deleting-c"></a><span data-ttu-id="5ce84-104">일괄 처리 삭제 (C#)</span><span class="sxs-lookup"><span data-stu-id="5ce84-104">Batch Deleting (C#)</span></span>
====================
<span data-ttu-id="5ce84-105">으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="5ce84-105">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="5ce84-106">[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_65_CS.zip) 또는 [PDF 다운로드](batch-deleting-cs/_static/datatutorial65cs1.pdf)</span><span class="sxs-lookup"><span data-stu-id="5ce84-106">[Download Code](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_65_CS.zip) or [Download PDF](batch-deleting-cs/_static/datatutorial65cs1.pdf)</span></span>

> <span data-ttu-id="5ce84-107">한 번에 여러 데이터베이스 레코드를 삭제 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-107">Learn how to delete multiple database records in a single operation.</span></span> <span data-ttu-id="5ce84-108">사용자 인터페이스 계층에서 이전 자습서에서 만든는 향상 된 GridView에 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-108">In the User Interface Layer we build upon an enhanced GridView created in an earlier tutorial.</span></span> <span data-ttu-id="5ce84-109">데이터 액세스 계층으로 모든 삭제 성공 하거나 모든 삭제 롤백되는 트랜잭션 내에서 여러 삭제 작업을 래핑할 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-109">In the Data Access Layer we wrap the multiple Delete operations within a transaction to ensure that all deletions succeed or all deletions are rolled back.</span></span>


## <a name="introduction"></a><span data-ttu-id="5ce84-110">소개</span><span class="sxs-lookup"><span data-stu-id="5ce84-110">Introduction</span></span>

<span data-ttu-id="5ce84-111">[이전 자습서](batch-updating-cs.md) 편집 인터페이스는 완벽 하 게 편집할 GridView를 사용 하 여 일괄 처리를 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-111">The [preceding tutorial](batch-updating-cs.md) explored how to create a batch editing interface using a fully-editable GridView.</span></span> <span data-ttu-id="5ce84-112">여기서 사용자가 일반적으로 편집 하는 여러 레코드가 한 번에 경우에 편집 인터페이스는 일괄 처리 및가 필요 훨씬 적은 포스트백 키보드와 마우스-컨텍스트 스위치, 최종 사용자의 효율성을 향상 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-112">In situations where users are commonly editing many records at once, a batch editing interface will require far fewer postbacks and keyboard-to-mouse context switches, thereby improving the end user s efficiency.</span></span> <span data-ttu-id="5ce84-113">이 기술은 한꺼번에 많은 레코드를 삭제 하는 사용자에 대 한 일반적인 경우 페이지에 대 한 마찬가지로 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-113">This technique is similarly useful for pages where it is common for users to delete many records in one go.</span></span>

<span data-ttu-id="5ce84-114">가 온라인 메일 클라이언트를 사용 하는 사람은 이미 익숙한가 인터페이스를 삭제 하는 가장 일반적인 일괄 처리 중 하나:는 해당 모든 선택 항목 삭제 된 눈금의 각 행에 확인란 단추 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="5ce84-114">Anyone who has used an online email client is already familiar with one of the most common batch deleting interfaces: a checkbox in each row in a grid with a corresponding Delete All Checked Items button (see Figure 1).</span></span> <span data-ttu-id="5ce84-115">이 자습서는 보다 짧은 때문에에서는 모든 웹 기반 인터페이스와 단일 원자 단위 연산으로 일련의 레코드를 삭제 하는 메서드를 만드는 이전 자습서에서 복잡 한 작업을 이미 수행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-115">This tutorial is rather short because we ve already done all of the hard work in previous tutorials in creating both the web-based interface and a method to delete a series of records as a single atomic operation.</span></span> <span data-ttu-id="5ce84-116">에 [확인란 GridView 열 추가](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs.md) 확인란의 및에서 열이 있는 GridView 만든 자습서는 [트랜잭션 내에서 데이터베이스 수정 내용을 래핑](wrapping-database-modifications-within-a-transaction-cs.md) 자습서에서 메서드를 만들었습니다 트랜잭션을 삭제를 사용 하 여 BLL는 `List<T>` 의 `ProductID` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-116">In the [Adding a GridView Column of Checkboxes](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs.md) tutorial we created a GridView with a column of checkboxes and in the [Wrapping Database Modifications within a Transaction](wrapping-database-modifications-within-a-transaction-cs.md) tutorial we created a method in the BLL that would use a transaction to delete a `List<T>` of `ProductID` values.</span></span> <span data-ttu-id="5ce84-117">이 자습서를 기반으로 작성 하 고 예제 삭제 작업 일괄 처리를 만들려는 이전 경험을 병합 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-117">In this tutorial, we will build upon and merge our previous experiences to create a working batch deleting example.</span></span>


<span data-ttu-id="5ce84-118">[![각 행에 Checkbox 포함 됩니다.](batch-deleting-cs/_static/image1.gif)](batch-deleting-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5ce84-118">[![Each Row Includes a Checkbox](batch-deleting-cs/_static/image1.gif)](batch-deleting-cs/_static/image1.png)</span></span>

<span data-ttu-id="5ce84-119">**그림 1**: 각 행에 확인란이 포함 됩니다 ([전체 크기 이미지를 보려면 클릭](batch-deleting-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="5ce84-119">**Figure 1**: Each Row Includes a Checkbox ([Click to view full-size image](batch-deleting-cs/_static/image2.png))</span></span>


## <a name="step-1-creating-the-batch-deleting-interface"></a><span data-ttu-id="5ce84-120">1 단계: 인터페이스 삭제 일괄 처리 만들기</span><span class="sxs-lookup"><span data-stu-id="5ce84-120">Step 1: Creating the Batch Deleting Interface</span></span>

<span data-ttu-id="5ce84-121">인터페이스에 삭제 일괄 처리를 이미 만들었습니다 있으므로 [확인란 GridView 열 추가](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs.md) 자습서에서는 복사 하기만 하면 되 게 `BatchDelete.aspx` 처음부터 새로 만드는 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-121">Since we already created the batch deleting interface in the [Adding a GridView Column of Checkboxes](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs.md) tutorial, we can simply copy it to `BatchDelete.aspx` rather than creating it from scratch.</span></span> <span data-ttu-id="5ce84-122">열어 시작는 `BatchDelete.aspx` 페이지에 `BatchData` 폴더 및 `CheckBoxField.aspx` 페이지에 `EnhancedGridView` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-122">Start by opening the `BatchDelete.aspx` page in the `BatchData` folder and the `CheckBoxField.aspx` page in the `EnhancedGridView` folder.</span></span> <span data-ttu-id="5ce84-123">`CheckBoxField.aspx` 페이지 소스 보기로 이동 하 고 태그 사이의 복사는 `<asp:Content>` 그림 2에 나와 있는 것 처럼 태그를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-123">From the `CheckBoxField.aspx` page, go to the Source view and copy the markup between the `<asp:Content>` tags as shown in Figure 2.</span></span>


<span data-ttu-id="5ce84-124">[![CheckBoxField.aspx의 선언적 태그를 클립보드에 복사 합니다.](batch-deleting-cs/_static/image2.gif)](batch-deleting-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="5ce84-124">[![Copy the Declarative Markup of CheckBoxField.aspx to the Clipboard](batch-deleting-cs/_static/image2.gif)](batch-deleting-cs/_static/image3.png)</span></span>

<span data-ttu-id="5ce84-125">**그림 2**:의 선언 태그 복사 `CheckBoxField.aspx` 클립보드로 ([전체 크기 이미지를 보려면 클릭](batch-deleting-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="5ce84-125">**Figure 2**: Copy the Declarative Markup of `CheckBoxField.aspx` to the Clipboard ([Click to view full-size image](batch-deleting-cs/_static/image4.png))</span></span>


<span data-ttu-id="5ce84-126">다음에 보기로 이동 하 여 원본에서 `BatchDelete.aspx` 내에서 클립보드의 내용을 붙여넣습니다는 `<asp:Content>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-126">Next, go to the Source view in `BatchDelete.aspx` and paste the contents of the clipboard within the `<asp:Content>` tags.</span></span> <span data-ttu-id="5ce84-127">복사 하에서 코드 숨김 클래스 내에서 코드 `CheckBoxField.aspx.cs` 를 코드 숨김 클래스 내에서 `BatchDelete.aspx.cs` (의 `DeleteSelectedProducts` 단추 s `Click` 이벤트 처리기는 `ToggleCheckState` 메서드, 및 `Click` 이벤트 처리기 에 대 한는 `CheckAll` 및 `UncheckAll` 단추).</span><span class="sxs-lookup"><span data-stu-id="5ce84-127">Also copy and paste the code from within the code-behind class in `CheckBoxField.aspx.cs` to within the code-behind class in `BatchDelete.aspx.cs` (the `DeleteSelectedProducts` Button s `Click` event handler, the `ToggleCheckState` method, and the `Click` event handlers for the `CheckAll` and `UncheckAll` Buttons).</span></span> <span data-ttu-id="5ce84-128">이 콘텐츠를 통해 복사한 후의 `BatchDelete.aspx`의 페이지 코드 숨김 클래스는 다음 코드를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-128">After copying over this content, the `BatchDelete.aspx` page s code-behind class should contain the following code:</span></span>


[!code-csharp[Main](batch-deleting-cs/samples/sample1.cs)]

<span data-ttu-id="5ce84-129">선언적 태그 및 소스 코드를 복사한 후 보십시오 테스트 `BatchDelete.aspx` 브라우저를 통해 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-129">After copying over the declarative markup and source code, take a moment to test `BatchDelete.aspx` by viewing it through a browser.</span></span> <span data-ttu-id="5ce84-130">각 행은 s 제품 이름, 범주 및 가격 checkbox 함께 나열 하는 GridView에 처음 10 개 제품을 나열 하는 GridView 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-130">You should see a GridView listing the first ten products in a GridView with each row listing the product s name, category, and price along with a checkbox.</span></span> <span data-ttu-id="5ce84-131">세 개의 단추가 있어야: 모든 확인, 모두 선택 취소 및 선택한 제품 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-131">There should be three buttons: Check All, Uncheck All, and Delete Selected Products.</span></span> <span data-ttu-id="5ce84-132">모든 확인 단추를 클릭 하면 모든 확인란을 지웁니다 모두 선택 취소 하는 동안 모든 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-132">Clicking the Check All button selects all checkboxes, while Uncheck All clears all checkboxes.</span></span> <span data-ttu-id="5ce84-133">선택 된 제품 삭제를 클릭 하면 나열 하는 메시지가 표시 됩니다.는 `ProductID` 값 선택 된 제품의 제품을 실제로 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-133">Clicking Delete Selected Products displays a message that lists the `ProductID` values of the selected products, but does not actually delete the products.</span></span>


<span data-ttu-id="5ce84-134">[![인터페이스를 CheckBoxField.aspx BatchDeleting.aspx로 이동 되었습니다.](batch-deleting-cs/_static/image3.gif)](batch-deleting-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="5ce84-134">[![The Interface from CheckBoxField.aspx has been Moved to BatchDeleting.aspx](batch-deleting-cs/_static/image3.gif)](batch-deleting-cs/_static/image5.png)</span></span>

<span data-ttu-id="5ce84-135">**그림 3**:에서 인터페이스 `CheckBoxField.aspx` 로 이동 되었습니다 `BatchDeleting.aspx` ([전체 크기 이미지를 보려면 클릭](batch-deleting-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="5ce84-135">**Figure 3**: The Interface from `CheckBoxField.aspx` has been Moved to `BatchDeleting.aspx` ([Click to view full-size image](batch-deleting-cs/_static/image6.png))</span></span>


## <a name="step-2-deleting-the-checked-products-using-transactions"></a><span data-ttu-id="5ce84-136">2 단계: 트랜잭션을 사용 하 여 선택 된 제품 삭제</span><span class="sxs-lookup"><span data-stu-id="5ce84-136">Step 2: Deleting the Checked Products Using Transactions</span></span>

<span data-ttu-id="5ce84-137">인터페이스를 통해 성공적으로 복사 삭제 일괄 처리와 `BatchDeleting.aspx`, 선택한 제품 삭제 단추를 사용 하 여 선택 된 제품을 삭제 하는 코드를 업데이트 하려면 남았습니다는 모두는 `DeleteProductsWithTransaction` 에서 메서드는 `ProductsBLL` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-137">With the batch deleting interface successfully copied over to `BatchDeleting.aspx`, all that remains is to update the code so that the Delete Selected Products button deletes the checked products using the `DeleteProductsWithTransaction` method in the `ProductsBLL` class.</span></span> <span data-ttu-id="5ce84-138">에 추가 된이 메서드는 [트랜잭션 내에서 데이터베이스 수정 내용을 래핑](wrapping-database-modifications-within-a-transaction-cs.md) 자습서에서는 입력으로 수락는 `List<T>` 의 `ProductID` 값 및 각 해당 삭제 `ProductID` 범위 내에서 트랜잭션입니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-138">This method, added in the [Wrapping Database Modifications within a Transaction](wrapping-database-modifications-within-a-transaction-cs.md) tutorial, accepts as its input a `List<T>` of `ProductID` values and deletes each corresponding `ProductID` within the scope of a transaction.</span></span>

<span data-ttu-id="5ce84-139">`DeleteSelectedProducts` 단추 s `Click` 이벤트 처리기는 다음에 현재 사용 하 여 `foreach` 각 GridView 행에서 반복 하는 루프:</span><span class="sxs-lookup"><span data-stu-id="5ce84-139">The `DeleteSelectedProducts` Button s `Click` event handler currently uses the following `foreach` loop to iterate through each GridView row:</span></span>


[!code-csharp[Main](batch-deleting-cs/samples/sample2.cs)]

<span data-ttu-id="5ce84-140">각 행에 대해는 `ProductSelector` CheckBox 웹 컨트롤은 프로그래밍 방식으로 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-140">For each row, the `ProductSelector` CheckBox Web control is programmatically referenced.</span></span> <span data-ttu-id="5ce84-141">이 옵션을 선택 하는 경우 s 행 `ProductID` 에서 검색 되는 `DataKeys` 컬렉션 및 `DeleteResults` 레이블의 `Text` 속성 행 삭제 하도록 선택 된 나타내는 메시지를 포함 하도록 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-141">If it is checked, the row s `ProductID` is retrieved from the `DataKeys` collection and the `DeleteResults` Label s `Text` property is updated to include a message indicating that the row was selected for deletion.</span></span>

<span data-ttu-id="5ce84-142">위의 코드는 모든 레코드에 대 한 호출으로 실제로 삭제 되지 않습니다는 `ProductsBLL` s 클래스 `Delete` 메서드 주석으로 처리 됩니다. 이 삭제 논리를 적용할 인 코드는 제품도 삭제 하지만 원자성 작업 내에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-142">The above code does not actually delete any records as the call to the `ProductsBLL` class s `Delete` method is commented out. Were this delete logic to be applied, the code would delete the products but not within an atomic operation.</span></span> <span data-ttu-id="5ce84-143">즉, 시퀀스에서 첫 번째 몇 삭제 했지만, 최신 실패 (으로 인해 foreign key 제약 조건 위반),이 예외가 throw 됩니다 있지만 이러한 제품이 이미 삭제은 삭제 된 상태로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-143">That is, if the first few deletes in the sequence succeeded, but a later one failed (perhaps due to a foreign key constraint violation), an exception would be thrown but those products already deleted would remain deleted.</span></span>

<span data-ttu-id="5ce84-144">원자성을 보장 하려면 대신 사용 하 여 해야는 `ProductsBLL` s 클래스 `DeleteProductsWithTransaction` 메서드.</span><span class="sxs-lookup"><span data-stu-id="5ce84-144">In order to assure atomicity, we need to instead use the `ProductsBLL` class s `DeleteProductsWithTransaction` method.</span></span> <span data-ttu-id="5ce84-145">이 방법의 목록을 허용 하기 때문에 `ProductID` 값, 해야 먼저 그리드에서이 목록을 컴파일하고 매개 변수로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-145">Because this method accepts a list of `ProductID` values, we need to first compile this list from the grid and then pass it as a parameter.</span></span> <span data-ttu-id="5ce84-146">인스턴스를 처음 만들면는 `List<T>` 형식의 `int`합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-146">We first create an instance of a `List<T>` of type `int`.</span></span> <span data-ttu-id="5ce84-147">내에서 `foreach` 선택 된 제품을 추가 해야 하는 루프 `ProductID` 값이 `List<T>`합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-147">Within the `foreach` loop we need to add the selected products `ProductID` values to this `List<T>`.</span></span> <span data-ttu-id="5ce84-148">루프 후이 `List<T>` 에 전달 되어야 합니다는 `ProductsBLL` s 클래스 `DeleteProductsWithTransaction` 메서드.</span><span class="sxs-lookup"><span data-stu-id="5ce84-148">After the loop this `List<T>` must be passed to the `ProductsBLL` class s `DeleteProductsWithTransaction` method.</span></span> <span data-ttu-id="5ce84-149">업데이트는 `DeleteSelectedProducts` 단추의 `Click` 이벤트 처리기를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="5ce84-149">Update the `DeleteSelectedProducts` Button s `Click` event handler with the following code:</span></span>


[!code-csharp[Main](batch-deleting-cs/samples/sample3.cs)]

<span data-ttu-id="5ce84-150">업데이트 된 코드를 만듭니다는 `List<T>` 형식의 `int` (`productIDsToDelete`) 사용 하 여 정보를 표시 하 고는 `ProductID` 값을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-150">The updated code creates a `List<T>` of type `int` (`productIDsToDelete`) and populates it with the `ProductID` values to delete.</span></span> <span data-ttu-id="5ce84-151">후의 `foreach` 하나 이상의 제품을 선택 하는 경우 루프는 `ProductsBLL` s 클래스 `DeleteProductsWithTransaction` 메서드가 호출 되 고이 목록에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-151">After the `foreach` loop, if there is at least one product selected, the `ProductsBLL` class s `DeleteProductsWithTransaction` method is called and passed this list.</span></span> <span data-ttu-id="5ce84-152">`DeleteResults` (새로 삭제할 레코드가 더 이상 표시 되도록 표에서 행으로) 데이터가 GridView에 리바운드 및 레이블도 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-152">The `DeleteResults` Label is also displayed and the data rebound to the GridView (so that the newly-deleted records no longer appear as rows in the grid).</span></span>

<span data-ttu-id="5ce84-153">그림 4에서는 삭제에 대 한 행의 수를 선택한 후 GridView를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-153">Figure 4 shows the GridView after a number of rows have been selected for deletion.</span></span> <span data-ttu-id="5ce84-154">그림 5는 선택한 제품 삭제 단추를 클릭 한 후에 즉시는 화면을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-154">Figure 5 shows the screen immediately after the Delete Selected Products button has been clicked.</span></span> <span data-ttu-id="5ce84-155">그림 5에서는 `ProductID` GridView 아래에 있는 레이블에 표시 되는 삭제 된 레코드의 값이 고 해당 행 GridView에서 더 이상이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-155">Note that in Figure 5 the `ProductID` values of the deleted records are displayed in the Label beneath the GridView and those rows are no longer in the GridView.</span></span>


<span data-ttu-id="5ce84-156">[![선택 된 제품 삭제](batch-deleting-cs/_static/image4.gif)](batch-deleting-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="5ce84-156">[![The Selected Products Will Be Deleted](batch-deleting-cs/_static/image4.gif)](batch-deleting-cs/_static/image7.png)</span></span>

<span data-ttu-id="5ce84-157">**그림 4**:은 선택한 제품 삭제 됩니다 ([전체 크기 이미지를 보려면 클릭](batch-deleting-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="5ce84-157">**Figure 4**: The Selected Products Will Be Deleted ([Click to view full-size image](batch-deleting-cs/_static/image8.png))</span></span>


<span data-ttu-id="5ce84-158">[![제품 ProductID 삭제 값은 GridView 아래에 나열 된](batch-deleting-cs/_static/image5.gif)](batch-deleting-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="5ce84-158">[![The Deleted Products ProductID Values are Listed Beneath the GridView](batch-deleting-cs/_static/image5.gif)](batch-deleting-cs/_static/image9.png)</span></span>

<span data-ttu-id="5ce84-159">**그림 5**: The 삭제 제품 `ProductID` 값은 GridView 아래에 나열 된 ([전체 크기 이미지를 보려면 클릭](batch-deleting-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="5ce84-159">**Figure 5**: The Deleted Products `ProductID` Values are Listed Beneath the GridView ([Click to view full-size image](batch-deleting-cs/_static/image10.png))</span></span>


> [!NOTE]
> <span data-ttu-id="5ce84-160">테스트 하는 `DeleteProductsWithTransaction` 메서드의 원자성의 제품에 대 한 항목을 수동으로 추가 `Order Details` 테이블 및 기타) (함께 해당 제품을 삭제 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-160">To test the `DeleteProductsWithTransaction` method s atomicity, manually add an entry for a product in the `Order Details` table and then attempt to delete that product (along with others).</span></span> <span data-ttu-id="5ce84-161">관련된 된 주문 인 제품을 삭제 하려면 어떻게 다른 선택 된 제품 삭제 롤백되는 동안 foreign key 제약 조건 위반을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-161">You will receive a foreign key constraint violation when attempting to delete the product with an associated order, but note how the other selected products deletions are rolled back.</span></span>


## <a name="summary"></a><span data-ttu-id="5ce84-162">요약</span><span class="sxs-lookup"><span data-stu-id="5ce84-162">Summary</span></span>

<span data-ttu-id="5ce84-163">확인란의 열이 있는 GridView를 추가 하는 것 인터페이스 삭제 일괄 처리를 만들지 및 Button 웹 컨트롤을 클릭 하면 선택 된 행의 모든 단일 원자 단위 작업으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-163">Creating a batch deleting interface involves adding a GridView with a column of checkboxes and a Button Web control that, when clicked, will delete all of the selected rows as a single atomic operation.</span></span> <span data-ttu-id="5ce84-164">이러한 인터페이스 정보를 결합 두 이전 자습서에서 작업을 수행 하 여 빌드된에서는이 자습서에서는 [확인란 GridView 열 추가](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs.md) 및 [트랜잭션 내에서 데이터베이스 수정 내용을 래핑](wrapping-database-modifications-within-a-transaction-cs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-164">In this tutorial we built such an interface by piecing together work done in two previous tutorials, [Adding a GridView Column of Checkboxes](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs.md) and [Wrapping Database Modifications within a Transaction](wrapping-database-modifications-within-a-transaction-cs.md).</span></span> <span data-ttu-id="5ce84-165">첫 번째 자습서에서 확인란의 열이 있는 GridView 만든 및 BLL에 메서드를 구현한 후자의 전달 될 때는 `List<T>` 의 `ProductID` 값을 트랜잭션의 범위 내에서 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-165">In the first tutorial we created a GridView with a column of checkboxes and in the latter we implemented a method in the BLL that, when passed a `List<T>` of `ProductID` values, deleted them all within the scope of a transaction.</span></span>

<span data-ttu-id="5ce84-166">다음 자습서에서 일괄 처리 삽입을 수행 하기 위한 인터페이스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-166">In the next tutorial we'll create an interface for performing batch inserts.</span></span>

<span data-ttu-id="5ce84-167">만족도 매우 프로그래밍!</span><span class="sxs-lookup"><span data-stu-id="5ce84-167">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="5ce84-168">작성자 정보</span><span class="sxs-lookup"><span data-stu-id="5ce84-168">About the Author</span></span>

<span data-ttu-id="5ce84-169">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-169">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="5ce84-170">Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-170">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="5ce84-171">그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-171">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="5ce84-172">에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-172">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

## <a name="special-thanks-to"></a><span data-ttu-id="5ce84-173">특별히 감사</span><span class="sxs-lookup"><span data-stu-id="5ce84-173">Special Thanks To</span></span>

<span data-ttu-id="5ce84-174">이 자습서 시리즈 많은 유용한 검토자가 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-174">This tutorial series was reviewed by many helpful reviewers.</span></span> <span data-ttu-id="5ce84-175">이 자습서에 대 한 선행 검토자 Hilton Giesenow 및 Teresa 머피의 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5ce84-175">Lead reviewers for this tutorial were Hilton Giesenow and Teresa Murphy.</span></span> <span data-ttu-id="5ce84-176">향후 내 MSDN 문서를 검토에 관심이 있으십니까?</span><span class="sxs-lookup"><span data-stu-id="5ce84-176">Interested in reviewing my upcoming MSDN articles?</span></span> <span data-ttu-id="5ce84-177">이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="5ce84-177">If so, drop me a line at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="5ce84-178">[이전](batch-updating-cs.md)
[다음](batch-inserting-cs.md)</span><span class="sxs-lookup"><span data-stu-id="5ce84-178">[Previous](batch-updating-cs.md)
[Next](batch-inserting-cs.md)</span></span>