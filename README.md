# Do it! C 언어 입문 - 김성엽
- 전반적으로 휼륭한 책입니다.

# 0. 차례
> [1. 프로그램과 C 언어](#1-프로그램과-c-언어-p16)\
> [2. C언어로 만드는 첫 번째 프로그램](#2-c언어로-만드는-첫-번째-프로그램-p32)\
> [3. 자료형](#3-자료형-p46)\
> [4. 상수와 변수](#4-상수와-변수-p65)\
> [5. 함수](#5-함수-p84)\
> [6. 표준 출력 함수](#6-표준-출력-함수-p105)\
> [7. 연산자](#7-연산자-p140)\
> [8. 조건문](#8-조건문-p151)\
> [9. 반복문](#9-반복문-p178)\
> [10. 시프트 연산자와 비트 연산자](#10-시프트-연산자와-비트-연산자-p203)\
> [11. 지역 변수와 전역변수](#11-지역-변수와-전역변수-p226)\
> [12. 배열과 문자열](#12-배열과-문자열-p252)\
> [13. 포인터](#13-포인터-p289)\
> [14. 표준 입력 함수](#14-표준-입력-함수-p334)\
> [15. 배열과 포인터](#15-배열과-포인터-p368)\
> [16. 메모리 할당](#16-메모리-할당-p384)\
> [17. 다차원 포인터](#17-다차원-포인터-p422)\
> [18. 구조체(struct)와 연결리스트](#18-구조체struct와-연결리스트-p455)\
> [19. 파일 입출력](#19-파일-입출력-p497)\
> [20. 함수포인터](#20-함수포인터-p525)

# 1. 프로그램과 C 언어 (p:16)
## 1-1. 프로그래밍 기초
## 1-2. C언어소개
## 1-3. 전자계산기 원리와 프로그래밍 개념
## 1-4. C언어 서술 형식
  ■ 주석문

   ```c
   /* 주석문은 /* 여러줄에 결쳐서도 */ 사용할 수 있습니다. */
   ```
  *Block주석은 사용하지 말 것*이며 Line 주석을 사용해야 한다.  
  - 위와 같은 문제가 발생하기도 하며,  
  - 찾기을 할 때도 Line 단위로 List Up 된다. (즉, 주석인지 아닌지 바로 확인불가)
  - 여러줄 주석처리 할때도 Editor의 Line Comment / UnComment 기능을 익혀서, 가급적 Line Comment한다.
    <https://github.com/zhangsob/Editor.html> 에서 Editor.html을 Down받아 Hot-Key을 익힌다.

  - 여러줄 주석처리하려면 확실하게.. 주석 시작 / 주석 끝을 표시한다.
  ```c
  /********************
  volatile int i = 0 ;
  for(i = 0; i < 1000; ++i)
      ; // Null Statement
  *********************/
  ```
  - 아래와 같이 전처리기로 ON (#if 1) / OFF(#if 0) 처리하는 것이 Test할 때 편리하다.
  ```c
  #if 0     // 의미 없는 것이라서 OFF처리함. 2024-01-01 전산과 부사수가
  volatile int i = 0 ;
  for(i = 0; i < 1000; ++i)
      ; // Null Statement
  #endif    // 의미 없는 부분이라서 주석처리함.
  ```
  - 부사수가 위와 같이 Off하니, 원작자인 사수가 다시 아래와 같이 Coding함.
  ```c
  #if 1     // [2024-08-04] 전자과 사수가 On한다. ("본 소스는 FirmWare 소스")
  volatile int i = 0 ;  // volatile은 compile에게 최적화할 때.
                        // 의미없다고 무시하지 말고, 그대로 수행하라고 하는 KeyWord
  for(i = 0; i < 1000; ++i)
      ; // Null Statement
  #else // OFF하면 Compile시 오류발생하도록 안전장치 추가
  #   error "FirmWare에서 Sleep을 주는 방법임.(위 부분 주석처리 금지)"
  #endif
  ```

## 1-5. C프로그램 실행 파일
- .c(.cpp) --> .obj(.o) + .lib(.a) --> .exe

# 2. C언어로 만드는 첫 번째 프로그램 (p:32)
## 2-1. C언어 개발 환경 구축하기
## 2-2. 비주얼 스튜디오 프로젝트 만들기
## 2-3. 내가 만든 첫 번째 프로그램

# 3. 자료형 (p:46)
## 3-1. 컴퓨터의 자료 기억 방식
## 3-2. 문자를 숫자로 표현하는 약속, 아스키(ASCII) 코드
  - **KSC5601**
    > *ASCII* + 한글완성형(행정전상망)코드
    - 한글영역 : 0xB0A1 ~ 0xC8FE (2,350자)
    - 한글Space : 0xA1A1
    - 한글Ascii(횡배,전각) : 0xA3A1 ~ 0xA3FE (= 0xA380 + ASCII )
  - **EUC-KR** ( MS949, CodePage 949 )
    > *KSC5601* + "갂,..,똠,..,힣" [ (11,172 - 2350)자 추가 ]
  - Unicode ( **UTF-8**, UTF-16LE, UTF-16BE, UTF-32LE, UTF-32BE )
    > UCS2 : 전세계 주요 글자\
    > UCS4 : 모든 문자 (이모지, 고대 이집트 파피루스, 옛 한자...)\
    > UTF-8 (CodePage 65001), UTF-16LE, UTF-16BE, UTF-32LE, UTF-32BE
    - unicode chart 로 검색 (<https://www.unicode.org/charts/>)
    - 한글영역 : 0xAC00 ~ 0xD7A3 (초성x중성x종성 : 19 x 21 x 28 = 11,172자)
    - 자음,모음 : 0x3131 ~ 0x3163
    - 한글Space : 0x3000
    - 한글Ascii(횡배,전각) : 0xFF01 ~ 0xFF5E (= 0xFF00 + ASCII - 0x20 )
    - 점자 : 0x2800 ~ 0x28FF

  - 자료형과 charset
    |  자료형   |    charset     |
    |:---------:|----------------|
    | char[]    | EUC-KR, UTF-8  |
    | wchar_t[] | UTF-16, UTF-32 |

    *sizeof(wchar_t)가 2이면 UTF-16, 4이면 UTF-32*

  - cmd창에서 charset변경
    ```cmd
    > chcp
    > chcp 65001
    > chcp 949
    ```
    위에서 *>는 cmd창의 Prompt*를 뜻한다.

## 3-3. 자료형의 종류

# 4. 상수와 변수 (p:65)
## 4-1. 항상 같은 수, 상수
  | literal       |   자료형          |
  |:-------------:|-------------------|
  | 10, 010, 0xB0 | const int         |
  | "가"          | const char[]      |
  | '0'           | const char        |
  | 0.314         | const double      |
  | 0.314f        | const float       |
  | 0.314lL       | const long double |
  | L'가'         | const wchar_t     |
  | L"가나다"     | const wchar_t[]   |
  | 10L           | const long        |
  | 10LL          | const long long   |

  - <https://en.cppreference.com/w/c/language/integer_constant>\
    여기서, C99 : 1999년에 확정된 Spec, C23 : 2023년에 확정된 Spec
  - <https://en.cppreference.com/w/c/language/character_constant>
  - <https://en.cppreference.com/w/c/language/string_literal>
  - <https://en.cppreference.com/w/c> 에서..C언어 Version을 확인할 수 있다.\
    ![C언어의 Spec](./image/c_spec.png)

## 4-2. 데이터 저장 공간, 변수  
## 4-3. 2진수를 16진수로 변환하는 방법

# 5. 함수 (p:84)
## 5-1. C언어와 함수
## 5-2. 함수 정의하고, 호출하기
  ```c
  int sum(int value1, int value2)
  {
      int result = value1 + value2 ;
      return result ;
  }
  
  int main()
  {
     int a = 2, b = 3 ;
     int s = sum(a, b) ;
  }
  ```
  - 함수 Call & Return
  ```c
  int main()
  {
      int a = 2, b = 3 ;
      int s = sum(a, b) ;
      // int value1 = a ;
      // int value2 = b ;
      // ... Call 파라미터 순서대로 assign
      // int result = value1 + value2 ;
      // return result ;
      // ... Return Rvalue
      // int s = result ;
  }
  ```

## 5-3. main 함수 정리하기

  ```c
  #include <stdio.h>

  int main(int argc, char *argv[], char *envp[])
  {
      int i = 0 ;
      // 파라미터 얻기
      for(i = 0; i < argc; ++i)
          fprintf(stdout, "argv[%d] : %s\n", i, argv[i]) ;
      // 환경변수 얻기 [ char *getenv( const char *name ); ]
      for(i = 0; i < 100 ; ++i) {
          if(envp[i]) {
              fprintf(stderr, "envp[%d] : %s\n", i, envp[i]) ;
          }
          else
              break ;
      }
      return argc + i+1 ;
  }
  ```

- Call
  *Build하고 cmd창에서 아래와 같이 하자.* 
  ```cmd
  > test.exe 1 param2 "파라 3"
  > test.exe 1 param2 "파라 3" > stdout.txt
  > type stdout.txt
  > test.exe 1 param2 "파라 3" 2> stderr.txt
  > type stderr.txt
  > test.exe 1 param2 "파라 3" 1> log.txt 2>&1
  > type log.txt
  > test.exe 1 param2 "파라 3" >> log.txt 2>&1
  > type log.txt
  > test.exe 1 param2 "파라 3" 2> nul
  ```
  *2> 1> 1>> 2>&1* 에서 1은 stdout을 2은 stderr을 뜻 한다. [ 참고 0은 stdin ]\
  *2> 1> 1>> 2>&1* 에서 >는 redirect로 전달한다. >>는 Append한다\
  *nul* 은 nul로 보낸다. 즉, 버린다.

- Return
  ```cmd
  > test.exe 1 param2 "파라 3"
  > echo %errorlevel%
  ```
  위와 같이 *Windows Batch 프로그램* 할 수 있으며, Unix은 경우 Shell Script할 수 있다.

## 5-4. 함수 원형 선언하기

## 5-A. 함수 설명서 만들기
  - Java는 javadoc가 있다.
  ```java
  /**
   * 문자를 숫자로
   * @param s             숫자화할 문자열
   * @param radix         8: 8진수 10: 10진수, 16: 16진수
   * @param defaultVAlue  s가 ""이거나 null이거나 올바르지 않은 경우 기본값
   * @return              숫자
   */
  public static int parseInt(String s, int radix, int defaultValue) {
    ...
  }
  ```
  - Javascript도 JSDoc이 있다.
  - c(cpp)도 비슷한 것이 있다. [Doxygen](https://www.doxygen.nl/)
  ```c
  /// 문자를 숫자로 ("0" -> 0, "" -> defaultValue, "10원" --> 10)
  /// @param s             숫자화할 문자열
  /// @param size          문자열의 길이
  /// @param defaultVAlue  s가 ""이거나 null이거나 올바르지 않은 경우 기본값
  /// @return              숫자
  int a2i(char *s, int size, int defaultValue) {
      int i = 0, ret = 0 ;
      for(i = 0; i < size; ++i) {
          if('0' <= s[i] && s[i] <= '9')
              ret = ret * 10 + (s[i] - '0')
          else
              break ;
      }
      return (i == 0) ? defaultValue : ret ;
  }
  ```

# 6. 표준 출력 함수 (p:105)
## 6-1. 라이브러리
## 6-2. 라이브러리 사용 설명서, 헤더 파일
## 6-3. 전처리기
- 화일찾기
```cmd
> cd \
> dir stdio.h /s
```
## 6-4. 표준 라이브러리와 표준 출력 함수
## 6-5. 문자열 출력 함수 printf
- printf format string
- <https://cplusplus.com/reference/cstdio/printf/>
- <https://en.cppreference.com/w/c/io/c/fprintf>

# 7. 연산자 (p:140)
## 7-1. 기본 연산자
## 7-2. 연산자 우선순위와 연산 방향
- 우선순위 모호하면 무조건 ( ) 한다.
- 특히, bit 연산자 와 ? : 는 무조건 ( ) 하는 것이 좋다. [경험상]
- ! 연산자대신 != 또는 == 연산자를 사용하는 것이 좋다.\
  ```c
  if (!strcmp(bankcode, "81"))      strcpy(bankname,"하나은행") ;
  ```
  - is not (bankcode가 81와 차이)
  - *!* 가 눈에 들어 오지 않는다. (Miss할 가능성이 높다.)
  ```c
  if (strcmp(bankcode, "81") == 0)  strcpy(bankname,"하나은행") ;
  ```
  - 우리말의 어순과 같다. [ bankcode가 81와 차이가 0이다. ]
  - *== 0* 가 확실히 눈에 들어 온다.

- 구간(x1부터 x2까지, x1과 x2 사이에)을 뜻할 때.
  
  ```c
  if (x >= 20 && x <= 40) return 1 ; 
  ```
  - *변수를 앞쪽에 비교값을 뒤쪽* 습관대로 한다.
  - x가 20보다 크고, x가 40보다 작은면

  ```c
  if (20 <= x && x <= 40) return 1 ;
  ```
  - 20 .... x .... 40 라는 느낌으로
  - 작은 것은 왼쪽에 큰 것은 오른쪽에.. 그래서 부등호는 < 또는 <= 으로 하는 것 바람직.. *수학의 X좌표*
  - 위와 같이 쓰고, *"x가 20 ~ 40 사이에 있으면"* 라고 읽는다.
  - kotlin 의 in연산자와 range, SQL의 BETWEEN 과 같은 느낌
    ```kotlin
    if(20 <= x && x <= 40)  return 1 ;  // kotlin에서도 아래과 같이 읽어도 된다.(전환하기도 좋다.)
    when(x) {
      in 20..40 -> return -1 ;
    }
    ```
    ```sql
    WHERE 20 <= X AND X <= 40 -- SQL에서도 아래와 같이 읽어도 된다.(전환하기도 좋다.)
    WHERE X BETWEEN 20 AND 40
    ```
# 8. 조건문 (p:151)
## 8-1. 제어문
## 8-2. if 조건문
- 참(true) : 0이 아님, 거짓(false) : 0임

■ c언어만 boolean형이 없다. (C23부터 생긴다.)
```c
if(!strcmp(str, "032"))   // 2000년이전 모니터가 640x480의 80 Column시절 Coding Style
    printf("인천(부천)\n") ;
if(strcmp(str, "034"))
    printf("개성공단이 아니다\n") ;
```
*!* 연산자는 눈에 잘 안보인다. 지양해야 할 것 ( *!* 은 부정적이다. )
```c
if(strcmp(str, "032") == 0)
    printf("인천(부천)\n") ;
if(strcmp(str, "034") != 0)
    printf("개성공단이 아니다\n") ;
```
*위와 같이 잘 보이게 한다. ( 긍정문을 사용하자! )*

■ =대입연산자와 ==관계연산자 혼동
```c
if(data = 3)  // if(data == 3)을 잘못 실수하여 data = 3 하였다. Run Time Error
if(3 == data) // 3 = data로 실수 하여도 Compile Time Error
```
- if(3 == data) // "if 3이 같다 data와"  읽기 불편하다.
- 즉, >=, <=, != 에 대하여도 위와 같이 하라는 뜻은 아닐 것이다.
- == 일때만 상수 == 변수로 하는 습관은 Safety Coding 방법이라는 뜻이다.
- Java에서도 아래와 같이 Safety Coding 방법이 있다.
```java
if(data.equal("string")) // data가 null 일때.. NullPointerException발생
if("string".equal(data)) // data가 null 일때.. false
```
그런데, 여기서 혼돈은 거의 없다. (실수일 뿐), 아래와 같을 때 혼돈이 발생한다.
```c
if(data==3)  // 왜 이분은 중국사람인가? 띄어쓰기를 안하네. 중국Programmer로 Coding할 때는 띄어쓰기한다.
if(data=3)   // 이분은 못배운 일본사람인가? 히라가나로만 글을 쓰네, 한자를 써서 의미전달를 확실해야야지.
```

■ 띄어쓰기 (예약어 및 2,3항 연산자은 반드시 양쪽 Spacing)
```c
if (data == 3)  // if while for else 예약어도 = == && || 연산자는 양쪽으로 Space하나로 띄어쓰기 한다.
if (data = 3)   // 띄어쓰기를 하면 = 가 단독으로 있는지 한눈에 보인다.
```

■ 띄어쓰기 (마침표를 뜻하는 ;도 Spacing)
```c
int data = 5;   // 국어선생님에 지적질을 많이 받아서.
if (data > 3);  // 줄끝에 ;를 아무생각없이 습관처럼 마침표를 찍었다.
    data++;     // 기호문자가 3자가 붙어 있다... 아휴..답답해.
```
아래와 같이 마침표도 ; 띄어 쓰기 한다면....
```c
int data = 5 ;    // 여기서, 시원시원해 보아지 않는가.
if (data > 3) ;   // 마침표가 확실히 잘 못 되었는지 확실히 보인다.
    ++data ;      // 우리는 시각적으로 [ 소문자 / 기호 / 숫자 / 대문자 / 한글 / WhiteSpace ]를 구분한다.
                  // data++; 를 ++data ; 로 시각적으로 읽기 좋다.
                  // C++ 아직 C언어이지요. ++C로 확실히 D언어로 하자..
```

■ 붙여쓰기
- 단항연산자 ++ -- ! ~ - + 전위 연산자로 앞쪽만 Spacing
- Separator(구분자) comma연산자 및 for문 안에 ; 뒤쪽만 Spacing
```c
int i = 0, j = 0, length = 0 ;
for (i = 0; i < length; ++i)
    ...
```

## 8-3. if ~ else ~ 조건문
## 8-4. 중첩된 if 조건문
  ```c
  #include <stdio.h>

  void main()
  {
      int score = 86 ;
      char grade ;

      if(score >= 90)      grade = 'A' ;  // 90점 이상
      else if(score >= 80) grade = 'B' ;  // 80점 이상
      else if(score >= 70) grade = 'C' ;  // 70점 이상
      else if(score >= 60) grade = 'D' ;  // 60점 이상
      else                 grade = 'F' ;  // 60점 미만

      printf("당신의 점수는 %d점이고, 등급은 %c입니다.\n", score, grade) ;
  }
  ```
  - 위와 같이 최대한 줄을 맞추어 작성한다.
  - 그러면, Editor에서 열 모드, Box 모드로 여러줄을 한번에 수정할 수 있다.
## 8-5. switch 조건문
  ```c
  #include <stdio.h>

  void main()
  {
      int score = 86 ;
      char grade ;

      switch(scroe / 10)
      {
      case 10 :
      case  9 :
                grade = 'A' ;
                break ;
      case  8 :
                grade = 'B' ;
                break ;
      case  7 :
                grade = 'C' ;
                break ;
      case  6 :
                grade = 'D' ;
                break ;
      default :
                grade = 'F' ;
                break ;
      }
      
      printf("당신의 점수는 %d점이고, 등급은 %c입니다.\n", score, grade) ;
  }
  ```
  *case 조건과 처리문*를 줄로 구분하면 한눈에 보기 좋다.
  ```c
  #include <stdio.h>

  void main()
  {
      int score = 86 ;
      char grade ;

      switch(scroe / 10)
      {
      case 10 : grade = 'A' ; break ;
      case  9 : grade = 'A' ; break ;
      case  8 : grade = 'B' ; break ;
      case  7 : grade = 'C' ; break ;
      case  6 : grade = 'D' ; break ;
      default : grade = 'F' ; break ;
      }
      
      printf("당신의 점수는 %d점이고, 등급은 %c입니다.\n", score, grade) ;
  }
  ```
  *작은처리문*은 한줄에 사용하면 더욱 깔끔하다.
  ```c
  #include <stdio.h>

  char grade(int score)
  {
      switch(scroe / 10)
      {
      case 10 : return 'A' ;
      case  9 : return 'A' ;
      case  8 : return 'B' ;
      case  7 : return 'C' ;
      case  6 : return 'D' ;
      default : return 'F' ;
      }
  }

  void main()
  {
      int score = 86 ;
      
      printf("당신의 점수는 %d점이고, 등급은 %c입니다.\n", score, grade(score)) ;
  }
  ```
  *함수화*하면 break대신 바로 return한다.

  | score | grade |
  |:------|:-----:|
  | 90 ~  | A     |
  | 80 ~  | B     |
  | 70 ~  | C     |
  | 60 ~  | D     |
  | ~ 59  | F     |
  
  *위 3가지 소스가 모두 위 표를 보는 듯한 Code이다.*

## 8-A. string도 switch로 가능하면.

  ```c
  if(strcmp(bankcode,"20") == 0)  strcpy(bankname,"우리은행") ;
  else if(strcmp(bankcode,"11") == 0)  strcpy(bankname,"농협중앙회") ;
  else if(strcmp(bankcode,"81") == 0)  strcpy(bankname,"하나은행") ;
  ```
  *보통사용하는형태*

  ```c
  if(strcmp(bankcode,"20") == 0)  strcpy(bankname,"우리은행"  ) ;
  if(strcmp(bankcode,"11") == 0)  strcpy(bankname,"농협중앙회") ;
  if(strcmp(bankcode,"81") == 0)  strcpy(bankname,"하나은행"  ) ;
  ```
  *줄맞춤(속도는 별차이 )*

  ```c
  switch(atoi(bankcode))
  {
  case 20 : strcpy(bankname,"우리은행"  ) ; break ;
  case 11 : strcpy(bankname,"농협중앙회") ; break ;
  case 81 : strcpy(bankname,"하나은행"  ) ; break ;
  }
  ```
  *Primitive(Number) Type*으로 전환하기

# 9. 반복문 (p:178)
## 9-1. 반복문의 기본 구조와 for반복문
## 9-2. while 반복문
## 9-3. 반복문 구성 방법
## 9-4. 중첩 반복문
## 9-5. break와 continue 제어문
  - continue ; // "이후 무시하고 다음"이라고 읽는다. [ 즉, 반복문안에서 전제조건으로 할용한다. ]
  ```c
  while(......) {
      .....
  // <--- continue의 이동위치
  }
  // <--- break의 이동위치
  ```

# 10. 시프트 연산자와 비트 연산자 (p:203)
## 10-1. 비트단위 연산과 비트 패턴
## 10-2. 시프트 연산자
## 10-3. 비트 연산자

# 11. 지역 변수와 전역변수 (p:226)
## 11-1. 함수 안에서만 사용하는 지역변수
## 11-2. 프로그램 전체에서 사용할 수 있는 전역변수
## 11-3. extern 키워드
## 11-4. static 키워드
## 11-A. 변수 선언 Scope 및 Memory 총정리

  |          | KeyWord  | Scope (유효범위)       |  Memory위치           |
  |----------|----------|------------------------|-----------------------|
  | 지역변수 | register | Block 안, 즉 { .... }  | register 또는 STACK   |
  | 지역변수 | [auto]   | Block 안, 즉 { .... }  | STACK                 |
  | 지역변수 | static   | Block 안               | DATA                  |
  | 전역변수 |          | Function 밖            | DATA                  |
  | 전역변수 | static   | Function 밖 && File 안 | DATA                  |
  | 외부변수 | extern   | File 밖 (다른.obj)     | Link만 한다.          |
  | literal  |          |                        | CODE                  |
  
  - const : assign 금지하기
  - volatile : 최적화 금지하기 (Compiler에게 무의미하다고 삭제금지 알리기)
  - register : 빈 register을 활용을 원하는 것이지, 반드시 register에 활용하는 것이 아니다.\
    --> 최적화 과정에서 auto변수를 알아서 register을 활용함.(속도 Up) 그래서, 의미 없음
  - HEAP은 alloc(malloc, calloc, realloc)함수에 의해 할당됨.\
    free가 필요하여.. memory leak 발생할 수 있음(가급적 사용금지)\
    대안, CPP의 STL을 활용하는 것이 바림직함.
  - [auto], [signed], [int]는 생략가능하다.

  ```c
  #include <stdio.h>

  //extern	i ;		// 기존 Library개발자가(.h화일 안 주고,) 전화로 알려주어 외부변수 Link 선언
  #include "other.h"	// 새로 온 Library개발자가 준 것(함수까지 정리해 줌)

  int	s = 0 ;

  void func()
  {
    static	s = 10;
    auto	i = 10 ;

    {
      static	s = 100 ;	// 함수지역변수 아니 임의 블럭지역변수는
      auto	i = 100 ;	// CASE1 : 함수가 지나치게 길(큰)때 사용한다. (임시 담당자가)
      printf("%-8s s : %3d (&s:%p), i : %3d (&i:%p)\n", __FUNCTION__ "()", ++s, &s, ++i, &i) ;
    }
    {
      static		s = 200 ;	// CASE2 : 변수명이 함수지역변수와 동일하나, 이 Block에서만 사용할 때.
      register	i = 200 ;	//         (우리는 영어가 native가 아니므로, 작명에 어려움이 있다.)
      //printf("%-8s s : %3d (&s:%p), i : %3d (&i:%p)\n", __FUNCTION__ "()", ++s, &s, ++i, &i) ;	// &i는 Error
      printf("%-8s s : %3d (&s:%p), i : %3d\n", __FUNCTION__ "()", ++s, &s, ++i) ;
    }
    printf("%-8s s = %3d (&s:%p), i = %3d (&i:%p)\n", __FUNCTION__ "()", ++s, &s, ++i, &i) ;
  }

  void callfunc()
  {
    func() ;
  }

  int main()
  {
    func() ;
    callfunc() ;	// func() ;를 대신 callfunc() ;하여 Stack깊이를 달리함.
    printf("%-8s s = %3d (&s:%p), i = %3d (&i:%p)\n", __FUNCTION__ "()", ++s, &s, ++i, &i) ;
    other() ;
    printf("%-8s s = %3d (&s:%p), i = %3d (&i:%p)\n", __FUNCTION__ "()", ++s, &s, ++i, &i) ;
    return 0 ;
  }
  ```
  *main.c*

  ```c
  #ifndef _OTHER_H_
  #define _OTHER_H_

  extern int i ;	// 0 이면 운영, 1 이면 개발
  void other() ;	// Test용도 함수

  #endif	//#ifndef _OTHER_H_
  ```
  *other.h*

  ```c
  #include <stdio.h>
  #include "other.h"	// 새로운 개발자가 추가함.

  static	s = 0 ;	// library개발자로 본 File내에서만 사용하고, main()개발자와 전역변수명 충돌방지
  extern	i = 0 ;	// 설정같은 것을 main()개발자에게 노출하기 위함.[extern은 보통생략함.]

  static void func()	// 함수명 충돌있다고 하여, static을 추가함. [함수도 static하면 본File에서만 유효함]
  {
    printf("%-8s s=> %3d (&s:%p), i=> %3d (&i:%p)\n", __FUNCTION__ "()", ++s, &s, ++i, &i) ;
  }

  extern void other()	// [extern은 보통생략함.]
  {
    printf("%-8s s=> %3d (&s:%p), i=> %3d (&i:%p)\n", __FUNCTION__ "()", ++s, &s, ++i, &i) ;
    func() ;	// 새로운 개발자가 함수추가함.
  }
  ```
  *other.c*

  ```
  func()   s : 101 (&s:00A77004), i : 101 (&i:012FFD54)
  func()   s : 201 (&s:00A77008), i : 201
  func()   s =  11 (&s:00A77000), i =  11 (&i:012FFD60)
  func()   s : 102 (&s:00A77004), i : 101 (&i:012FFC80)
  func()   s : 202 (&s:00A77008), i : 201
  func()   s =  12 (&s:00A77000), i =  11 (&i:012FFC8C)
  main()   s =   1 (&s:00A7715C), i =   1 (&i:00A77154)
  other()  s=>   1 (&s:00A77150), i=>   2 (&i:00A77154)
  func()   s=>   2 (&s:00A77150), i=>   3 (&i:00A77154)
  main()   s =   2 (&s:00A7715C), i =   4 (&i:00A77154)
  ```
  *실행결과* : 변수 값 및 변수의 주소값을 살펴보세요.

  - 예약어(reserved keyword) : <https://en.cppreference.com/w/c/keyword>
    - C언어 쉽다고 하는 것은 예약어 갯수(C99이전:32) 적어서
    - C언어 어렵다고 하는 것은 표준Library가 적어서

## 11-B. const와 함수선언문 읽기.
  - string.h화일에 strcpy함수가 아래와 같다고 한다.
    ```c
    char *strcpy( char *dest, const char *src );
    ```
    C언의 문자열은 Null Terminated String으로 pointer로 주고 받는다.
    - 파라미터 char *dest는 함수내부에서 값이 변경될 수도 있다.\
      --> *출력/입력/입출력* 알 수가 없다. (소스코드을 읽거나, 함수 설명서가 필요하다.)
    - 파라미터 const char *src는 함수내부에서 변경되지 않는다.\
      --> 즉, *입력전용* 이라는 뜻이다.\
      --> pointer 파라미터에서 const를 넣어 주어야 입력전용임을 명확히 할 수 있다.

  - 아래의 함수도 읽어보자.
    ```c
    int strcmp( const char* lhs, const char* rhs );
    size_t strlen( const char* str );
    char* strchr( const char* str, int ch );
    int memcmp( const void* lhs, const void* rhs, size_t count );
    ```
    <https://en.cppreference.com/w/c/string/byte> 에서

# 12. 배열과 문자열 (p:252)
## 12-1. 배열
## 12-2. 문자열
## 12-3. 2차원배열

# 13. 포인터 (p:289)
## 13-1. 운영체제의 메모리 관리 방식
## 13-2. 포인터
## 13-3. 포인터와 const 키워드
## 13-4. 포인터 변수의 주소 연산
  ```c
  {
      char name[10] = "name" ;	// name의 type "char * const" 이다.
      char *p = name ;
      printf("p = %p, name = %p\n", p, name) ;
      p = p + 3 ;
      printf("p = %p, name = %p\n", p, name) ;
      name = p + 3 ;  // Error
      p = name + 3 ;  // OK
  }
  {
      short name[10] = { 0, 1, 2, 3 } ;	// name의 type "short * const" 이다.
      short *p = name ;
      printf("p = %p, name = %p\n", p, name) ;
      p = p + 3 ;
      printf("p = %p, name = %p, &name[0] = %p\n", p, name, &name[0]) ;   // name == &name[0]
      printf("p = %p, &name[3] = %p, (name+3) = %p\n", p, &name[3], name+3) ;
  }
  ```
## 13-5. 포인터와 대상의 크기
## 13-6. void *형 포인터
  - void* memset( void* dest, int ch, std::size_t count );
  - void* memcpy( void* dest, const void* src, std::size_t count );
  - int memcmp( const void* lhs, const void* rhs, std::size_t count );

# 14. 표준 입력 함수 (p:334)
## 14-1. 표준 입력 함수
## 14-3. 문자열을 정수로 변환하기
  - int atoi( const char *str );    // <https://en.cppreference.com/w/c/string/byte/atoi>
  ```c
  /// 십진수 문자열을 숫자로
  /// @param str    문자열
  /// @param len    대상길이
  /// @return       값
  int a2i(const char str[], int len)
  {
      int ret = 0, i = 0 ;
      for(i = 0; i < len; ++i) {
          if('0' <= str[i] && str[i] <= '9')
              ret = ret * 10 + (str[i] - '0') ;
          else
              break ;
      }
      return ret ;
  }
  ```
## 14-4. 표준 입력 함수 scanf

# 15. 배열과 포인터 (p:368)
## 15-1. 배열과 포인터 표기법
## 15-2. 배열 시작 주소
## 15-3. 배열을 사용하는 포인터
## 15-4. 배열과 포인터의 합체

# 16. 메모리 할당 (p:384)
## 16-1. 프로세스와 메모리 할당
## 16-2. 지역변수와 스택
## 16-3. 동적 메모리 할당 및 해제
## 16-4. 동적 메모리 사용하기

# 17. 다차원 포인터 (p:422)
## 17-1. 다차원 포인터 개념
## 17-2. 2차원 포인터
## 17-3. 2차원 포인터와 함수의 매개변수
## 17-4. 2차원 포인터와 2차원 배열

# 18. 구조체(struct)와 연결리스트 (p:455)
## 18-1. typedef 문법
## 18-2. 데이터를 구룹으로 묶는 구조체
## 18-3. 배열과 구조체
  - struct에서 사용할 수 있는 유일한 연산자(= assignment operator)
    ```c
    #include <stdio.h>
      
    struct Point {
    	int x, y ;
    } ;
    
    void printPoint(struct Point pt)	{ printf("(%d,%d)\n", pt.x, pt.y) ;  }
    
    struct Point doublePoint(struct Point pt)
    {
    	struct Point ret = { pt.x * 2, pt.y * 2 } ;
    	return ret ;
    }
    
    int main(int argc, char *argv[])
    {
    	struct Point pt = { 1, 1 }, pt1 = { 0, 0 } ;
    	printPoint(pt) ;
    
    	pt1 = pt ;        // assign[ memcpy(&pt1, &pt, sizeof(pt)) ; ]
    	printPoint(pt1) ; // parameter passing도 assign [ memcpy(&pt, &pt1, sizeof(pt1)) ; ]
    
    	pt1 = doublePoint(pt) ; // return도 assign [ memcpy(&pt1, &ret, sizeof(ret)) ; ]
    	printPoint(pt1) ;
    
    	return 0 ;
    }
    ```
    ```
    (1,1)
    (1,1)
    (2,2)
    ```

    **여기서, 단 배열은 안 된다. (array is Pointer)**
    ```c
    #include <stdio.h>
    #include <string.h>
    
    struct People {
    	char name[14] ;
    	unsigned char age ;
    	int height ;
    } ;
    
    void printPeople(struct People* p)
    {
    	printf("{name=%p[%s], age=%d, height=%d}\n", p->name, p->name, p->age, p->height) ;
    }
    
    struct People increaseHeight(struct People p, int amount)
    {
    	struct People r = p ;
    	printf(" p.name=%p ",  p.name) ;	printf("p =") ; printPeople(&p) ;
    	strcat(r.name, "2") ;
    	printf(" r.name=%p ",  r.name) ;	printf("r =") ; printPeople(&r) ;
    	return r ;
    }
    
    int main(int argc, char *argv[])
    {
    	struct People p = { "first", 1, 80 }, p1 = { "p1", 0, 0 } ;
    	printf(" p.name:%p ",  p.name) ;	printf("p =") ;	printPeople(&p) ;	
    	printf("p1.name:%p ", p1.name) ;	printf("p1=") ;	printPeople(&p1) ;	
    
    	p1 = p ;			// memcpy(&p1, &p, sizeof(struct People)) ;
    	printf("p1.name:%p ", p1.name) ;	printf("p1=") ;	printPeople(&p1) ;
    
    	p1 = increaseHeight(p, +5) ;	// memcpy(&p1, &r, sizeof(struct People)) ;
    	printf("p1.name:%p ", p1.name) ;	printf("p1=") ;	printPeople(&p1) ;
    
    	return 0 ;
    }
    ```
    *msc*
    ```
     p.name:004FFAA8 p ={name=004FFAA8[first], age=1, height=80}
    p1.name:004FFA8C p1={name=004FFA8C[p1], age=0, height=0}
    p1.name:004FFA8C p1={name=004FFA8C[first], age=1, height=80}
     p.name=004FF96C p ={name=004FF96C[first], age=1, height=80}
     r.name=004FF944 r ={name=004FF944[first2], age=1, height=80}
    p1.name:004FFA8C p1={name=004FFA8C[first2], age=1, height=80}
    ```
    *gcc*
    ```
    zhang@rupang:~/tmp$ gcc struct.c
    zhang@rupang:~/tmp$ ./a.out
     p.name:0x7ffd7a1b50a0 p ={name=0x7ffd7a1b50a0[first], age=1, height=80}
    p1.name:0x7ffd7a1b50c0 p1={name=0x7ffd7a1b50c0[p1], age=0, height=0}
    p1.name:0x7ffd7a1b50c0 p1={name=0x7ffd7a1b50c0[first], age=1, height=80}
     p.name=0x7ffd7a1b5050 p ={name=0x7ffd7a1b5050[first], age=1, height=80}
     r.name=0x7ffd7a1b5020 r ={name=0x7ffd7a1b5020[first2], age=1, height=80}
    p1.name:0x7ffd7a1b50c0 p1={name=0x7ffd7a1b50c0[first2], age=1, height=80}
    ```

## 18-4. 구조체로 만든 자료형의 크기
  - #pragma pack(push)  
  - #pragma pack(1)  
  - #pragma pack(pop)  
  ```c
  #include <stdio.h>
  
  struct Test0 {
  	char c;
  	double d;
  	unsigned char u;
  	short s;
  } ;
  
  #pragma pack(push)	// pack값 넣어두기
  #pragma pack(1)
  struct Test1 {
  	char c;
  	double d;
  	unsigned char u;
  	short s;
  };
  
  #pragma pack(2)
  struct Test2 {
  	char c;
  	double d;
  	unsigned char u;
  	short s;
  };
  
  #pragma pack(4)
  struct Test4 {
  	char c;
  	double d;
  	unsigned char u;
  	short s;
  };
  #pragma pack(pop)	// 넣어둔 pack값얻기
  
  int main() {
  	struct Test0 t0 ;
  	struct Test1 t1;
  	struct Test2 t2;
  	struct Test4 t4;
  
  	printf("sizeof(struct Test0): %zd\n", sizeof(struct Test0));
  	printf("sizeof(t0  ): %2zd, &t0  : %p, &t0   - &t0:%td\n", sizeof(t0  ), &t0  ,   ((char*)&t0   - (char*)&t0));
  	printf("sizeof(t0.c): %2zd, &t0.c: %p, &t0.c - &t0:%td\n", sizeof(t0.c), &t0.c,   ((char*)&t0.c - (char*)&t0));
  	printf("sizeof(t0.d): %2zd, &t0.d: %p, &t0.d - &t0:%td\n", sizeof(t0.d), &t0.d,   ((char*)&t0.d - (char*)&t0));
  	printf("sizeof(t0.u): %2zd, &t0.u: %p, &t0.u - &t0:%td\n", sizeof(t0.u), &t0.u,   ((char*)&t0.u - (char*)&t0));
  	printf("sizeof(t0.s): %2zd, &t0.s: %p, &t0.s - &t0:%td\n", sizeof(t0.s), &t0.s,   ((char*)&t0.s - (char*)&t0));
  
  	printf("sizeof(struct Test1): %zd\n", sizeof(struct Test1));
  	printf("sizeof(t1  ): %2zd, &t1  : %p, &t1   - &t1:%td\n", sizeof(t1  ), &t1  ,   ((char*)&t1   - (char*)&t1));
  	printf("sizeof(t1.c): %2zd, &t1.c: %p, &t1.c - &t1:%td\n", sizeof(t1.c), &t1.c,   ((char*)&t1.c - (char*)&t1));
  	printf("sizeof(t1.d): %2zd, &t1.d: %p, &t1.d - &t1:%td\n", sizeof(t1.d), &t1.d,   ((char*)&t1.d - (char*)&t1));
  	printf("sizeof(t1.u): %2zd, &t1.u: %p, &t1.u - &t1:%td\n", sizeof(t1.u), &t1.u,   ((char*)&t1.u - (char*)&t1));
  	printf("sizeof(t1.s): %2zd, &t1.s: %p, &t1.s - &t1:%td\n", sizeof(t1.s), &t1.s,   ((char*)&t1.s - (char*)&t1));
  
  	printf("sizeof(struct Test2): %zd\n", sizeof(struct Test2));
  	printf("sizeof(t2  ): %2zd, &t2  : %p, &t2   - &t2:%td\n", sizeof(t2)  , &t2  ,   ((char*)&t2   - (char*)&t2));
  	printf("sizeof(t2.c): %2zd, &t2.c: %p, &t2.c - &t2:%td\n", sizeof(t2.c), &t2.c,   ((char*)&t2.c - (char*)&t2));
  	printf("sizeof(t2.d): %2zd, &t2.d: %p, &t2.d - &t2:%td\n", sizeof(t2.d), &t2.d,   ((char*)&t2.d - (char*)&t2));
  	printf("sizeof(t2.u): %2zd, &t2.u: %p, &t2.u - &t2:%td\n", sizeof(t2.u), &t2.u,   ((char*)&t2.u - (char*)&t2));
  	printf("sizeof(t2.s): %2zd, &t2.s: %p, &t2.s - &t2:%td\n", sizeof(t2.s), &t2.s,   ((char*)&t2.s - (char*)&t2));
  
  	printf("sizeof(struct Test4): %zd\n", sizeof(struct Test4));
  	printf("sizeof(t4  ): %2zd, &t4  : %p, &t4   - &t4:%td\n", sizeof(t4)  , &t4  ,   ((char*)&t4   - (char*)&t4));
  	printf("sizeof(t4.c): %2zd, &t4.c: %p, &t4.c - &t4:%td\n", sizeof(t4.c), &t4.c,   ((char*)&t4.c - (char*)&t4));
  	printf("sizeof(t4.d): %2zd, &t4.d: %p, &t4.d - &t4:%td\n", sizeof(t4.d), &t4.d,   ((char*)&t4.d - (char*)&t4));
  	printf("sizeof(t4.u): %2zd, &t4.u: %p, &t4.u - &t4:%td\n", sizeof(t4.u), &t4.u,   ((char*)&t4.u - (char*)&t4));
  	printf("sizeof(t4.s): %2zd, &t4.s: %p, &t4.s - &t4:%td\n", sizeof(t4.s), &t4.s,   ((char*)&t4.s - (char*)&t4));
  
  	return 0 ;
  }
  ```

  *VS2022 x64*
  ```
  sizeof(struct Test0): 24
  sizeof(t0  ): 24, &t0  : 00000020D50FFC78, &t0   - &t0:0
  sizeof(t0.c):  1, &t0.c: 00000020D50FFC78, &t0.c - &t0:0
  sizeof(t0.d):  8, &t0.d: 00000020D50FFC80, &t0.d - &t0:8
  sizeof(t0.u):  1, &t0.u: 00000020D50FFC88, &t0.u - &t0:16
  sizeof(t0.s):  2, &t0.s: 00000020D50FFC8A, &t0.s - &t0:18
  sizeof(struct Test1): 12
  sizeof(t1  ): 12, &t1  : 00000020D50FFCA8, &t1   - &t1:0
  sizeof(t1.c):  1, &t1.c: 00000020D50FFCA8, &t1.c - &t1:0
  sizeof(t1.d):  8, &t1.d: 00000020D50FFCA9, &t1.d - &t1:1
  sizeof(t1.u):  1, &t1.u: 00000020D50FFCB1, &t1.u - &t1:9
  sizeof(t1.s):  2, &t1.s: 00000020D50FFCB2, &t1.s - &t1:10
  sizeof(struct Test2): 14
  sizeof(t2  ): 14, &t2  : 00000020D50FFCD8, &t2   - &t2:0
  sizeof(t2.c):  1, &t2.c: 00000020D50FFCD8, &t2.c - &t2:0
  sizeof(t2.d):  8, &t2.d: 00000020D50FFCDA, &t2.d - &t2:2
  sizeof(t2.u):  1, &t2.u: 00000020D50FFCE2, &t2.u - &t2:10
  sizeof(t2.s):  2, &t2.s: 00000020D50FFCE4, &t2.s - &t2:12
  sizeof(struct Test4): 16
  sizeof(t4  ): 16, &t4  : 00000020D50FFD08, &t4   - &t4:0
  sizeof(t4.c):  1, &t4.c: 00000020D50FFD08, &t4.c - &t4:0
  sizeof(t4.d):  8, &t4.d: 00000020D50FFD0C, &t4.d - &t4:4
  sizeof(t4.u):  1, &t4.u: 00000020D50FFD14, &t4.u - &t4:12
  sizeof(t4.s):  2, &t4.s: 00000020D50FFD16, &t4.s - &t4:14
  ```

  *VS2022 x86(Win32)*
  ```
  sizeof(struct Test0): 24
  sizeof(t0  ): 24, &t0  : 00CFFDD4, &t0   - &t0:0
  sizeof(t0.c):  1, &t0.c: 00CFFDD4, &t0.c - &t0:0
  sizeof(t0.d):  8, &t0.d: 00CFFDDC, &t0.d - &t0:8
  sizeof(t0.u):  1, &t0.u: 00CFFDE4, &t0.u - &t0:16
  sizeof(t0.s):  2, &t0.s: 00CFFDE6, &t0.s - &t0:18
  sizeof(struct Test1): 12
  sizeof(t1  ): 12, &t1  : 00CFFDC0, &t1   - &t1:0
  sizeof(t1.c):  1, &t1.c: 00CFFDC0, &t1.c - &t1:0
  sizeof(t1.d):  8, &t1.d: 00CFFDC1, &t1.d - &t1:1
  sizeof(t1.u):  1, &t1.u: 00CFFDC9, &t1.u - &t1:9
  sizeof(t1.s):  2, &t1.s: 00CFFDCA, &t1.s - &t1:10
  sizeof(struct Test2): 14
  sizeof(t2  ): 14, &t2  : 00CFFDA8, &t2   - &t2:0
  sizeof(t2.c):  1, &t2.c: 00CFFDA8, &t2.c - &t2:0
  sizeof(t2.d):  8, &t2.d: 00CFFDAA, &t2.d - &t2:2
  sizeof(t2.u):  1, &t2.u: 00CFFDB2, &t2.u - &t2:10
  sizeof(t2.s):  2, &t2.s: 00CFFDB4, &t2.s - &t2:12
  sizeof(struct Test4): 16
  sizeof(t4  ): 16, &t4  : 00CFFD90, &t4   - &t4:0
  sizeof(t4.c):  1, &t4.c: 00CFFD90, &t4.c - &t4:0
  sizeof(t4.d):  8, &t4.d: 00CFFD94, &t4.d - &t4:4
  sizeof(t4.u):  1, &t4.u: 00CFFD9C, &t4.u - &t4:12
  sizeof(t4.s):  2, &t4.s: 00CFFD9E, &t4.s - &t4:14
  ```

  *VS2010 x86(Win32)*
  ```
  sizeof(struct Test0): 24
  sizeof(t0  ): 24, &t0  : 00EFF778, &t0   - &t0:0
  sizeof(t0.c):  1, &t0.c: 00EFF778, &t0.c - &t0:0
  sizeof(t0.d):  8, &t0.d: 00EFF780, &t0.d - &t0:8
  sizeof(t0.u):  1, &t0.u: 00EFF788, &t0.u - &t0:16
  sizeof(t0.s):  2, &t0.s: 00EFF78A, &t0.s - &t0:18
  sizeof(struct Test1): 12
  sizeof(t1  ): 12, &t1  : 00EFF764, &t1   - &t1:0
  sizeof(t1.c):  1, &t1.c: 00EFF764, &t1.c - &t1:0
  sizeof(t1.d):  8, &t1.d: 00EFF765, &t1.d - &t1:1
  sizeof(t1.u):  1, &t1.u: 00EFF76D, &t1.u - &t1:9
  sizeof(t1.s):  2, &t1.s: 00EFF76E, &t1.s - &t1:10
  sizeof(struct Test2): 14
  sizeof(t2  ): 14, &t2  : 00EFF74C, &t2   - &t2:0
  sizeof(t2.c):  1, &t2.c: 00EFF74C, &t2.c - &t2:0
  sizeof(t2.d):  8, &t2.d: 00EFF74E, &t2.d - &t2:2
  sizeof(t2.u):  1, &t2.u: 00EFF756, &t2.u - &t2:10
  sizeof(t2.s):  2, &t2.s: 00EFF758, &t2.s - &t2:12
  sizeof(struct Test4): 16
  sizeof(t4  ): 16, &t4  : 00EFF734, &t4   - &t4:0
  sizeof(t4.c):  1, &t4.c: 00EFF734, &t4.c - &t4:0
  sizeof(t4.d):  8, &t4.d: 00EFF738, &t4.d - &t4:4
  sizeof(t4.u):  1, &t4.u: 00EFF740, &t4.u - &t4:12
  sizeof(t4.s):  2, &t4.s: 00EFF742, &t4.s - &t4:14
  ```

  *VS6.0 x86(Win32)*
  ```
  sizeof(struct Test0): 24
  sizeof(t0  ): 24, &t0  : 0019FF1C, &t0   - &t0:0
  sizeof(t0.c):  1, &t0.c: 0019FF1C, &t0.c - &t0:0
  sizeof(t0.d):  8, &t0.d: 0019FF24, &t0.d - &t0:8
  sizeof(t0.u):  1, &t0.u: 0019FF2C, &t0.u - &t0:16
  sizeof(t0.s):  2, &t0.s: 0019FF2E, &t0.s - &t0:18
  sizeof(struct Test1): 12
  sizeof(t1  ): 12, &t1  : 0019FF10, &t1   - &t1:0
  sizeof(t1.c):  1, &t1.c: 0019FF10, &t1.c - &t1:0
  sizeof(t1.d):  8, &t1.d: 0019FF11, &t1.d - &t1:1
  sizeof(t1.u):  1, &t1.u: 0019FF19, &t1.u - &t1:9
  sizeof(t1.s):  2, &t1.s: 0019FF1A, &t1.s - &t1:10
  sizeof(struct Test2): 14
  sizeof(t2  ): 14, &t2  : 0019FF00, &t2   - &t2:0
  sizeof(t2.c):  1, &t2.c: 0019FF00, &t2.c - &t2:0
  sizeof(t2.d):  8, &t2.d: 0019FF02, &t2.d - &t2:2
  sizeof(t2.u):  1, &t2.u: 0019FF0A, &t2.u - &t2:10
  sizeof(t2.s):  2, &t2.s: 0019FF0C, &t2.s - &t2:12
  sizeof(struct Test4): 16
  sizeof(t4  ): 16, &t4  : 0019FEF0, &t4   - &t4:0
  sizeof(t4.c):  1, &t4.c: 0019FEF0, &t4.c - &t4:0
  sizeof(t4.d):  8, &t4.d: 0019FEF4, &t4.d - &t4:4
  sizeof(t4.u):  1, &t4.u: 0019FEFC, &t4.u - &t4:12
  sizeof(t4.s):  2, &t4.s: 0019FEFE, &t4.s - &t4:14
  ```

  - *Visual Studio default pragma pack value* 로 검색하면. 
  https://learn.microsoft.com/en-us/cpp/preprocessor/pack?view=msvc-170 에서

    ```
    the default value is 8 for x86, ARM, and ARM64. The default is 16 for x64 native and ARM64EC.
    ```    
  **구조체의 Size는 pack size의 배수이다. [ *sizeof(struct XXX) % pack size == 0* ]**

## 18-5. 구조체로 활용한 연결 리스트
  - linked list (직접 구현할 일 없음.. 그리고, 위험함.)
  - CPP의 STL을 사용하는 것이 바람직함.

# 19. 파일 입출력 (p:497)
## 19-1. 표준 입출력 라이브러리
## 19-2. Text File과 Binary File
  - Magic Number

## 19-3. 파열 열기와 닫기
## 19-4. Text 파일에 데이터 읽고 쓰기
## 19-5. Binary 파일에 테이터 읽고 쓰기

# 20. 함수포인터 (p:525)
## 20-1. 함수포인터
## 20-2. 함수 그룹
## 20-3. 콜백 함수

# A. 동적라이브러리
  - Static Link
  - Dynamic Link

# B. 다른 언어어 C함수 호출하기
  - Deplphi, PowerBuilder, C# : DLL
  - Java : JNI
  - Node : napi
  - Browser : webasm

# C. LittleEndian, BigEndian
  ```c
  int isLittleEndian() {
      union {
          short si ;
          char ch[2] ;
      }
      ch[0] = 0x01 ;
      ch[1] = 0x00 ;
      return (si == 1) ;
  }
  ```
