# 배열(array)

* 맵(map)으로 이루어진 , 순서가 있는 집합
* map : 한 쌍의 key와 value로 이루어져 있음
* 배열 요소(array element) : 배열을 구성하는 각각의 맵

## 1차원 배열

* 선언

  ```php
  $[ARRAYNAME] = array();
  $[ARRAYNAME][[INDEX]]
  ```

* 배열 요소의 참조

  * 배열 요소에 접근하기 위해 인덱스(index) 사용함
  * 인덱스는 0부터 시작함
  * `[]`연산자를 사용하여 배열의 각 요소를 참조함

* 배열 요소의 추가

  * 코드를 명확하게 하고 오류를 피하기 위해서는 배열을 먼저 선언해 주는 것이 좋음

  ```php
  $arr = array();     // 배열 생성
  $arr[0] = "apple";  // 배열 요소 추가
  $arr[1] = "banana";
  $arr[2] = "orange";
  ```

  * 배열 생성과 동시에 요소 초기화 기능

    ```php
    $[ARRAYNAME] = array([ARRAYELEMENT1], [ARRAYELEMENT2], ...);
    ```

    * 초기화 리스트에 따라 각각의 배열 요소가 순서대로 추가된 배열이 생성됨

    ```php
    $arr = array("apple", "banana", "orange");  // 배열 생성과 동시에 초기화
    ```

  * 배열이 존재하지 않는 경우 해당 이름으로 새로운 배열 만든 후에 배열 요소 추가

    ```php
    $arr[0] = "apple";  // 배열이 존재하지 않으므로, 먼저 배열을 생성한 후에 요소가 추가됨.
    $arr[1] = "banana";
    $arr[2] = "orange";
    var_dump($arr); // [apple, banana, orange]
    ```

  * 배열 요소의 인덱스 생략 가능함

    * 인덱스가 0부터 시작하여 1씩 증가하며 순서대로 저장됨

    ```php
    $arr[] = "apple";  // 배열 인덱스를 생략하여, 순서대로 배열에 추가됨.
    $arr[] = "banana";
    $arr[] = "orange";
    ```

* 홀(hole)

  * 인덱스에 대응하는 배열 요소가 없는 부분
    * 특정인덱스(지정한인덱스)에만 배열 요소를 추가할 수 있음
    * 배열요소를 추가한 인덱스를 제외한 나머지 인덱스에는 배열 요소 존재하지 않음
  * 배열의 홀(hole)을 참조하게 되면, 초기화되지 않은 변수를 참조할 때처럼 NULL을 반환함

  ```php
  $arr = array();            // 배열의 생성
  $arr[10] = "banana";       // 인덱스 10에만 배열 요소를 추가함.
  
  var_dump($arr);
  var_dump($arr[0]);         // NULL
  var_dump(isset($arr[0]));  // bool(false)
  var_dump(isset($arr[10])); // bool(true)
  ```

* 루프를 이용한 배열로의 접근

  * for문을 사용하면 배열의 인덱스를 이용하여 쉽고 간단하게 배열 요소 접근 가능

    ```php
    $arr = array("apple", "banana", "orange");
    for($i = 0; $i < count($arr); $i++){
        echo $arr[$i]."\n";
        // apple
        // banana
        // orange
    }
    ```

    * hole을 가지는 배열에서는 for문을 사용하여 접근불가

  * foreach 문을 사용하여 간편하게 배열 요소에 접근 가능

    * hole이 있는 배열에서 hole이 아닌 배열 요소에만 정확히 접근함

    ```php
    $arr = array(); // 배열의 생성
    $arr[2] = "apple";
    $arr[3] = "banana";
    $arr[4] = "orange";
    // $arr[0]과 $arr[1]은 배열의 홀(hole)이 됨.
    
    for ($i = 0; $i < count($arr); $i++) {
        echo "\$arr[{$i}] : ".$arr[$i]."\n";
        // $arr[0] : 
        // $arr[1] : 
        // $arr[2] : apple
    }
    
    foreach ($arr as $element){
        echo $element."\n";
        // apple
        // banana
        // orange
    }
    ```

## 다차원 배열(multidimensional array)

* 2차원 이상의 배열
* 배열 요소로 또 다른 배열 사용함

### 2차원 배열

* 배열 요소로 또 다른 1차원 배열을 사용하는 배열

* 행과 열을 가진 행렬과 같은 모양으로 구성됨

* 선언

  ```php
  $[ARRAYNAME] = array(
  	array(),
      array(),
      ...
  );
  ```

  * 행의 수 : 1차원 배열의 개수
  * 열의 수 : 각 1차원 배열의 배열 요소 개수

* 배열 요소 입력

  * 배열 요소에 접근하기 위해 인덱스 사용함
  * `[]`연산자를 두 번 사용하에 2차원 배열에 속한 요소에 접근함

  ```php
  $arr = array( // 1차원 배열을 3개 갖는 2차원 배열 선언
      array(),
      array(),
      array()
  );
  
  $arr[0][0] = "apple"; // 배열 요소 입력
  $arr[0][1] = "korea";
  $arr[0][2] = 1000;
  
  $arr[1][0] = "banana";
  $arr[1][1] = "philippines";
  $arr[1][2] = 2000;
  
  $arr[2][0] = "orange";
  $arr[2][1] = "us";
  $arr[2][2] = 1500;
  
  echo $arr[0][0].", ".$arr[0][1].", ".$arr[0][2]."\n"; // apple, korea, 1000
  echo $arr[1][0].", ".$arr[1][1].", ".$arr[1][2]."\n"; // banana, philippines, 2000
  echo $arr[2][0].", ".$arr[2][1].", ".$arr[2][2]; // orange, us, 1500
  ```

  * 배열 생성과 동시에 초기화 가능

    ```php
    $[ARRAYNAME] = array(
    	array([ARRAYARGUMENT00], [ARRAYARGUMENT01], ...),
        array([ARRAYARGUMENT10], [ARRAYARGUMENT01], ...),
        ...
    );
    ```

    ```php
    $arr = array( // 1차원 배열을 3개 갖는 2차원 배열 선언과 동시에 초기화
        array("apple", "korea", 1000),
        array("banana", "philippines", 2000),
        array("orange", "us", 1500)
    );
    var_dump($arr);
    ```

* 루프를 이용한 2차원 배열로의 접근

  * for 문에 배열의 인덱스를 이용하여 배열 요소에 접근 가능
  * 행과 열에 대해 for문을 2번 사용

  ```php
  $arr = array( // 1차원 배열을 3개 갖는 2차원 배열 선언과 동시에 초기화
      array("apple", "korea", 1000),
      array("banana", "philippines", 2000),
      array("orange", "us", 1500)
  );
  for($row = 0; $row < 3; $row++) {
      for($column = 0; $column < count($arr[$row]); $column++){
          echo $arr[$row][$column].", "; // apple, // korea, // 1000, // banana, // philippines, // 2000, // orange, // us, // 1500, 
      }
  }
  ```

### 3차원 배열

* 배열 요소로 2차원 배열을 사용하는 배열

* 선언

  ```php
  $[ARRAYNAME] = array(
  	array(
          array(),
          array(),
          ...
      ),
      array(
          array(),
          array(),
          ...
      ),
      ...
  );
  ```

* 생성과 동시에 초기화 가능

  ```php
  $[ARRAYNAME] = array(
  	array(
          array([ARRAYARGUMENT000], [ARRAYARGUMENT001], ...),
          array([ARRAYARGUMENT010], [ARRAYARGUMENT011], ...),
          ...
      ),
      array(
          array([ARRAYARGUMENT100], [ARRAYARGUMENT101], ...),
          array([ARRAYARGUMENT110], [ARRAYARGUMENT111], ...),
          ...
      ),
      ...
  );
  ```

  ```php
  $arr = array( // 2차원 배열을 2개 갖는 3차원 배열 선언과 동시에 초기화
      array(
          array("apple", "korea", 1000),
          array("banana", "philippines", 2000),
          array("orange", "us", 1500)
      ),
      array(
          array("carrot", "vietnam", 500),
          array("cucumber", "korea", 1000),
          array("pumpkin", "china", 2000)
      )
  );
  var_dump($arr);
  ```

## 연관 배열

* 연관 배열(associative array)

  * 배열의 인덱스를 다양한 타입으로 설정한 배열

  * 정수와 문자열 이외에 다른 타입의 값을 key로 사용하면, 내부적으로 정수와 문자열로 타입 변환이 이루어짐

  * 선언

    ```php
    $[ARRAYNAME] = array();
    ```

* 연관 배열의 참조

  * 배열 이름과 key를 사용하여 각 요소를 참조함

    ```php
    $[ARRAYNAME]["[KEY]"] = [VALUE];
    ```

  ```php
  $arr = array();        // 배열 생성
  $arr["apple"] = 1000;  // 연관 배열 요소 추가
  $arr["banana"] = 2000;
  $arr["orange"] = 1500;
  var_dump($arr);
  ```

  * 생성과 동시에 초기화 가능

    * key와 value 사이에 `=>`를 넣어주면 배열 요소에 저장될 key와 value 지정 가능

    ```php
    $[ARRAYNAME] = array("[KEY1]" => "[VALUE1]", "[KEY2]" => "[VALUE2]", ...);
    ```

    ```php
    // 연관 배열 생성과 동시에 초기화
    $arr = array("apple" => 1000, "banana" => 2000, "orange" => 1500);
    echo $arr["apple"].", ".$arr["banana"].", ".$arr["orange"]; // 1000, 2000, 1500
    ```

  * 생성된 연관 배열에 새로운 요소 추가 가능

    ```php
    $arr = array("apple" => 1000); // 연관 배열 생성과 동시에 초기화
    $arr["banana"] = 2000;         // 생성된 연관 배열에 요소 추가
    $arr["orange"] = 1500;
    var_dump($arr);
    ```

* 루프를 이용한 연관 배열로의 접근

  * foreach 문을 사용하여 접근함

    * 연관 배열 요소의 key와 value를 변수에 따로 저장하여 루프 내에서 사용 가능

    ```php
    $arr = array("apple" => 1000, "banana" => 2000, "orange" => 1500);
    
    foreach ($arr as $key => $value) {
        echo $key." ".$value."\n";
        // apple 1000
        // banana 2000
        // orange 1500
    }
    ```

  * `each()`함수를 사용하여 접근함

    * 배열 커서(array cursor)가 현재 가리키고 있는 배열 요소를 반환하고, 다음 배열 요소를 가리키도록 함
    * 가리키는 요소의 다음 요소가 배열의 마지막 요소이면, 더 이상 동작하지 않음

    ```php
    $arr = array("apple" => 1000, "banana" => 2000, "orange" => 1500);
    
    while($element = each($arr)) {
        echo $element['key']." ".$element['value']."\n";
        // apple 1000
        // banana 2000
        // orange 1500
    }
    ```

    

