# C 내용 정리

본 문서는 C를 학습하면서 새롭게 알게 된 내용들을 정리한 문서이다.

---

- **변수 선언**
  - 변수 이름은 영문과 밑줄문자(_)로 시작할 수 있지만 숫자로는 시작할 수 없다.
  - ```C
    int num1 = 20, num2 = 30; 
    ```
    이런 식으로 여러 번수를 한꺼번에 초기화 하면서 선언할 수 있다.

---

- **디버깅 중지**

  *Shift + F5*

---

- **정수형 변수**
  1. 부호 있는 정수형 변수
      - char(1byte) < short(2byte) < int(4byte) = long(4byte) < long long(8byte)
      - char, short, int는 서식지정자 %d로 출력하지만 long은 %ld, long long은 %lld로 출력한다.
      - C에서는 char형이 기본적으로 정수형이다. 문자형과 정수형 둘 다 쓰인다.
        ```C
        char a = 65;
        printf("%c", a);
        // A 출력
        printf("%d", a);
        // 65 출력
      
  2. 부호 없는 정수형 변수
      - 부호 없는 정수형 변수는 unsigned를 붙인다. 나머지는 부호 있는 정수형 변수와 동일하다.
      - unsigned char, short는 서식지정자 %d로 출력하지만 unsigned int는 %u, long은 %lu, long long은           %llu로 출력한다.
      
---

- **오버플로우, 언더플로우**
  
  char, short, int, long, long long등에 저장할 수 있는 범위를 넘어서면 오버플로우(overflow)가 발생하여   최솟값부터 다시 시작하고 
  
  반대로 최솟값보다 작아지면 언더플로우(underflow)가 발생하여최댓값부터 다시 시작하게 된다.
  
  ![overflow, underflow](https://dojang.io/pluginfile.php/75/mod_page/content/34/unit7-2.png)
  
---

- **sizeof**
  - 자료형(타입)의 크기를 바이트(byte)단위로 구하는 연산자
  - 사용 방법
    - sizeof 표현식
    - sizeof(자료형)
    - sizeof(표현식)
    
    ex)
    ```C++
    int num1 = 0;
    int size = sizeof num1; // size = 4
    size = sizeof(short); // size = 2
  
    char num2 = 1;
    size = sizeof(num2); // size = 1
    ```
  
---

- **정수 자료형의 최솟값과 최댓값**
  - `<limits.h>`헤더파일에 정리되어 있다.
    |자료형|최솟값|최댓값|
    |------|------|------|
    |char|CHAR_MIN|CHAR_MAX|
    |short|SHRT_MIN|SHRT_MAX|
    |int|INT_MIN|INT_MAX|
    |long|LONG_MIN|LONG_MAX|
    |long long|LLONG_MIN|LLONG_MAX|
    |unsigned char|0|UCHAR_MAX|
    |unsigned short|0|USHRT_MAX|
    |unsigned int|0|UINT_MAX|
    |unsigned long|0|ULONG_MAX|
    |unsigned long long|0|ULLONG_MAX|
  - `<limits.h>`에 정의된 최댓값, 최솟값을 넘어서도 오버플로우, 언더플로우가 발생한다.
  
---

- **크기가 표시된 정수 자료형 사용하기**
  - `<stdint.h>`헤더파일을 사용
  - ```C++
    #include <stdint.h>    // 크기별로 정수 자료형이 정의된 헤더 파일

    int main()
    {
      int8_t num1 = -128;                    // 8비트(1바이트) 크기의 부호 있는 정수형 변수 선언
      int16_t num2 = 32767;                  // 16비트(2바이트) 크기의 부호 있는 정수형 변수 선언 
      int32_t num3 = 2147483647;             // 32비트(4바이트) 크기의 부호 있는 정수형 변수 선언
      int64_t num4 = 9223372036854775807;    // 64비트(8바이트) 크기의 부호 있는 정수형 변수 선언
      
      uint8_t num5 = 255;                      // 8비트(1바이트) 크기의 부호 없는 정수형 변수 선언
      uint16_t num6 = 65535;                   // 16비트(2바이트) 크기의 부호 없는 정수형 변수 선언
      uint32_t num7 = 4294967295;              // 32비트(4바이트) 크기의 부호 없는 정수형 변수 선언
      uint64_t num8 = 18446744073709551615;    // 64비트(8바이트) 크기의 부호 없는 정수형 변수 선언
    }
    ```
  - 이런 자료형은 크기를 정확하게 표현해야 하는 파일 압축 및 암호화, 네트워크 프로그래밍을 할 때 특히 유용하며, 일반적인 프로그래밍을 할 때도 처음부터 `<stdint.h>`를 사용하는 것이 좋다. 서식지정자도 %d로 동일하다.
  - stdint의 최소, 최댓값은 `<stdint.h>` 헤더 파일 안에 정의되어 있으므로 `<limits.h>` 헤더 파일을 사용하지 않아도 된다.
    - 부호 있는 정수(signed) 최솟값: INT8_MIN, INT16_MIN, INT32_MIN, INT64_MIN
    - 부호 있는 정수 최댓값: INT8_MAX, INT16_MAX, INT32_MAX, INT64_MAX
    - 부호 없는 정수(unsigned) 최솟값: 0
    - 부호 없는 정수 최댓값: UINT8_MAX, UINT16_MAX, UINT32_MAX, UINT64_MAX

---

- **실수 자료형**
  - float은 숫자 뒤에 f를 붙이고 long double은 l, L을 붙여주고 double은 아무것도 붙이지 않는다.
    ```C
    float num1 = 0.1f;
    double num2 = 3.14;
    long double num3 = 10.324235l;
    ```
  - 소수점 앞 또는 뒤의 0은 생략 가능 ex) .1f, 1. f
  - float과 double을 printf로 출력할 때는 서식지정자 %f를 사용하고 long double은 %Lf 사용
  - Window기준 float은 4byte 7자리, double, long double은 8byte 15자리이다.
  - 지수 표기법으로 표기할 때는 정수부분은 한 자릿수만 적고, 소수자릿수 뒤에 e와 지수를 표기한다.
    - f와 l을 붙이는 것은 동일
    - e는 x10^를 뜻한다.
    - printf로 지수표기법 그대로 출력하려면 서식 지정자 %e, %Le를 사용한다.
  - 양수 최댓값, 최솟값은 헤더파일 `<float.h>`에 존재한다.
    - float : FLT_MIN, FLT_MAX
    - double : DBL_MIN, DBL_MAX
    - long double : LDBL_MIN, LDBL_MAX
  - 실수형의 언더플로우는 0 또는 쓰레기 값으로 처리하고 오버플로우는 무한대(inf)로 출력한다.

---

- **8, 16진수 서식 지정자**
  
  16진수를 표기할 때 서식 지정자는 %x로 사용한다. 하지만 10진수와 구분하기 어려우므로 보통 "0x%x"와 같은 형태로 출력한다.
  ```C
  char c1 = 0x61;
  printf("%c, %d, 0x%x\n", c1, c1, c1);
  // 출력값
  // a, 97, 0x61
  ```
  
  8진수를 표기할 때 서식 지정자는 %o로 사용한다. 하지만 10진수와 구분하기 어려우므로 보통 "0%o"와 같은 형태로 출력한다.
  
  Tip. 문자열의 서식 지정자는 %s이다.
---

- **문자 자료형**
  - 정수를 더하거나 빼면 그에 해당하는 ASCII코드의 문자를 반환한다.
    ```C
    printf("%c, %d\n", 'a' + 1, 'a' + 1);
    // 출력값
    // b, 98
    ```
  - 자주 사용하는 제어문자
    |ASCII|문자|표기법|설명|
    |-----|----|------|----|
    |10|LF|\n|개행, Line Feed, 줄바꿈|
    |13|CR|\r|복귀, Carriage Return, 줄의 끝에서 시작 위치로 되돌아감|
    |9|TAB|\t|수평 탭(horizontal tab)|

---

- **상수와 리터럴**
  
  상수란 변하지 않는 값을 뜻한다. 변수는 한 번 선언하면 값을 계속 바꿀 수 있지만 상수는 처음 선언할 때만 값을 할당 할 수 있으며 그 다음부터는 값을 바꿀 수 없다.
  
  리터럴(literal)은 "문자 그대로"라는 뜻인데 C 언어에서는 값 그 자체를 뜻한다. 그리고 상수는 변수처럼 리터럴이 저장된 공간이다.
  
  ```C
  //         ↓ 상수
  const int con1 = 10;
  //                ↑ 리터럴
  ```
  
  - const를 사용하여 상수를 사용할 수 있다. 위치는 자료형의 앞 뒤 모두 상관 없다.
  ```C
  const int num1 = 1;
  int const num1 = 1;
  ```
  
  - 리터럴의 크기를 명확하게 표현하기 위해 접미사(suffix)를 사용할 수도 있다. 변수를 선언할 때는 long, long long, unsigned long처럼 정수 자료형으로 크기를 정할 수 있지만 리터럴은 접미사를 활용하여 크기를 명시적으로 표기한다. 8, 16진수에도 접미사 사용 가능하다.
    ```C
    // 접미사 생략하면 int
    // 정수형
    printf("%ld\n", -10L);                       // long 크기의 정수 리터럴
    printf("%lld\n", -1234567890123456789LL);    // long long 크기의 정수 리터럴

    printf("%u\n", 10U);                         // unsigned int 크기의 정수 리터럴
    printf("%lu\n", 1234567890UL);               // unsigned long 크기의 정수 리터럴

    printf("%lu\n", 10UL);                       // unsigned long 크기의 정수 리터럴
    printf("%llu\n", 1234567890123456789ULL);    // unsigned long long 크기의 정수 리터럴
    
    //실수형
    printf("%f\n", 0.1f);     // 0.100000: float 크기의 실수 리터럴
    printf("%f\n", 0.1F);     // 0.100000: float 크기의 실수 리터럴
    
    printf("%f\n", 0.1);      // 0.100000: double 크기의 실수 리터럴
    
    printf("%Lf\n", 0.1l);    // 0.100000: long double 크기의 실수 리터럴
    printf("%Lf\n", 0.1L);    // 0.100000: long double 크기의 실수 리터럴
    ```
    
---

- **scanf**
  
  - scanf(서식, 변수의주소);
    - int scanf(char const * const _Format, ...);
    - 성공하면 가져온 값의 개수를 반환, 실패하면 EOF(-1)를 반환
    ```C
    //     ↓ 첫 번째 인수
    scanf("%d", &num1);    // 표준 입력을 받아서 변수에 저장
    //            ↑ 두 번째 인수
    ```
    
  - `#define _CRT_SECURE_NO_WARNINGS`는 Visual Studio에서만 넣어주면 된다.(리눅스, OS X 사용자라면 넣지 않아도 된다). scanf는 나온 지 오래된 함수라 입력 값의 길이를 설정할 수가 없다. 따라서 보안에 취약하기 때문에 Visual Studio에서는 사용하지 말라는 경고가 출력되고 컴파일 에러가 발생합니다. `#define _CRT_SECURE_NO_WARNINGS`를 넣지 않고 scanf 함수를 사용하면 scanf_s 함수를 대신 사용하거나 _CRT_SECURE_NO_WARNINGS를 사용하라고 나온다. scanf_s 함수는 입력 값의 길이를 설정할 수 있지만 C 언어 표준 함수는 아니며 Visual studio(Visual C++) 전용이다.
  
  - scanf 함수는 printf 함수와 사용 방법이 유사하다. 입력받을 개수만큼 서식 지정자를 넣어주고, 서식 지정자 개수만큼 변수를 넣어주면 된다. 
    ```C
    printf("정수를 두 개 입력하세요: ");
    scanf("%d %d", &num1, &num2);    // 값을 두 개 입력받아서 변수 두 개에 저장
    ```
    
  - 여기서 변수를 double로 선언했다면 scanf에는 서식 지정자로 %lf를 넣고, long double로 선언했다면 %Lf를 넣어야 한다(double은 printf로 출력할 때 %f를 써도 되지만 scanf는 %lf를 써야 한다).
    ```C
    double num1;
    scanf("%lf", &num1);    // 자료형이 double일 때는 %lf

    long double num2;
    scanf("%Lf", &num2);    // 자료형이 long double일 때는 %Lf
    ```
    
---

- **getchar, putchar**

  getchar 함수는 표준 입력에서 문자 하나를 입력받은 뒤 결과를 반환한다. 만약 문자 여러 개를 입력해도 첫 번째 문자만 반환된다.

  getchar 함수에 대응하는 함수로 putchar가 있는데 이 함수는 문자 하나를 화면에 출력한다.
  
  둘 다 모두 `<stdio.h>`헤더파일에 선언되어 있다.
  
  ```C
  char c1 = getchar();    // 문자 하나를 입력받음
  printf("%c\n", c1);
  // 키보드로 a를 입력받으면 a를 출력
  
  char c1 = 'a';
  putchar(c1);
  // 출력값 a
  ```
  
---

- **참, 거짓**
  
  - C언어에서는 0 이외의 모든 수를 참으로 처리하고 0은 거짓으로 처리한다.
  ```C
  if(1)
    printf("True\n");
    
  else
    printf("False\n");
    
  // 출력값
  // True
  // 1이 아니라 0이었으면 False 출력
  ```
  - `<stdbool.h>`를 사용하면 bool자료형이 사용 가능하다. (true, false)
  
---

- **&& 연산자**

  &&연산자는 첫번째 조건이 만족하지 않으면 뒤의 조건들은 검사하지 않는다.
 