---
title: "Entity Framework Core를 사용한 Razor 페이지 - 자습서 1/8"
author: rick-anderson
description: "Entity Framework Core를 사용하여 Razor 페이지 앱을 만드는 방법을 보여 줍니다."
manager: wpickett
ms.author: riande
ms.date: 11/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: data/ef-rp/intro
ms.openlocfilehash: 091f34da347d52ba8e3e87779ddc4aeb790c2800
ms.sourcegitcommit: 18d1dc86770f2e272d93c7e1cddfc095c5995d9e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2018
---
# <a name="getting-started-with-razor-pages-and-entity-framework-core-using-visual-studio-1-of-8"></a>Visual Studio를 사용하여 Razor 페이지 및 Entity Framework Core 시작(1/8)

작성자: [Tom Dykstra](https://github.com/tdykstra) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)

Contoso University 샘플 웹앱은 EF(Entity Framework) Core 2.0 및 Visual Studio 2017을 사용하여 ASP.NET Core 2.0 MVC 웹 응용 프로그램을 만드는 방법을 보여 줍니다.

샘플 앱은 가상 Contoso University의 웹 사이트입니다. 학생 입학, 강좌 개설 및 강사 할당과 같은 기능이 있습니다. 이 페이지는 Contoso University 샘플 앱을 빌드하는 방법을 설명하는 일련의 자습서 중 첫 번째 작업입니다.

[완성된 앱을 다운로드하거나 확인하세요.](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples) [지침을 다운로드하세요](xref:tutorials/index#how-to-download-a-sample).

## <a name="prerequisites"></a>필수 구성 요소

[!INCLUDE[install 2.0](../../includes/install2.0.md)]

[Razor 페이지](xref:mvc/razor-pages/index)에 익숙함. 신규 프로그래머는 이 시리즈를 시작하기 전에 [Razor 페이지 시작하기](xref:tutorials/razor-pages/razor-pages-start)를 완료해야 합니다.

## <a name="troubleshooting"></a>문제 해결

해결할 수 없는 문제가 발생한 경우 일반적으로 [완료된 단계](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots) 또는 [완료된 프로젝트](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu-final)와 코드를 비교하여 해결책을 찾을 수 있습니다. 일반적인 오류 목록 및 해결 방법은 [시리즈 중 마지막 자습서의 문제 해결 섹션](xref:data/ef-mvc/advanced#common-errors)을 참조하세요. 필요한 내용을 찾지 못한 경우 질문을 [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) 또는 [EF Core](https://stackoverflow.com/questions/tagged/entity-framework-core)에 대한 [StackOverflow.com](https://stackoverflow.com/questions/tagged/asp.net-core)에 게시할 수 있습니다.

> [!TIP]
> 이 자습서 시리즈는 이전 자습서에서 수행되는 내용을 기반으로 합니다. 각 자습서를 성공적으로 완료한 후에 프로젝트 복사본의 저장을 고려합니다. 문제가 발생한 경우 다시 처음으로 이동하는 대신 이전 자습서부터 시작할 수 있습니다. 또는 [완료된 단계](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots)를 다운로드하고 완료된 단계를 사용하여 다시 시작할 수 있습니다.

## <a name="the-contoso-university-web-app"></a>Contoso University 웹앱

이러한 자습서에서 빌드한 앱은 기본 대학 웹 사이트입니다.

사용자는 학생, 강좌 및 강사 정보를 보고 업데이트할 수 있습니다. 자습서에서 만든 화면 중 몇 가지 예가 나와 있습니다.

![학생 인덱스 페이지](intro/_static/students-index.png)

![학생 편집 페이지](intro/_static/student-edit.png)

이 사이트의 UI 스타일은 기본 제공 템플릿에서 생성된 것과 가깝습니다. 자습서는 UI가 아닌 Razor 페이지를 사용한 EF Core 자습서 위주로 설명됩니다.

## <a name="create-a-razor-pages-web-app"></a>Razor 페이지 웹앱 만들기

* Visual Studio **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.
* 새 ASP.NET Core 웹 응용 프로그램을 만듭니다. 프로젝트 이름을 **ContosoUniversity**로 지정합니다. 코드를 복사/붙여넣을 때 네임스페이스와 일치할 수 있도록 프로젝트 이름을 *ContosoUniversity*로 지정하는 것이 중요합니다.
 ![새 ASP.NET Core 웹 응용 프로그램](intro/_static/np.png)
* 드롭다운에서 **ASP.NET Core 2.0**을 선택하고 **웹 응용 프로그램**을 선택합니다.
 ![웹 응용 프로그램(Razor 페이지)](../../mvc/razor-pages/index/_static/np2.png)

**F5** 키를 눌러 디버그 모드에서 앱을 실행하거나 **Ctrl-F5**를 눌러 디버거를 연결하지 않고 실행합니다.

## <a name="set-up-the-site-style"></a>사이트 스타일 설정

몇 가지 변경 내용으로 사이트 메뉴, 레이아웃 및 홈페이지를 설정합니다.

*Pages/_Layout.cshtml*을 열고 다음과 같이 변경합니다.

* 모든 “ContosoUniversity”를 “Contoso University”로 변경합니다. 세 번 나옵니다.

* **학생**, **강좌**, **강사** 및 **부서**에 대한 메뉴 항목을 추가하고 **연락처** 메뉴 항목을 삭제합니다.

변경 내용은 강조 표시되어 있습니다. (모든 표시가 표시되지는 *않습니다*.)

[!code-html[](intro/samples/cu/Pages/_Layout.cshtml?highlight=6,29,35-38,47&range=1-50)]

*Pages/Index.cshtml*에서 다음 코드로 파일의 콘텐츠를 텍스트를 대체하여 ASP.NET 및 MVC에 대한 텍스트를 이 앱에 대한 텍스트로 바꿉니다.

[!code-html[](intro/samples/cu/Pages/Index.cshtml)]

Ctrl+F5를 눌러 프로젝트를 실행합니다. 다음 자습서에서 만든 탭과 함께 홈페이지가 표시됩니다.

![Contoso University 홈페이지](intro/_static/home-page.png)

## <a name="create-the-data-model"></a>데이터 모델 만들기

Contoso University 앱에 대한 엔터티 클래스를 만듭니다. 다음과 같은 세 가지 엔터티로 시작합니다.

![과정-등록-학생 데이터 모델 다이어그램](intro/_static/data-model-diagram.png)

`Student` 및 `Enrollment` 엔터티 사이에 일 대 다 관계가 있습니다. `Course` 및 `Enrollment` 엔터티 사이에 일 대 다 관계가 있습니다. 학생은 여러 강좌에 등록할 수 있습니다. 강좌는 등록된 학생이 여러 명일 수 있습니다.

다음 섹션에서 각각에 대한 이러한 엔터티에 대한 클래스를 만듭니다.

### <a name="the-student-entity"></a>학생 엔터티

![학생 엔터티 다이어그램](intro/_static/student-entity.png)

*모델* 폴더를 만듭니다. *모델* 폴더에서 다음 코드로 *Student.cs*라는 이름의 클래스 파일을 만듭니다.

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_Intro)]

`ID` 속성은 이 클래스에 해당하는 DB(데이터베이스) 테이블의 기본 키 열이 됩니다. 기본적으로 EF 코어는 `ID` 또는 `classnameID`로 명명된 속성을 기본 키로 해석합니다.

`Enrollments` 속성은 탐색 속성입니다. 탐색 속성은 이 엔터티와 관련된 다른 엔터티에 연결됩니다. 이 경우 `Student entity`의 `Enrollments` 속성은 해당 `Student`에 관련된 모든 `Enrollment` 엔터티를 포함합니다. 예를 들어 DB의 학생 행에 두 개의 관련 등록 행이 있는 경우 `Enrollments` 탐색 속성은 그 두 `Enrollment` 엔터티를 포함합니다. 관련된 `Enrollment` 행은 `StudentID` 열에서 해당 학생의 기본 키 값을 포함하는 열입니다. 예를 들어 ID=1인 학생에 `Enrollment` 테이블의 두 개 행이 있다고 가정합니다. `Enrollment` 테이블에 `StudentID` = 1인 두 개의 행이 있습니다. `StudentID`는 `Student` 테이블에서 학생을 지정하는 `Enrollment` 테이블의 외래 키입니다.

탐색 속성이 여러 엔터티를 포함하는 경우 탐색 속성은 `ICollection<T>`와 같은 목록 유형이어야 합니다. `ICollection<T>`는 지정할 수 있으며, `List<T>` 또는 `HashSet<T>`와 같은 형식일 수 있습니다. `ICollection<T>`가 사용되는 경우 EF Core는 기본적으로 `HashSet<T>` 컬렉션을 만듭니다. 여러 엔터티를 포함하는 탐색 속성은 다대다 및 일대다 관계에서 제공됩니다.

### <a name="the-enrollment-entity"></a>등록 엔터티

![등록 엔터티 다이어그램](intro/_static/enrollment-entity.png)

*모델* 폴더에서 다음 코드로 *Enrollment.cs*를 만듭니다.

[!code-csharp[Main](intro/samples/cu/Models/Enrollment.cs?name=snippet_Intro)]

`EnrollmentID` 속성은 기본 키입니다. 이 엔터티는 `Student` 엔터티 같은 `ID` 대신 `classnameID` 패턴을 사용합니다. 일반적으로 개발자는 하나의 패턴을 선택하여 데이터 모델 전체에 사용합니다. 자습서의 뒷부분에서는 클래스 이름 없이 ID를 사용하여 더 손쉽게 데이터 모델에서 상속을 구현하는 내용이 나옵니다.

`Grade` 속성은 `enum`입니다. `Grade` 형식 선언 뒤에 있는 물음표는 `Grade` 속성이 null을 허용한다는 것을 나타냅니다. null인 등급은 0 등급과는 다릅니다. null 의미는 알려지지 않거나 아직 등록되지 않은 등급을 뜻합니다.

`StudentID` 속성은 외래 키로, 해당 탐색 속성은 `Student`입니다. `Enrollment` 엔터티는 하나의 `Student` 엔터티와 연결되므로 속성은 단일 `Student` 엔터티를 포함합니다. `Student` 엔터티는 여러 `Enrollment` 엔터티를 포함하는 `Student.Enrollments` 탐색 속성과 다릅니다.

`CourseID` 속성은 외래 키로, 해당 탐색 속성은 `Course`입니다. `Enrollment` 엔터티는 하나의 `Course` 엔터티와 연결됩니다.

EF Core는 속성 이름이 `<navigation property name><primary key property name>`인 경우 외래 키로 해석합니다. 예를 들어 `Student` 탐색 속성의 경우 `Student` 엔터티의 기본 키가 `ID`이므로 `StudentID`입니다. 외래 키 속성의 이름은 `<primary key property name>`으로 지정할 수 있습니다. 예를 들어 `Course` 엔터티의 기본 키가 `CourseID`이므로 `CourseID`라고 할 수 있습니다.

### <a name="the-course-entity"></a>강좌 엔터티

![강좌 엔터티 다이어그램](intro/_static/course-entity.png)

*모델* 폴더에서 다음 코드로 *Course.cs*를 만듭니다.

[!code-csharp[Main](intro/samples/cu/Models/Course.cs?name=snippet_Intro)]

`Enrollments` 속성은 탐색 속성입니다. `Course` 엔터티는 `Enrollment` 엔터티의 개수와 관련이 있을 수 있습니다.

앱은 `DatabaseGenerated` 특성을 통해 DB가 생성하도록 하는 대신 기본 키를 지정할 수 있습니다.

## <a name="create-the-schoolcontext-db-context"></a>SchoolContext DB 컨텍스트 만들기

특정 데이터 모델에 맞게 EF Core 기능을 조정하는 주 클래스는 DB 컨텍스트 클래스입니다. 데이터 컨텍스트는 `Microsoft.EntityFrameworkCore.DbContext`에서 파생됩니다. 데이터 컨텍스트는 데이터 모델에 포함되는 엔터티를 지정합니다. 이 프로젝트에서 클래스 이름은 `SchoolContext`로 지정됩니다.

프로젝트 폴더에서 *Data*라는 이름의 폴더를 만듭니다.

*Data* 폴더에서 다음 코드로 *SchoolContext.cs*를 만듭니다.

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_Intro)]

이 코드는 각 엔터티 집합에 대한 `DbSet` 속성을 만듭니다. EF Core 용어에서:

* 엔터티 집합은 일반적으로 DB 테이블에 해당합니다.
* 엔터티는 테이블의 행에 해당합니다.

`DbSet<Enrollment>` 및 `DbSet<Course>`는 생략할 수 있습니다. `Student` 엔터티는 `Enrollment` 엔터티를 참조하고 `Enrollment` 엔터티는 `Course` 엔터티를 참조하기 때문에 EF Core는 이를 암시적으로 포함합니다. 이 자습서의 경우 `DbSet<Enrollment>` 및 `DbSet<Course>`를 `SchoolContext`에 유지합니다.

DB가 만들어지면 EF Core는 `DbSet` 속성 이름과 동일한 이름을 갖는 테이블을 만듭니다. 컬렉션에 대한 속성 이름은 일반적으로 복수(Student가 아닌 Students)입니다. 개발자는 테이블 이름을 복수화할지 여부에 대해 동의하지 않습니다. 이러한 자습서의 경우 기본 동작은 DbContext에서 단수 테이블 이름을 지정하여 재정의됩니다. 단수 테이블 이름을 지정하려면 다음 강조 표시된 코드를 추가합니다.

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_TableNames&highlight=16-21)]

## <a name="register-the-context-with-dependency-injection"></a>종속성 주입으로 컨텍스트 등록

ASP.NET Core는 [종속성 주입](xref:fundamentals/dependency-injection)을 포함합니다. 서비스(예: EF Core DB 컨텍스트)는 응용 프로그램 시작 중에 종속성 주입에 등록됩니다. 이러한 서비스(예: Razor 페이지)가 필요한 구성 요소에는 생성자 매개 변수를 통해 이러한 서비스가 제공됩니다. DB 컨텍스트 인스턴스를 가져오는 생성자 코드는 자습서 뒷부분에 나옵니다.

`SchoolContext`를 서비스로 등록하려면 *Startup.cs*를 열고 강조 표시된 줄을 `ConfigureServices` 메서드에 추가합니다.

[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_SchoolContext&highlight=3-4)]

`DbContextOptionsBuilder` 개체에서 메서드를 호출하여 연결 문자열의 이름을 컨텍스트에 전달합니다. 로컬 개발의 경우 [ASP.NET Core 구성 시스템](xref:fundamentals/configuration/index)은 *appsettings.json* 파일에서 연결 문자열을 읽습니다.

`ContosoUniversity.Data` 및 `Microsoft.EntityFrameworkCore` 네임스페이스에 대한 `using` 문을 추가합니다. 프로젝트를 빌드합니다.

[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_Usings)]

*appsettings.json* 파일을 열고 다음 코드에 표시된 대로 연결 문자열을 추가합니다.

[!code-json[](./intro/samples/cu/appsettings1.json?highlight=2-4)]

위의 연결 문자열은 `ConnectRetryCount=0`을 사용하여 [SQLClient](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/sqlclient-for-the-entity-framework)가 중단되는 것을 방지합니다.

### <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

연결 문자열은 SQL Server LocalDB DB를 지정합니다. LocalDB는 프로덕션 사용이 아닌 앱 개발용으로 고안된 SQL Server Express 데이터베이스 엔진의 경량 버전입니다. LocalDB는 요청 시 시작하고 사용자 모드에서 실행되므로 복잡한 구성이 없습니다. 기본적으로 LocalDB는 *.mdf* DB 파일을 `C:/Users/<user>` 디렉터리에 만듭니다.

## <a name="add-code-to-initialize-the-db-with-test-data"></a>코드를 추가하여 테스트 데이터로 DB 초기화

EF Core가 빈 DB를 만듭니다. 이 섹션에서는 테스트 데이터로 채울 *Seed* 메서드가 작성됩니다.

*Data* 폴더에서 *DbInitializer.cs*라는 새 클래스 파일을 만들고 다음 코드를 추가합니다.

[!code-csharp[Main](intro/samples/cu/Data/DbInitializer.cs?name=snippet_Intro)]

코드는 DB에 학생이 있는지를 확인합니다. DB에 학생이 없는 경우 DB는 테스트 데이터로 시드됩니다. `List<T>` 컬렉션이 아닌 배열에 테스트 데이터를 로드하여 성능을 최적화합니다.

`EnsureCreated` 메서드는 자동으로 DB 컨텍스트에 대한 DB를 만듭니다. DB가 있는 경우 `EnsureCreated`는 DB를 수정하지 않고 반환합니다.

*Program.cs*에서 다음을 수행하는 `Main` 메서드를 수정합니다.

* 종속성 주입 컨테이너에서 DB 컨텍스트 인스턴스를 가져옵니다.
* 컨텍스트를 전달하는 시드 메서드를 호출합니다.
* 시드 메서드가 완료되면 컨텍스트를 삭제합니다.

다음 코드는 업데이트된 *Program.cs* 파일을 보여 줍니다.

[!code-csharp[Main](intro/samples/cu/ProgramOriginal.cs?name=snippet)]

처음으로 앱이 실행되고 DB가 생성되며 테스트 데이터로 시드됩니다. 데이터 모델이 업데이트되면:
* DB를 삭제합니다.
* 시드 메서드를 업데이트합니다.
* 앱을 실행하면 새 시드된 DB가 만들어집니다. 

이후의 자습서에서는 데이터 모델이 변경될 때 DB를 삭제하고 다시 작성하지 않고 DB가 업데이트됩니다.

<a name="pmc"></a>
## <a name="add-scaffold-tooling"></a>스캐폴드 도구 추가

이 섹션에서는 Visual Studio 웹 코드 생성 패키지를 추가하는 데 PMC(패키지 관리자 콘솔)가 사용됩니다. 스캐폴딩 엔진을 실행하려면 이 패키지가 필요합니다.

**도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다.

PMC(패키지 관리자 콘솔)에서 다음 명령을 입력합니다.

```powershell
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Design
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Utils
```

위 명령은 *.csproj 파일에 NuGet 패키지를 추가합니다.

[!code-csharp[Main](intro/samples/cu/ContosoUniversity1_csproj.txt?highlight=7-8)]

<a name="scaffold"></a>
## <a name="scaffold-the-model"></a>모델 스캐폴드

* 프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)에서 명령 창을 엽니다.
* 다음 명령을 실행합니다.


 ```console
dotnet restore
dotnet aspnet-codegenerator razorpage -m Student -dc SchoolContext -udl -outDir Pages\Students --referenceScriptLibraries
 ```
 
다음 오류가 생성되는 경우:

```text
Unhandled Exception: System.IO.FileNotFoundException: 
Could not load file or assembly 
'Microsoft.VisualStudio.Web.CodeGeneration.Utils, 
Version=2.0.0.0, Culture=neutral, PublicKeyToken=adb9793829ddae60'.
The system cannot find the file specified.
```

명령을 다시 실행하고 페이지 아래쪽에 의견을 남깁니다.

오류가 표시될 경우:
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)에서 명령 창을 엽니다.


프로젝트를 빌드합니다. 빌드는 다음과 같은 오류를 생성합니다.

 `1>Pages\Students\Index.cshtml.cs(26,38,26,45): error CS1061: 'SchoolContext' does not contain a definition for 'Student'`

 전체적으로 `_context.Student`를 `_context.Students`로 변경합니다(즉, “s”를 `Student`에 추가). 7개 항목이 발견되어 업데이트됩니다. 다음 릴리스에서 [이 버그](https://github.com/aspnet/Scaffolding/issues/633)를 해결하기 위해 노력하고 있습니다.

[!INCLUDE[model4tbl](../../includes/RP/model4tbl.md)]

 <a name="test"></a>
### <a name="test-the-app"></a>앱 테스트

앱을 실행하고 **학생** 링크를 선택합니다. 브라우저 너비에 따라 **학생** 링크가 페이지의 맨 위에 나타납니다. **학생** 링크가 표시되지 않으면 오른쪽 위 모서리에 있는 탐색 아이콘을 클릭합니다.

![좁은 Contoso University 홈페이지](intro/_static/home-page-narrow.png)

**만들기**, **편집** 및 **세부 정보** 링크를 테스트합니다.

## <a name="view-the-db"></a>DB 보기

앱이 시작되면 `DbInitializer.Initialize`는 `EnsureCreated`를 호출합니다. `EnsureCreated`는 DB가 존재하는지 감지하고 필요한 경우 DB를 만듭니다. DB에 학생이 없는 경우 `Initialize` 메서드는 학생을 추가합니다.

Visual Studio의 **보기** 메뉴에서 **SSOX(SQL Server 개체 탐색기)**를 엽니다.
SSOX에서 **(localdb)\MSSQLLocalDB > 데이터베이스 > ContosoUniversity1**을 클릭합니다.

**테이블** 노드를 확장합니다.

**학생** 테이블을 마우스 오른쪽 단추로 클릭하고, **데이터 보기**를 클릭하여 만든 열 및 테이블에 삽입된 행을 볼 수 있습니다.

*.mdf* 및 *.ldf* DB 파일은 *C:\Users\\<yourusername>* 폴더에 있습니다.

앱 시작 시 다음 작업 흐름을 허용하는 `EnsureCreated`가 호출됩니다.

* DB를 삭제합니다.
* DB 스키마를 변경합니다(예: `EmailAddress` 필드 추가).
* 앱을 실행합니다.

`EnsureCreated`가 `EmailAddress` 열이 있는 DB를 만듭니다.

## <a name="conventions"></a>규칙

EF Core에서 수행하는 규칙 또는 가정의 사용으로 인해 EF Core에서 완벽한 DB를 만들기 위해 작성한 규칙의 양은 최소여야 합니다.

* `DbSet` 속성의 이름은 테이블 이름으로 사용됩니다. `DbSet` 속성에서 참조하지 않는 엔터티의 경우 엔터티 클래스 이름이 테이블 이름으로 사용됩니다.

* 엔터티 속성 이름은 열 이름에 사용됩니다.

* ID 또는 classnameID로 명명된 엔터티 속성은 기본 키 속성으로 인식됩니다.

* 속성 이름이 *<navigation property name><primary key property name>*인 경우 외래 키 속성으로는 해석됩니다(예를 들어 `Student` 엔터티의 기본 키가 `ID`이므로 `Student` 탐색 속성의 경우 `StudentID`). 외래 키 속성의 이름을 *<primary key property name>*으로 지정할 수 있습니다(예를 들어 `Enrollment` 엔터티의 기본 키가 `EnrollmentID`이므로 `EnrollmentID`).

기본 동작은 재정의할 수 있습니다. 예를 들어 이 자습서의 앞부분에 나온 것처럼 테이블 이름을 명시적으로 지정할 수 있습니다. 열 이름을 명시적으로 설정할 수 있습니다. 기본 키와 외래 키를 명시적으로 설정할 수 있습니다.

## <a name="asynchronous-code"></a>비동기 코드

비동기 프로그래밍은 ASP.NET Core 및 EF Core에 대한 기본 모드입니다.

웹 서버에는 사용할 수 있는 스레드 수가 제한적이며, 로드 양이 많은 상황에서는 사용 가능한 모든 스레드가 사용될 수 있습니다. 이 경우 서버는 스레드가 해제될 때까지 새 요청을 처리할 수 없습니다. 동기 코드를 사용하면 I/O 완료를 대기하느라 작업을 실제로 수행하지 않는 동안에 많은 스레드가 정체될 수 있습니다. 비동기 코드를 사용하면 프로세스가 I/O 완료를 대기할 때 다른 요청을 처리하는 데 사용하도록 해당 스레드가 서버에서 해제됩니다. 따라서 비동기 코드를 사용하면 서버 리소스를 더 효율적으로 사용할 수 있으며 서버가 지연 없이 더 많은 트래픽을 처리할 수 있습니다.

비동기 코드는 런타임 시 약간의 오버헤드를 도입합니다. 트래픽이 높은 상황에서는 잠재적 성능 향상이 상당한 반면, 트래픽이 낮은 상황의 경우 성능 저하는 미미합니다.

다음 코드에서 `async` 키워드, `Task<T>` 반환 값, `await` 키워드 및 `ToListAsync` 메서드는 비동기적으로 코드 실행을 수행합니다.

[!code-csharp[Main](intro/samples/cu/Pages/Students/Index.cshtml.cs?name=snippet_ScaffoldedIndex)]

* `async` 키워드는 컴파일러가 다음을 수행하도록 합니다.

  * 메서드 본문의 부분에 대한 콜백을 생성합니다.
  * 반환되는 [작업](https://docs.microsoft.com/dotnet/api/system.threading.tasks.task?view=netframework-4.7) 개체를 자동으로 만듭니다. 자세한 내용은 [작업 반환 형식](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/async/async-return-types#BKMK_TaskReturnType)을 참조하세요.

* 암시적 반환 형식 `Task`는 진행 중인 작업을 나타냅니다.

* `await` 키워드로 인해 컴파일러는 메서드를 두 부분으로 분할합니다. 첫 번째 부분은 비동기적으로 시작되는 작업을 종료합니다. 두 번째 부분은 작업이 완료될 때 호출되는 콜백 메서드에 배치됩니다.

* `ToListAsync`는 `ToList` 확장 메서드의 비동기 버전입니다.

EF Core를 사용하는 비동기 코드를 작성할 때 고려해야 할 몇 가지 사항은 다음과 같습니다.

* 쿼리 또는 명령을 DB에 보내는 명령문만 비동기적으로 실행됩니다. 여기에는 `ToListAsync`, `SingleOrDefaultAsync`, `FirstOrDefaultAsync` 및 `SaveChangesAsync`가 포함됩니다. `var students = context.Students.Where(s => s.LastName == "Davolio")`와 같은 `IQueryable`을 변경하는 명령문은 포함되지 않습니다.

* EF Core 컨텍스트는 스레드로부터 안전하지 않습니다. 동시에 여러 작업을 수행하지 마십시오. 

* 비동기 코드의 성능 이점을 활용하려면 쿼리를 DB에 보내는 EF Core 메서드를 호출하는 경우 라이브러리 패키지(예: 페이징)가 비동기를 사용하는지 확인합니다.

.NET에서의 비동기 프로그래밍에 대한 자세한 내용은 [비동기 개요](https://docs.microsoft.com/dotnet/articles/standard/async)를 참조하세요.

다음 자습서에서는 기본 CRUD(만들기, 읽기, 업데이트, 삭제) 작업을 검사합니다.

>[!div class="step-by-step"]
[다음](xref:data/ef-rp/crud)
