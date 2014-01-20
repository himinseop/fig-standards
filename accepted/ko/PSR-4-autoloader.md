# Autoloader

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](http://tools.ietf.org/html/rfc2119).


## 1. 개요

이 PSR 에서는 파일경로부터 [autoloading][] 클래스에 대한 내용을 설명합니다. 모두가 공통으로 이용할 수 있고 누구든지 [PSR-0][]를 포함한 다른 자동로딩의 내용에 추가해서 사용할 수 있습니다. 뿐만아니라 명세서에 따라 자동로드될 파일을 배치할 위치도 설명합니다.


## 2. 명세서

1. "클래스"는 클래스와 인터페이스, traits, 다른 유사한 구조를 포함합니다.

2. 정규화된 클래스명은 다음의 형태와 같습니다:

        \<NamespaceName>(\<SubNamespaceNames>)*\<ClassName>
        
    1. 정규화된 클래스명은 "vendor namespage"처럼 알려진 최상위 네임스페이스명이 있어야 합니다.
    
    2. 정규화된 클래스명은 하나 이상의 sub-namespace를 가질 수 있습니다.
    
    3. 정규화된 클래스명은 종료된 클래스명이 있어야 합니다.
    
    4. 정규화된 클래스명의 밑줄은 어떤 위치에서도 특별한 의미가 없습니다.
    
    5. 정규화된 클래스명은 알파벳 소문자와 대문자의 조합으로 이루어질 수 있습니다.
    
    6. 모든 클래스명은 대소문자를 구분해서 참조해야합니다.
        
3. 파일을 불러올 때 정규화된 클래스명은...

	1. 하나 이상의 namespace와 sub-namespace명에 인접하고있는 


3. When loading a file that corresponds to a fully qualified class name ...

    1. A contiguous series of one or more leading namespace and sub-namespace
       names, not including the leading namespace separator, in the fully
       qualified class name (a "namespace prefix") corresponds to at least one
       "base directory".

    2. The contiguous sub-namespace names after the "namespace prefix"
       correspond to a subdirectory within a "base directory", in which the
       namespace separators represent directory separators. The subdirectory
       name MUST match the case of the sub-namespace names.

    3. The terminating class name corresponds to a file name ending in `.php`.
       The file name MUST match the case of the terminating class name.

4. Autoloader implementations MUST NOT throw exceptions, MUST NOT raise errors
   of any level, and SHOULD NOT return a value.


## 3. 예제

The table below shows the corresponding file path for a given fully qualified
class name, namespace prefix, and base directory.

| Fully Qualified Class Name    | Namespace Prefix   | Base Directory           | Resulting File Path
| ----------------------------- |--------------------|--------------------------|-------------------------------------------
| \Acme\Log\Writer\File_Writer  | Acme\Log\Writer    | ./acme-log-writer/lib/   | ./acme-log-writer/lib/File_Writer.php
| \Aura\Web\Response\Status     | Aura\Web           | /path/to/aura-web/src/   | /path/to/aura-web/src/Response/Status.php
| \Symfony\Core\Request         | Symfony\Core       | ./vendor/Symfony/Core/   | ./vendor/Symfony/Core/Request.php
| \Zend\Acl                     | Zend               | /usr/includes/Zend/      | /usr/includes/Zend/Acl.php

For example implementations of autoloaders conforming to the specification,
please see the [examples file][]. Example implementations MUST NOT be regarded
as part of the specification and MAY change at any time.

[autoloading]: http://php.net/autoload
[PSR-0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[examples file]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader-examples.md
