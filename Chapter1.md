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
