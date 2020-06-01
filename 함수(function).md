# 함수(function)

* 전역 범위(global scope)를 가짐
  * 같은 스크립트 내에서는 정의된 위치와 상관없이 호출 가능
* 오버로딩을 지원하지 않음
  * 이미 선언된 함수를 다시 선언할 수 없음



## 정의

```php
function [FUNCTIONNAME]([PARAMETER1], [PARAMETER2], ...)
{
    함수가 호출되었을 때 실행될 코드;
}
```

* `function`로 함수의 정의 시작
* 함수의 이름, 매개변수, 블록({}) 사이에 들어갈 코드 명시



## 장점

* 반복적인 코드작성을 줄일 수 있음
* 모듈화로 인하여 코드의 가독성이 좋아짐
* 유지보수가 용이함



## 구조

```php
function [FUNCTIONNAME]($[PARAMETER1], $[PARAMETER2], ...)
{
    함수가 호출 되었을 때 실행될 코드;
}

// 함수 호출
[FUNCTIONNAME]([ARGUMENT1], [ARGUMENT2], ...)
```

* `[FUNCTIONNAME]` : 함수를 구분하는 식별자(identifier)
* `[PARAMETER]` : 함수를 호출할 때 인수로 전달된 값을 함수 내부에서 사용할 수 잇도록 해주는 변수
  * 인수로 전달받은 값을 함수에서 사용
  * 여러 개를 가질 수 있으며, 쉼표(,)를 사용하여 구분
  * `[ARGUMENT]` : 함수가 호출될 때 함수로 값을 전달해주는 변수
  * `{}` : 함수가 호출되면 중괄호 안의 코드가 실행됨



## 함수 이름

* 문자와 숫자, 언더스코어(`_`)만 사용 가능
* 숫자로 시작 불가
* 독립적인 이름 가짐(중복 불가)
* 대소문자 구별하지 않음(but, 구별하는 것을 선호함)



## 사용자 정의 함수(user defined functino)

* 사용자가 직접 만든 함수
* 해당 함수가 정의된 PHP 스크립트에서만 호출 가능



## 호출

* 내장함수 : 모든 PHP 스크립트에서 호출가능

* 사용자 정의 함수 : 해당 PHP 스크립트에서만 호출 가능

* 방법

  * 함수의 정의와 같은 형태

  ```php
  $[VARIABLE] = [FUNCTIONNAME]([ARGUMENT1], [ARGUMENT2], ...);
  ```

  * gkatn `[FUNCTIONNAME]`을 호출하면서 인수로 `[ARGUMENT]`를 전달함

  * 인수로 전달된 값들은 함수에서 정의된 `[PARAMETER]`에 대임 됨

    `[ARGUMENT1]` => `[PARAMETER1]`, `[ARGUMENT2]` => `[PARAMETER2]`

* 함수 호출 시 전달된 인수는 매개변수의 왼쪽부터 차례대로 대입됨



## 값 반환

* return 문

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



## 매개변수(parameter)와 인수(argument)

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



## 함수의 활용

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



## 내장 함수

### magic method

* 특수한 기능을 위해 미리 정의한 메소드
* 메소드 이름, 매개변수, 반환 타입, 호출의 타이밍만 정해져 있음
* 내용은 사용자가 직접 작성 가능함
* 모든 매직 메소드의 이름은 두 개의 언더스코어(`__`)로 시작함

### 변수 관련 함수

* 변수의 타입 변경

  * `gettype()`
    * 변수를 전달하면 타입에 따라 해당 타입의 이름을 문자열로 반환함
    * `float`형의 경우에는 `double` 반환함
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
  |                is_null()                 | 전달받은 변수의 타입이 NULL인지를 확인함                 |
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

  * `unser()`

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

### 배열 관련 함수

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
    * 두 번째 인수로 배열 요소를 정렬할 기준 전달
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

  * 사용자가 정의한 비교 함수를 사용하여, 배열 요소의 key를 기준으로 정렬함

  * `uasort()`

    * 사용자가 정의한 비교함수를 사용하여, 인덱스 연관성을 유지한 채 배열 요소를 정렬함

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

### 문자열 관련 함수

* 문자열의 길이

  * `strlen()`
    * 전달받은 문자열의 길이(문자열에 포함된 문자의 개수)를 반환함
    * 함수에 전달된 문자열에 한글이 포함되면 문자열의 총 바이트(byte) 수를 반환함
  * `mb_strlen()`
    * 한글이 포함된 문자열의 정확한 문자열 길이를 반환함
    * 두 번째 인수로 인코딩 방식 전달받을 수 있음
      * 전달받은 인코딩 방식으로 해당 문자열 해석하여 문자열 길이 반환함
    * 두 번째 인수를 전달받지 못하는 경우, 현재 시스템의 내부 인코딩 방식을 사용함

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
    * 전달받은 두 개의 문자열으 서로 비교함
    * 첫 번째 인수의 문자열이 두 번째 인수의 문자열보다 크면 양수를, 작으면 음수를, 완전히 같으면 0을 반환함
    * 대소문자 구분하지 않음
  * `strnatcasecmp()`
    * 전달받은 두 개의 문자열을 서로 비교함
    * 첫 번째 인수의 문자열이 두 번째 인수의 문자열보다 크면 양수를, 작으면 음술르, 완전히 같으면 0을 반환함
    * 대소문자 구분
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
    * 해당 문자열에 일치한느 부분이 존재하면, 처음으로 일치하는 부분을 포함한 이후의 모든 문자를 같이 반환함
    * 일치하는 부분이 존재하지 않으면 false 반환함
  * `stristr()`
    * 해당 문자열에서 전달받은 문자열과 처음으로 일치하는 부분을 찾음
    * 대소문자를 구별하지 않음
    * 해당 문자열에 일치하는 부분이 존재하면, 처음으로  일치하는 부분을 포함한 이후의 모든 문자를 같이 반환함
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
      * 전달받은 길이가 음수인 경우 특정 인덱스부터 문자열 끝부터 전달받은 음수의 절댓값까지의 문자열을 반환함

* 문자열 대소문자 바꾸기

  * `strtolower()`
    * 전달받은 문자열의 모든 문자를 소문자로 바꿔줌
  * `strtoupper()`
    * 전달받은 문자열의 모든 문자를 대문자로 바꿔줌
  * `ucfirst()`
    * 전달받은 문자열의 첫 번째 문자만을 대문자로 바꿔줌
  * `ucwords()`
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
    * 전달받은 배열의 각 요소를 특정 문자를 사용하여 하나로 합쳐진 문자열로 반환함
  * `strtok()`
    * 전달받은 문자열을 특정 문자를 기준으로 토큰화함
    * 해당 문자열을 한 번에 모두 나누지 않고, 한 번에 하나씩만 코든화함
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

### 날짜와 시간 관련 함수

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

    |      형태      | 설명                                                         | 예시                            |
    | :------------: | ------------------------------------------------------------ | ------------------------------- |
    |       d        | 날짜를 두 자리 숫자로 표현함                                 | 00부터 31                       |
    |       D        | 요일을 세 개의 문자로 표현함                                 | Mon에서 Sun                     |
    |       j        | 날짜를 숫자로 표현함                                         | 1부터 31                        |
    | ㅣ(소문자 'L') | 요일을 완전한 문자열로 표현함                                | Sunday부터 Saturday             |
    |       N        | 요일을 ISO-8601 숫자로 표현함                                | 1(월요일)부터 7(일요일)         |
    |       S        | 날짜 뒤에 영어 서수를 붙임                                   | st, nd, rd, th, j               |
    |       w        | 요일을 숫자로 표현함                                         | 0(일요일)부터 6(토요일)         |
    |       z        | 일 년 중 몇 번째날인지를 숫자로 표현함                       | 0부터 365                       |
    |       W        | 일 년 중 몇 번째 주인지를 숫자로 표현함                      | 42(그 해의 42번째 주)           |
    |       F        | 월을 완전한 문자열로 표현함                                  | January에서 December            |
    |       m        | 월을 두 자리 숫자로 표현함                                   | 01부터 12                       |
    |       M        | 월의 축약형을 세 개의 문자로 표현함                          | Jan에서 Dec                     |
    |       n        | 월을 숫자로 표현함                                           | 1부터 12                        |
    |       t        | 해당 월의 총일 수를 숫자로 표현함                            | 28부터 31                       |
    |       L        | 윤년 여부를 표현함                                           | 윤년엔 1, 그 외엔 0             |
    |       o        | ISO-8601 연도값으로 Y값과 같은 값을 나타냄<br/>하지만 W값이 이전 해나 다음 해에 포함되면, 연도를 이 값으로 사용함 | 1999나 2003                     |
    |       Y        | 연도를 완전한 네 자리 숫자로 표현함                          | 1999나 2003                     |
    |       y        | 연도를 두 자리 숫자로 표현함                                 | 99나 03                         |
    |       a        | 오전과 오후의 소문자를 표현함                                | am 또는 pm                      |
    |       A        | 오전과 오후의 대문자를 표현함                                | AM 또는 PM                      |
    |       B        | 견본 인터넷 시간을 표현함                                    | 000에서 999                     |
    |       g        | 12시간 형식으로 시간을 표현함                                | 1부터 12                        |
    |       G        | 24시간 형식으로 시간을 표현함                                | 0부터 23                        |
    |       h        | 12시간 형식 시간을 두 자리 숫자로 표현함                     | 01부터 12                       |
    |       H        | 24시간 형식 시간을 두 자리 숫자로 표현함                     | 00부터 23                       |
    |       i        | 분을 두 자리 숫자로 표현함                                   | 00부터 59                       |
    |       s        | 초를 두 자리 숫자로 표현함                                   | 00부터 59                       |
    |       u        | 초를 마이크로초로 표현함                                     | 54321                           |
    |       e        | 시간대(timezone) 식별자를 표현함                             | UTC, GMT                        |
    | I(대문자 'i')  | 서머타임 적용 여부를 표현함                                  | 서머타임이면 1, 아니면 0        |
    |       O        | 그리니치 시각(GMT)과 시차를 표현함                           | +0200                           |
    |       P        | 시와 분 사이에 콜론이 들어가는 그리니치 시각(GMT)과 시차를 표현함 | +02:00                          |
    |       T        | 시간대(timezone)를 나타내는 축약어                           | EST, MDT                        |
    |       Z        | 시간대(timezone)를 나타내는 오프셋 초를 표현함.<br/>UTC 서쪽은 항상 음수, UTC 동쪽은 항상 양수로 표현됨 | -43200부터 50400                |
    |       c        | ISO-8601 형식의 날짜를 표현함                                | 2004-02-12T15:19:21+00:00       |
    |       r        | RFC 2822 형식의 날짜를 표현함                                | Thu, 21 Dec 2000 16:01:07 +0200 |
    |       U        | timestamp를 표현함                                           | time() 참조                     |

    * timestamp : GMT 기준 1970년 1월 1일 0시 0분부터 지금까지의 시간을 초(second) 단위로 나타낸 것

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

### 수학 관련 함수

* 최댓값과 최솟값

  * `max()`
    * 전달받은 수 중에서 가장 큰 수를 반환함
  * `min()`
    * 전달받은 수 중에서 가장 작은 수를 반환함

* 올림과 내림

  * `floor()`
    * 인수로 전달받은 값과 같거나 작은 수 중에서 가장 큰 정수를 반환함
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

