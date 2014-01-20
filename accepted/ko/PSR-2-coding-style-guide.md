코딩 스타일 가이드
==================

이 가이드는 기본 코딩 규칙 [PSR-1][]을 바탕으로 내용을 확장합니다.

이 가이드는 다른 개발자가 코드를 살펴볼 때 인지할 수 있는 마찰을 줄이기 위한 가이드입니다. 가이드에는 PHP코드를 어떻게 작성하는가에 대한 공유된 규칙과 목표들의 집합을 나열하고있습니다.

The style rules herein are derived from commonalities among the various member
projects. When various authors collaborate across multiple projects, it helps
to have one set of guidelines to be used among all those projects. Thus, the
benefit of this guide is not in the rules themselves, but in the sharing of
those rules.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119][].

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt
[PSR-0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[PSR-1]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md


1. 개요
-----------

- 코드는 반드시 [PSR-1][]을 따릅니다.

- 코드는 스페이스 4칸 크기의 탭을 사용하고, 가독성을 위해 스페이스를 혼합할 수 있습니다.

- 한 줄의 길이는 최대 제한을 넘지 않아야 합니다; 약 120자 정도로 제한합니다; 한 줄에 80자 이내로 작성해야합니다.

- `namespace`를 선언하고 다음줄은 한 줄을 띄어서 작성합니다. 그리고, `use`를 선언한 다음줄도 한 줄을 띄어서 작성합니다.

- 클래스의 여는 괄호는 다음줄에 작성하고, 닫는 괄호는 내용 다음줄에 작성해야합니다.

- 메소드의 여는 괄호는 다음줄에 작성하고, 닫는 괄호는 내용 다음줄에 작성해야 합니다.

- 모든 properties와 메소드는 반드시 visibility를 선언해야합니다; `abstract`와 `final`은 visibility 이전에 선언해야합니다. `static`은 visibility 다음에 선언해야합니다.

- 제어문 다음에는 반드시 한칸을 띄어쓰기 해야 합니다. 메소드와 함수호출 다음은 띄어쓰기를 하지 않아야 합니다.

- 제어문의 여는 괄호는 같은 줄에 작성해야하고, 닫는 괄호는 내용 이후에 작성해야 합니다.

- 제어문 조건의 여는 괄효 다음에는 공백이 없어야 하고, 제어문 조건의 닫는 괄호 이전에도 공백이 없어야 합니다.

### 1.1. 예제

아래 예제에는 개요의 몇가지 규칙을 포함하고 있습니다:

```php
<?php
namespace Vendor\Package;

use FooInterface;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class Foo extends Bar implements FooInterface
{
    public function sampleFunction($a, $b = null)
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar()
    {
        // method body
    }
}
```

2. 일반
----------

### 2.1 기본 코딩 규칙

코드는 [PSR-1][]에 명시된 모든 규칙을 따라야 합니다.

### 2.2 파일

모든 PHP파일 라인의 끝은 Unix LF(줄바꿈)를 사용해야합니다.

모든 PHP파일은 하나의 공백라인으로 끝나야 합니다.

PHP만 사용된 파일에서는 종료태그 `?>`는 사용하지 않아야 합니다.

### 2.3. Lines

한 줄의 길이는 최대 제한길이를 넘지 않아야 합니다.

The soft limit on line length MUST be 120 characters; automated style checkers
MUST warn but MUST NOT error at the soft limit.

한 줄은 80자를 넘지 않아야 합니다; 그보다 큰 라인은 80자 이하의 여러 후속라인으로 나눠져야합니다.

공백이 아닌 줄의 끝에는 반드시 여백이 없어야 합니다.

라인의 공백은 가독성을 높이거나 들여쓰기 위한 블럭일 수 있습니다.

그런 공백 라인은 한 줄에 하나 이상 사용하지 않아야 합니다.

### 2.4. Indenting

코드는 스페이스 4칸 크기의 탭을 사용하고, 가독성을 위해 스페이스를 혼합할 수 있습니다.

### 2.5. Keywords와 True/False/Null

PHP [keywords][]는 반드시 소문자로 사용해야 합니다.

PHP의 `true`와 `false`, `null`은 반드시 소문자로 사용해야 합니다.

[keywords]: http://php.net/manual/en/reserved.keywords.php



3. Namespace와 Use 선언
---------------------------------

`namespace`를 선언한 다음에는 한 줄을 띄어써야 합니다.

모든 `use`는 `namesapge` 이후에 선언해야합니다.

`use`는 선언할때마다 하나씩 사용해야 합니다.  

`use` 블럭 다음에는 한 줄을 띄어써야 합니다.

예를 들어 다음과 같습니다:

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

// ... additional PHP code ...

```


4. 클래스와 Properties, 메소드
-----------------------------------

"클래스"는 클래스와 interfaces, traits을 모두 포함합니다.

### 4.1. Extends and Implements

`extends`와 `implements`는 클래스명과 같은 줄에서 선언되어야 합니다.

클래스의 여는 괄호는 선언문 다음줄에 위치해야 합니다; 닫는 괄호는 내용 다음줄에 위치해야 합니다.

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements \ArrayAccess, \Countable
{
    // constants, properties, methods
}
```

`implements`의 목록은 한단계 들여쓰고 여러 줄에 걸쳐 나눠질 수 있습니다. 이렇게 작성했을 때 목록의 첫번째 항목은 클래스 선언문 다음줄에 작성되어야하고 라인마다 하나의 인터페이스만 선언되어야 합니다.

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // constants, properties, methods
}
```

### 4.2. Properties

Visibility는 모든 properties에 반드시 선언되어야 합니다.

`var`는 property 선언에 사용하지 말아야 합니다.

한번에 하나의 property만 선언되어야 합니다.
There MUST NOT be more than one property declared per statement.

protected나 private으로 지정하기 위해 property명을 하나의 밑줄로 시작하면 안됩니다.

property 선언은 다음과 같습니다.

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public $foo = null;
}
```

### 4.3. 메소드

visibility는 모든 메소드에 선언되어야 합니다.

protected나 private으로 지정하기 위해 메소드명을 단일밑줄로 시작해서는 안됩니다.

메소드명 뒤에 공백을 넣고 선언하면 안됩니다. 메소드를 여는 괄호는 다음줄에 있어야하고, 닫는 괄호는 내용이 끝난 다음줄에 위치해야 합니다. 여는괄호 다음과 닫는괄호 전에는 공백이 없어야 합니다.

메소드 선언은 다음과 같습니다. 괄호와 콤마, 공백, 괄호의 위치를 주목해주세요:

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```    

### 4.4. 메소드 독립변수 (Method Argument)

독립변수를 나열할 때 콤마 이전에는 공백이 없어야 하고, 콤마 이후에는 공백이 하나 추가되어야 합니다.

기본값을 가진 메소드 독립변수는 독립변수 목록의 끝에 위치해야 합니다.

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function foo($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```

독립변수 목록은 한단계 들여쓰고 여러 줄에 걸쳐 분할될수도 있습니다. 이 때, 첫번째 항목은 다음줄에 위치해야하고 한 줄에 하나의 변수만 위치해야합니다.

독립변수가 여러 줄에 걸쳐 작성된 경우, 변수를 닫는 소괄호와 내용을 시작하는 중괄호는 중간에 한칸의 공백을 두고 같은 줄에 배치해야 합니다.

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = []
    ) {
        // method body
    }
}
```

### 4.5. `abstract`, `final`, and `static`

`abstract`과 `final`는 visibility 이전에 선언해야합니다.

`static`은 visibility 뒤에 선언해야 합니다.
When present, the `static` declaration MUST come after the visibility
declaration.

```php
<?php
namespace Vendor\Package;

abstract class ClassName
{
    protected static $foo;

    abstract protected function zim();

    final public static function bar()
    {
        // method body
    }
}
```

### 4.6. 메소드와 함수 호출

메소드나 함수를 호출할 때, 메소드명이나 함수명과 여는 괄호 사이에는 공백이 없어야 합니다. 여는 괄호 이후나 닫는괄호 이전에도 공백이 없어야 합니다. 독립변수를 나열할 때에는 각 콤마 이전에는 공백이 없어야 하고 콤마 이후에는 공백을 사용해야 합니다.

```php
<?php
bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);
```

독립변수를 나열할 때 한단계 들여쓴 연속된 여러 줄에 걸쳐 나눠질 수도 있습니다. 이 때, 첫번째 항목은 다음줄에 위치해야하고 한 줄에는 하나의 독립변수만 위치해야 합니다.

```php
<?php
$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
);
```

5. 제어문
---------------------

제어문의 일반적인 스타일 규칙은 다음과 같습니다:

- 제어문 뒤에는 스페이스 한 칸이 들어갑니다.
- 조건절을 여는 괄호이후에는 공백을 넣지 말아야 합니다.
- 조건절을 닫는 괄호이전에는 공백을 넣지 말아야 합니다.
- 조건절을 닫는 소괄호와 제어문을 여는 중괄호 사이에는 스페이스 한 칸이 들어가야합니다.
- 제어문 내용은 한단계 들여써야 합니다.
- 제어문 종료 괄호는 내용 다음 줄에 위치해야 합니다.

각 제어문의 내용은 괄호로 감싸야 합니다. 이 표준 규칙은 본문에 새로운 라인을 추가할 때 오류가 발생할 수 있는 가능성을 줄일 수 있습니다.


### 5.1. `if`, `elseif`, `else`

`if` 구조는 다음과 같습니다. 조건절 괄호와 공백, 제어문 괄호에 주목해주세요; 그리고 `else`와 `elseif`는 내용 이전줄에 닫는 중괄호와 같은 위치에 있습니다.

```php
<?php
if ($expr1) {
    // if body
} elseif ($expr2) {
    // elseif body
} else {
    // else body;
}
```

`else if` 대신 `elseif`를 사용해야 합니다. 모든 제어문은 하나의 단어처럼 보여져야 합니다.


### 5.2. `switch`, `case`

`switch`구조의 형태는 다음과 같습니다. 조건절 소괄호와 공백, 제어문 중괄호의 위치에 주목해주세요. `case`문은 `switch`보다 한단계 들여써야하고, `break`는 `case`내용과 같은 레벨로 들여써야 합니다. `case`내용이 있고 의도적으로 통화하는 경우 `//no break` 주석을 반드시 작성해야합니다.

```php
<?php
switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
```


### 5.3. `while`, `do while`

`while`문의 형태는 다음과 같습니다. 조건절 괄호와 공백, 제어문 괄호의 위치에 주목해 주세요.

```php
<?php
while ($expr) {
    // structure body
}
```

이와 비슷하게 `do while`문의 형태는 다음과 같습니다. 조건절 괄호와 공백, 제어문 괄호의 위치에 주목해 주세요.

```php
<?php
do {
    // structure body;
} while ($expr);
```

### 5.4. `for`

`for`문의 형태는 다음과 같습니다. 조건절 괄호와 공백, 제어문 괄호의 위치에 주목해 주세요.

```php
<?php
for ($i = 0; $i < 10; $i++) {
    // for body
}
```

### 5.5. `foreach`

`foreach`문의 형태는 다음과 같습니다. 조건절 괄호와 공백, 제어문 괄호의 위치에 주목해 주세요.

```php
<?php
foreach ($iterable as $key => $value) {
    // foreach body
}
```

### 5.6. `try`, `catch`

`try catch` 블럭의 형태는 다음과 같습니다. 조건절 괄호와 공백, 제어문 괄호의 위치에 주목해 주세요.

```php
<?php
try {
    // try body
} catch (FirstExceptionType $e) {
    // catch body
} catch (OtherExceptionType $e) {
    // catch body
}
```

6. 클로져
-----------

클로져에는 `function` 이후에 공백을 추가해야하고 `use` 앞뒤에 공백을 추가해야합니다.

여는 괄호는 같은 줄에 위치해야하고, 닫는 괄호는 내용이 끝난 다음줄에 위치해야합니다.

독립변수의 목록이나 변수의 목록을 감싸는 괄호는 여는괄호 이후와 닫는괄호 이전에 공백이 포함되지 말아야 합니다.

독립변수나 변수를 나열할 때 콤마이전에는 공백을 추가하지 않아야 하고, 콤마 이후에는 스페이스 한 칸을 추가해야 합니다.

기본값을 가진 클로져 독립변수는 독립변수 목록의 마지막에 배치해야 합니다.

클로져 선언의 형태는 다음과 같습니다. 조건절 괄호와 콤마, 공백, 제어문 괄호의 위치에 주목해 주세요:

```php
<?php
$closureWithArgs = function ($arg1, $arg2) {
    // body
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // body
};
```

독립변수 목록과 변수 목록은 한단계 들여쓴 연속된 여러 줄에 걸쳐 나눠질 수 있습니다. 이 때, 첫번째 항목은 다음줄에 위치해야하고, 한 줄에는 하나의 독립변수나 하나의 변수만 위치해야 합니다.

여러줄로 나눠진 목록(독립변수나 변수의 유무에 관계없이)이 종료될 때 닫는 소괄호와 여는 중괄호 사이에는 한 칸의 스페이스를 두고 같은 줄에 위치해야 합니다.

독립변수와 변수가 여러줄에 걸쳐 나눠진 클로져와 변수가 없는 클로져의 예제는 다음과 같습니다.

```php
<?php
$longArgs_noVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) {
   // body
};

$noArgs_longVars = function () use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_longVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_shortVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use ($var1) {
   // body
};

$shortArgs_longVars = function ($arg) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};
```

뿐만 아니라 함수나 메소드를 호출하는 독립변수에서 직접 클로져를 사용했을 때의 형태를 주목해주세요.

```php
<?php
$foo->bar(
    $arg1,
    function ($arg2) use ($var1) {
        // body
    },
    $arg3
);
```


7. 결론
--------------

이 가이드의 스타일과 예제의 많은 부분들은 의도적으로 삭제되었습니다. 아래의 내용들이 그 중 일부입니다: 

- 전역 변수와 전역 상수 선언

- 함수 선언

- 연산자와 할당

- 행간 정렬

- 주석과 문서 블록

- 클래스명의 접두사와 접미사

- 모범 사례

앞으로 권장사항들은 스타일과 예제에 다른 요소를 더하거나 권장사항들을 해결하기 위해 이 문서를 수정하고 확장할 수 있습니다. 



Appendix A. Survey
------------------

In writing this style guide, the group took a survey of member projects to
determine common practices.  The survey is retained herein for posterity.

### A.1. Survey Data

    url,http://www.horde.org/apps/horde/docs/CODING_STANDARDS,http://pear.php.net/manual/en/standards.php,http://solarphp.com/manual/appendix-standards.style,http://framework.zend.com/manual/en/coding-standard.html,http://symfony.com/doc/2.0/contributing/code/standards.html,http://www.ppi.io/docs/coding-standards.html,https://github.com/ezsystems/ezp-next/wiki/codingstandards,http://book.cakephp.org/2.0/en/contributing/cakephp-coding-conventions.html,https://github.com/UnionOfRAD/lithium/wiki/Spec%3A-Coding,http://drupal.org/coding-standards,http://code.google.com/p/sabredav/,http://area51.phpbb.com/docs/31x/coding-guidelines.html,https://docs.google.com/a/zikula.org/document/edit?authkey=CPCU0Us&hgd=1&id=1fcqb93Sn-hR9c0mkN6m_tyWnmEvoswKBtSc0tKkZmJA,http://www.chisimba.com,n/a,https://github.com/Respect/project-info/blob/master/coding-standards-sample.php,n/a,Object Calisthenics for PHP,http://doc.nette.org/en/coding-standard,http://flow3.typo3.org,https://github.com/propelorm/Propel2/wiki/Coding-Standards,http://developer.joomla.org/coding-standards.html
    voting,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,no,no,no,?,yes,no,yes
    indent_type,4,4,4,4,4,tab,4,tab,tab,2,4,tab,4,4,4,4,4,4,tab,tab,4,tab
    line_length_limit_soft,75,75,75,75,no,85,120,120,80,80,80,no,100,80,80,?,?,120,80,120,no,150
    line_length_limit_hard,85,85,85,85,no,no,no,no,100,?,no,no,no,100,100,?,120,120,no,no,no,no
    class_names,studly,studly,studly,studly,studly,studly,studly,studly,studly,studly,studly,lower_under,studly,lower,studly,studly,studly,studly,?,studly,studly,studly
    class_brace_line,next,next,next,next,next,same,next,same,same,same,same,next,next,next,next,next,next,next,next,same,next,next
    constant_names,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper
    true_false_null,lower,lower,lower,lower,lower,lower,lower,lower,lower,upper,lower,lower,lower,upper,lower,lower,lower,lower,lower,upper,lower,lower
    method_names,camel,camel,camel,camel,camel,camel,camel,camel,camel,camel,camel,lower_under,camel,camel,camel,camel,camel,camel,camel,camel,camel,camel
    method_brace_line,next,next,next,next,next,same,next,same,same,same,same,next,next,same,next,next,next,next,next,same,next,next
    control_brace_line,same,same,same,same,same,same,next,same,same,same,same,next,same,same,next,same,same,same,same,same,same,next
    control_space_after,yes,yes,yes,yes,yes,no,yes,yes,yes,yes,no,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes
    always_use_control_braces,yes,yes,yes,yes,yes,yes,no,yes,yes,yes,no,yes,yes,yes,yes,no,yes,yes,yes,yes,yes,yes
    else_elseif_line,same,same,same,same,same,same,next,same,same,next,same,next,same,next,next,same,same,same,same,same,same,next
    case_break_indent_from_switch,0/1,0/1,0/1,1/2,1/2,1/2,1/2,1/1,1/1,1/2,1/2,1/1,1/2,1/2,1/2,1/2,1/2,1/2,0/1,1/1,1/2,1/2
    function_space_after,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no
    closing_php_tag_required,no,no,no,no,no,no,no,no,yes,no,no,no,no,yes,no,no,no,no,no,yes,no,no
    line_endings,LF,LF,LF,LF,LF,LF,LF,LF,?,LF,?,LF,LF,LF,LF,?,,LF,?,LF,LF,LF
    static_or_visibility_first,static,?,static,either,either,either,visibility,visibility,visibility,either,static,either,?,visibility,?,?,either,either,visibility,visibility,static,?
    control_space_parens,no,no,no,no,no,no,yes,no,no,no,no,no,no,yes,?,no,no,no,no,no,no,no
    blank_line_after_php,no,no,no,no,yes,no,no,no,no,yes,yes,no,no,yes,?,yes,yes,no,yes,no,yes,no
    class_method_control_brace,next/next/same,next/next/same,next/next/same,next/next/same,next/next/same,same/same/same,next/next/next,same/same/same,same/same/same,same/same/same,same/same/same,next/next/next,next/next/same,next/same/same,next/next/next,next/next/same,next/next/same,next/next/same,next/next/same,same/same/same,next/next/same,next/next/next

### A.2. Survey Legend

`indent_type`:
The type of indenting. `tab` = "Use a tab", `2` or `4` = "number of spaces"

`line_length_limit_soft`:
The "soft" line length limit, in characters. `?` = not discernible or no response, `no` means no limit.

`line_length_limit_hard`:
The "hard" line length limit, in characters. `?` = not discernible or no response, `no` means no limit.

`class_names`:
How classes are named. `lower` = lowercase only, `lower_under` = lowercase with underscore separators, `studly` = StudlyCase.

`class_brace_line`:
Does the opening brace for a class go on the `same` line as the class keyword, or on the `next` line after it?

`constant_names`:
How are class constants named? `upper` = Uppercase with underscore separators.

`true_false_null`:
Are the `true`, `false`, and `null` keywords spelled as all `lower` case, or all `upper` case?

`method_names`:
How are methods named? `camel` = `camelCase`, `lower_under` = lowercase with underscore separators.

`method_brace_line`:
Does the opening brace for a method go on the `same` line as the method name, or on the `next` line?

`control_brace_line`:
Does the opening brace for a control structure go on the `same` line, or on the `next` line?

`control_space_after`:
Is there a space after the control structure keyword?

`always_use_control_braces`:
Do control structures always use braces?

`else_elseif_line`:
When using `else` or `elseif`, does it go on the `same` line as the previous closing brace, or does it go on the `next` line?

`case_break_indent_from_switch`:
How many times are `case` and `break` indented from an opening `switch` statement?

`function_space_after`:
Do function calls have a space after the function name and before the opening parenthesis?

`closing_php_tag_required`:
In files containing only PHP, is the closing `?>` tag required?

`line_endings`:
What type of line ending is used?

`static_or_visibility_first`:
When declaring a method, does `static` come first, or does the visibility come first?

`control_space_parens`:
In a control structure expression, is there a space after the opening parenthesis and a space before the closing parenthesis? `yes` = `if ( $expr )`, `no` = `if ($expr)`.

`blank_line_after_php`:
Is there a blank line after the opening PHP tag?

`class_method_control_brace`:
A summary of what line the opening braces go on for classes, methods, and control structures.

### A.3. Survey Results

    indent_type:
        tab: 7
        2: 1
        4: 14
    line_length_limit_soft:
        ?: 2
        no: 3
        75: 4
        80: 6
        85: 1
        100: 1
        120: 4
        150: 1
    line_length_limit_hard:
        ?: 2
        no: 11
        85: 4
        100: 3
        120: 2
    class_names:
        ?: 1
        lower: 1
        lower_under: 1
        studly: 19
    class_brace_line:
        next: 16
        same: 6
    constant_names:
        upper: 22
    true_false_null:
        lower: 19
        upper: 3
    method_names:
        camel: 21
        lower_under: 1
    method_brace_line:
        next: 15
        same: 7
    control_brace_line:
        next: 4
        same: 18
    control_space_after:
        no: 2
        yes: 20
    always_use_control_braces:
        no: 3
        yes: 19
    else_elseif_line:
        next: 6
        same: 16
    case_break_indent_from_switch:
        0/1: 4
        1/1: 4
        1/2: 14
    function_space_after:
        no: 22
    closing_php_tag_required:
        no: 19
        yes: 3
    line_endings:
        ?: 5
        LF: 17
    static_or_visibility_first:
        ?: 5
        either: 7
        static: 4
        visibility: 6
    control_space_parens:
        ?: 1
        no: 19
        yes: 2
    blank_line_after_php:
        ?: 1
        no: 13
        yes: 8
    class_method_control_brace:
        next/next/next: 4
        next/next/same: 11
        next/same/same: 1
        same/same/same: 6
