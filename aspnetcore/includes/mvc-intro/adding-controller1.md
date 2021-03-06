MVC(모델-뷰-컨트롤러) 아키텍처 패턴은 **M**odel, **V**iew 및 **C**ontroller라는 세 가지 주요 구성 요소으로 앱을 구분합니다. MVC 패턴을 통해 기존 모놀리식 응용 프로그램보다 쉽게 테스트 가능하고 업데이트할 수 있는 앱을 만들 수 있습니다. MVC 기반 앱에는 다음이 포함됩니다.

* **M**odels: 앱의 데이터를 나타내는 클래스입니다. 모델 클래스는 유효성 검사 논리를 사용하여 해당 데이터의 비즈니스 규칙을 적용합니다. 일반적으로 모델 개체는 모델 상태를 검색하고 데이터베이스에 저장합니다. 이 자습서에서 `Movie` 모델은 데이터베이스에서 영화 데이터를 검색하고 뷰로 제공하거나 업데이트합니다. 업데이트된 데이터는 데이터베이스에 기록됩니다.

* **V**iews: 뷰는 앱의 UI(사용자 인터페이스)를 표시하는 구성 요소입니다. 일반적으로 이 UI는 모델 데이터를 표시합니다.

* **C**ontrollers: 브라우저 요청을 처리하는 클래스입니다. 모델 데이터를 검색하고 응답을 반환하는 뷰 템플릿을 호출합니다. MVC 앱에서 뷰는 정보만 표시합니다. 컨트롤러가 사용자 입력 및 상호 작용을 처리하고 응답합니다. 예를 들어 컨트롤러는 경로 데이터 및 쿼리 문자열 값을 처리하고 모델에 이러한 값을 전달합니다. 모델은 이러한 값을 사용하여 데이터베이스를 쿼리할 수 있습니다. 예를 들어 `http://localhost:1234/Home/About`에는 `Home`(컨트롤러) 및 `About`(홈 컨트롤러에서 호출하는 작업 메서드)라는 경로 데이터가 있습니다. `http://localhost:1234/Movies/Edit/5`는 영화 컨트롤러를 사용하는 ID=5를 포함한 영화를 편집하는 요청입니다.  자습서의 뒷부분에서 경로 데이터에 대해 알아봅니다.

MVC 패턴을 통해 이러한 요소 간의 느슨한 결합을 제공하는 앱의 다양한 측면(입력 논리, 비즈니스 논리 및 UI 논리)을 구분하는 앱을 만들 수 있습니다. 패턴은 각 종류의 논리가 앱에 있어야 하는 위치를 지정합니다. UI 논리는 뷰에 속해 있습니다. 입력 논리는 컨트롤러에 속해 있습니다. 비즈니스 논리는 모델에 속해 있습니다. 이러한 분리를 통해 다른 코드에 영향을 주지 않고 한 번에 구현의 하나의 측면에서 작업할 수 있기 때문에 앱을 빌드하는 경우 복잡성을 관리할 수 있습니다. 예를 들어 비즈니스 논리 코드에 따라 달리지지 않고 뷰 코드에서 작업할 수 있습니다.

이 자습서 시리즈에서 이러한 개념을 설명하고 영화 앱을 빌드하기 위해 사용하는 방법을 보여줍니다. MVC 프로젝트에는 *컨트롤러* 및 *뷰*에 대한 폴더가 포함됩니다.
