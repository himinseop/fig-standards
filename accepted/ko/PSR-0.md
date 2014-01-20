Autoloading Standard
====================

The following describes the mandatory requirements that must be adhered
to for autoloader interoperability.

필수사항
---------
* 정규화된 namesapce와 class는 반드시 `\<Vendor Name>\(<Namespace>\)*<Class Name>` 구조를 따라야 합니다.
* 각 namespace는 반드시 최상위 namespace("Vendor Name")가 있어야 합니다.
* 각 namespace는 원하는 서브namespace를 여러개 가질 수 있습니다.
* 파일을 불러올 때 각 namespace 구분자는 `DIRECTORY_SEPARATOR`로 변환됩니다.
* CLASS NAME의 각 `_`는 `DIRECTORY_SEPERATOR`로 변환됩니다. `_`는 namespace에서 특별한 의미를 갖지 않습니다.
* 파일을 불러올 때, 정규화된 namespace와 class 뒤에 `.php`를 붙입니다.
* Vendor명과 namespace, class명의 알파벳은 대소문자 조합으로 할 수 있습니다.

예제
--------

* `\Doctrine\Common\IsolatedClassLoader` => `/path/to/project/lib/vendor/Doctrine/Common/IsolatedClassLoader.php`
* `\Symfony\Core\Request` => `/path/to/project/lib/vendor/Symfony/Core/Request.php`
* `\Zend\Acl` => `/path/to/project/lib/vendor/Zend/Acl.php`
* `\Zend\Mail\Message` => `/path/to/project/lib/vendor/Zend/Mail/Message.php`

Namespaces와 Class명의 밑줄
-----------------------------------------

* `\namespace\package\Class_Name` => `/path/to/project/lib/vendor/namespace/package/Class/Name.php`
* `\namespace\package_name\Class_Name` => `/path/to/project/lib/vendor/namespace/package_name/Class/Name.php`

우리가 이곳에 구성한 표준은 자동로더를 쉽게 조작하기위해 소문자를 공통기준으로 적용합니다. 당신은 PHP 5.3 클래스들에 사용할 수 있는 splClassLoader 예제를 활용하여 시험 할 수 있습니다.

구현 예제
----------------------

아래 간단히 구현된 예제함수에는 위에서 제안된 표준이 포함되어 있습니다.

```php
<?php

function autoload($className)
{
    $className = ltrim($className, '\\');
    $fileName  = '';
    $namespace = '';
    if ($lastNsPos = strrpos($className, '\\')) {
        $namespace = substr($className, 0, $lastNsPos);
        $className = substr($className, $lastNsPos + 1);
        $fileName  = str_replace('\\', DIRECTORY_SEPARATOR, $namespace) . DIRECTORY_SEPARATOR;
    }
    $fileName .= str_replace('_', DIRECTORY_SEPARATOR, $className) . '.php';

    require $fileName;
}
```

SplClassLoader Implementation
-----------------------------

The following gist is a sample SplClassLoader implementation that can
load your classes if you follow the autoloader interoperability
standards proposed above. It is the current recommended way to load PHP
5.3 classes that follow these standards.

* [http://gist.github.com/221634](http://gist.github.com/221634)

