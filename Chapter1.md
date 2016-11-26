# Chapter.1 Introduction

컴파일러는 source program을 target program으로 변환해주는 프로그램이다. 인터프리터는 source program을 target program으로 변환하는게 아니라, 즉석에서 연산을 바로 실행한다는 차이가 있다.

## 컴파일러의 구조

```
      character stream
             |
             V
       Lexical Analyzer
             |
        token stream
             |
             V
       Syntax Analyzer
             |
        syntax tree
             |
             V
Intermediate Code Generator
             |
intermediate representation
             |                               Symbol Table
             V
    Machine-Independent
      Code Optimizer
             |
intermediate representation
             |
             V
       Code Generator
             |
    target-machine code
             |
             V
     Machine-Dependent
      Code Optimizer
             |
    target-machine code
```

컴파일 과정은 크게 분석(analysis) 과정과 통합(synthesis) 과정으로 나눌 수 있다.

### analysis(front end)

분석 과정은 소스 프로그램을 구성 요소로 분할한 다음 거기에 문법적인 구조를 만든다. 그리고 그 구조를 이용해서 소스 프로그램의 중간 표현형(Intermediate representation)을 만들어낸다. 이 단계에서 문법적으로 잘못된 코드나 의미적으로 이상한 코드를 발견하면 에러 메시지를 내뱉음. 또 여기서 수집한 소스 프로그램에 대한 정보를 심볼 테이블(symbol table)이라는 이름의 자료구조에 저장해둔다. 이 정보는 중간 표현형과 함꼐 synthesis 단계로 넘어감.

### Synthesis(back end)

이 단계에서는 중간 표현형을 이용해 타겟 프로그램을 만들어 냄. 

이 두가지 단계를 더 자세하게 나누면 위와 같은 그림이 나옴. 

### Lexical Analysis

컴파일러의 첫 단계는 어휘 분석(Lexical Analysis, 혹은 scanning). 이 단계에서는 소스 프로그램(character stream)을 입력으로 받아서 문자들을 어휘(lexeme)라고 불리는 의미있는 덩어리로 묶어냄. 각각의 어휘에 대해서 어휘 분석기는 (토큰 명, 속성 값)으로 구성된 형태의 토큰을 만들어 냄. 그리고 이 토큰을 구문 분석(syntax analysis) 단계로 넘긴다. 여기서 토큰 이름(token name)은 구문 분석 단계에서 쓰이는 추상적인 기호고, 속성 값(attribute value)은 이 토큰 정보가 심볼 테이블 어디에 저장되어 있는지 가리키는 값이다. 이 값은 의미 해석(semantic analysis) 단계와 코드 생성(code generation) 단계에서 쓰인다.

### Syntax Analysis

두 번째 단계는 구문 분석(혹은 파싱parsing). 이건 예전에 공부할 때 정리했던 [ppt 자료](http://www.slideshare.net/namhyeonuk90/pl-1)도 좀 쓸만한 듯. 이 단계에서 파서는 어휘 분석기가 만든 토큰 스트림을 이용해서 문법적인 구조를 나타내는 트리 같은 형태의 중간 표현형을 만들어 낸다. 일반적인 형태는 구문 트리(syntax tree). 이 트리의 중간 노드는 연산, 자식 노드는 그 연산의 인자를 나타낸다. 이 트리는 연산의 우선 순위를 나타내줌(자식에 가까울 수록 빨리 계산 - ppt 참조).

### Semantic Analysis

Semantic analyzer는 구문 트리와 심볼 테이블의 정보를 이용해 소스 프로그램이 의미적으로 일관성을 갖고 있는지 검사한다. 또 이 단계에서 타입 정보를 수집해 구문 트리 혹은 심볼 테이블에 해당 정보를 저장하며, 이 정보는 이후 중간 코드를 생성할 때 사용된다. 이 단계에서 중요한 부분은 바로 타입 체킹(type checking). 이 쪽 관련된 내용도 위의 ppt 자료에 같이 묶여서 좀 설명되어 있으니 그걸 참조.

### Intermediate Code Generation

컴파일러는 컴파일 단계에서 보통 하나 이상의 중간 표현형(Intermediate representation)을 사용한다. 구문 트리도 일종의 중간 표현형. 위의 분석 단계가 끝나고 나면 컴파일러는 좀 더 기계에 가까운 로우 레벨의 중간 코드를 만들어낸다. 중간 단계의 코드는 만들어내기 쉬워야 하며, target program으로의 번역도 쉬워야한다.  

### Code Optimization

딱히 특기할 만한 사항 없음. 최적화가 최적화지 뭐

### Code Generation

중간 코드를 target program으로 번역.

### Symbol-Table Management

컴파일러가 하는 중요한 작업 중 하나가 심볼 테이블 관리. 심볼 테이블은 각 이름들의 타입, 범위(scope), 저장되는 위치 등등의 다양한 특성을 저장한다. 그리고 이 걸 빠르고 효율적으로 관리해야 함(컴파일 타임과 직결되므로). 

### Compiler-Construction Tools

컴파일러를 만들 때 일반적으로 사용되는 툴로는 아래와 같은 것들이 있다.

1. Parser Generator : 프로그래밍 언어의 문법에 대한 기술(Description)로부터 자동으로 구문 분석기(syntax analyzer)를 만들어준다.

2. Scanner Generator : 언어의 토큰에 대한 정규 표현식 기술로부터 어휘 분석기(Lexical Analyzer)를 만들어준다.

3. Syntax-directed translation engines : parse tree 탐색과 중간 코드 생성과 관련된 여러 루틴들의 집합을 제공.

4. Code-generator generator : 각 연산들의 중간 코드 -> 목적 코드(target code)에 대한 번역 규칙으로부터 코드 제너레이터를 만들어낸다.

5. Data-flow analysis engines : 각각의 값들이 프로그램의 한 부분에서 다른 부분으로 어떻게 전달되는지에 대한 정보를 모을 수 있게 해준다. Data-flow analysis는 코드 최적화에서 가장 핵심적인 부분.

6. Compiler-Construction toolkits : 컴파일러의 다양한 부분들을 구성하기 위한 루틴들의 집합을 제공해줌.

챕터 1.5부터 이어보면 됨