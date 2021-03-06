# php

http://tcpschool.com/php/intro

## 스타일

```php
<?php
    
?>
```

## 문법

* 명령문은 세미콜론(;)으로 끝남
  * 코드가 종료되면 자동으로 세미콜론을 적용해주기 때문에 마지막 명령문의 세미콜론은 생략가능
* php 크도 영역을 나타내는 종료 태그 생략가능

## PHP 표현식(expressions)

* 가장 중요한 구성요소
* 모든것이 값을 갖는다는 의미
* 변수, 상수, 함수, 제어문, 명령문 등 거의 모든것이 표현식에 속함

## 변수(variable)

* 데이터를 저장할 수 있는 메모리 공간

* 스크립트가 실행되는 동안 저장한 데이터 변경 가능

* type을 따로 명시하지 않음

* 해당 변수에 대입하는 값에 따라 자동으로 결정됨

  ```php
  $var = 10; // 정수
  $var = 3.14; // 실수
  $var = "PHP"; // 문자열
  ```

### 변수 이름

* 영문 대소문자, 숫자, 언더스코어(_)로 구성됨
* 숫자로 시작 불가(숫자와 구분하기 위함)
* 공백 포함 불가
* this 사용 불가
* 대소문자 구분함

### 문자열 내에서 변수를 사용하는 경우

* 해당 변수에 저장된 값으로 자동 변환해줌

  ```php
  $var = 20;
      
  echo "$var"; // 20
  echo "{$var}"; // 20
  ```

* 변수가 문자열 중간에 있는 경우 변수 이름을 구분해주지 않으면 `$`를 기준으로 오른쪽의 모든 문자열을 변수명으로 인지함

  ```php
  $var = 20;
  
  echo "변수 \$var : $var"; // 변수 $var : 20
  echo "변수 \$var에 저장된 값은 $var입니다."; // 변수 $var에 저장된 값은 .
  // error 변수 : $var입니다
  echo "변수 \$var에 저장된 값은 {$var}입니다."; // 변수 $var에 저장된 값은 20입니다.
  ```

* 변수이름을 명시하기 위해 중괄호({})를 사용함

### 변수의 선언 및 초기화

* 변수를 선언해주지 않아도 사용가능함

* 초기화되지 않은 변수는 해당 변수가 참조되거나 사용되는 위치에 따라 자동으로 초기화 됨

* 기본값

  | type                                | 기본값    |
  | ----------------------------------- | --------- |
  | boolean                             | False     |
  | integer                             | 0         |
  | float                               | 0.0       |
  | string                              | 빈 문자열 |
  | array                               | 빈 배열   |
  | 아직 어떠한 값도 대입되지 않은 변수 | NULL      |

  ```php
  var_dump($var); // NULL // 타입을 알 수 없는 변수
  echo $bool ? "true" : "false"; // false
  $int += 20; var_dump($int); // int(20)
  $float += 3.14; var_dump($float); // float(3.14)
  $str .= "php"; var_dump($str); // string(3) "php"
  $arr[3] = "3번째 배열 요소"; var_dump($arr);
  // array(1) {
  // 	[3]=>
  //  string(21) "3번째 배열 요소"
  // }
  ```

### 변수의 종류

* 지역변수(local variable)

  * 함수 내부에 선언된 변수
  * 함수 내부에서만 접근 가능
  * 함수의 호출 종료되면 메모리에서 제거됨

  ```php
  function localFunction() {
      $var = 20;
      echo "함수 내부에서 호출한 지역변수 : {$var}";
  }
  localFunction(); // 함수 내부에서 호출한 지역변수 : 20
  echo "함수 외부에서 호출한 지역변수 : {$var}"; // 함수 외부에서 호출한 지역변수 : 
  ```

* 전역변수(global variable)

  * 함수 밖에서 선언된 변수
  * 함수 밖에서만 접근 가능
  * 함수 내부에서 사용 시 `global`키워드 사용

  ```php
  $var = 20; // 전역변수
  function globalFunction() {
      echo "함수 내부에서 호출한 전역변수 \$var : {$var}";
      // 함수 내부에서 호출한 전역변수 $var
      global $var; // 함수 내에서 사용할 전역변수 명시
      echo "함수 내부에서 호출한 전역변수 \$var : {$var}";
      // 함수 내부에서 호출한 전역변수 $var : 20
  }
  globalFunction();
  echo "함수 밖에서 호출된 전역변수 \$var : {$var}";
  // 함수 밖에서 호출된 전역변수 $var : 20
  ```

  * 전역변수는 `$GLOBALS`배열에 저장됨
  * `$GLOBALS`배열의 인덱스는 변수이름
  * `$GLOBALS`배열은 함수 내/외부에서 접근 가능하며, 값 변경도 가능함

* 슈퍼글로벌(superglobal)

  * 미리 정의된 전역 변수

  * 특별한 선언 없이 사용 가능

  * 종류

    ```php
    $GLOBALS
    $_SERVER
    $_GET
    $_POST
    $_FILES
    $_COOKIE
    $_SESSION
    $_REQUEST
    $_ENV
    ```

* 정적 변수(static variable)

  * 함수 내부에서 static 키워드로 선언한 변수
  * 함수 내부에서만 접근 가능(지역변수 특징)
  * 함수의 호출이 종료되어도 메모리상에서 사라지지 않음

  ```php
  function counter() {
      static $count = 0;
      echo "함수 내부에서 호출한 static 변수 count의 값은 {$count}입니다.";
      $count++;
  }
  counter(); // 함수 내부에서 호출한 static 변수 count의 값은 0입니다.
  counter(); // 함수 내부에서 호출한 static 변수 count의 값은 1입니다.
  counter(); // 함수 내부에서 호출한 static 변수 count의 값은 2입니다.
  ```

## 상수(constant)

* 데이터를 저장할 수 있는 메모리 공간
* 스크립트가 실행되는 동안 데이터를 변경하거나 해제(undefined)할 수 없음
* 함수 내부에서 선언되어도 외부에서 사용 가능

### `define()`

* 상수 선언 함수

* 원형

  ```php
  define(상수이름, 상수값, 대소문자구분여부)
  ```

* 값

  * true : 대소문자를 구분하지 않음
  * false : 대소문자를 구분함 (기본값)

  ```php
  define("VAR","HELLO PHP"); // 대소문자 구분함(기본설정)
  echo PHP; // HELLO PHP
  echo php; // php
  define("VAR","HELLO PHP"); // 대소문자 구분하지 않음
  echo PHP; // HELLO PHP
  echo php; // HELLO PHP
  ```

* 상수가 선언되기 이전의 스크립트 영역에서는 참조불가능

  ```php
  function constFunction() {
      echo PHP; // PHP
      define("PHP", "HELLO PHP");
      echo PHP; // HELLO PHP
  }
  constFunction();
  echo PHP; // HELLO PHP
  ```

### 마법 상수(magic constants)

* 대소문자 구별하지 않음

  | 상수 이름         | 설명                                                         |
  | ----------------- | ------------------------------------------------------------ |
  | \_\_LINE\_\_      | 파일의 현재 줄 번호를 반환함                                 |
  | \_\_FILE\_\_      | 파일의 전체 경로와 이름을 반환함<br>include 내부에서 사용할 경우 include된 파일명을 반환함 |
  | \_\_DIR\_\_       | 파일의 디렉터리를 반환함<br>포함한 파일 안에서 사용할 경우 포함된 파일의 디렉터리를 반환함<br>dirname(\_\_FILE\_\_)과 같은 결과를 반환함 |
  | \_\_FUNCTION\_\_  | 함수의 이름을 반환함                                         |
  | \_\_CLASS\_\_     | 클래스의 이름을 반환함. 클래스 이름은 대소문자 구분함        |
  | \_\_TRAIT\_\_     | trait의 이름을 반환함<br>trait의 이름은 trait를 선언한 namespace를 포함함 |
  | \_\_METHOD\_\_    | 클래스의 메소드 이름을 반환함                                |
  | \_\_NAMESPACE\_\_ | 현재 namespace의 이름을 반환함                               |

  ```php
  function magicConstantFunction(){
      echo __LINE__; // 파일의 현재 줄 번호를 반환함
      echo __FUNCTION__; // 함수의 이름을 반환함
      echo __METHOD__; // 클래스의 메소드 이름을 반환함
  }
  magicConstantFunction(); // 3magicConstantFunctionmagicConstantFunction
  ```

### `get_defined_constants()`

* 미리 정의된 모든 상수를 위 함수를 통해 알 수 있음

  ```php
  print_r(get_defined_constants())
  ```

  * 참고
    * `PHP_INT_SIZE` : 정수 타입의 크기
    * `PHP_INT_MAX` : 정수 타입이 표현할 수 있는 가장 큰 수
    * `INF` : 무한(infinite)

## 타입(data type)

* 프로그램에서 다룰 수 있는 값의 종류

### 기본타입

* boolean

  * `true`와 `false`을 표현함
  * 대소문자 구별하지 않음
  * `false`로 인식되는 값
    * boolean : false
    * int : 0
    * float : 0.0
    * 빈 문자열과 문자열 "0"
    * 빈 배열
    * NULL
  * `false`로 인식되는 값을 제외한 음수를 포함한 모든 값은 `true`로 인식됨

  ```php
  var_dump((bool) false);   // bool(false)
  var_dump((bool) "false"); // bool(true)
  var_dump((bool) 0);       // bool(false)
  var_dump((bool) -100);    // bool(true)
  var_dump((bool) 0.0);     // bool(false)
  var_dump((bool) "");      // bool(false)
  var_dump((bool) "0");     // bool(false)
  var_dump((bool) array()); // bool(false)
  var_dump((bool) null);    // bool(false)
  ```

* int

  * 부호를 가지는 소수부가 없는 수

  * 표현범위

    * 운영체제에 따라 달라짐
    * 64비트 운영체제 기준 : -2^63^ ~ (2^63^ -1) 사이의 값

  * 부호가 없는 정수(unsigned integer)는 지원하지 않음

  * 10진수, 8진수(0으로 시작), 16진수(0x로 시작)로 표현 가능

  * 변수에 정수의 최대 범위를 넘는 값이 대입되면, 자동으로 실수형(float)로 인식됨

    ```php
    echo "integer 타입의 크기는 ".PHP_INT_SIZE."바이트 입니다.";
    echo "integer 타입이 표현할 수 있는 가장 큰 수는 ".PHP_INT_MAX." 입니다.";
    $int_01 = 100;
    $int_02 = 9223372036854775807; // integer가 표현할 수 있는 범위를 넘지 않는 값을 대입함.
    $int_03 = 9223372036854775808; // integer가 표현할 수 있는 범위를 넘는 값을 대입함.
    var_dump($int_01); // int(100)
    var_dump($int_02); // int(9223372036854775807)
    var_dump($int_03); // float(9.2233720368548E+18)
    ```

* float

  * 소수부나 지수부를 가지는 수
  * 정수보다 더 넓은 표현 범위를 가짐
  * 표현범위
    * 운영체제에 따라 달라짐
    * 약 ~ 1.8e307 까지 표현 가능
  * 컴퓨터에서 실수를 표현하는 방식은 반드시 오차가 존재하는 한계를 지니므로, 실수형끼리 직접 값을 비교하는 것은 피하는 것이 좋음
  * `e` 지수 표현과`E`지수 표현 모두 가능
  * 변수에 실수의 최대 범위를 넘는 값이 대입되면, 자동으로 미리 정의된 상수인 `INF`로 인식됨

* string

  * 일련의 연속된 문자(character)들의 집합

  * 문자열 리터럴은 큰따옴표("") 또는 작은따옴표('')로 감싸서 표현함

  * 아스키(ASCII) 인코딩 환경에서 영문자는 한 글자당 1byte, 한글은 한 글자당 2byte로 표현됨

  * UTF-8 인코딩 환경에서는 영문자는 한 글자당 1byte, 한글은 한 문자당 3byte로 표현됨

    ```php
    $str_01 = "PHP";
    $str_02 = "안녕";
    
    echo strlen($str_01); // 3
    echo strlen($str_02); // 6
    ```

* array

  * 한 쌍의 키(key)와 값(value)로 이루어진 맵(map)으로 구성되는 순서가 있는 집합

  * map의 key값

    * 정수와 문자열만 가능

    * 배열과 객체는 배열의 키값으로 사용할 수 없음

    * 하나의 배열에 두 가지 키 값을 같이 사용할 수 있음

    * 정수와 문자열 이외에 다른 타입의 값을 키 값으로 사용하는 경우

      * true => 1, false => 0 으로 자동 타입 변환됨

      * 유효한 숫자로만 이루어진 문자열은 정수나 실수로 자동 타입 변환됨

        "1" 과 1은 같은 값 => 둘 다 선언된 경우 나중에 선언된 값만 남음

      * 실수는 소수 부분이 제거되고, 정수로 자동 타입 변환됨

      * NULL은 빈 문자열("")로 자동 타입 변환됨

    * 같은 key값으로 여러번 map을 선언한 경우, key에 해당하는 value를 계속 덮어써서 맨 마지막에 선언된 값만을 저장함

    ```php
    $arr = array(
        1 => "첫 번째 값",   // PHP의 배열에서 키값의 1과 "1"은 같은 값을 나타냄.
        "1" => "두 번째 값", // 같은 키값을 사용하여 두 번 선언했기 때문에 나중에 선언된 "두 번째 값"만 남게됨.
        10 => "세 번째 값",
        -10 => "네 번째 값"
    );
    var_dump($arr);
    //array(3) {
    //  [1]=>
    //  string(14) "두 번째 값"
    //  [10]=>
    //  string(14) "세 번째 값"
    //  [-10]=>
    //  string(14) "네 번째 값"
    //}
    echo $arr[1]; // 두 번째 값
    echo $arr["1"]; // 두 번째 값
    echo $arr[10]; // 세 번째 값
    echo $arr[-10]; // 네 번째 값
    ```

* object

  * 클래스의 인스턴스(instance)를 저장하기 위한 타입

  * properties와 methods를 포함할 수 있음

    ```php
    class ObjectClass {
        function ObjectClass() {
            $this->obj_01 = "PHP";
            $this->obj_02 = "MySQL";
        }
    }
    $var = new ObjectClass; // 객체 생성
    echo $var->obj_01;  // 객체의 속성 접근 // PHP
    echo $var->obj_02; // 객체의 속성 접근 // MySQL
    ```

* resource

  * php 외부에 존재하는 외부 자원
  * 데이터베이스 함수 등에서 데이터베이스 연결 등을 반환할 때 사용

* NULL

  * 오직 한 가지 값(NULL 상수)만을 가질 수 있는 특별한 타입

  * NULL타입의 변수 : 아직 어떠한 값도 대입되지 않은 변수

  * 초기화하지 않은 변수, 삭제된 변수, 존재하지 않는 변수를 찹조할 경우 NULL을 반환함

    ```php
    $var1;
    var_dump($var1); // 초기화되지 않은 변수를 참조 // NULL
    
    $var1 = 100;     // $var_01 변수를 초기화함.
    var_dump($var1); // int(100)
    
    unset($var2);    // $var_01 변수를 삭제함.
    var_dump($var2); // 삭제된 변수를 참조 // NULL
    ```

### 타입변환

* 자동 타입 변환(type juggling)

  * 타입이 상황에 따라 자동으로 변환되는 것

  * php의 타입강도(type strength)는 매우 약하며, type이 동적으로 결정됨

    ```php
    $var = "문자열"; // string
    $var = 10; // int
    $var = 3.14; // float
    ```

* 강제 타입 변환(type casting)

  * 타입 캐스트 연산자 괄호(`()`)를 사용하여 수행함

  * 변환시키고자 하는 데이터나 변수의 앞에 괄호를 붙이고, 그 괄호 안에 변환할 타입을 적으면 됨

    ```php
    $var1 = 10;
    var_dump($var1);           // int(10)
    $var2 = (boolean) $var1;
    var_dump($var2);           // bool(true)
    $var3 = 0;
    var_dump($var3);           // int(0)
    $var4 = (boolean) $var3;
    var_dump($var4);           // bool(false)
    ```

* 가변 변수(variable variables)

  * 변수 이름을 동적으로 바꿈

  * 해당 변수의 값을  또다른 변수의 이름으로 취급함

  * `$`기호를 사용하여 변수 이름을 유동적으로 설정하거나 사용 가능함

    ```php
    $PHP = "HTML";
    $HTML = "CSS";
    $CSS = "JavaScript";
    $JavaScript = "Ajax";
    $Ajax = "PHP";  
    
     
    echo $PHP;       // HTML // HTML
    echo $$PHP;      // $HTML -> CSS // CSS
    echo $$$PHP;     // $$HTML -> $CSS -> JavaScript // JavaScript
    echo $$$$PHP;    // $$$HTML -> $$CSS -> $JavaScript -> Ajax // Ajax
    echo $$$$$PHP;   // $$$$HTML -> $$$CSS -> $$JavaScript -> $Ajax -> PHP // PHP
    echo $$$$$$PHP;  // $$$$$HTML -> $$$$CSS -> $$$JavaScript -> $$Ajax -> $PHP -> HTML // HTML
    echo $$$$$$$PHP; // $$$$$$HTML -> $$$$$CSS -> $$$$JavaScript -> $$$Ajax -> $$PHP -> $HTML -> CSS // CSS
    ```



## 함수(function)

* 전역 범위(global scope)를 가짐
  * 같은 스크립트 내에서는 정의된 위치와 상관없이 호출 가능
* 오버로딩을 지원하지 않음
  * 이미 선언된 함수를 다시 선언할 수 없음

### 정의

```php
function [FUNCTIONNAME]([PARAMETER1], [PARAMETER2], ...)
{
    함수가 호출되었을 때 실행될 코드;
}
```

* `function`로 함수의 정의 시작
* 함수의 이름, 매개변수, 블록({}) 사이에 들어갈 코드 명시

### 장점

* 반복적인 코드작성을 줄일 수 있음
* 모듈화로 인하여 코드의 가독성이 좋아짐
* 유지보수가 용이함

### 구조

```php
function [FUNCTIONNAME]($[PARAMETER1], $[PARAMETER2], ...)
{
    함수가 호출 되었을 때 실행될 코드;
}

// 함수 호출
[FUNCTIONNAME]([ARGUMENT1], [ARGUMENT2], ...)
```

* `[FUNCTIONNAME]` : 함수를 구분하는 식별자(identifier)
* `[PARAMETER]` : 함수를 호출할 때 인수로 전달된 값을 함수 내부에서 사용할 수 있도록 해주는 변수
  * 인수로 전달받은 값을 함수에서 사용
  * 여러 개를 가질 수 있으며, 쉼표(,)를 사용하여 구분
* `[ARGUMENT]` : 함수가 호출될 때 함수로 값을 전달해주는 변수
* `{}` : 함수가 호출되면 중괄호 안의 코드가 실행됨

### 함수 이름

* 문자와 숫자, 언더스코어(_)만 사용 가능
* 숫자로 시작 불가
* 독립적인 이름 가짐(중복 불가)
* 대소문자 구별하지 않음(but, 구별하는 것을 선호함)

### 사용자 정의 함수(user defined function)

* 사용자가 직접 만든 함수
* 해당 함수가 정의된 PHP 스크립트에서만 호출 가능

### 호출

* 내장함수 : 모든 PHP 스크립트에서 호출가능

* 사용자 정의 함수 : 해당 PHP 스크립트에서만 호출 가능

* 방법

  * 함수의 정의와 같은 형태

  ```php
  $[VARIABLE] = [FUNCTIONNAME]([ARGUMENT1], [ARGUMENT2], ...);
  ```

  * 함수 `[FUNCTIONNAME]`을 호출하면서 인수로 `[ARGUMENT]`를 전달함

  * 인수로 전달된 값들은 함수에서 정의된 `[PARAMETER]`에 대입 됨

    `[ARGUMENT1]` => `[PARAMETER1]`, `[ARGUMENT2]` => `[PARAMETER2]`
  
* 함수 호출 시 전달된 인수는 매개변수의 왼쪽부터 차례대로 대입됨

### 값 반환

* return문

  * 포함할 수도 있고, 포함하지 않을 수도 있음
  * `return` 키워드를 사용하여 명시 가능
  * 호출자에게 함수 블록 내에서 실행된 코드의 결과를 반환함
  * 모든 타입의 값 반환 가능

* return 값 type (PHP 7)

  * 함수의 return 값을 원하는 type으로 반환받을 수 있도록 지정

  * type 지정할 때 강도 설정 가능

    * 기본값이 약한 강도인 경우 : type이 일치하지 않으면, 자동 타입 변환을 통해 명시된 타입으로 변환된 반환값을 반환함

      ```php
      function sum($x, $y): float // 반환값의 타입을 float 타입으로 설정함
      {
          return $x + $y;
      }
      
      var_dump(sum(3, 4)); // 결과의 type은 int 이지만 설정한 반환값 타입인 float로 변환됨 // float(7)
      ```

    * 기본값이 강한 강도인 경우 : 반환값의 타입이 일치하지 않으면, 오류 발생함

      * 변환 가능한 경우 오류 발생하지 않음..

        "1", 정수와 실수 변환 등등

      ```php
      declare(strict_types = 1); // declare문을 사용하여 strice 모드로 설정함
      
      function sum($x, $y): bool // 반환값의 타입을 float 타입으로 설정함
      {
          echo ($x + $y); // $x의 type이 int, value가 0으로 바뀜 // 4
          echo "\n"; // 
          return $x + $y; // 오류 발생
      }
      
      var_dump(sum("a", 4));
      ```

### 매개변수(parameter)와 인수(argument)

* parameter

  * 함수를 호출할 때 인수로 전달된 값을 함수 내부에서 사용할 수 있게 해주는 변수
  * 대부분의 함수는 하나 이상의 매개변수를 가지지만, 매개변수가 없는 함수도 존재함

* argument

  * 함수가 호출될 때 함수로 값을 전달해주는 변수

* parameter의 전달방식

  * 값 전달(passing by value)

    * 함수의 인수가 매개변수로 전달되는 기본방식
    * 인수를 함수에 전달하면, 새롭게 생성된 매개변수에 전달받은 값이 복사되어 저장됨
    * 매개변수에 저장된 값은 전달받은 데이터의 복사본이므로 함수 안에서 변경되어도 함수 밖의 원본 데이터에는 영향을 주지 않음

    ```php
    function increment($para)
    {
        $para++; // $value의 값을 복사하여 increment() 함수에 인수로 전달함.
        echo "\$para : ".$para."\n"; // $para : 2
    }
    $value = 1;
    increment($value);
    echo "\$value : ".$value; // $value : 1
    ```

  * 참조 전달(passing by value)

    * 전달받은 원본 데이터에 대한 참조 변수를 매개변수에 전달함
    * 함수 내부에서 값을 변경하면, 함수 밖의 원본 데이터도 같이 바뀜
    * 함수를 선언할 때 매개변수 앞에 '`&`'기호를 붙여 참조 전달을 사용함

    ```php
    function increment(&$para) // 인수로 전달되는 값의 원본을 참조함.
    {
        $para++;
        echo "\$para : ".$para."\n"; // $para : 2
    }
    $value = 1;
    increment($value);
    echo "\$value : ".$value; // $value : 2
    ```

* default parameter

  * 함수를 호출할 때 명시된 매개변수를 전달하지 않았을 경우에 사용하는 기본값

  * default parameter를 설정한 매개변수는 함수 호출시 인수가 전달되지 않았을 경우 기본값을 사용하며, 오류가 발생하지 않음

  * 설정방법

    ```php
    function [FUNCTIONNAME]($[PARAMETER1], $[PARAMETER2] = 0, $[PARAMETER3] = 0)
    ```

    * [PARAMETER1]은 인수가 전달되지 않으면 함수 호출시 오류 발생함

  * 함수 호출시 전달된 인수는 매개변수의 왼쪽부터 차례대로 대입되므로 default parameter 설정은 매개변수 리스트의 맨 오른쪽 끝 매개변수부터 시작하는 것이 좋음

  ```php
  function sum($value1 = 0, $value2, $value3 = 0)
  {
      return $value1 + $value2 + $value3;
  }
  
  echo sum(1, 2, 3); // 6
  echo sum(1, 2);    // 3
  echo sum(1);     // 오류가 발생함.
  echo sum();      // 오류가 발생함.
  ```

* 가변 길이 인수 목록(variable-length argument list)

  * 함수를 선언할 때 전달받을 인수의 개수를 미리 정하지 않고, 호출할 때마다 유동적으로 인수를 넘기는 기능
  * '`...`'토큰을 사용하여 함수가 호출될 때 전달받은 인수들을 배열 형태로 저장함

  ```php
  function sum(...$num) // PHP 5.6 이상
  {
      $sum = 0;
      foreach($num as $n) {
          $sum += $n;
      }
      return $sum;
  }
  $res = sum();
  echo $res."\n"; // 0
  $res = sum(1);
  echo $res."\n"; // 1
  $res = sum(1, 2);
  echo $res."\n"; // 3
  ```

### 함수의 활용

* conditional function

  * 특정 조건을 만족할 때만 선언되는 함수

  ```php
  $makefunc = true;
  //func(); // 이 부분은 func() 함수가 선언되기 전이므로, 함수를 호출할 수 없습니다.
  
  if($makefunc) {
      function func()
      {
          echo "이제 함수를 사용할 수 있습니다";
      }
  
      func(); // 이 부분은 func() 함수가 선언되었으므로, 함수를 호출할 수 있습니다. // 이제 함수를 사용할 수 있습니다
  }
  ```

* 함수안의 함수(function within function)

  * 함수 안에 또 다른 함수 선언 가능

  ```php
  function out()
  {
      function in()
      {
          echo "이제 함수를 사용할 수 있습니다";
      }
  }
  
  in(); // 이 부분은 in() 함수가 선언되기 전이므로, 함수를 호출할 수 없습니다. // error
  out(); // in() 함수 선언
  
  in();   // 이 부분은 in() 함수가 선언되었으므로, 함수를 호출할 수 있습니다. // 이제 함수를 사용할 수 있습니다
  ```

* 재귀 함수(recursive function)

  * 함수 내부에서 함수가 자기 자신을 호출하는 함수
  * 무한 반복되므로, 함수 내에 재귀 호출을 중단하도록 조건이 변경될 명령문을 반드시 포함해야 함
  * 100번 이상의 재귀 호출은 스택의 한계에 도달하여 스크립트가 중단될 수 있음

  ```php
  function factorial($num)
  {
      if($num > 1)                           // 1이 될 때까지
          return $num * factorial($num - 1); // 1씩 감소시킨 값을 전달하여 자기 자신을 계속 호출함.
      else
          return 1;
  }
  echo factorial(4); // 24
  ```

* 가변 함수(variable function)

  * 변수를 사용하여 함수를 호출하는 것
  * 변수 이름에 괄호(`()`)를 붙이면, 해당 변수의 값과 같은 이름을 가지는 함수를 호출함
  * 변수에 함수의 이름을 별도로 지정 가능

  ```php
  function first()
  {
      echo "first() 함수입니다.\n\n";
  }
  function second($para)
  {
      echo "second() 함수입니다.\n";
      echo "함수 호출 시 전달받은 인수의 값은 {$para}입니다.";
  }
  $func = "first";
  $func();    // first() 함수를 호출함.
  $func = "second";
  $func(20);  // second() 함수를 호출함.
  ```

### 내장 함수

#### magic method

* 특수한 기능을 위해 미리 정의한 메소드
* 메소드 이름, 매개변수, 반환 타입, 호출의 타이밍만 정해져 있음
* 내용은 사용자가 직접 작성 가능함
* 모든 매직 메소드의 이름은 두 개의 언더스코어(`__`)로 시작함

#### 변수 관련 함수

* 변수의 타입 변경

  * `gettype()`
    * 변수를 전달하면 타입에 따라 해당 타입의 이름을 `문자열`로 반환함
    * `float`형의 경우에는 `double`반환함
    * 표준 타입이 아닌 경우 `unknown type`반환함
    * 내부적으로 문자열을 비교하므로 실행 속도가 느림
  * `settype()`
    * 전달받은 변수의 타입 변경함
    * 변환할 타입 : `bool`, `int`, `string`, `array`, `object`, `float`, `null`
    * 전달받은 변수의 타입을 성공적으로 변경하면 true 반환

  ```php
  $x = 5;
  echo gettype($x)."\n"; // integer
  
  
  settype($x, "string");
  echo gettype($x);      // string
  ```

* 변수의 타입 검사

  |                   함수                   | 설명                                                     |
  | :--------------------------------------: | -------------------------------------------------------- |
  |                is_array()                | 전달받은 변수의 타입이 배열인지를 확인함                 |
  |                is_bool()                 | 전달받은 변수의 타입이 논리형인지를 확인함               |
  |              is_callable()               | 변수의 내용을 함수처럼 호출할 수 있는지를 확인함         |
  | is_float(),<br>is_double(),<br>is_real() | 전달받은 변수의 타입이 실수인지를 확인함                 |
  | is_int(),<br>is_integer(),<br>is_long()  | 전달받은 변수의 타입이 정수인지를 확인함                 |
  |                is_null()                 | 잔달받은 변수의 타입이 NULL인지를 확인함                 |
  |               is_numeric()               | 전달받은 변수가 수나 숫자로 이루어진 문자열인지를 확인함 |
  |               is_object()                | 전달받은 변수의 타입이 객체인지를 확인함                 |
  |              is_resource()               | 전달받은 변수의 타입이 자원인지를 확인함                 |
  |               is_scalar()                | 전달받은 변수가 스칼라값인지를 확인함                    |
  |               is_string()                | 전달받은 변수의 타입이 문자열인지를 확인함               |

  * 스칼라 값 : `integer`, `float`, `string`, `boolean`

* 변수의 상태 변경

  * `isset()`

    * 전달받은 변수가 초기화 되어 있는지 확인함
    * 선언된 변수가 존재하면 true 반환함

  * `unset()`

    * 전달받은 변수를 제거함

  * `empty()`

    * 전달받은 변수가 비어있는지를 검사함

    * 전달받은 변수가 존재하고, 해당 변수가 비어있지 않으면 false 반환함

    * 변수가 비어있다고 인식하는 경우

      * int : 0, float : 0.0, 문자열 "0", 빈 문자열 "", null, false, 빈 배열 array(), 초기화되지 않은 변수

    * 내부적으로 동작하는 방식

      ```php
      !isset($var) | $var==false
      ```

  ```php
  $var;
  var_dump(isset($var)); // bool(false)
  var_dump(empty($var)); // bool(true)
  
  $var = 5;
  var_dump(isset($var)); // bool(true)
  var_dump(empty($var)); // bool(false)
  
  $var = 0;
  var_dump(isset($var)); // bool(true)
  var_dump(empty($var)); // bool(true)
  
  unset($var);
  var_dump(isset($var)); // bool(false)
  var_dump(empty($var)); // bool(true)
  ```

* 특정 타입으로 변경

  * `intval()`
    * 전달받은 변수에 해당하는 정수를 반환
  * `floatval()`, `doubleval()`
    * 전달받은 변수에 해당하는 실수를 반환
  * `strval()`
    * 전달받은 변수에 해당하는 문자열 반환

  ```php
  $x = "123.56789abc";
  echo intval($x)."\n";   // 123
  echo floatval($x)."\n"; // 123.56789
  echo strval($x);   // 123.56789abc
  ```

#### 배열 관련 함수

* 배열의 생성

  * `array()`

    * 배열을 생성하는 함수

    ```php
    $arr = array(1, 2, 3, 4, 5);
    ```

* 배열 요소의 개수

  * `count()` 
    * 배열에 저장된 모든 배열 요소의 개수를 반환함
    * 배열에 hole이 있는 경우 hole이 아닌 배열 요소의 개수를 반환함 => 정확한 배열의 길이 구할 수 없음
  * `sizeof()`
    * 배열에 저장된 모든 배열 요소의 개수를 반환함
  * `array_count_values()`
    * 전달받은 배열의 배열 요소 값을 모두 확인하여, 해당 값이 몇 번 등장하는지 확인함
    * 배열 요소의 값을 key로, 해당 값의 등장 빈도를 value로 하는 연관 배열을 반환함

  ```php
  $arr = array(1, 5, 7, 3, 3, 1, 2);
  
  echo "배열 요소의 수는 ".count($arr)."입니다.";  // 배열 요소의 수는 7입니다.
  echo "배열 요소의 수는 ".sizeof($arr)."입니다."; // 배열 요소의 수는 7입니다.
  
  $acv = array_count_values($arr);                 // 1 : 2번, 5 : 1번, 7 : 1번, 3 : 2번, 2 : 1번
  var_dump($acv);
  ```

* 배열의 탐색

  * 배열 포인터
    * 현재 선택된 배열 요소가 어느 요소인지를 가리킴
    * 배열이 생성되면 자동으로 배열의 첫 번째 요소를 가리킴
  * `current()`, `pos()`
    * 배열 포인터가 현재 가리키고 있는 요소를 반환함
  * `next()`
    * 배열 포인터를 앞으로 하나 이동시킨 후에, 해당 요소를 반환함
  * `prev()`
    * 배열 포인터를 뒤로 하나 이동시킨 후에, 해당 요소를 반환함
  * `each()`
    * 배열 포인터가 현재 가리키고 있는 요소의 key와 value을 연관 배열로 반환하고, 배열 포인터를 앞으로 하나 이동시킴
  * `reset()`
    * 배열 포인터가 첫 번째 배열 요소를 가리키도록 한 뒤에, 해당 요소의 값을 반환함
  * `end()`
    * 배열 포인터가 마지막 배열 요소를 가리키도록 한 뒤에, 해당 요소의 값을 반환함

  ```php
  $arr = array(2, 3, 7, 4, 6);
  
  $element = current($arr);  // 배열의 첫 번째 요소를 가리킴.
  while($element) {          // 배열의 마지막 요소까지
      echo $element."\n";         // 해당 요소의 값을 출력하고,
      $element = next($arr); // 다음 요소를 가리킨 후에 해당 요소를 반환함.
  }                          // 2, 3, 7, 4, 6
  
  $element = end($arr);      // 배열의 마지막 요소를 가리킴.
  while($element) {          // 배열의 첫 번째 요소까지
      echo $element."\n";         // 해당 요소의 값을 출력하고,
      $element = prev($arr); // 이전 요소를 가리킨 후에 해당 요소를 반환함.
  }                          // 6, 4, 7, 3, 2
  ```

* 배열의 정렬

  * `sort()`

    * 배열 요소들을 정렬 기준에 맞게 정렬함
    * 두번 째 인수로 배열 요소를 정렬할 기준 전달 가능
      * `SORT_NUMERIC` : 배열 요소를 숫자로 비교
      * `SORT_STRING` : 배열 요소를 문자열로 비교
    * 정렬 기준 전달하지 않을 경우, 배열 요소들의 타입을 변경하지 않고 그대로 비교함
    * 대소문자 구별하며, 대문자가 소문자보다 앞쪽에 정렬됨
    * 배열 요소의 정렬에 성공하면 true 반환함

    ```php
    $arr = array(3, 2, 7, 6, 4);
    sort($arr); // 배열 정렬 -> 2, 3, 4, 6, 7
    var_dump($arr);
    ```

    ```php
    $arr = array(15, 2, 1, 21, 121);
    
    sort($arr, SORT_NUMERIC); // 배열 요소를 숫자로 비교함.   -> 1, 2, 15, 21, 121
    var_dump($arr);
    sort($arr, SORT_STRING);  // 배열 요소를 문자열로 비교함. -> 1, 121, 15, 2, 21
    var_dump($arr);
    ```

  * `array_multisort()`

    * 여러 배열이나 다차원 배열의 배열 요소를 정렬함

  * `natcasesort()`

    * 대소문자를 구분하지 않는 영문숫자 순(natural order)의 알고리즘으로 배열 요소를 정렬함

  * `natsort()`

    * 영문숫자 순(natural order)의 알고리즘으로 배열 요소를 정렬함

  * `usort()`

    * 사용자가 정의한 비교 함수를 사용하여, 배열 요소의 value을 기준으로 정렬함

  * `uksort()`

    * 사용자가 정의한 비교 함수를 사용하여, 배열 요소의 keyㄹ 기준으로 정렬함

  * `uasort()`

    * 사용자가 정의한 비교 함수를 사용하여, 인덱스 연관성을 유지한 채 배열 요소를 정렬함

* 연관 배열의 정렬

  * 연관 배열은 문자열을 인덱스로 사용하므로, key와 value로 따로 정렬 가능함
  * `ksort()`
    * 각 요소의 key를 기준으로 정렬함
  * `asort()`
    * 각 요소의 value을 기준으로 정렬함

  ```php
  $arr = array("apple" => 1000, "banana" => 2000, "orange" => 1500);
  
  asort($arr); // 요소의 값을 기준으로 배열 정렬 -> apple, orange, banana
  var_dump($arr);
  ksort($arr); // 키값을 기준으로 배열 정렬      -> apple, banana, orange
  var_dump($arr);
  ```

* 배열 요소의 재배치

  * `shuffle()`

    * 배열 요소를 섞은 뒤에 무작위로 재배치함

    ```php
    $arr = array(1, 2, 3, 4, 5);
    shuffle($arr);              // 배열 요소를 무작위로 재배치함.
    var_dump($arr);
    ```

  * `array_reverse()`

    * 전달받은 배열의 순서를 역순으로 변경한 새로운 배열을 반환함
    * 원본 배열에 영향 주지 않음

    ```php
    $arr1 = array(1, 2, 3, 4, 5);
    $arr2 = array_reverse($arr1);       // 배열 요소를 역순으로 바꾼 새로운 배열을 반환함.
    
    for($i = 0; $i < count($arr2); $i++){ // 새로 생성된 배열인 $arr_02의 모든 요소를 출력함.
        echo $arr2[$i].", ";              // 5, 4, 3, 2, 1
    }
    
    for($i = 0; $i < count($arr1); $i++){ // 원본 배열인 $arr_01의 모든 요소를 출력함.
        echo $arr1[$i].", ";              // 1, 2, 3, 4, 5
    }
    ```

#### 문자열 관련 함수

* 문자열의 길이

  * `strlen()`
    * 전달받은 문자열의 길이(문자열에 포함된 문자의 개수)를 반환함
    * 함수에 전달된 문자열에 한글이 포함되면 문자열의 총 바이트(byte) 수를 반환함
  * `mb_strlen()`
    * 한글이 포함된 문자열의 정확한 문자열 길이를 반환함
    * 두 번째 인수로 인코딩 방식 전달받을 수 있음
      * 전달받은 인코딩 방식으로 해당 문자열 해석하여 문자열 길이 반환함
    * 두 번재 인수를 전달받지 못하는 경우, 현재 시스템의 내부 인코딩 방식을 사용함

  ```php
  $str = "12345678";
  echo strlen($str)."\n"; // 8
  
  $str = "한글로된문자열";
  echo strlen($str)."\n";             // 7 * 3 = 21 // 21
  echo mb_strlen($str)."\n";          // 7 * 3 = 21
  echo mb_strlen($str, "UTF-8"); // 7
  ```

* 문자열 비교하기

  * `strcmp()`
    * 전달받은 두 개의 문자열을 서로 비교함
    * 첫 번째 인수의 문자열이 두 번째 인수의 문자열보다 크면 양수를, 작으면 음수를, 완전히 같으면 0을 반환함
    * 대소문자 구분함
  * `strnatcmp()`
    * 전달받은 두 개의 문자열을 서로 비교함
    * 첫 번째 인수의 문자열이 두 번째 인수의 문자열보다 크면 양수를, 작으면 음수를, 완전히 같으면 0을 반환함
    * 대소문자 구분함
    * 영숫자 순(natural ordering)으로 문자열 비교
  * `strcasecmp()`
    * 전달받은 두 개의 문자열을 서로 비교함
    * 첫 번째 인수의 문자열이 두 번째 인수의 문자열보다 크면 양수를, 작으면 음수를, 완전히 같으면 0을 반환함
    * 대소문자 구분하지 않음
  * `strnatcasecmp()`
    * 전달받은 두 개의 문자열을 서로 비교함
    * 첫 번째 인수의 문자열이 두 번째 인수의 문자열보다 크면 양수를, 작으면 음수를, 완전히 같으면 0을 반환함
    * 대소문자 구분하지 않음
    * 영숫자 순(natural ordering)으로 문자열 비교

  ```php
  echo strcmp("abc", "ABC")."\n";         // 1
  echo strnatcmp("abc", "ABC")."\n";      // 1
  echo strcasecmp("abc", "ABC")."\n";     // 0
  echo strnatcasecmp("abc", "ABC")."\n";  // 0
  echo strcmp("2", "10")."\n";            // 1
  echo strnatcmp("2", "10")."\n";         // -1 // 영숫자순으로 비교
  echo strcasecmp("2", "10")."\n";        // 1
  echo strnatcasecmp("2", "10");          // -1 // 영숫자순으로 비교
  ```

* 특정 문자열 검색

  * `strstr()`, `strchr()`
    * 해당 문자열에서 전달받은 문자열과 처음으로 일치하는 부분을 찾음
    * 대소문자를 구별함
    * 해당 문자열에 일치하는 부분이 존재하면, 처음으로 일치하는 부분을 포함한 이후의 모든 문자를 같이 반환함
    * 일치하는 부분이 존재하지 않으면 false 반환함
  * `stristr()`
    * 해당 문자열에서 전달받은 문자열과 처음으로 일치하는 부분을 찾음
    * 대소문자를 구별하지 않음
    * 해당 문자열에 일치하는 부분이 존재하면, 처음으로 일치하는 부분을 포함한 이후의 모든 문자를 같이 반환함
    * 일치하는 부분이 존재하지 않으면 false 반환함
  * `strrchr()`
    * 해당 문자열에서 전달받은 문자열과 마지막으로 일치하는 부분을 찾음
    * 대소문자를 구별함
    * 해당 문자열에 일치하는 부분이 존재하면, 마지막으로 일치하는 부분을 포함한 이후의 모든 문자를 같이 반환함
    * 일치하는 부분이 존재하지 않으면 false 반환함

  ```php
  echo strstr("ABCabcDEFabc", "abc")."\n";   // abcDEFabc
  echo strrchr("ABCabcDEFabc", "abc")."\n"; // abc
  echo stristr("ABCabcDEFabc", "abc");  // ABCabcDEFabc
  ```

* 특정 문자열 위치 찾기

  * `strpos()`
    * 해당 문자열에서 전달받은 문자열과 처음으로 일치하는 부분의 시작 인덱스 반환함
  * `strrpos()`
    * 해당 문자열에서 전달받은 문자열과 마지막으로 일치하는 부분의 시작 인덱스를 반환함

  ```php
  echo strpos("ABCabcDEFabc", "abc")."\n";  // 3
  echo strrpos("ABCabcDEFabc", "abc"); // 9
  ```

* 문자열 추출하기

  * `substr()`
    * 해당 문자열에서 특정 인덱스(두 번째 인수)부터 전달받은 길이(세 번째 인수)만큼의 일부분을 추출하여 반환함
    * 두 번째 인수 
      * 전달받은 인덱스가 양수인 경우 해당 인덱스부터 해당 문자열의 끝까지를 반환함
      * 전달받은 인덱스가 음수인 경우 해당 문자열 끝부터 전달받은 음수의 절댓값만큼의 문자열을 반환함
    * 세 번째 인수
      * 전달받은 길이가 양수인 경우 반환할 문자열의 길이를 나타냄
      * 전달받은 길이가 음수인 경우 특정 인덱스부터 문자열  끝부터 전달받은 음수의 절댓값까지의 문자열을 반환함

* 문자열 대소문자 바꾸기

  * `strtolower()`
    * 전달받은 문자열의 모든 문자를 소문자로 바꿔줌
  * `strtoupper()`
    * 전달받은 문자열의 모든 문자를 대문자로 바꿔줌
  * `ucfirst()`
    * 전달받은 문자열의 첫 번째 문자만을 대문자로 바꿔줌
  * `ucwords`()
    * 전달받은 문자열에서 단어별로 첫 번째 문자만을 대문자로 바꿔줌

  ```php
  echo strtolower("HELLO, WORLD!")."\n"; // 모두 소문자로 바꿈. // hello, world!
  echo strtoupper("hello, world!")."\n"; // 모두 대문자로 바꿈. // HELLO, WORLD!
  echo ucfirst("hello, world!")."\n";    // 문자열의 첫 번째 문자만 대문자로 바꿈. // Hello, world!
  echo ucwords("hello, world!");    // 각 단어의 첫 번째 문자를 대문자로 바꿈. // Hello, World!
  ```

* 문자열 합치고 나누기

  * `explode()`
    * 특정 문자를 기준으로 전달받은 문자열을 나누어서 하나의 배열로 반환함
  * `implode()`, `join()`
    * 전달받은 배열의 각 요소를 특정 문자를 사용하여 하나로 함쳐진 문자열로 반환함
  * `strtok()`
    * 전달받은 문자열을 특정 문자를 기준으로 토큰화함
    * 해당 문자열을 한 번에 모두 나누지 않고, 한 번에 하나씩만 토큰화함
    * 첫 번째 토큰 : 인수로 해당 문자열과 기준이 되는 문자를 함께 전달
    * 두 번째 토큰 부터 : 기준이 되는 문자 전달

  ```php
  $str = "hello, beautiful, world!";
  
  $arr = explode(',', $str);  // ','를 기준으로 문자열을 나눔.
  echo $arr[0]."\n";               // hello
  echo $arr[1]."\n";               // beautiful
  echo $arr[2]."\n";               // world!
  
  $str2 = implode('!', $arr); // '!'를 기준으로 문자열을 결합함.
  echo $str2."\n";                   // hello! beautiful! world!
  
  $token = strtok($str2, '!');  // '!'를 기준으로 토큰화
  echo $token."\n";                  // hello
  while($token != ""){          // 문자열이 끝날 때까지
      $token = strtok('!');     // '!'를 기준으로 토근화하고 출력함.
      echo $token."\n";              // beautiful // world
  }
  ```

* 문자열 대체하기

  * `str_replace()`
    * 해당 문자열에서 전달받은 문자열을 모두 찾은 후에, 찾은 문자열을 대체 문자열로 교체함
  * `substr_replace()`
    * 해당 문자열에서 특정 위치의 문자들을 대체 문자열로 교체함
    * 세 번째 인수 : 교체를 시작할 부분의 인덱스
    * 네 번째 인수 : 교체할 부분의 길이
      * 전달된 길이가 양수인 경우 시작 인덱스부터 교체할 글자의 개수를 나타냄
      * 전달된 길이가 음수인 경우 시작 인덱스부터 문자열 끝부터 음수의 절댓값까지의 문자열을 대체 문자열로 대체함
      * 전달된 길이가 0인 경우 해당 문자열의 시작 인덱스에 대체 문자열을 삽입함
      * 길이를 전달하지 않는 경우 시작 인덱스부터 해당 문자열의 끝까지 모두 대체됨

  ```php
  $str = "hello, world!";
  echo str_replace('o', '*', $str)."\n";      // 문자열의 모든 'o'를 '*'로 대체함. // hell*, w*rld!
  echo substr_replace($str, '*', 2)."\n";     // 세 번째 문자부터 끝까지를 '*'로 대체함. // he*
  echo substr_replace($str, '*', -2)."\n";    // 끝에서 두 번째 문자부터 끝까지를 '*'로 대체함. // hello, worl*
  echo substr_replace($str, '*', 2, 4)."\n";  // 세 번째 문자부터 네 글자를 '*'로 대체함. // he* world!
  echo substr_replace($str, '*', 2, -4)."\n"; // 세 번째 문자부터 끝에서 다섯 번째 문자까지를 '*'로 대체함. // he*rld!
  echo substr_replace($str, '*', 2, 0);  // 두 번째 문자 뒤에 '*'을 삽입함. // he*llo, world!
  ```

* 문자열 다듬기

  * `ltrim()`
    * 문자열 앞부분에 있는 공백 제거
  * `rtrim()`, `chop()`
    * 문자열 끝부분에 있는 공백 제거
  * `trim()`
    * 문자열의 처음과 끝부분에 있는 공백 모두 제거
  * 제거하는 문자
    * 띄어쓰기 " ", 탭 문자 "\\t", 줄 바꿈 문자 "\\n", "\\r", 널 문자 "\\0", 수직 탭 문자 "\\x0B"

  ```php
  $str = "  hello, world!  ";
  echo "'".ltrim($str)."'\n"; // 문자열의 처음 부분 공백을 모두 지움. // 'hello, world!  '
  echo "'".rtrim($str)."'\n"; // 문자열의 끝부분 공백을 모두 지움. // '  hello, world!'
  echo "'".trim($str)."'";       // 문자열의 처음과 끝부분 공백을 모두 지움. // 'hello, world!'
  ```

#### 날짜와 시간 관련 함수

* 날짜와 시간의 형식화

  * `date()`

    * 전달받은 형식에 맞춰 날짜와 시간 정보를 문자열로 반환함

    * 수를 전달하지 않는 경우 현재 날짜와 시간의 타임스탬프 반환함

      ```php
      $array = getdate();
      
      foreach ($array as $key => $value) {
          echo $key." ".$value."\n";
          // seconds 4
          // minutes 23
          // hours 2
          // mday 23
          // wday 1
          // mon 3
          // year 2020
          // yday 82
          // weekday Monday
          // month March
          // 0 1584930184
      }
      ```

    * 인수로 전달할 수 있는 날짜와 시간 표현의 형식(아래 표)

    |     형태      | 설명                                                         | 예시                            |
    | :-----------: | ------------------------------------------------------------ | ------------------------------- |
    |       d       | 날짜를 두 자리 숫자로 표현함                                 | 00부터 31                       |
    |       D       | 요일을 세 개의 문자로 표현함                                 | Mon에서 Sun                     |
    |       j       | 날짜를 숫자로 표현함                                         | 1부터 31                        |
    | l(소문자 'L') | 요일을 완전한 문자열로 표현함                                | Sunday부터 Saturday             |
    |       N       | 요일을 ISO-8601 숫자로 표현함                                | 1(월요일)부터 7(일요일)         |
    |       S       | 날짜 뒤에 영어 서수를 붙임                                   | st, nd, rd, th, j               |
    |       w       | 요일을 숫자로 표현함                                         | 0(일요일)부터 6(토요일)         |
    |       z       | 일 년 중 몇 번째 날인지를 수자로 표현함                      | 0부터 365                       |
    |       W       | 일 년 중 몇 번째 주인지를 숫자로 표현함                      | 42(그 해의 42번째 주)           |
    |       F       | 월을 완전한 문자열로 표현함                                  | January에서 December            |
    |       m       | 월을 두 자리 숫자로 표현함                                   | 01부터 12                       |
    |       M       | 월의 축약형을 세 개의 문자로 표현함                          | Jan에서 Dec                     |
    |       n       | 월을 숫자로 표현함                                           | 1부터 12                        |
    |       t       | 해당 월의 총일 수를 숫자로 표현함                            | 28부터 31                       |
    |       L       | 윤년 여부를 표현함                                           | 윤년엔 1, 그 외엔 0             |
    |       o       | ISO-8601 연도값으로 Y값과 같은 값을 나타냄<br>하지만 W값이 이전 해나 다음 해에 포함되면, 연도를 이 값으로 사용함 | 1999나 2003                     |
    |       Y       | 연도를 완전한 네 자리 숫자로 표현함                          | 1999나 2003                     |
    |       y       | 연도를 두 자리 숫자로 표현함                                 | 99나 03                         |
    |       a       | 오전과 오후의 소문자를 표현함                                | am 또는 pm                      |
    |       A       | 오전과 오후의 대문자를 표현함                                | AM 또는 PM                      |
    |       B       | 견본 인터넷 시간을 표현함                                    | 000에서 999                     |
    |       g       | 12시간 형식으로 시간을 표현함                                | 1부터 12                        |
    |       G       | 24시간 형식으로 시간을 표현함                                | 0부터 23                        |
    |       h       | 12시간 형식 시간을 두 자리 숫자로 표현함                     | 01부터 12                       |
    |       H       | 24시간 형식 시간을 두 자리 숫자로 표현함                     | 00부터 23                       |
    |       i       | 분을 두 자리 숫자로 표현함                                   | 00부터 59                       |
    |       s       | 초를 두 자리 숫자로 표현함                                   | 00부터 59                       |
    |       u       | 초를 마이크로초로 표현함                                     | 54321                           |
    |       e       | 시간대(timezone) 식별자를 표현함                             | UTC, GMT                        |
    |  I(대문자 i)  | 서머타임 적용 여부를 표현함                                  | 서머타임이면 1, 아니면 0        |
    |       O       | 그리니치 시각(GMT)과 시차를 표현함                           | +0200                           |
    |       P       | 시와 분 사이에 콜론이 들어가는 그리니치 시각(GMT)과 시차를 표현함 | +02:00                          |
    |       T       | 시간대(timezone)를 나타내는 축약어                           | EST, MDT                        |
    |       Z       | 시간대(timezone)를 나타내는 오프셋 초를 표현함.<br>UTC 서쪽은 항상 음수, UTC 동쪽은 항상 양수로 표현됨 | -43200부터 50400                |
    |       c       | ISO-8601 형식의 날짜를 표현함                                | 2004-02-12T15:19:21+00:00       |
    |       r       | RFC 2822 형식의 날짜를 표현함                                | Thu, 21 Dec 2000 16:01:07 +0200 |
    |       U       | 타임스템프를 표현함                                          | time() 참조                     |

    * 타임스탬프 : GMT 기준 1970년 1월 1일 0시 0분부터 지금까지의 시간을 초(second) 단위로 나타낸 것

* 타임 존(Time Zone)

  * `date_default_timezone_set()`
    * 해당 스크립트에서 사용되는 날짜와 시간에 관련된 모든 함수에서 사용될 타임 존 설정함
  * `date_default_timezone_get()`
    * 현재 설정되어 있는 타임 존을 반환함

  ```php
  echo date_default_timezone_get()." : ".date("h:i:s\n"); // 현재 타임 존과 시간을 받아옴. // UTC : 02:25:19
  date_default_timezone_set("America/Los_Angeles");     // 타임 존을 변경함.
  echo date_default_timezone_get()." : ".date("h:i:s"); // America/Los_Angeles : 07:25:19
  ```

* 날짜의 유효성 검사

  * `checkdate()`
    * 전달받은 날짜의 유효성 검사함
    * 인수로 월, 일, 연도를 전달하면, 해당 날짜가 유효한 날짜인지 확인함
    * 윤년까지 고려함
    * 검사항목
      * 월이 1월부터 12월까지인지 검사함
      * 일자가 해당 월에 존재하는 날짜인지를 검사함
      * 연도가 0에서 32767까지의 정수인지 검사함
    * 날짜가 유효하면 true 반환함

  ```php
  var_dump(checkdate(1, 31, 2000)); // 유효한 날짜 // bool(true)
  var_dump(checkdate(2, 31, 2000)); // 유효하지 않은 날짜 // bool(false)
  ```

#### 수학 관련 함수

* 최댓값과 최솟값

  * `max()`
    * 전달받은 수 중에서 가장 큰 수를 반환함
  * `min()`
    * 전달받은 수 중에서 가장 작은 수를 반환함

* 올림과 내림

  * `floor()`
    * 인수로 전달받은 값과 같거나 작은 수 중에서 가장  큰 정수를 반환함
  * `ceil()`
    * 인수로 전달받은 값과 같거나 큰 수 중에서 가장 작은 정수를 반환함
  * `round()`
    * 소수점에서의 반올림

  ```php
  echo floor(10.95);  // 10 
  echo floor(11.01);  // 11
  echo floor(-10.95); // -11
  echo floor(-11.01); // -12
  
  echo ceil(10.95);   // 11
  echo ceil(11.01);   // 12
  echo ceil(11);      // 11
  echo ceil(-10.95);  // -10
  echo ceil(-11.01);  // -11
  
  echo round(10.49);  // 10
  echo round(10.5);   // 11
  echo round(-10.5);  // -11
  echo round(-10.51); // -11
  ```

* 지수와 로그

  * `pow()`
    * 전달받은 수의 거듭제곱을 반환함
    * 첫 번째 인수 : 밑수, 두 번째 인수 : 지수
  * `exp()`
    * 인수로 지수를 전달받아, e의 거듭제곱을 계산하여 반환함
  * `log()`
    * 전달받은 수의 자연로그 값을 계산하여 반환함

  ```php
  echo "2의 3제곱은 ".pow(2, 3)."입니다.\n"; // 2의 3제곱은 8입니다.
  echo "e의 3제곱은 ".exp(3)."입니다.\n"; // e의 3제곱은 20.085536923188입니다.
  echo "log3은 ".log(3)."입니다."; // log3은 1.0986122886681입니다.
  ```

* 삼각 함수

  * `sin()`
    * 전달받은 수의 사인값을 반환함 
  * `cos()`
    * 전달받은 수의 코사인값을 반환함
  * `tan()`
    * 전달받은 수의 탄젠트값을 반환함
  * `pi()`
    * 파이(π) 값을 반환함
    * `M_PI` 상수와 같은 값 반환함

  ```php
  echo "sin3.14는 ".sin(pi()/2)."입니다.\n"; // sin(π/2) == 1 // sin3.14는 1입니다.
  echo "cos3.14는 ".cos(M_PI)."입니다.\n";   // cos(π) == -1 // cos3.14는 -1입니다.
  echo "tan3.14는 ".tan(M_PI/4)."입니다.\n"; // tan(π/4) == 1 // tan3.14는 1입니다.
  ```

* 기타 함수

  * `abs()`
    * 전달받은 수의 절댓값을 반환함
  * `rand()`
    * 0보다 크거나 같고 `getrandmax()` 함수의 반환값보다 작은 하나의 정수를 무작위로 생성하여 반환함
  * `getrandmax()`
    * `rand()` 함수로 생성할 수 있는 정수의 최댓값을 나타냄

  ```php
  echo "-3의 절댓값은 ".abs(-3)."입니다.\n"; // -3의 절댓값은 3입니다.
  echo "0부터 ".getrandmax()."까지의 정수를 하나 무작위로 생성합니다 : ".rand(); // 0부터 2147483647까지의 정수를 하나 무작위로 생성합니다 : 1330635331
  ```

#### 정규 표현식 관련 함수

* `preg_match()`

  * 해당 문자열에서 전달받은 정규 표현식과 일치하는 패턴 검색

  * 문법

    ```php
    preg_match($pattern, $subject [,$matches]);
    ```

  * 첫 번째 인수로 전달받은 정규 표현식에 해당하는 패턴을 두 번째 인수로 전달받은 문자열에서 검색함

  * 반환값

    * 검색 결과를 배열로 반환함
    * 또는 세 번째 인수로 반환값이 저장될 배열을 직접 전달 가능
    * 일치하는 패턴이 존재하면 1을 반환함
    * 일치하는 패턴이 존재하지 않으면 0을 반환함

  * 정규 표현식에 해당하는 패턴이 검색되면 검색 중단함

* `preg_match_all()`

  * 해당 문자열에서 전달받은 정규 표현식과 일치하는 패턴을 모두 검색하여, 세 먼째 인수로 전달되는 배열에 저장함

  ```php
  $subject = "bcabcAB";
  
  // 기본 설정으로 검색 패턴을 비교할 때 대소문자를 구분함.
  echo preg_match_all('/AB/', $subject, $matches_01)."\n";      // "AB" // 1
  var_dump($matches_01);
  
  // 검색 패턴을 비교할 때 대소문자를 구분하지 않도록 설정함.
  echo preg_match_all('/AB/i', $subject, $matches_02)."\n"; // "ab", "AB" // 2
  var_dump($matches_02);
  ```

* `preg_replace()`

  * 해당 문자열에서 전달받은 정규 표현식과 일치하는 패턴을 검색하여, 해당 부분을 두 번째 인수로 전달되는 문자열로 대체한 새로운 문자열을 반환함

  ```php
  $subject = "abcdef defabc";
  
  // 단어가 문자열 "abc"로 시작하는 경우를 검색하여, 해당 부분 문자열을 'ABC'로 대체함.
  $match_01 = preg_replace('/^abc/', 'ABC',$subject);
  echo $match_01."\n"; // ABCdef defabc
  
  // 단어가 문자열 "abc"로 끝나는 경우를 검색하여, 해당 부분 문자열을 'ABC'로 대체함.
  $match_02 = preg_replace('/abc$/', 'ABC', $subject);
  echo $match_02; // abcdef defABC
  ```

* `filter_var()`

  * 유효한 형식의 이메일 주소인지 확인해주는 함수

  ```php
  $com = "help@abcd.com";
  $co = "help@abcd.co.kr";
  
  if (filter_var($com, FILTER_VALIDATE_EMAIL)) {
      echo $com."\n"; // help@abcd.com
  } else {
      echo "{$com}은 유효한 형식의 이메일 주소가 아닙니다.\n";
  }
  
  if (filter_var($co, FILTER_VALIDATE_EMAIL)) {
      echo $co."\n"; // help@abcd.co.kr
  } else {
      echo "{$co}은 유효한 형식의 이메일 주소가 아닙니다.\n";
  }
  ```

## 정규 표현식(regular expression)

* 문자열에서 특정한 규칙을 가지는 문자열의 집합을 찾아내기 위한 검색 패턴

* 모든 종류의 문자열 검색이나 교체 등의 작업에서 사용 가능

* PHP에서 지원하는 정규 표현식

  * POSIX
    * 실행 속도가 빠름
  * PCRE(Perl-Compatible Regular Expression)
    * POSIX 정규 표현식을 확장
    * POSIX에 비해 더 강력하고 유연하게 동작함

* literal
  * 슬래시(`/`) 기호로 시작하여, 슬래시(`/`) 기호로 끝남

  * 필요에 따라 플래그를 추가하여 기본 검색설정 변경 가능

    ```php
    /검색패턴/플래그
    ```

### 단순한 패턴 검색

* 찾고자 하는 문자열을 직접 나열하여 패턴 검색을 함

  ```php
  /abc/
  ```

  * 위의 표현식으로 검사하면 "abc"라는 문자열만 일치할 것

  ```php
  $subject = "간장 공장 공장장은 강 공장장이고, 된장 공장 공장장은 장 공장장이다.";
  
  if (preg_match('/공장/', $subject)) {
      echo "해당 문자열에서 '공장'을 발견했습니다.\n"; // 해당 문자열에서 '공장'을 발견했습니다.
  } else {
      echo "해당 문자열에서 '공장'을 발견하지 못했습니다.\n";
  }
  
  if (preg_match('/장공/', $subject)) {
      echo "해당 문자열에서 '장공'을 발견했습니다.\n";
  } else {
      echo "해당 문자열에서 '장공'을 발견하지 못했습니다.\n"; // 해당 문자열에서 '장공'을 발견하지 못했습니다.
  }
  ```

### 플래그(flag)

* 정규 표현식 literal을 작성할 때 플래그를 사용하여 기본 검색 설정 변경 가능

  | 플래그(flag) | 설명                                                         |
  | :----------: | ------------------------------------------------------------ |
  |      i       | 검색 패턴을 비교할 때 대소문자를 구분하지 않도록 설정함      |
  |      g       | 검색 패턴을 비교할 때 일치하는 모든 부분을 선택하도록 설정함 |
  |      m       | 검색 패턴을 비교할 때 여러 줄의 입력 문자열을 그 상태 그대로 여러 줄로 비교하도록 설정함 |
  |      y       | 대상 문자열의 현재 위치부터 비교를 시작하도록 설정함         |
  |      u       | 대상 문자열이 UTF-8로 인코딩된 것으로 설정함                 |

  ```php
  $subject = "bcabcAB";
  
  // 기본 설정으로 검색 패턴을 비교할 때 대소문자를 구분함.
  echo preg_match_all('/AB/', $subject, $matches_01)."\n";      // "AB" // 1
  var_dump($matches_01);
  
  // 검색 패턴을 비교할 때 대소문자를 구분하지 않도록 설정함.
  echo preg_match_all('/AB/i', $subject, $matches_02)."\n"; // "ab", "AB" // 2
  var_dump($matches_02);
  ```

### 정규 표현식의 기초

* 특수 문자(special characters)

  * 정규 표현식에서 사용하는 특정 의미를 가진 기호
  * 정확히 일치하는 패턴보다 더 복잡한 조건을 사용하는 경우에 사용함(숫자만 검색, 띄어쓰기 찾기 등)
  * 메타(meta)라고도 함

  | 특수문자 | 설명                                               |
  | :------: | -------------------------------------------------- |
  |    .     | 줄 바꿈 문자(\\n)를 제외한 임의의 한 문자를 의미함 |
  |    ?     | 해당 문자 패턴이 0번 또는 1번만 반복됨             |
  |    *     | 해당 문자 패턴이 0번 이상 반복됨                   |
  |    +     | 해당 문자 패턴이 1번 이상 반복됨                   |
  |  {...}   | 반복되는 횟수를 지정함                             |
  |    ^     | 문자열의 처음을 의미함                             |
  |    $     | 문자열의 끝을 의미함                               |
  |    \     | 특수문자를 무시함                                  |
  |    \|    | 선택을 의미함(OR)                                  |
  |  (...)   | 그룹화의 시작과 끝을 의미함                        |

  ```php
  /.ap/         // 문자열 "ap" 앞에 임의의 한 문자가 등장하는 문자열 : aap, bap, cap, @ap, #ap, ...
  
  /a?b/         // b 앞에 a가 0번 또는 1번 등장하는 문자열 : b, ab
  /a*b/         // b 앞에 a가 0번 이상 등장하는 문자열 : b, ab, aab, aaab, ...
  
  /a+b/         // b 앞에 a가 1번 이상 등장하는 문자열 : ab, aab, aaab, aaaab, ...
  /a{2,4}b/     // b 앞에 a가 2번 이상 4번 이하 등장하는 문자열 : aab, aaab, aaaab
  /a{2,}b/      // b 앞에 a가 2번 이상 등장하는 문자열 : aab, aaab, aaaab, aaaaab, ...
  
  /^abc/        // abc로 시작하는 문자열 : abc, abcd, abcdef, ...
  
  /abc$/        // abc로 끝나는 문자열 : abc, zabc, xyzabc, ...
  
  /abc|def|ghi/ // abc, def 또는 ghi 중 하나의 문자열
  ```

* 양화사(quantifier)

  * 수량을 나타냄
  * '`*`'
    * 바로 앞의 문자가 0번 이상 나타날 경우를 검색함({0, }와 같음)
  * '`+`'
    * 바로 앞의 문자가 1번 이상 나타날 경우를 검색함({1, }와 같음)
  * '`?`'
    * 바로 앞의 문자가 0번 또는 1번만 나타날 경우를 검색함({0, 1}과 같음)
  * '`{n, m}`'
    * 바로 앞의 문자가 반복되는 횟수를 지정함
    * 바로 앞의 문자가 최소 n번 이상 최대 m번 이하로 나타날 경우를 검색함(n과 m은 반드시 양의 정수이어야만 함)

  ```php
  $subject = "PHP is cooooool!";
  
  // 문자 'l' 바로 앞에 문자 'o'가 0 또는 1번 나타나는 경우를 검색함.
  echo preg_match_all('/o?l/', $subject, $match_01); // 1
  
  // 문자 'l' 바로 앞에 문자 'o'가 0번 이상 나타나는 경우를 검색함.
  echo preg_match_all('/o*l/', $subject, $match_02); // 1
  
  // 문자 'l' 바로 앞에 문자 'o'가 1번 이상 나타나는 경우를 검색함.
  echo preg_match_all('/o+l/', $subject, $match_03); // 1
  
  // 영문 소문자가 1번 이상 나타나는 경우를 검색함.
  // 즉, 영문 소문자만으로 이루어진 부분 문자열을 검색함.
  echo preg_match_all('/[a-z]+/', $subject, $match_04); // 2
  
  // 문자 'l' 바로 앞에 문자 'o'가 최소 2번 이상 최대 4번 이하로 나타나는 경우를 검색함.
  preg_match_all('/o{2,4}l/', $subject, $match_01);
  var_dump($match_01);
  
  // 문자 'l' 바로 앞에 문자 'o'가 최소 2번 이상 나타나는 경우를 검색함.
  preg_match_all('/o{2,}l/', $subject, $match_02);
  var_dump($match_02);
  
  // 문자 'l' 바로 앞에 문자 'o'가 정확히 6번 나타나는 경우를 검색함.
  preg_match_all('/o{6}l/', $subject, $match_03);
  var_dump($match_03);
  ```

* 위치 문자

  * 해당 문자열에서 패턴을 검색할 단어의 위치 지정함
  * '`^`'
    * 단어의 맨 앞에 위치한 해당 패턴만을 검색함
  * '`$`'
    * 단어의 맨 뒤에 위치한 해당 패턴만을 검색함

  ```php
  $subject = "abcdef defabc";
  
  // 단어가 문자열 "abc"로 시작하는 경우를 검색하여, 해당 부분 문자열을 'ABC'로 대체함.
  $match_01 = preg_replace('/^abc/', 'ABC',$subject);
  echo $match_01."\n"; // ABCdef defabc
  
  // 단어가 문자열 "abc"로 끝나는 경우를 검색하여, 해당 부분 문자열을 'ABC'로 대체함.
  $match_02 = preg_replace('/abc$/', 'ABC', $subject);
  echo $match_02; // abcdef defABC
  ```

* 선택 문자

  * '`|`'

    * 정규 표현식에서 여러 개의 검색 패턴 사용할 수 있도록 함
    * 특수문자 '`|`'로 구분된 정규 표현식 중 어느 하나에만 일치해도 검색됨

    ```php
    $subject = "ABCdefGHIjkl";
    
    // 문자열 'abc' 또는 'def' 또는 'jkl'만을 검색함.
    // 즉, 위의 세 문자열 중 어느 하나에만 일치해도 검색됨.
    preg_match_all('/abc|def|jkl/', $subject, $match);
    var_dump($match);
    ```

* 문자 클래스(character class)

  * 정규 표현식에서 명시된 범위에 해당하는 한 문자만을 선택하기 위해 사용되는 문자
  * 꺾쇠 괄호 ('`[]`') 사용하여 표현함

  ```php
  /[0-3]/        // 0부터 3까지의 숫자에 해당하는 한 문자
  /[a-z]/        // 영문 소문자에 해당하는 한 문자
  /[0-9a-zA-Z]/  // 숫자 또는 영문 대소문자에 해당하는 한 문자
  ```

  ```php
  $subject = "@ap";
  
  preg_match("/.ap/", $subject, $match_01);        // "ap" 문자열 앞에 임의의 한 문자가 나타나는 경우를 검색함.
  var_dump($match_01);
  preg_match("/[a-zA-Z]ap/", $subject, $match_01); // "ap" 문자열 앞에 영문자 한 문자가 나타나는 경우를 검색함.
  var_dump($match_01);
  ```

* POSIX 문자 클래스

  * POSIX 정규 표현식에서만 사용할 수 있는 문자 클래스

  | 문자 클래스 | 설명                                                         |
  | :---------: | ------------------------------------------------------------ |
  |  [:alnum:]  | 영문자와 숫자에 포함되는지를 확인함                          |
  |  [:alpha:]  | 영문 대소문자에 포함되는지를 확인함                          |
  |  [:lower:]  | 영문 소문자에 포함되는지를 확인함                            |
  |  [:upper:]  | 영문 대문자에 포함되는지를 확인함                            |
  |  [:digit:]  | 십진법 숫자에 포함되는지를 확인함                            |
  | [:xdigit:]  | 16지넙 숫자나 문자에 포함되는지를 확인함                     |
  |  [:punct:]  | 구두점에 포함되는지를 확인함                                 |
  |  [:blank:]  | 탭과 띄어쓰기에 포함되는지를 확인함                          |
  |  [:space:]  | 공백 문자에 포함되는지를 확인함                              |
  |  [:cntrl:]  | 제어 문자에 포함되는지를 확인함                              |
  |  [:print:]  | 출력할 수 있는 문자에 포함되는지를 확인함                    |
  |  [:graph:]  | 띄어쓰기를 제외한 모든 출력할 수 있는 문자에 포함되는지를 확인함 |

  * 기본적으로 꺾쇠 괄호([])를 포함하고 있음
  * 꺾쇠 괄호 두 번 사용하여 표현함

  ```php
  /[[:alpha:]][[:digit:]]/ // 첫 번째 문자가 영문자이고, 두 번째 문자가 숫자인 길이가 2인 문자열
                           // a1, a2, ..., b1, b2, ...
  ```

  ```php
  $subject = "Hello PHP is cool!";
  
  // 첫 번째와 세 번째 문자가 영문 소문자이고, 두 번째 문자가 띄어쓰기인 경우를 검색함.
  preg_match_all('/[[:lower:]][[:space:]][[:lower:]]/', $subject, $match_01);
  var_dump($match_01);
  
  // 첫 번째 문자가 영문 소문자이고, 두 번째 문자가 띄어쓰기, 세 번째 문자가 영문 대문자인 경우를 검색함.
  preg_match('/[[:lower:]][[:space:]][[:upper:]]/', $subject, $match_02);
  var_dump($match_02);
  ```

### 정규 표현식의 활용

* 전화번호 확인

  * 해당 전화번호가 유효한 형식의 전화번호인지 확인

  * 정규 표현식

    ```php
    /^[[:digit:]]{2}\-[[:digit:]]{4}\-[[:digit:]]{4}/     // 02-1234-5678, ...
    ```

    * 전화번호의 맨 앞자리가 2자리이고 국번이 4자리인 전환번호만 검색 가능

    ```php
    /^[[:digit:]]{2,3}\-[[:digit:]]{3,4}\-[[:digit:]]{4}/ // 02-1234-5678, 031-123-5678, 010-1234-5678, ...
    ```

    * 전화번호의 맨 앞자리가 2자리나 3자리이고 국번이 3자리나 4자리인 전화번호까지 검색 가능

  ```php
  $tel = "02-1234-5678";
  $cell = "010-1234-5678";
  $pattern_01 = "/^[[:digit:]]{2}\-[[:digit:]]{4}\-[[:digit:]]{4}/";
  
  if (preg_match($pattern_01, $tel, $matches_01)) {
      var_dump($matches_01);
  } else {
      echo "{$tel}은 유효한 형식의 전화번호가 아닙니다.\n";
  }
  
  if (preg_match($pattern_01, $cell, $matches_02)) {
      var_dump($matches_02);
  } else {
      echo "{$cell}은 유효한 형식의 전화번호가 아닙니다.\n"; // 010-1234-5678은 유효한 형식의 전화번호가 아닙니다.
  }
  
  $pattern_02 = "/^[[:digit:]]{2,3}\-[[:digit:]]{3,4}\-[[:digit:]]{4}/";
  if (preg_match($pattern_02, $tel, $matches_03)) {
      var_dump($matches_03);
  } else {
      echo "{$tel}은 유효한 형식의 전화번호가 아닙니다.\n";
  }
  
  if (preg_match($pattern_02, $cell, $matches_04)) {
      var_dump($matches_04);
  } else {
      echo "{$cell}은 유효한 형식의 전화번호가 아닙니다.\n";
  }
  ```

* 이메일 주소 확인

  * 해당 이메일 주소가 유효한 형식의 이메일 주소인지 확인함

  * 정규 표현식

    ```php
    [0-9a-zA-Z_-]+
    ```

    * 숫자나 영문 대소문자, 언더스코어(_) 또는 '-'기호를 포함한 문자가 1번 이상 반복되는 문자열을 의미함

    ```php
    /([0-9a-zA-Z_-]+)@([0-9a-zA-Z_-]+)\.([0-9a-zA-Z_-]+)/      // help@abcd.com, ...
    ```

    * '@'문자와 '.'문자를 각각 하나씩만 포함하는 이메일 주소만을 검색함

    ```php
    /([0-9a-zA-Z_-]+)@([0-9a-zA-Z_-]+)(\.[0-9a-zA-Z_-]+){1,2}/ // help@abcd.com, help@abcd.co.kr, ...
    ```

    * '.'문자를 2개 이상 포함하는 이메일 주소 검색함

    ```php
    (\.[0-9a-zA-Z_-]+){1,2}
    ```

    * '.'문자로 시작하고, 숫자나 영문 대소문자, 언더스코어(_) 또는 '-'기호를 포함한 문자가 1번 이상 반복되는 문자열이 1번 또는 2번 반복되는 문자열을 의미함

  ```php
  $com = "help@abcd.com";
  $co = "help@abcd.co.kr";
  $pattern_01 = "/([0-9a-zA-Z_-]+)@([0-9a-zA-Z_-]+)\.([0-9a-zA-Z_-]+)/";
  
  if (preg_match($pattern_01, $com, $matches_01)) {
      var_dump($matches_01[0]); // string(13) "help@abcd.com"
  } else {
      echo "{$com}은 유효한 형식의 이메일 주소가 아닙니다.\n";
  }
  
  if (preg_match($pattern_01, $co, $matches_02)) {
      var_dump($matches_02[0]); // string(12) "help@abcd.co"
  } else {
      echo "{$co}은 유효한 형식의 이메일 주소가 아닙니다.\n";
  }
  
  $pattern_02 = "/([0-9a-zA-Z_-]+)@([0-9a-zA-Z_-]+)(\.[0-9a-zA-Z_-]+){1,2}/";
  if (preg_match($pattern_02, $com, $matches_03)) {
      var_dump($matches_03[0]); // string(13) "help@abcd.com"
  } else {
      echo "{$com}은 유효한 형식의 이메일 주소가 아닙니다.\n";
  }
  
  if (preg_match($pattern_02, $co, $matches_04)) {
      var_dump($matches_04[0]); // string(15) "help@abcd.co.kr"
  } else {
      echo "{$co}은 유효한 형식의 이메일 주소가 아닙니다.\n";
  }
  ```

* 한글 확인

  * 해당 문자가 한글인지 확인함

  * 한글 소리 마디(hangul syllables)

    * 초성 19개, 중성 21개, 종성 28개로 이루어지는 총 11,172개의 한글 문자를 가리킴

  * 정규 표현식

    ```php
    /[가-힣]/                // 한글 소리 마디
    ```

    * 현대 한글에서 표현할 수 있는 11,172개의 한글 소리 마디를 모두 검색할 수 있음
    * 언어 설정이 한글이 아닌 시스템에서 동작이 안 될 수 있음

    ```php
    /[\\x{ac00}-\\x{d7af}]/u // 한글 소리 마디의 유니코드 범위 목록값
    ```

    * 현대 한글에서 표현할 수 있는 11,172개의 한글 소리 마디를 모두 검색할 수 있음
    * 'u'플래그를 추가하여 해당 정규 표현식 문자열을 UTF-8로 인코딩된 것처럼 취급 가능

  ```php
  $eng = "gil-dong Hong";
  $kor = "홍길동";
  $pattern = "/[가-힣]+/"; // 한글 소리 마디
  
  if (preg_match($pattern, $eng, $matches_01)) {
      var_dump($matches_01);
  } else {
      echo "{$eng}에는 한글이 포함되어 있지 않습니다.\n"; // gil-dong Hong에는 한글이 포함되어 있지 않습니다.
  }
  
  if (preg_match($pattern, $kor, $matches_02)) {
      var_dump($matches_02);
  } else {
      echo "{$eng}에는 한글이 포함되어 있지 않습니다.\n";
  }
  ```

  ```php
  // 한글만 제거
  $text = "123가나abc다라";
  $pattern = "/[\\x{ac00}-\\x{d7af}]+/u";         // 한글 소리 마디(UTF-8)
  
  $arr = preg_match_all('/./u', $text, $matches); // 줄 바꿈 문자(\n)를 제외한 임의의 한 문자씩 검색함.
  var_dump($arr); // int(10)
  echo preg_replace($pattern, '', $text);         // 해당 문자가 한글이면, 빈 문자열로 대체함. // 123abc
  ```

## 클래스(class)

* 객체(object)를 만들어 내기 위한 틀이나 설계도와 같은 개념

### 구조

* 문법

  ```php
  class [클래스명]
  {
      클래스의 property와 method 정의;
  }
  ```

### 클래스 이름

* 숫자로 시작 불가
* 영문자(대소문자), 숫자, 언더스코어(_)로만 구성됨
* 이름 사이에 공백 포함 불가
* 대소문자 구분함
* 예약어(reserved word) 사용 불가

### property

* 클래스만의 상수와 변수
* object의 상태(state)를 구현함
* instance마다 값이 다름

### method

* 연산
* object의 행동(behavior)을 구현함

### 생성자(constructor)

* 새로운 객체를 생성할 때마다 클래스가 호출하는 메서드

* 객체가 생성될 때마다 자동으로 호출됨

* 해당 객체의 프로퍼티를 초기화 하거나, 필요한 다른 객체를 생성하는 등의 초기화 작업을 수행함

* 매개변수 가질 수 있음

* 이름

  ```php
  __construct()
  ```

* 문법

  ```php
  class [CLASSNAME]
  {
      function __construct([PARAMETER1], [PARAMETER2], ...)
      {
          생성자가 호출될 때 실행될 코드;
      }
  }
  ```

### 소멸자(destructor)

* 해당 객체를 삭제할 때 호출함

* 매개변수 가질 수 없음

* 이름

  ```php
  __destruct()
  ```

* 문법

  ```php
  class [CLASSNAME]
  {
      function __destruct()
      {
          소멸자가 호출될 때 실행될 코드;
      }
  }
  ```


### 인스턴스(instance)

* 메모리에 생성된 객체

* 생성

  ```php
  $[OBJECTNAME] = new [CLASSNAME]([ARGUMENT1], [ARGUMENT2], ...);
  ```

### 클래스 멤버에 접근

* `->`

  * property에 접근
  * method를 호출

  ```php
  $[OBJECTNAME]->[PROPERTYNAME];
  $[OBJECTNAME]->[METHODNAME];
  ```

* property와 method의 접근 범위 제한 가능

  * 클래스 외부에서 접근 제어자에 따라 접근 가능/불가능

* `$this`

  * 해당 instance가 자기 자신을 가리키는 데 사용하는 변수
  * 객체 내부에서 해당 instance의 property에 접근하고 싶을 때 사용가능

  ```php
  $this->[PROPERTYNAME];
  ```

### 접근 제어(access modifier)

* `public`

  * 외부로 공개됨
  * 해당 객체를 사용하는 어디에서나 직접 접근 가능
  * `var`키워드로 class의 property를 정의하는 경우, 해당 property의 접근 제어가 자동으로 public로 정의됨
  * method를 작성할 때 접근 제어자를 생략하는 경우, 자동으로 public로 정의됨
  * `private`멤버나 `protected`멤버와 프로그램 사이의 interface 역할을 수행함

* `private`

  * 외부로 공개되지 않음
  * 해당 클래스의 멤버에서만 접근 가능

* `protected`

  * 해당 클래스의 멤버와 해당 클래스를 상속받은 자식 클래스에서만 접근 가능
    * 상위 클래스에 대해서 public멤버처럼 취급됨
    * 외부에서는 private멤버처럼 취급됨

  ```php
  class ClassName
  {
      public $publicVar;
      private $privateVar;
      protected $protectedVar;
  
      public function __constructor()
      {
          $this->publicVar = "public property\n";
          $this->privateVar = "private property\n";
          $this->protectedVar = "protected property\n";
      }
  
      public function publicMethod()
      {
          echo "public method\n";
          $this->protectedMethod();
          $this->privateMethod();
      }
      protected function protectedMethod()
      {
          echo "protected method\n";
          echo $this->protectedVar;
      }
      private function privateMethod()
      {
          echo "private method\n";
          echo $this->privateVar;
      }
  }
  
  $object = new ClassName();
  
  echo $object->publicVar;      // 접근 가능
  //echo $object->protectedVar; // 접근 불가능
  //echo $object->privateVar;     // 접근 불가능
  
  $object->publicMethod();      // 호출 가능 // public method
  //$object->protectedMethod(); // 호출 불가능
  //$object->privateMethod();   // 호출 불가능
  ```

### 정보 은닉(data hiding)

* 외부에서 바로 데이터로 접근하지 못하게 함

* 클래스 외부에서 `private`멤버와 `protected`멤버로 직접 접근 불가능

* `public`메소드를 사용하여 해당 클래스의 `private`멤버나 `protected`멤버로 접근 가능

  ```php
  class ClassName
  {
      private $privateVar;
  
      public function __constructor()
      {
          $this->privateVar = "private property";
      }
  
      public function getValue()
      {
          return $this->privateVar;
      }
  
      public function setValue($value)
      {
          $this->privateVar = $value;
      }
  }
  $object = new ClassName();
  $object->setValue("hello"); // setValue() 함수를 통해 $private의 값을 변경할 수 있음.
  echo $object->getValue();     // getValue() 함수를 통해 $private의 값을 출력할 수 있음. // hello
  ```

## 객체 지향 프로그래밍(OOP, Object-Oriented Programming)

* 모든 데이터를 객체(object)로 취급함
* 코드 관리, 코드 변경, 유지 관리가 쉬움
* 특징
  * 추상화(abstraction)
  * 캡슐화(encapsulation)
    * 작성된 코드 재사용
  * 정보 은닉(data hiding)
    * 객체의 실제 구현내용을 외부에서 알지 못하도록 감춤
    * 사용자에게 불필요한 정보를 감춤
    * 객체의 인터페이스를 통해서만 데이터에 접근 가능
    * 보안 강화
  * 상속성(inheritance)
    * 클래스 간의 계층 관계를 만들어 논리적이고 체계적으로 다른 클래스의 기능과 데이터를 사용할 수 있도록 함
  * 다형성(polymorphism)
  * 하나의 변수나 함수 이름이 상황에 따라 다른 의미로 해석될 수 있도록 함
  

### 상속(inheritance)

* 기존의 클래스에 기능을 추가하거나 재정의하여 새로운 클래스를 만드는 것

* 클래스 간의 계층 관계를 만듬

* 상속을 이용하여 기존에 정의되어 있는 클래스의 public, protected에 해당하는 모든 property와 method를 물려받아 새로운 클래스 생성함

  * parent class(부모 클래스)/super class(상위 클래스)
    * 기존에 미리 정의되어 있던 클래스
  * child class(자식 클래스)/sub class(하위 클래스)

* `extend`

* 정의

  ```php
  class [CHILDCLASSNAME] extends [PARENTCLASSNAME]
  {
      [CHILDCLASSNAME] 클래스만의 property와 method;
  }
  ```

* 자식 클래스에서 중복되는 부분 제거 가능

* 기존에 작성된 클래스 재활용 가능

* 하나의 부모 클래스가 여러 자식 클래스 가질 수 있음

* 자식클래스는 하나의 부모 클래스만 가질 수 있음

### 오버라이딩(overriding)

* 이미 정의된 메소드를 같은 이름의 메소드로 다시 정의함

* method overriding

  * 상속받은 부모 클래스의 메소드를 재정의하여 사용하는 것

  ```php
  class A
  {
      public $property = "class A";
      public function showProperty()
      {
          echo $this->property."\n";
      }
  }
  
  class B extends A                    // 클래스 A를 상속 받음.
  {
      public $property = "class B";
      public function showProperty()   // 클래스 A의 메소드를 오버라이딩
      {
          echo "hello ".$this->property."\n";
      }
  }
  
  $a = new A();
  $a->showProperty();                  // 클래스 A의 메소드 호출 // class A
  $b = new B();
  $b->showProperty();                  // 클래스 B의 메소드 호출 // hello class B
  ```

### 정적 멤버(static member)

#### static 키워드

* 클래스를 정의할 때 static 키워드를 사용한 property와 method는 해당 클래스의 instance를 생성하지 않아도 접근 가능

* 특징

  * static property는 인스턴스화된 객체에서 접근 불가
  * static method는 인스턴스화된 객체에서 접근 가능
  * static method내에서는 `$this`  의사 변수 사용 불가

  ```php
  class StaticMember
  {
      public static $staticProperty = "static property";
      public static function showProperty()
      {
          echo self::$staticProperty."\n";
      }
  }
  
  echo StaticMember::showProperty();  // 호출 가능 // static property
  echo StaticMember::$staticProperty . "\n"; // 접근 가능 // static property
  
  $var = new StaticMember();          // 인스턴스 생성
  echo $var->showProperty();          // 호출 가능 // static property
  
  //echo $var->$staticProperty;       // 접근 불가능
  ```

#### 범위 지정 연산자(::)

* 클래스의 정의 내에서 property 또는 method를 사용하고 싶은 경우

* 클래스의 상수, 정적(static)멤버 또는 재정의된 멤버에 접근 가능하게 함

* 클래스의 정의 외부에서 클래스에 접근하는 경우

  ```php
  [CLASSNAME]::[CONSTANTNAME];
  [CLASSNAME]::$[PROPERTYNAME];
  [CLASSNAME]::[METHODNAME]();
  ```

* 클래스의 정의 내에서 특정 property 또는 metho에 접근하는 경우

  * `self` : 자기 자신에 접근
  * `parent` : 부모 클래스에 접근

  ```php
  self::$[PROPERTYNAME];
  parent::[CONSTANTNAME];
  ```

### 인터페이스

#### 추상 메소드(abstract method)

* 자식 클래스에서 overriding 해야만 사용 가능한 method

* 선언부만 존재함(구현부 없음)

* 작성되어 있지 않은 구현부를 자식 클래스에서 오버라이딩 하여 사용함

* 문법

  ```php
  abstract 접근제어자 fuction [METHODNAME]();
  ```

### 추상 클래스(abstract class)

* 최소 하나 이상의 추상 메소드를 포함하는 클래스

* 다형성을 가진 method의 집합 정의해줌

* 반드시 사용되어야 하는 method를 추상 메소드로 선언해 놓으면, 이 클래스를 상속받는 모든 클래스에서는 이 추상 메소드를 반드시 재정의해야함

* 상속을 통해 자식 클래스를 만들고 만든 자식 클래스에서 추상 클래스의 모든 추상 메소드를 오버라이딩한 후, 자식 클래스의 인스턴스 생성 가능

  ```php
  abstract class AbstractClass            // 추상 클래스
  {
      abstract protected function move(); // 추상 메소드
  
      abstract protected function stop();
      
      public function start() // 공통 메소드
  
      {
  		...
      }
  }
  ```

  * 동작이 정의되어 있지 않은 추상 메소드를 포함하고 있으므로 인스턴스 생성 불가

### 인터페이스(interface)

* 다른 클래스를 작성할 때 기본이 되는 틀 제공

* 다른 클래스 사이의 중간 매개 역할을 담당

* 일종의 추상 클래스

* 인터페이스를 사용하면, 클래스가 반드시 구현해야 할 메소드가 어떻게 동작하는지 알 필요 없이 다른 부분의 코드 작성 가능

* 메소드의 구현부가 정의되어 있지 않은 추상 메소드들로 구성되어 있음

* 내부의 모든 추상 메소드는 public method

* `interface` 키워드

* 문법

  ```php
  interface [INTERFACENAME]
  {
      구현할 메소드;
  }
  ```

* `implements` 키워드를 사용하여 구현함

* interface를 구현하는 클래스는 인터페이스의 모든 method를 구현해야함, 이렇게 구현되는 메소드는 interface에서 정의된 형태와 완전히 같은 형태로 정의되어야 함

* interface의 모든 method는 클래스 안에서 모두 구현되어야 함

  ```php
  interface Transport              // 인터페이스의 정의
  {
      public function move();      // 구현할 메소드
      public function stop();
  }
  
  class Car implements Transport   // Transport 인터페이스를 구현하는 Car 클래스
  {
      function move()              // 메소드 구현
      {
          ...
      }
  
      function stop()              // 메소드 구현
      {
          ...
      }
  }
  ```

* 클래스처럼 `extends` 키워드를 사용하여 상속받을 수 있음

  ```php
  interface Transport                  // 인터페이스의 정의
  {
      public function move();          // 구현할 메소드
  
      public function stop();          // 구현할 메소드
  }
  
  
  interface Overland extends Transport // Transport 인터페이스를 상속받는 Overland 인터페이스
  {
      public function highpass();      // 구현할 메소드
  }
  
  class Car implements Overload        // Overland 인터페이스를 구현하는 Car 클래스
  {
      function move()                  // 메소드 구현
      {
          ...
      }
  
      function stop()                  // 메소드 구현
      {
          ...
      }
  
      function highpass()              // 메소드 구현
      {
          ...
      }
  }
  ```

* 각각의 interface를 쉼표(`,`)로 구분하여 여러 개의 interface를 동시에 상속받을 수 있음

### 오버로딩

#### 다형성(polymorphism)

* 하나의 property가 여러 가지 상태를 가질 수 있는 것
* overloading과 late static bindings을 통해 다형성을 구현함

#### 오버로딩(overloading)

* property 또는 method를 동적으로 생성함
* overloading으로 생성된 멤버는 해당 클래스의 magic method를 통해 다양한 형태로 처리 가능
* overloading되는 method는 반드시 public로 정의되어야 함

#### 프로퍼티 오버로딩(property overloading)

* inaccessible property를 오버로딩하기 위해 아래와 같은 매직 메소드를 구현해야함

  * inaccessible property : 현재 영역에서는 정의되어 있지 않거나, 접근 제어로 인해 보이지 않는 프로퍼티를 의미함

* magic methon 원형

  ```php
  public void __set(string $name, mixed $value)
  public mixed __get(string $name)
  public bool __isset(string $name)
  public bool __unset(string $name)
  ```

  * `__set()` : 접근 불가 프로퍼티의 값을 설정할 때 호출됨
  * `__get()` : 접근 불가 프로퍼티의 값을 읽을 때 호출됨
  * `__isset()` : 접근 불가 프로퍼티에 대해 isset() 함수 또는 empty() 함수가 호출될 때 호출됨
  * `__unset()` : 접근 불가 프로퍼티에 대해 unset() 함수가 호출될 때 호출됨

  ```php
  class PropertyOverloading
  {
      private $data = array(); // 오버로딩된 변수가 저장될 배열 생성
      public $declared = 10;   // public으로 선언된 프로퍼티
      private $hidden = 20;    // private로 선언된 프로퍼티
  
      public function __set($name, $value)
      {
          echo "$name 프로퍼티를 {$value}의 값으로 생성합니다!(__set)\n";
          $this->data[$name] = $value;
      }
  
      public function __get($name)
      {
          echo "$name 프로퍼티의 값을 읽습니다!(__get)\n";
          if (array_key_exists($name, $this->data)) {
              return $this->data[$name];
          } else {
              return null;
          }
      }
  
      public function __isset($name)
      {
          echo "$name 프로퍼티가 설정되어 있는지 확인합니다!(__isset)\n";
          return isset($this->data[$name]);
      }
  
      public function __unset($name)
      {
          echo "$name 프로퍼티를 해지합니다!(__unset)\n";
          unset($this->data[$name]);
      }
  }
  
  $obj = new PropertyOverloading(); // PropertyOverloading 객체 생성
  
  $obj->prop = 1;              // 동적 프로퍼티 생성 // prop 프로퍼티를 1의 값으로 생성합니다!
  
  echo $obj->prop;             // 동적 프로퍼티에 접근 // prop 프로퍼티의 값을 읽습니다!
  
  var_dump(isset($obj->prop)); // 동적 프로퍼티로 isset() 함수 호출 // 1prop 프로퍼티가 설정되어 있는지 확인합니다! bool(true)
  
  unset($obj->prop);           // 동적 프로퍼티로 unset() 함수 호출 // prop 프로퍼티를 해지합니다!(__unset)
  var_dump(isset($obj->prop)); // 동적 프로퍼티로 isset() 함수 호출 // prop 프로퍼티가 설정되어 있는지 확인합니다!(__isset) bool(false)
  echo $obj->declared; // 선언된 프로퍼티는 오버로딩을 사용하지 않음. // 10 // 일반적인 방법으로 선언된 프로퍼티로 접근할 때 __get() 메소드 호출하지 않음
  echo $obj->hidden;   // private로 선언된 프로퍼티는 클래스 외부에서 접근할 수 없으므로, 오버로딩을 사용함. // hidden 프로퍼티의 값을 읽습니다!(__get) // __get() 메소드 호출함
  ```

#### 메소드 오버로딩(method overloading)

* inaccessible method를 오버로딩하기 위해 아래와 같은 매직 메소드를 구현해야 함

* magic method의 원형

  ```php
  public mixed __call(string $name, array $arguments)
  public static mixed __callStatic(string $name, array $arguments)
  ```

  * `__call()` : 클래스 영역에서 접근 불가 메소드를 호출할 때 호출됨
  * `__callStatic()` : 정적(static) 영역에서 접근 불가 메소드를 호출할 때 호출됨

  ```php
  class MethodOverloading
  {
      public function __call($name, $arguments)
      {
          echo join(", ", $arguments)."에서 접근 불가 메소드를 호출합니다!\n";
      }
  
      public static function __callStatic($name, $arguments)
      {
          echo join(", ", $arguments)."에서 접근 불가 메소드를 호출합니다!\n";
      }
  }
  
  $obj = new MethodOverloading();             // MethodOverloading 객체 생성
  $obj->testMethod("클래스 영역");            // 클래스 영역에서 접근 불가 메소드 호출 // 클래스 영역에서 접근 불가 메소드를 호출합니다!
  MethodOverloading::testMethod("정적 영역"); // 정적 영역에서 접근 불가 메소드 호출 // 정적 영역에서 접근 불가 메소드를 호출합니다!
  ```

### 늦은 정적 바인딩

#### 바인딩(binding)

* 프로그램에 사용된 구성 요소의 실제 값 또는 프로퍼티를 결정짓는 행위
  * static binding : 실행 시간 전에 일어나고, 실행 시간에는 변하지 않은 상태로 유지되는 바인딩
  * dynamic binding : 실행 시간에 이루어지거나 실행 시간에 변경되는 바인딩으로, late binding 이라고도 불림
* php에서는 static binding 과 dynamic binding의 중간 정도 수준인 늦은 정적 바인딩(LSB)를 제공함

#### 늦은 정적 바인딩(late static bindings, LSB)

* static 키워드와 범위 지정 연산자(::)를 사용하여 수행함
* 마지막으로 호출한 비전송 호출(non-forwarding call)의 클래스 이름을 저장하여 동작함
  * 정적 메소드 호출에서는 범위 지정 연산자(::) 좌측에 명시된 클래스 이름을 저장함
  * 비정적 메소드 호출에서는 해당 객체의 클래스 이름을 저장함
* `static::`
  * 늦은 바인딩 : 정의된 클래스를 컴파일 시간에 결정할 수 없고, 프로그램 실행 시 전달되는 정보로 결정함
  * 정적 바인딩 : 정적 메소드 호출에 사용 가능함

#### 정적 메소드 호출에서의 늦은 정적 바인딩

* self 키워드와 범위 지정 연산자(::)를 사용하여 정적 메소드를 호출함

  ```php
  class A
  {
      public static function className()
      {
          echo __CLASS__;
      }
  
      public static function printClass()
      {
          self::className();
      }
  }
  
  class B extends A
  {
      public static function className()
      {
          echo __CLASS__;
      }
  }
  
  B::printClass(); // A
  ```

  

* `array_key_exists()`
  
* 인수로 전달받은 키가 해당 배열에 저장되어 있으면 true 반환함
  
* `declare()`

* `register_tick_function()`

  * 명령문을 실행할 때마다 호출하는 함수(명령문 먼저 실행됨)
  * 함수 호출시부터 명령문을 실행할 때마다 호출됨

  ```php
  register_tick_function(callable $function [,mixed $...]) : bool
  ```

  * return 값 : bool

  * parameter로 함수 대입

    ```php
    function tick_handler()
    {
        echo "tick_handler\n"
    }
    
    $y = 1; // register_tick_function() 호출 전이므로 실행되지 않음
    
    register_tick_function('tick_handler', true) // tick_handler()
    
    $a = 1; // 명령문 실행되면서 register_tick_function함수도 실행됨 // tick_handler()
    
    if ($a > 0) {
        $a += 2;// 명령문 실행되면서 register_tick_function함수도 실행됨 // tick_handler()
        print($a); // 명령문 실행되면서 register_tick_function함수도 실행됨 // 3tick_handler()
    }
    ```

  * parameter로 클래스 안의 함수 대입

    ```php
    declare(ticks=1);
    
    class Counter {
        private $counter = 0;
    
        public function increase()
        {
            $this->counter++;
        }
    
        public function print()
        {
            return $this->counter;
        }
    }
    
    $obj = new Counter;
    
    register_tick_function([&$obj, 'increase'], true); // increase() 실행됨
    
    for ($i = 0; $i < 100; $i++)
    {
        $a = 3; // increate() 실행됨
    }
    echo $a; // 3 // increase() 실행됨
    
    var_dump("Number of basic low level operations: " . $obj->print()); // string(41) "Number of basic low level operations: 103" // increase() 실행됨 but 출력되는 값에 적용되지 않음(출력이 먼저)
    ```

* `unregister_tick_function()`

  * `register_tick_function()`을 해제하는 함수

    ```php
    declare(ticks=1);
    
    class Counter {
        private $counter = 0;
    
        public function increase()
        {
            $this->counter++;
        }
    
        public function print()
        {
            return $this->counter;
        }
    }
    
    $obj = new Counter;
    
    register_tick_function([&$obj, 'increase'], true); // increase() 실행됨
    
    for ($i = 0; $i < 100; $i++)
    {
        $a = 3; // increate() 실행됨
    }
    unregister_tick_function([&$obj, 'increase']);
    echo $a; // 3 // increase() 실행됨
    
    var_dump("Number of basic low level operations: " . $obj->print()); // string(41) "Number of basic low level operations: 102" // increase() 실행됨 but 출력되는 값에 적용되지 않음(출력이 먼저)
    ```

* 

* `var_dump()`

​    

