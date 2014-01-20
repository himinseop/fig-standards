기본 코딩 규칙
=====================

This section of the standard comprises what should be considered the standard
coding elements that are required to ensure a high level of technical
interoperability between shared PHP code.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119][].

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt
[PSR-0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md


1. 개요
-----------

- PHP파일에는 반드시 `<?php` 와 `<?=` 태그만 사용합니다.

- PHP파일에는 반드시 BOM코드가 없는 UTF-8을 사용합니다.

- PHP파일에서 심볼(classes, functions, constants, etc.)선언 *또는* 부작용을 일으킬 수 있는 작업은 *모두* 하지 말아야 합니다.

- 네임스페이스와 클래스는 반드시 [PSR-0][]를 따라야 합니다.

- 클래스명은 반드시 `StudlyCaps`로 선언되어야합니다.

- 클래스 상수는 반드시 언더스코어로 연결된 대문자여야 합니다.

- 메소드명은 반드시 `camelCase`로 선언되어야 합니다.



2. 파일
--------

### 2.1. PHP 태그

PHP코드는 `<?php ?>`이나 단축태그 `<?= ?>`만 사용합니다; 다른 형태의 태그는 절대 사용하지 말아야 합니다.

### 2.2. 문자 인코딩

PHP코드는 BOM코드가 없는 UTF-8만을 사용합니다.

### 2.3. 부작용

파일에는 새로운 심볼(classes, functions, constants, etc.)을 선언하거나 다른 부작용을 일으킬 수 있는 것, 또는 부작용이 일어날 수 있는 로직을 실행하는 행위들은 모두 하지 말아야 합니다.

여기서"부작용"은 *단순히* 로직 실행에 직접적인 관련이 없는 클래스, 함수, 상수 등이 *파일에 포함된 것*을 의미합니다.

"부작용"에는 다음사항은 포함되지 않습니다:
결과물 생산, 명시적인 `require`나 `include` 사용, 외부 서비스 연동, ini 설정 변경, 오류나 예외처리 발생, global 또는 static 변수 변경, 파일 읽고 쓰기, 등등.

파일에서 선언과 부작용은 다음과 같습니다;
즉, 이런 경우는 피해야 합니다:

```php
<?php
// side effect: change ini settings
ini_set('error_reporting', E_ALL);

// side effect: loads a file
include "file.php";

// side effect: generates output
echo "<html>\n";

// declaration
function foo()
{
    // function body
}
```

부작용이 없는 선언을 포함한 파일은 다음과 같습니다;
즉, 다음과 같이 사용해야합니다:

```php
<?php
// declaration
function foo()
{
    // function body
}

// conditional declaration is *not* a side effect
if (! function_exists('bar')) {
    function bar()
    {
        // function body
    }
}
```


3. 네임스페이스와 클래스명
----------------------------

네임스페이스와 클래스는 반드시 [PSR-0][]을 따라야 합니다.

이것은 각 클래스가 각자의 파일이 있고, 각 네임스페이스는 최상위 공급업체명부터 한 단계 이상의 수준에 있음을 의미합니다.

클래스 명은 반드시 `StudlyCaps`으로 선언되어야 합니다.

코드는 PHP 5.3 이상의 공식적인 네임스페이스로 작성되어야합니다.

예를들어 다음과 같습니다:

```php
<?php
// PHP 5.3 and later:
namespace Vendor\Model;

class Foo
{
}
```

PHP 5.2.x 이전에서는 클래스명 앞에 `제공업체(Vendor)_`를 붙이는 규칙으로 가짜-네임스페이스를 사용할 수 있습니다.

```php
<?php
// PHP 5.2.x and earlier:
class Vendor_Model_Foo
{
}
```

4. 클래스 상수와 properties, 메소드
-------------------------------------------

"클래스"는 모든 클래스와 인터페이스, 특성클래스를 의미합니다.

### 4.1. 상수

클래스 상수는 반드시 언더스코어로 연결된 대문자로 선언되어야 합니다.
예를들어 다음과 같습니다:

```php
<?php
namespace Vendor\Model;

class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
```

### 4.2. Properties

이 가이드에서는 추천으로 간주되는 `$StudlyCaps`, `$camelCase`, 또는 `$under_score`과 같은 property명의 사용을 의도적으로 피하고 있습니다.

무슨 이름 규칙이든 알맞은 영역에서 일관되게 적용할 수 있다. 그 영역은 제공업체나 패키지, 클래스, 메소드 수준으로 해도 좋습니다.


### 4.3. 메소드

메소드명은 반드시 `camelCase()`로 선언되어야 합니다.
