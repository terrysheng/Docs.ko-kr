---
title: "Entity Framework Core-8 자습서 1 사용 하 여 razor 페이지"
author: rick-anderson
description: "Entity Framework Core를 사용 하 여 Razor 페이지 앱을 만드는 방법을 보여 줍니다."
keywords: "ASP.NET Core, Entity Framework Core 자습서"
ms.author: riande
manager: wpickett
ms.date: 11/15/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: data/ef-rp/intro
ms.openlocfilehash: d3bcf9aaf7fa809825a0ba8631ee52d3860b090d
ms.sourcegitcommit: 05e798c9bac7b9e9983599afb227ef393905d023
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="getting-started-with-razor-pages-and-entity-framework-core-using-visual-studio-1-of-8"></a><span data-ttu-id="de949-104">Razor 페이지 및 Visual Studio (1 / 8)를 사용 하 여 Entity Framework Core 시작</span><span class="sxs-lookup"><span data-stu-id="de949-104">Getting started with Razor Pages and Entity Framework Core using Visual Studio (1 of 8)</span></span>

<span data-ttu-id="de949-105">여 [Tom Dykstra](https://github.com/tdykstra) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="de949-105">By [Tom Dykstra](https://github.com/tdykstra) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="de949-106">Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework (EF) 코어 2.0 및 Visual Studio 2017을 사용 하 여 ASP.NET 코어 2.0 MVC 웹 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="de949-106">The Contoso University sample web app demonstrates how to create ASP.NET Core 2.0 MVC web applications using Entity Framework (EF) Core 2.0 and Visual Studio 2017.</span></span>

<span data-ttu-id="de949-107">샘플 응용 프로그램은 웹 사이트 가상 Contoso 대학입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-107">The sample app is a web site for a fictional Contoso University.</span></span> <span data-ttu-id="de949-108">학생 진입, 과정 만들기 및 강사 할당 등의 기능을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-108">It includes functionality such as student admission, course creation, and instructor assignments.</span></span> <span data-ttu-id="de949-109">이 페이지는 일련의 Contoso 대학 샘플 응용 프로그램을 빌드하는 방법을 설명 하는 자습서의 첫 번째 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de949-109">This page is the first in a series of tutorials that explain how to build the Contoso University sample app.</span></span>

[<span data-ttu-id="de949-110">완성 된 앱을 보거나 다운로드.</span><span class="sxs-lookup"><span data-stu-id="de949-110">Download or view the completed app.</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples) <span data-ttu-id="de949-111">[다운로드 지침](xref:tutorials/index#how-to-download-a-sample)합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-111">[Download instructions](xref:tutorials/index#how-to-download-a-sample).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de949-112">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="de949-112">Prerequisites</span></span>

[!INCLUDE[install 2.0](../../includes/install2.0.md)]

## <a name="troubleshooting"></a><span data-ttu-id="de949-113">문제 해결</span><span class="sxs-lookup"><span data-stu-id="de949-113">Troubleshooting</span></span>

<span data-ttu-id="de949-114">솔루션에 코드를 비교 하 여 일반적으로 찾을 수 문제를 해결할 수 없는 실행 하는 경우는 [단계 완료](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots) 또는 [완료 된 프로젝트](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu-final)합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-114">If you run into a problem you can't resolve, you can generally find the solution by comparing your code to the [completed stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots) or [completed project](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu-final).</span></span> <span data-ttu-id="de949-115">일반적인 오류 및 해결 방법을 목록은 참조 하십시오. [계열의 마지막 자습서의 문제 해결 섹션](xref:data/ef-mvc/advanced#common-errors)합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-115">For a list of common errors and how to solve them, see [the Troubleshooting section of the last tutorial in the series](xref:data/ef-mvc/advanced#common-errors).</span></span> <span data-ttu-id="de949-116">에 대 한 StackOverflow.com에 질문을 게시할 수 필요한 있습니다을 찾지 못한 경우 [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) 또는 [EF 코어](https://stackoverflow.com/questions/tagged/entity-framework-core)합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-116">If you don't find what you need there, you can post a question to StackOverflow.com for [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) or [EF Core](https://stackoverflow.com/questions/tagged/entity-framework-core).</span></span>

> [!TIP]
> <span data-ttu-id="de949-117">이 일련의 자습서 이전 자습서에서 수행 되는 동작과 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-117">This series of tutorials builds on what is done in earlier tutorials.</span></span> <span data-ttu-id="de949-118">각 자습서 완료 후 프로젝트의 복사본을 저장 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="de949-118">Consider saving a copy of the project after each successful tutorial completion.</span></span> <span data-ttu-id="de949-119">문제를 실행 하는 경우 시작 부분으로 다시 이동 하지 않고도 이전 자습서에서를 통해 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de949-119">If you run into problems, you can start over from the previous tutorial instead of going back to the beginning.</span></span> <span data-ttu-id="de949-120">다운로드할 수 있습니다는 [단계 완료](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots) 고 완료 된 단계를 사용 하 여 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-120">Alternatively, you can download a [completed stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots) and start over using the completed stage.</span></span>

## <a name="the-contoso-university-web-app"></a><span data-ttu-id="de949-121">Contoso 대학 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="de949-121">The Contoso University web app</span></span>

<span data-ttu-id="de949-122">이 자습서에 빌드한 앱에는 기본 대학 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-122">The app built in these tutorials is a basic university web site.</span></span>

<span data-ttu-id="de949-123">사용자가 볼 수 있으며 학생과에서는 강사 정보 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-123">Users can view and update student, course, and instructor information.</span></span> <span data-ttu-id="de949-124">자습서에서 만든 화면 중 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-124">Here are a few of the screens created in the tutorial.</span></span>

![학생 인덱스 페이지](intro/_static/students-index.png)

![학생 편집 페이지](intro/_static/student-edit.png)

<span data-ttu-id="de949-127">이 사이트의 사용자 인터페이스 스타일에는 기본 제공 템플릿에서 생성 내용을 가깝습니다.</span><span class="sxs-lookup"><span data-stu-id="de949-127">The UI style of this site is close to what's generated by the built-in templates.</span></span> <span data-ttu-id="de949-128">Razor 페이지 되지 않는 UI EF 코어 자습서 위주로 설명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-128">The tutorial focus is on EF Core with Razor Pages, not the UI.</span></span>

## <a name="create-a-razor-pages-web-app"></a><span data-ttu-id="de949-129">Razor 페이지 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="de949-129">Create a Razor Pages web app</span></span>

* <span data-ttu-id="de949-130">Visual Studio **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-130">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="de949-131">새 ASP.NET Core 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="de949-131">Create a new ASP.NET Core Web Application.</span></span> <span data-ttu-id="de949-132">프로젝트 이름을 **ContosoUniversity**합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-132">Name the project **ContosoUniversity**.</span></span> <span data-ttu-id="de949-133">프로젝트 이름을 해야 *ContosoUniversity* 되므로 코드를 복사/붙여 넣을 때 네임 스페이스와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-133">It's important to name the project *ContosoUniversity* so the namespaces match when code is copy/pasted.</span></span>
 <span data-ttu-id="de949-134">![새 ASP.NET Core 웹 응용 프로그램](intro/_static/np.png)</span><span class="sxs-lookup"><span data-stu-id="de949-134">![new ASP.NET Core Web Application](intro/_static/np.png)</span></span>
* <span data-ttu-id="de949-135">드롭다운에서 **ASP.NET Core 2.0**을 선택하고 **웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-135">Select **ASP.NET Core 2.0** in the dropdown, and then select **Web Application**.</span></span>
 <span data-ttu-id="de949-136">![웹 응용 프로그램(Razor 페이지)](../../mvc/razor-pages/index/_static/np2.png)</span><span class="sxs-lookup"><span data-stu-id="de949-136">![Web Application (Razor Pages)](../../mvc/razor-pages/index/_static/np2.png)</span></span>

<span data-ttu-id="de949-137">**F5** 키를 눌러 디버그 모드에서 앱을 실행하거나 **Ctrl-F5**를 눌러 디버거를 연결하지 않고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-137">Press **F5** to run the app in debug mode or **Ctrl-F5** to run without attaching the debugger</span></span>

## <a name="set-up-the-site-style"></a><span data-ttu-id="de949-138">사이트 스타일 설정</span><span class="sxs-lookup"><span data-stu-id="de949-138">Set up the site style</span></span>

<span data-ttu-id="de949-139">몇 가지 변경을 사이트 메뉴, 레이아웃 및 홈 페이지를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-139">A few changes set up the site menu, layout, and home page.</span></span>

<span data-ttu-id="de949-140">열기 *Pages/_Layout.cshtml* 다음과 같이 변경 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de949-140">Open *Pages/_Layout.cshtml* and make the following changes:</span></span>

* <span data-ttu-id="de949-141">"ContosoUniversity"의 "Contoso 대학."으로 변경</span><span class="sxs-lookup"><span data-stu-id="de949-141">Change each occurrence of "ContosoUniversity" to "Contoso University."</span></span> <span data-ttu-id="de949-142">다음과 같은 세 가지 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="de949-142">There are three occurrences.</span></span>

* <span data-ttu-id="de949-143">메뉴 항목에 대 한 추가 **학생**, **Courses**, **강사**, 및 **부서**, 및 삭제는 **연락처** 메뉴 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-143">Add menu entries for **Students**, **Courses**, **Instructors**, and **Departments**, and delete the **Contact** menu entry.</span></span>

<span data-ttu-id="de949-144">변경 내용은 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-144">The changes are highlighted.</span></span>

[!code-html[](intro/samples/cu/Pages/_Layout.cshtml?highlight=6,29,35-39,47&range=1-50)]

<span data-ttu-id="de949-145">*Views/Home/Index.cshtml*, 파일의 내용을 텍스트를 바꿀 ASP.NET MVC에 대 한이 앱에 대 한 텍스트를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="de949-145">In *Views/Home/Index.cshtml*, replace the contents of the file with the following code to replace the text about ASP.NET and MVC with text about this app:</span></span>

[!code-html[](intro/samples/cu/Pages/Index.cshtml)]

<span data-ttu-id="de949-146">Ctrl+F5를 눌러 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-146">Press CTRL+F5 to run the project.</span></span> <span data-ttu-id="de949-147">홈 페이지는 다음 자습서에서 만든 탭으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-147">The home page is displayed with tabs created in the following tutorials:</span></span>

![Contoso 대학 홈 페이지](intro/_static/home-page.png)

## <a name="create-the-data-model"></a><span data-ttu-id="de949-149">데이터 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="de949-149">Create the data model</span></span>

<span data-ttu-id="de949-150">Contoso 대학 앱에 대 한 엔터티 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="de949-150">Create entity classes for the Contoso University app.</span></span> <span data-ttu-id="de949-151">다음 세 가지 엔터티로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-151">Start with the following three entities:</span></span>

![학생-등록 과정-데이터 모델 다이어그램](intro/_static/data-model-diagram.png)

<span data-ttu-id="de949-153">간의 일 대 다 관계가 `Student` 및 `Enrollment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="de949-153">There's a one-to-many relationship between `Student` and `Enrollment` entities.</span></span> <span data-ttu-id="de949-154">간의 일 대 다 관계가 `Course` 및 `Enrollment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="de949-154">There's a one-to-many relationship between `Course` and `Enrollment` entities.</span></span> <span data-ttu-id="de949-155">학생 원하는 수의 과목에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de949-155">A student can enroll in any number of courses.</span></span> <span data-ttu-id="de949-156">과정을 학생에 등록 된 개수에 관계 없이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de949-156">A course can have any number of students enrolled in it.</span></span>

<span data-ttu-id="de949-157">다음 섹션에서 각각에 대 한 이러한 엔터티는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="de949-157">In the following sections, a class for each one of these entities is created.</span></span>

### <a name="the-student-entity"></a><span data-ttu-id="de949-158">학생 엔터티</span><span class="sxs-lookup"><span data-stu-id="de949-158">The Student entity</span></span>

![학생 엔터티 다이어그램](intro/_static/student-entity.png)

<span data-ttu-id="de949-160">만들기는 *모델* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-160">Create a *Models* folder.</span></span> <span data-ttu-id="de949-161">에 *모델* 폴더 라는 클래스 파일을 만들어 *Student.cs* 를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="de949-161">In the *Models* folder, create a class file named *Student.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_Intro)]

<span data-ttu-id="de949-162">`ID` 속성은이 클래스에 해당 하는 데이터베이스 (DB) 테이블의 기본 키 열입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-162">The `ID` property becomes the primary key column of the database (DB) table that corresponds to this class.</span></span> <span data-ttu-id="de949-163">EF 코어를 기본적으로 명명 된 속성을 해석 `ID` 또는 `classnameID` 기본 키로 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-163">By default, EF Core interprets a property that's named `ID` or `classnameID` as the primary key.</span></span>

<span data-ttu-id="de949-164">`Enrollments` 속성은 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-164">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="de949-165">이 엔터티와 관련 된 다른 엔터티에 대 한 탐색 속성 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-165">Navigation properties link to other entities that are related to this entity.</span></span> <span data-ttu-id="de949-166">이 경우에 `Enrollments` 속성은 `Student entity` 모두 보유는 `Enrollment` 엔터티는 관련 된 `Student`합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-166">In this case, the `Enrollments` property of a `Student entity` holds all of the `Enrollment` entities that are related to that `Student`.</span></span> <span data-ttu-id="de949-167">예를 들어 경우 DB에 학생 행에 두 개의 관련 등록 행의 `Enrollments` 탐색 속성 포함 그 두 `Enrollment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="de949-167">For example, if a Student row in the DB has two related Enrollment rows, the `Enrollments` navigation property contains those two `Enrollment` entities.</span></span> <span data-ttu-id="de949-168">관련 `Enrollment` 행은 행의 해당 학생의 기본 키 값을 포함 하는 `StudentID` 열입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-168">A related `Enrollment` row is a row that contains that student's primary key value in the `StudentID` column.</span></span> <span data-ttu-id="de949-169">예를 들어 ID와 학생 = 1 두 개의 행에는 `Enrollment` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-169">For example, suppose the student with ID=1 has two rows in the `Enrollment` table.</span></span> <span data-ttu-id="de949-170">`Enrollment` 테이블에 두 개의 행이 `StudentID` = 1입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-170">The `Enrollment` table has two rows with `StudentID` = 1.</span></span> <span data-ttu-id="de949-171">`StudentID`외래 키에 `Enrollment` 테이블에서 학생을 지정 하는 `Student` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-171">`StudentID` is a foreign key in the `Enrollment` table that specifies the student in the `Student` table.</span></span>

<span data-ttu-id="de949-172">탐색 속성 같은 목록 유형 이어야 합니다는 탐색 속성에는 여러 엔터티 보유할 수, 하는 경우 `ICollection<T>`합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-172">If a navigation property can hold multiple entities, the navigation property must be a list type, such as `ICollection<T>`.</span></span> <span data-ttu-id="de949-173">`ICollection<T>`지정할 수 있습니다 또는 형식으로 `List<T>` 또는 `HashSet<T>`합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-173">`ICollection<T>` can be specified, or a type such as `List<T>` or `HashSet<T>`.</span></span> <span data-ttu-id="de949-174">때 `ICollection<T>` 는 사용 하는 EF 코어 만듭니다는 `HashSet<T>` 기본적으로 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-174">When `ICollection<T>` is used, EF Core creates a `HashSet<T>` collection by default.</span></span> <span data-ttu-id="de949-175">여러 엔터티를 포함 하는 탐색 속성은 다 대 다 및 1 대 다 관계에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-175">Navigation properties that hold multiple entities come from many-to-many and one-to-many relationships.</span></span>

### <a name="the-enrollment-entity"></a><span data-ttu-id="de949-176">등록 엔터티</span><span class="sxs-lookup"><span data-stu-id="de949-176">The Enrollment entity</span></span>

![등록 엔터티 다이어그램](intro/_static/enrollment-entity.png)

<span data-ttu-id="de949-178">에 *모델* 폴더를 만들 *Enrollment.cs* 를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="de949-178">In the *Models* folder, create *Enrollment.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Enrollment.cs?name=snippet_Intro)]

<span data-ttu-id="de949-179">`EnrollmentID` 속성은 기본 키입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-179">The `EnrollmentID` property is the primary key.</span></span> <span data-ttu-id="de949-180">사용 하 여이 엔터티는 `classnameID` 대신 패턴 `ID` 같은 `Student` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="de949-180">This entity uses the `classnameID` pattern instead of `ID` like the `Student` entity.</span></span> <span data-ttu-id="de949-181">일반적으로 개발자는 패턴 중 하나를 선택 하 고 데이터 모델 전체에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-181">Typically developers choose one pattern and use it throughout the data model.</span></span> <span data-ttu-id="de949-182">자습서의 뒷부분에서 ID를 사용 하 여 응용 프로그램 이름 없이 데이터 모델에서 상속을 구현 하는 쉽게 수행할 수 있도록 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-182">In a later tutorial, using ID without classname is shown to make it easier to implement inheritance in the data model.</span></span>

<span data-ttu-id="de949-183">`Grade` 속성은 한 `enum`합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-183">The `Grade` property is an `enum`.</span></span> <span data-ttu-id="de949-184">다음 매개 변수는 `Grade` 형식 선언을 나타냅니다는 `Grade` 속성은 null을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-184">The question mark after the `Grade` type declaration indicates that the `Grade` property is nullable.</span></span> <span data-ttu-id="de949-185">Null이 등급은 0 개 등급 다릅니다-null 의미는 등급 알려진 또는 아직 할당 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="de949-185">A grade that's null is different from a zero grade -- null means a grade isn't known or hasn't been assigned yet.</span></span>

<span data-ttu-id="de949-186">`StudentID` 속성은 외래 키 및 해당 탐색 속성은 `Student`합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-186">The `StudentID` property is a foreign key, and the corresponding navigation property is `Student`.</span></span> <span data-ttu-id="de949-187">`Enrollment` 엔터티는 하 나와 연결 `Student` 속성 하나를 포함 하므로 엔터티 `Student` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="de949-187">An `Enrollment` entity is associated with one `Student` entity, so the property contains a single `Student` entity.</span></span> <span data-ttu-id="de949-188">`Student` 에서 다른 엔터티는 `Student.Enrollments` 여러 포함 된 탐색 속성을 `Enrollment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="de949-188">The `Student` entity differs from the `Student.Enrollments` navigation property, which contains multiple `Enrollment` entities.</span></span>

<span data-ttu-id="de949-189">`CourseID` 속성은 외래 키 및 해당 탐색 속성은 `Course`합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-189">The `CourseID` property is a foreign key, and the corresponding navigation property is `Course`.</span></span> <span data-ttu-id="de949-190">`Enrollment` 엔터티는 하 나와 연결 `Course` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="de949-190">An `Enrollment` entity is associated with one `Course` entity.</span></span>

<span data-ttu-id="de949-191">EF 코어 라고 하는 경우 외래 키로 속성을 해석 `<navigation property name><primary key property name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-191">EF Core interprets a property as a foreign key if it's named `<navigation property name><primary key property name>`.</span></span> <span data-ttu-id="de949-192">예를 들어`StudentID` 에 대 한는 `Student` 탐색 속성이 있으므로 `Student` 엔터티의 기본 키가 `ID`합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-192">For example,`StudentID` for the `Student` navigation property, since the `Student` entity's primary key is `ID`.</span></span> <span data-ttu-id="de949-193">외래 키 속성 이름을 지정할 수 `<primary key property name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-193">Foreign key properties can also be named `<primary key property name>`.</span></span> <span data-ttu-id="de949-194">예를 들어 `CourseID` 이후는 `Course` 엔터티의 기본 키가 `CourseID`합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-194">For example, `CourseID` since the `Course` entity's primary key is `CourseID`.</span></span>

### <a name="the-course-entity"></a><span data-ttu-id="de949-195">과정 엔터티</span><span class="sxs-lookup"><span data-stu-id="de949-195">The Course entity</span></span>

![과정 엔터티 다이어그램](intro/_static/course-entity.png)

<span data-ttu-id="de949-197">에 *모델* 폴더를 만들 *Course.cs* 를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="de949-197">In the *Models* folder, create *Course.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Course.cs?name=snippet_Intro)]

<span data-ttu-id="de949-198">`Enrollments` 속성은 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-198">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="de949-199">A `Course` 개수에 관계 없이 관련 될 수 있는 엔터티 `Enrollment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="de949-199">A `Course` entity can be related to any number of `Enrollment` entities.</span></span>

<span data-ttu-id="de949-200">`DatabaseGenerated` 생성 DB 필요 하지 않고 특성을 사용 하면 응용 프로그램에서 기본 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-200">The `DatabaseGenerated` attribute allows the app to specify the primary key rather than having the DB generate it.</span></span>

## <a name="create-the-schoolcontext-db-context"></a><span data-ttu-id="de949-201">SchoolContext DB 컨텍스트 만들기</span><span class="sxs-lookup"><span data-stu-id="de949-201">Create the SchoolContext DB context</span></span>

<span data-ttu-id="de949-202">지정된 된 데이터 모델에 대 한 EF 핵심 기능을 조정 하는 주 클래스는 DB 컨텍스트 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-202">The main class that coordinates EF Core functionality for a given data model is the DB context class.</span></span> <span data-ttu-id="de949-203">파생 되는 데이터 컨텍스트 `Microsoft.EntityFrameworkCore.DbContext`합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-203">The data context is derived from `Microsoft.EntityFrameworkCore.DbContext`.</span></span> <span data-ttu-id="de949-204">엔터티 데이터 모델에 포함 된 데이터 컨텍스트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-204">The data context specifies which entities are included in the data model.</span></span> <span data-ttu-id="de949-205">이 프로젝트에 클래스 이름은 `SchoolContext`합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-205">In this project, the class is named `SchoolContext`.</span></span>

<span data-ttu-id="de949-206">프로젝트 폴더에 라는 폴더를 만듭니다 *데이터*합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-206">In the project folder, create a folder named *Data*.</span></span>

<span data-ttu-id="de949-207">에 *데이터* 폴더 만들기 *SchoolContext.cs* 를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="de949-207">In the *Data* folder create *SchoolContext.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_Intro)]

<span data-ttu-id="de949-208">이 코드에서는 `DbSet` 각 엔터티 집합에 대 한 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-208">This code creates a `DbSet` property for each entity set.</span></span> <span data-ttu-id="de949-209">EF 핵심 용어:</span><span class="sxs-lookup"><span data-stu-id="de949-209">In EF Core terminology:</span></span>

* <span data-ttu-id="de949-210">엔터티 집합을 일반적으로 DB 테이블에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-210">An entity set typically corresponds to a DB table.</span></span>
* <span data-ttu-id="de949-211">엔터티는 테이블의 행에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-211">An entity corresponds to a row in the table.</span></span>

<span data-ttu-id="de949-212">`DbSet<Enrollment>`및 `DbSet<Course>` 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de949-212">`DbSet<Enrollment>` and `DbSet<Course>` can be omitted.</span></span> <span data-ttu-id="de949-213">EF 코어 포함 암시적으로 하기 때문에 `Student` 엔터티 참조는 `Enrollment` 엔터티 및 `Enrollment` 엔터티 참조는 `Course` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="de949-213">EF Core includes them implicitly because the `Student` entity references the `Enrollment` entity, and the `Enrollment` entity references the `Course` entity.</span></span> <span data-ttu-id="de949-214">이 자습서에는 유지 `DbSet<Enrollment>` 및 `DbSet<Course>` 에 `SchoolContext`합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-214">For this tutorial, keep `DbSet<Enrollment>` and `DbSet<Course>` in the `SchoolContext`.</span></span>

<span data-ttu-id="de949-215">DB 만들어지면 EF 코어와 동일한 이름을 갖는 테이블을 만듭니다는 `DbSet` 속성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-215">When the DB is created, EF Core creates tables that have names the same as the `DbSet` property names.</span></span> <span data-ttu-id="de949-216">컬렉션에 대 한 속성 이름에는 일반적으로 복수 (학생 아님 학생).</span><span class="sxs-lookup"><span data-stu-id="de949-216">Property names for collections are typically plural (Students rather than Student).</span></span> <span data-ttu-id="de949-217">개발자가 테이블 이름이 복수형 여야 하는지 여부에 대 한 동의.</span><span class="sxs-lookup"><span data-stu-id="de949-217">Developers disagree about whether table names should be plural.</span></span> <span data-ttu-id="de949-218">이 자습서에 대 한 DbContext 단 수 테이블 이름을 지정 하 여 기본 동작 재정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-218">For these tutorials, the default behavior is overridden by specifying singular table names in the DbContext.</span></span> <span data-ttu-id="de949-219">를 단일 테이블 이름을 지정 하려면 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-219">To specify singular table names, add the following highlighted code:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_TableNames&highlight=16-21)]

## <a name="register-the-context-with-dependency-injection"></a><span data-ttu-id="de949-220">종속성 주입 컨텍스트 등록</span><span class="sxs-lookup"><span data-stu-id="de949-220">Register the context with dependency injection</span></span>

<span data-ttu-id="de949-221">ASP.NET Core 포함 [종속성 주입](xref:fundamentals/dependency-injection)합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-221">ASP.NET Core includes [dependency injection](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="de949-222">서비스 (예: EF 코어 DB 컨텍스트) 종속성 주입 응용 프로그램 시작 중에 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-222">Services (such as the EF Core DB context) are registered with dependency injection during application startup.</span></span> <span data-ttu-id="de949-223">이러한 서비스 (예: Razor 페이지)에 필요한 구성 요소를 생성자 매개 변수를 통해 이러한 서비스 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-223">Components that require these services (such as Razor Pages) are provided these services via constructor parameters.</span></span> <span data-ttu-id="de949-224">Db 컨텍스트 인스턴스를 가져오는 생성자 코드는이 자습서의 뒷부분에 나오는 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-224">The constructor code that gets a db context instance is shown later in the tutorial.</span></span>

<span data-ttu-id="de949-225">등록 하려면 `SchoolContext` 서비스를 열고 *Startup.cs*, 강조 표시 된 줄을 추가 하 고는 `ConfigureServices` 메서드.</span><span class="sxs-lookup"><span data-stu-id="de949-225">To register `SchoolContext` as a service, open *Startup.cs*, and add the highlighted lines to the `ConfigureServices` method.</span></span>

[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_SchoolContext&highlight=3-4)]

<span data-ttu-id="de949-226">연결 문자열의 이름에는 메서드를 호출 하 여 컨텍스트에 전달 됩니다는 `DbContextOptionsBuilder` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-226">The name of the connection string is passed in to the context by calling a method on a `DbContextOptionsBuilder` object.</span></span> <span data-ttu-id="de949-227">로컬 개발에 대 한는 [ASP.NET Core 구성 시스템](xref:fundamentals/configuration/index) 는 연결 문자열에서 *appsettings.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-227">For local development, the [ASP.NET Core configuration system](xref:fundamentals/configuration/index) reads the connection string from the *appsettings.json* file.</span></span>

<span data-ttu-id="de949-228">추가 `using` 에 대 한 문을 `ContosoUniversity.Data` 및 `Microsoft.EntityFrameworkCore` 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-228">Add `using` statements for `ContosoUniversity.Data` and `Microsoft.EntityFrameworkCore` namespaces.</span></span> <span data-ttu-id="de949-229">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-229">Build the project.</span></span>

[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_Usings)]

<span data-ttu-id="de949-230">열기는 *appsettings.json* 파일을 다음 코드에 표시 된 대로 연결 문자열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-230">Open the *appsettings.json* file and add a connection string as shown in the following code:</span></span>

[!code-json[](./intro/samples/cu/appsettings1.json?highlight=2-4)]

<span data-ttu-id="de949-231">위의 연결 문자열에 사용 하 여 `ConnectRetryCount=0` 방지 하기 위해 [SQLClient](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/sqlclient-for-the-entity-framework) 내어쓰기에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-231">The preceding connection string uses `ConnectRetryCount=0` to prevent [SQLClient](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/sqlclient-for-the-entity-framework) from hanging.</span></span>

### <a name="sql-server-express-localdb"></a><span data-ttu-id="de949-232">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="de949-232">SQL Server Express LocalDB</span></span>

<span data-ttu-id="de949-233">연결 문자열에는 SQL Server LocalDB DB 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-233">The connection string specifies a SQL Server LocalDB DB.</span></span> <span data-ttu-id="de949-234">LocalDB는 SQL Server Express 데이터베이스 엔진의 경량 버전 하며 응용 프로그램 개발의 경우 프로덕션 환경에서 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="de949-234">LocalDB is a lightweight version of the SQL Server Express Database Engine and is intended for app development, not production use.</span></span> <span data-ttu-id="de949-235">LocalDB는 요청 시 시작하고 사용자 모드에서 실행되므로 복잡한 구성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="de949-235">LocalDB starts on demand and runs in user mode, so there is no complex configuration.</span></span> <span data-ttu-id="de949-236">기본적으로 LocalDB 만듭니다 *.mdf* DB 파일에 `C:/Users/<user>` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-236">By default, LocalDB creates *.mdf* DB files in the `C:/Users/<user>` directory.</span></span>

## <a name="add-code-to-initialize-the-db-with-test-data"></a><span data-ttu-id="de949-237">테스트 데이터로 DB 초기화 코드를 추가</span><span class="sxs-lookup"><span data-stu-id="de949-237">Add code to initialize the DB with test data</span></span>

<span data-ttu-id="de949-238">EF 코어 빈 DB를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="de949-238">EF Core creates an empty DB.</span></span> <span data-ttu-id="de949-239">이 섹션에서는 *시드* 테스트 데이터로 채울 메서드가 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-239">In this section, a *Seed* method is written to populate it with test data.</span></span>

<span data-ttu-id="de949-240">에 *데이터* 폴더 라는 새 클래스 파일을 만들 *DbInitializer.cs* 다음 코드를 추가 하 고:</span><span class="sxs-lookup"><span data-stu-id="de949-240">In the *Data* folder, create a new class file named *DbInitializer.cs* and add the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/DbInitializer.cs?name=snippet_Intro)]

<span data-ttu-id="de949-241">DB에 어떤 학생 되어 있는지 확인 하는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-241">The code checks if there are any students in the DB.</span></span> <span data-ttu-id="de949-242">DB에 없는 학생 인 DB 테스트 데이터로 마련 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-242">If there are no students in the DB, the DB is seeded with test data.</span></span> <span data-ttu-id="de949-243">배열에 테스트 데이터를 로드 하지 않고 `List<T>` 성능을 최적화 하는 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-243">It loads test data into arrays rather than `List<T>` collections to optimize performance.</span></span>

<span data-ttu-id="de949-244">`EnsureCreated` 메서드는 자동으로 DB DB 컨텍스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="de949-244">The `EnsureCreated` method automatically creates the DB for the DB context.</span></span> <span data-ttu-id="de949-245">DB 있으면 `EnsureCreated` DB 수정 하지 않고 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-245">If the DB exists, `EnsureCreated` returns without modifying the DB.</span></span>

<span data-ttu-id="de949-246">*Program.cs*, 수정 된 `Main` 다음을 수행 하는 메서드:</span><span class="sxs-lookup"><span data-stu-id="de949-246">In *Program.cs*, modify the `Main` method to do the following:</span></span>

* <span data-ttu-id="de949-247">종속성 주입 컨테이너에서 DB 컨텍스트 인스턴스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="de949-247">Get a DB context instance from the dependency injection container.</span></span>
* <span data-ttu-id="de949-248">컨텍스트를 전달 하는 초기값 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-248">Call the seed method, passing to it the context.</span></span>
* <span data-ttu-id="de949-249">시드 메서드가 완료 되는 컨텍스트를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-249">Dispose the context when the seed method completes.</span></span>

<span data-ttu-id="de949-250">다음 코드에서는 업데이트 된 *Program.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-250">The following code shows the updated *Program.cs* file.</span></span>

[!code-csharp[Main](intro/samples/cu/ProgramOriginal.cs?name=snippet)]

<span data-ttu-id="de949-251">처음으로 앱이 실행 되는 DB 작성 되 고 시드 테스트 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-251">The first time the app is run, the DB is created and seeded with test data.</span></span> <span data-ttu-id="de949-252">데이터 모델 업데이트 될 때를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="de949-252">When the data model is updated:</span></span>
* <span data-ttu-id="de949-253">DB를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-253">Delete the DB.</span></span>
* <span data-ttu-id="de949-254">Seed 메서드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-254">Update the seed method.</span></span>
* <span data-ttu-id="de949-255">응용 프로그램을 실행 하 고 새 시드 DB 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="de949-255">Run the app and a new seeded DB is created.</span></span> 

<span data-ttu-id="de949-256">이후의 자습서에서는 데이터 모델이 변경, 삭제 및 DB를 다시 작성 하지 않고 DB 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-256">In later tutorials, the DB is updated when the data model changes, without deleting and re-creating the DB.</span></span>

<a name="pmc"></a>
## <a name="add-scaffold-tooling"></a><span data-ttu-id="de949-257">스 캐 폴드 도구 추가</span><span class="sxs-lookup"><span data-stu-id="de949-257">Add scaffold tooling</span></span>

<span data-ttu-id="de949-258">이 섹션에서는 패키지 관리자 콘솔 (PMC)는 Visual Studio 웹 코드 생성 패키지를 추가 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-258">In this section, the Package Manager Console (PMC) is used to add the Visual Studio web code generation package.</span></span> <span data-ttu-id="de949-259">스캐폴딩 엔진을 실행하려면 이 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-259">This package is required to run the scaffolding engine.</span></span>

<span data-ttu-id="de949-260">**도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-260">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="de949-261">패키지 관리자 콘솔 (PMC)에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-261">In the Package Manager Console (PMC), enter the following commands:</span></span>

```powershell
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Design
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Utils
```

<span data-ttu-id="de949-262">위 명령은 *.csproj 파일을 NuGet 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-262">The previous command adds the NuGet packages to the *.csproj file:</span></span>

[!code-csharp[Main](intro/samples/cu/ContosoUniversity1_csproj.txt?highlight=7-8)]

<a name="scaffold"></a>
## <a name="scaffold-the-model"></a><span data-ttu-id="de949-263">스 캐 폴드 모델</span><span class="sxs-lookup"><span data-stu-id="de949-263">Scaffold the model</span></span>

* <span data-ttu-id="de949-264">프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)에서 명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="de949-264">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="de949-265">다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-265">Run the following commands:</span></span>


 ```console
dotnet restore
dotnet aspnet-codegenerator razorpage -m Student -dc SchoolContext -udl -outDir Pages\Students --referenceScriptLibraries
 ```
 
<span data-ttu-id="de949-266">경우 다음과 같은 오류가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-266">If the following error is generated:</span></span>

```text
Unhandled Exception: System.IO.FileNotFoundException: 
Could not load file or assembly 
'Microsoft.VisualStudio.Web.CodeGeneration.Utils, 
Version=2.0.0.0, Culture=neutral, PublicKeyToken=adb9793829ddae60'.
The system cannot find the file specified.
```

<span data-ttu-id="de949-267">명령을 다시 실행 하 고 페이지 아래쪽에 의견을 남겨 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-267">Run the command again and leave a comment at the bottom of the page.</span></span>

<span data-ttu-id="de949-268">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-268">Build the project.</span></span> <span data-ttu-id="de949-269">빌드에서는 다음과 같은 오류를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-269">The build generates errors like the following:</span></span>

 `1>Pages\Students\Index.cshtml.cs(26,38,26,45): error CS1061: 'SchoolContext' does not contain a definition for 'Student'`

 <span data-ttu-id="de949-270">전역으로 변경 `_context.Student` 를 `_context.Students` (즉, "s"에 추가 `Student`).</span><span class="sxs-lookup"><span data-stu-id="de949-270">Globally change `_context.Student` to `_context.Students` (that is, add an "s" to `Student`).</span></span> <span data-ttu-id="de949-271">7 번 발견 되 고 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-271">7 occurrences are found and updated.</span></span> <span data-ttu-id="de949-272">수정 하기 위해 노력 [이 버그](https://github.com/aspnet/Scaffolding/issues/633) 다음 릴리스에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-272">We hope to fix [this bug](https://github.com/aspnet/Scaffolding/issues/633) in the next release.</span></span>

[!INCLUDE[model4tbl](../../includes/RP/model4tbl.md)]

 <a name="test"></a>
### <a name="test-the-app"></a><span data-ttu-id="de949-273">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="de949-273">Test the app</span></span>

<span data-ttu-id="de949-274">응용 프로그램을 실행 하 고 선택 된 **학생** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-274">Run the app and select the **Students** link.</span></span> <span data-ttu-id="de949-275">브라우저 너비에 따라는 **학생** 링크 페이지의 맨 위에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="de949-275">Depending on the browser width, the **Students** link appears at the top of the page.</span></span> <span data-ttu-id="de949-276">경우는 **학생** 링크가 표시 되지 않는, 오른쪽 위 모서리에서 탐색 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-276">If the **Students** link is not visible, click the navigation icon in the upper right corner.</span></span>

![좁은 Contoso 대학 홈 페이지](intro/_static/home-page-narrow.png)

<span data-ttu-id="de949-278">테스트는 **만들기**, **편집**, 및 **세부 정보** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-278">Test the **Create**, **Edit**, and **Details** links.</span></span>

## <a name="view-the-db"></a><span data-ttu-id="de949-279">DB 보기</span><span class="sxs-lookup"><span data-stu-id="de949-279">View the DB</span></span>

<span data-ttu-id="de949-280">앱이 시작 되 면 `DbInitializer.Initialize` 호출 `EnsureCreated`합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-280">When the app is started, `DbInitializer.Initialize` calls `EnsureCreated`.</span></span> <span data-ttu-id="de949-281">`EnsureCreated`감지 하 여 DB 존재 하 고, 필요한 경우 하나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="de949-281">`EnsureCreated` detects if the DB exists, and creates one if necessary.</span></span> <span data-ttu-id="de949-282">에 있는 경우 없습니다 학생 DB는 `Initialize` 메서드 학생을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-282">If there are no Students in the DB, the `Initialize` method adds students.</span></span>

<span data-ttu-id="de949-283">열기 **SQL Server 개체 탐색기** (SSOX)에서 고 **보기** Visual Studio에서 메뉴.</span><span class="sxs-lookup"><span data-stu-id="de949-283">Open **SQL Server Object Explorer** (SSOX) from the **View** menu in Visual Studio.</span></span>
<span data-ttu-id="de949-284">SSOX, 클릭 **(localdb) \MSSQLLocalDB > 데이터베이스 > ContosoUniversity1**합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-284">In SSOX, click **(localdb)\MSSQLLocalDB > Databases > ContosoUniversity1**.</span></span>

<span data-ttu-id="de949-285">확장 된 **테이블** 노드.</span><span class="sxs-lookup"><span data-stu-id="de949-285">Expand the **Tables** node.</span></span>

<span data-ttu-id="de949-286">마우스 오른쪽 단추로 클릭는 **학생** 테이블 마우스 클릭 **데이터 보기** 만든 열 및 테이블에 삽입 된 행을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de949-286">Right-click the **Student** table and click **View Data** to see the columns created and the rows inserted into the table.</span></span>

<span data-ttu-id="de949-287">*.mdf* 및 *.ldf* DB 파일에 있는 *C:\Users\<yourusername >* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-287">The *.mdf* and *.ldf* DB files are in the *C:\Users\<yourusername>* folder.</span></span>

<span data-ttu-id="de949-288">`EnsureCreated`다음 작업 흐름을 허용 하는 응용 프로그램 시작에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-288">`EnsureCreated` is called on app start, which allows the following work flow:</span></span>

* <span data-ttu-id="de949-289">DB를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-289">Delete the DB.</span></span>
* <span data-ttu-id="de949-290">DB 스키마를 변경 (예: 추가 `EmailAddress` 필드).</span><span class="sxs-lookup"><span data-stu-id="de949-290">Change the DB schema (for example, add an `EmailAddress` field).</span></span>
* <span data-ttu-id="de949-291">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-291">Run the app.</span></span>

<span data-ttu-id="de949-292">`EnsureCreated`DB가 만듭니다는`EmailAddress` 열입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-292">`EnsureCreated` creates a DB with the`EmailAddress` column.</span></span>

## <a name="conventions"></a><span data-ttu-id="de949-293">규칙</span><span class="sxs-lookup"><span data-stu-id="de949-293">Conventions</span></span>

<span data-ttu-id="de949-294">규칙 또는 EF 코어에 수행 하는 가정을 사용 되기 때문에 전체 DB를 만들려면 EF 코어를 위해 작성 된 코드의 양을 최소화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-294">The amount of code written in order for EF Core to create a complete DB is minimal because of the use of conventions, or assumptions that EF Core makes.</span></span>

* <span data-ttu-id="de949-295">이름을 `DbSet` 속성 테이블 이름으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-295">The names of `DbSet` properties are used as table names.</span></span> <span data-ttu-id="de949-296">엔터티에 의해 참조 되지 않는 한 `DbSet` 속성, 엔터티 클래스 이름이 테이블 이름으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-296">For entities not referenced by a `DbSet` property, entity class names are used as table names.</span></span>

* <span data-ttu-id="de949-297">엔터티 속성 이름은 열 이름에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-297">Entity property names are used for column names.</span></span>

* <span data-ttu-id="de949-298">ID 또는 classnameID 명명 된 엔터티 속성은 기본 키 속성으로 인식 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-298">Entity properties that are named ID or classnameID are recognized as primary key properties.</span></span>

* <span data-ttu-id="de949-299">라고 하는 경우 외래 키 속성으로는 속성을 해석  *<navigation property name> <primary key property name>*  (예를 들어 `StudentID` 에 대 한는 `Student` 이후 탐색 속성은 `Student` 엔터티의 기본 키가 `ID`).</span><span class="sxs-lookup"><span data-stu-id="de949-299">A property is interpreted as a foreign key property if it's named *<navigation property name><primary key property name>* (for example, `StudentID` for the `Student` navigation property since the `Student` entity's primary key is `ID`).</span></span> <span data-ttu-id="de949-300">외래 키 속성 이름을 지정할 수  *<primary key property name>*  (예를 들어 `EnrollmentID` 이후는 `Enrollment` 엔터티의 기본 키가 `EnrollmentID`).</span><span class="sxs-lookup"><span data-stu-id="de949-300">Foreign key properties can be named *<primary key property name>* (for example, `EnrollmentID` since the `Enrollment` entity's primary key is `EnrollmentID`).</span></span>

<span data-ttu-id="de949-301">기본 동작을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de949-301">Conventional behavior can be overridden.</span></span> <span data-ttu-id="de949-302">예를 들어 테이블 이름은 지정할 수 있습니다 명시적으로,이 자습서의 앞부분에 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-302">For example, the table names can be explicitly specified, as shown earlier in this tutorial.</span></span> <span data-ttu-id="de949-303">열 이름은 명시적으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de949-303">The column names can be explicitly set.</span></span> <span data-ttu-id="de949-304">기본 키와 외래 키 명시적으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de949-304">Primary keys and foreign keys can be explicitly set.</span></span>

## <a name="asynchronous-code"></a><span data-ttu-id="de949-305">비동기 코드</span><span class="sxs-lookup"><span data-stu-id="de949-305">Asynchronous code</span></span>

<span data-ttu-id="de949-306">비동기 프로그래밍은 ASP.NET 코어 및 EF 코어에 대 한 기본 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-306">Asynchronous programming is the default mode for ASP.NET Core and EF Core.</span></span>

<span data-ttu-id="de949-307">웹 서버를 사용할 수 있는 스레드 수가 제한에 및 로드 양이 많으면 상황에서 모든 사용 가능한 스레드 수 사용.</span><span class="sxs-lookup"><span data-stu-id="de949-307">A web server has a limited number of threads available, and in high load situations all of the available threads might be in use.</span></span> <span data-ttu-id="de949-308">이 경우 서버를 스레드가 해제 될 때까지 새 요청을 처리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="de949-308">When that happens, the server can't process new requests until the threads are freed up.</span></span> <span data-ttu-id="de949-309">I/O가 완료를 대기 하 고 있으므로 작업을 실제로 수행 되지 않습니다은 동안 많은 스레드가 동기 코드와 함께 하느라 정체 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de949-309">With synchronous code, many threads may be tied up while they aren't actually doing any work because they're waiting for I/O to complete.</span></span> <span data-ttu-id="de949-310">비동기 코드로 i/o가 완료를 대기 하는 프로세스 스레드에서 다른 요청을 처리에 사용할 서버에 대해 해제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-310">With asynchronous code, when a process is waiting for I/O to complete, its thread is freed up for the server to use for processing other requests.</span></span> <span data-ttu-id="de949-311">따라서 비동기 코드 서버 리소스를 보다 효율적으로 사용할 수 있으며 특정가 지연 없이 더 많은 트래픽을 처리 하도록 서버를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-311">As a result, asynchronous code enables server resources to be used more efficiently, and the server is enabled to handle more traffic without delays.</span></span>

<span data-ttu-id="de949-312">비동기 코드는 런타임 시 약간의 오버 헤드를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-312">Asynchronous code does introduce a small amount of overhead at run time.</span></span> <span data-ttu-id="de949-313">트래픽이 적은 경우에 대 한 성능 저하가 트래픽이 많은 상황에 대 한 동안 무시할를 잠재적 성능 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-313">For low traffic situations, the performance hit is negligible, while for high traffic situations, the potential performance improvement is substantial.</span></span>

<span data-ttu-id="de949-314">다음 코드에서는 `async` 키워드를 `Task<T>` 값을 반환 `await` 키워드 및 `ToListAsync` 메서드를 비동기적으로 실행 하는 코드를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-314">In the following code, the `async` keyword, `Task<T>` return value, `await` keyword, and `ToListAsync` method make the code execute asynchronously.</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Students/Index.cshtml.cs?name=snippet_ScaffoldedIndex)]

* <span data-ttu-id="de949-315">`async` 키워드는 컴파일러에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-315">The `async` keyword tells the compiler to:</span></span>

  * <span data-ttu-id="de949-316">메서드 본문의 부분에 대 한 콜백을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-316">Generate callbacks for parts of the method body.</span></span>
  * <span data-ttu-id="de949-317">자동으로 만듭니다는 [작업](https://docs.microsoft.com/dotnet/api/system.threading.tasks.task?view=netframework-4.7) 반환 되는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="de949-317">Automatically create the [Task](https://docs.microsoft.com/dotnet/api/system.threading.tasks.task?view=netframework-4.7) object that is returned.</span></span> <span data-ttu-id="de949-318">자세한 내용은 참조 [작업 반환 형식](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/async/async-return-types#BKMK_TaskReturnType)합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-318">For more information, see [Task Return Type](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/async/async-return-types#BKMK_TaskReturnType).</span></span>

* <span data-ttu-id="de949-319">암시적 반환 형식 `Task` 은 진행 중인 작업을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="de949-319">The implicit return type `Task` represents ongoing work.</span></span>

* <span data-ttu-id="de949-320">`await` 키워드는 컴파일러에 메서드가 두 부분으로 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-320">The `await` keyword causes the compiler to split the method into two parts.</span></span> <span data-ttu-id="de949-321">첫 번째 부분은 비동기적으로 시작 된 작업을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-321">The first part ends with the operation that is started asynchronously.</span></span> <span data-ttu-id="de949-322">두 번째 부분은 작업이 완료 될 때 호출 되는 콜백 메서드에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-322">The second part is put into a callback method that is called when the operation completes.</span></span>

* <span data-ttu-id="de949-323">`ToListAsync`비동기 버전의 `ToList` 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="de949-323">`ToListAsync` is the asynchronous version of the `ToList` extension method.</span></span>

<span data-ttu-id="de949-324">EF 코어를 사용 하는 비동기 코드를 작성 하는 경우 고려해 야 할 몇 가지 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="de949-324">Some things to be aware of when writing asynchronous code that uses EF Core:</span></span>

* <span data-ttu-id="de949-325">쿼리 또는 여 DB에 보내야 하는 명령을 발생 하는 명령문만 비동기적으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de949-325">Only statements that cause queries or commands to be sent to the DB are executed asynchronously.</span></span> <span data-ttu-id="de949-326">포함 된 `ToListAsync`, `SingleOrDefaultAsync`, `FirstOrDefaultAsync`, 및 `SaveChangesAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-326">That includes, `ToListAsync`, `SingleOrDefaultAsync`, `FirstOrDefaultAsync`, and `SaveChangesAsync`.</span></span> <span data-ttu-id="de949-327">방금 변경 하는 문을 포함 하지 않습니다는 `IQueryable`와 같은 `var students = context.Students.Where(s => s.LastName == "Davolio")`합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-327">It does not include statements that just change an `IQueryable`, such as `var students = context.Students.Where(s => s.LastName == "Davolio")`.</span></span>

* <span data-ttu-id="de949-328">EF 코어 컨텍스트는 스레드 안전 하지 않습니다: 동시에 여러 작업을 수행 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="de949-328">An EF Core context is not threaded safe: don't try to do multiple operations in parallel.</span></span> 

* <span data-ttu-id="de949-329">비동기 코드의 성능 이점을 활용 하려면 있는지 라이브러리 패키지 (예: 페이징) 비동기 메서드를 사용 DB에 쿼리를 전송 하는 EF 코어 메서드를 호출 하는 경우를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-329">To take advantage of the performance benefits of async code, verify that library packages (such as for paging) use async if they call EF Core methods that send queries to the DB.</span></span>

<span data-ttu-id="de949-330">.NET의 비동기 프로그래밍에 대 한 자세한 내용은 참조 [비동기 개요](https://docs.microsoft.com/dotnet/articles/standard/async)합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-330">For more information about asynchronous programming in .NET, see [Async Overview](https://docs.microsoft.com/dotnet/articles/standard/async).</span></span>

<span data-ttu-id="de949-331">다음 자습서에서는 기본 CRUD (만들기, 읽기, 업데이트, 삭제) 작업을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="de949-331">In the next tutorial, basic CRUD (create, read, update, delete) operations are examined.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="de949-332">다음</span><span class="sxs-lookup"><span data-stu-id="de949-332">Next</span></span>](xref:data/ef-rp/crud)