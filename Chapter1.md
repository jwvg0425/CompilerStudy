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

