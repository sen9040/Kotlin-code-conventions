
Kotlin Style Guide
=================


본 문서는  [Kotlin Style Guide](https://developer.android.com/kotlin/style-guide)를 기반으로 작성되었습니다.

- [코드 레이아웃](#코드-레이아웃)
    - [들여쓰기 및 띄어쓰기](#들여쓰기-및-띄어쓰기)
    - [줄바꿈](#줄바꿈)
    - [최대 줄 길이](#최대-줄-길이)
    - [람다 형식](#람다-형식)
    - [임포트](#임포트)
- [네이밍](#네이밍)
    - [클래스](#클래스)
    - [함수](#함수)
    - [변수](#변수)
    - [상수](#상수)
    - [리소스 룰](#리소스-룰)
    - [열거형](#열거형)
    - [지원 속성](#지원-속성)
    - [약어](#약어)
- [타입](#타입)
- [주석](#주석)
- [프로그래밍 권장사항](#프로그래밍-권장사항)

## 코드 레이아웃

### 들여쓰기 및 띄어쓰기 

- 새 블록 또는 블록 형식 구문이 열릴 떄마다 들여쓰기가 4칸씩 증가합니다.
- class 또는 interface를 지정하기 위해 클래스 선언에 사용된 경우나 일반 제약조건의 where 절에 사용된 경우에만 콜론(:) 앞에 줄바꿈을 넣습니다.

    **좋은 예:**
    ```kotlin
    class Foo : Runnable
    fun <T : Comparable> max(a: T, b:T)
    fun <T> max(a: T, b: T) where T : Comparable<T>
    ```

    **나쁜 예:**
    ```kotlin
    class Foo: Runnable
    fun <T: Comparable> max(a: T, b: T)
    fun <T> max(a: T, b: T) where T: Comparable<T>
    ```
- 변수 선언과 그 타입을 분리할 때 콜론 : 앞에 공백을 두지 않는다.
  콜론 : 뒤에는 항상 공백을 둔다.

### 줄바꿈

- 함수 정의가 최대 길이를 초과하는 경우에는 아래와 같이 줄바꿈합니다.

    ```kotlin
    fun <T> Iterable<T>.joinToString(
        separator: CharSequence = ", ",
        prefix: CharSequence = "",
        postfix: CharSequence = ""
    ): String {
    // …
    }
     ```

- 함수에 표현식이 하나만 포함되는 경우 표현식 함수로 표현될 수 있습니다.

  ```kotlin
  override fun toString(): String {
    return "Hey"
  }
  ```

  ```kotlin
  override fun toString(): String = "Hey"
  ```
  
### 최대 줄 길이

- 한 줄은 열 제한은 100자입니다. 

  **예외:**
  - 열제한을 준수할 수 없는 줄(예: KDoc의 긴 URL)
  - package 및 import 문
  - 잘라서 셀에 붙여넣을 수 있는 주석의 명령줄 

### 람다 형식

- 람다 표현식에서 {}, -> 주변에도 공백을 두어야 한다.
- 호출에 사용된 람다가 한 개인 경우 가능한 한 소괄호 () 를 제거해야 한다.

  ```kotlin
  list.filter { it > 10 }
  ```

### 임포트

- 클래스, 함수 및 속성의 import문의 단일 목록으로 그룹화되고 ASCII정렬됩니다.
- 모든 유형의 와일드 카드 가져오기는 **허용되지 않습니다.**
- package 문과 마찬가지로 import 문은 열 제한을 받지 않으며 줄바꿈되지 않습니다.

## 네이밍

### 클래스

- 클래스 이름에는 파일의 콘텐츠를 설명하는 이름을 선택하고 PascalCase를 사용합니다.

### 함수

- 함수 이름에는 camelCase로 작성되며 일반적으로 동사 또는 동사구입니다.(예 : sendMessage)
- Unit을 반환하는 @Composable로 주석 처리된 함수는 PascalCased이며 명사처럼 이름이 지정되어 있습니다.
  ```kotlin
  @Composable
  fun NameTag(name: String) {
  // …
  }
  ```

- Action 함수의 네이밍은 '주어 + 동사 + 목적어' 형태를 사용합니다.

  - *Tap(눌렀다 뗌)*은 `UIControlEvents`의 `.touchUpInside`에 대응하고, *Press(누름)*는 `.touchDown`에 대응합니다.
  - *will~*은 특정 행위가 일어나기 직전이고, *did~*는 특정 행위가 일어난 직후입니다.
  - *should~*는 일반적으로 `Bool`을 반환하는 함수에 사용됩니다.

  **좋은 예:**

    ```kotlin
    fun backButtonDidTap() {
      // ...
    }
    ```

  **나쁜 예:**

    ```kotlin
    fun back() {
      // ...
    }

    fun pressBack() {
      // ...
    }
    ```

### 변수

- 변수 이름에는 lowerCamelCase를 사용합니다.

### 상수

- 상수 이름에는 UPPER_SNAKE_CASE(모두 대문자)를 사용하며 밑줄로 단어를 구분합니다.  

### 리소스 룰 
- WHAT_WHERE_DESCRIPTION_SIZE
- 단점 리펙토링 자동 미지원
  - WHAT 리소스가 실제로 무엇을 나타내는지 (예:MainActivity - activity)
  - WHERE 속하는 위치를 설명 (에: MainActivity - main)
  - DESCRIPTION 한 화면에서 여러 요소를 구분 (예: title)
  - SIZE 정확한 크기 또는 드로어블 및 치수 (예: 24dp,small)
  
#### Layout 
- WHAT_WHERE.xml
- activity, fragment, view, item, layout (예: activity_main.xml)

#### XML View Ids
- WHAT_DESCRIPTION  or WHAT_WHERE_DESCRIPTION
- xml view 이름은 약어로 사용한다. (예: TextView - tv)
- DESCRIPTION 중복될경우 WHERE 을 추가하여 명확히 사용한다.
- (예: tv_title, tv_menu_title)

#### Strings
- WHERE_DESCRIPTION
- 공통적인 문자열은 WHERE 에 all 또는 common을 사용 (예: article_title, common_number)

#### Drawables
- WHAT_DESCRIPTION_SIZE
- ic, img, draw....(예: ic_push_24dp)

#### Dimensions
- WHAT_WHERE_DESCRIPTION_SIZE
- WHAT 은 width, height, size, margin....같은 것들이 들어갈 수 있다.(예: margin_menu_profileimage_24dp)
 

### 열거형

- enum의 각 case에는 UPPER_SNAKE_CASE(모두 대문자)를 사용합니다.

    ```kotlin
    enum class Answer {
      YES,
      NO,
  
      MAYBE {
          override fun toString() = """¯\_(ツ)_/¯"""
      }
    }
    ```



### 지원 속성

- 지원 속성이 필요한 경우 밑줄 처리된 접두사를 제외하고 이름이 실제 속성의 이름과 정확히 일치해야 합니다

  ```kotlin
  private var _table: Map? = null
  val table: Map
  get() {
  if (_table == null) {
  _table = HashMap()
  }
  return _table ?: throw AssertionError()
  }
  ```

### 약어

- 약어로 시작하는 경우 소문자로 표기하고, 그 외의 경우에는 항상 대문자로 표기합니다.

  **좋은 예:**

    <pre>
    var user<strong>Id</strong>: Int?
    var <strong>HTML</strong>: String?
    var website<strong>Url</strong>: NSURL?
    var <strong>URL</strong>String: String?
    </pre>

  **나쁜 예:**

    <pre>
    var user<strong>ID</strong>: Int?
    var <strong>html</strong>: String?
    var website<strong>URL</strong>: URL?
    var <strong>url</strong>String: String?
    </pre>


## 타입

- 초기값이 없는 변수 등 컴파일러가 타입을 추론할 수 없는 경우를 제외한 모든 변수 및 상수에는 타입을 명시해주지 않습니다.

  **좋은 예:**

    ```kotlin
    var name = "Taejun Kim"
    var age = 27
    var point = CGPoint.zero
    var emptyStringArray = [String]()
    ```

## 주석

- `/**`  `*/`를 사용해서 문서화에 사용되는 주석을 남깁니다.
- 일반적으로 @param과 @return 태그는 사용하지 마라.
- 대신, 파라미터 및 반환 값에 대한 설명을 주석 내용에 직접 포함시키고, 언급된 모든 파라미터에 링크를 추가한다.
- 주석 내용의 흐름에 맞지 않는 장황한 설명이 필요한 경우에만 @param 및 @return을 사용해라.


## 프로그래밍 권장사항

### 조건문 사용 
- try, if, when 아래와 같은 표현식을 사용하는것이 좋다.

  ```kotlin
  return if (x) foo() else bar()

  return when(x) {
    0 -> "zero"
    1 -> "one"
    else -> "nonzero"
  }
  ```
  
### 루프 사용 
- 루프에는 filter, map 과 같은 고차 함수를 사용하는 것이 좋다.
- 예외적으로 forEach의 경우 forEach의 리시버가 Nullable 이거나 forEach가 긴 호출 체인의 일부로 사용되는 경우가 아니라면 일반적인 for 루프가 더 좋다.
- 복수의 고차 함수를 이용한 복잡한 표현과 루프를 선택할 때에는 각 상황에서 실행되는 operation들의 비용을 이해해야 하고 성능 고려 사항들을 유념해라.

### 상수 관리
- 상수를 정의할 떄에는 object를 만들어 비슷한 상수끼리 모아둡니다. 재사용성과 유지보수 측면에서 큰 향상을 가져옵니다.

  ```kotlin
   object BaseUrl{
      const val BASE_URL = "https://dog.ceo/"
    }
    
    object Shard{
      const val KEY = "key"
    }
  ```
  이렇게 선언된 상수들은 다음과 같이 사용될 수 있습니다.
  ```kotlin
   binding.tvKey.text = Shard.KEY
  ```


