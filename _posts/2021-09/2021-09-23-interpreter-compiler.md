---
title: "Interpreted vs Compiled Language"
date: 2021-09-23 21:12:00 +0900
classes: wide
toc: true
tags:
    - tech
    - language
    - python
    - interpreter
    - compiler
    - runtime
---

What is the difference between a compiled and an interpreted program?

## Intro

많은 프로그램들은 C나 Java와 같은 고차원의 언어로 쓰여져 있다. 마치 사람의 언어가 사람들 간의 의사소통을 쉽게 해주듯이, 컴퓨터 언어 또한 컴퓨터가 해야할 일을 단순화 시켜준다. 하지만, 컴퓨터는 오직 0과 1만 읽을 수 있으므로 컴퓨터와 대화하기 위해서는 적절하게 번역해줄 수 있는 'interpreter'와 'compiler'가 필요하게 된다.

`Interpreted Language`와 `Compiled Language`의 차이점은 프로세스의 결과가 Interprete한 결과인지 Compile한 결과인지이다. 인터프리터는 프로그램으로 부터 결과를 생산(produce)하는 반면, 컴파일러는 'Assembly Language'로 작성된 프로그램을 생산한다. 그 후 해당 아키텍처의 'Assembler`는 'Binary Code'로 변환한다. 이 때, 어셈블리 언어는 각 컴퓨터의 아키텍처에 따라 다르다. 결과적으로, 컴파일된 프로그램은 컴파일이 일어난 아키텍처와 같은 아키텍처의 컴퓨터에서만 동작 가능하다.

## Compiled Programs

`Compiled Programs`(컴파일된 프로그램)은 사람이 읽기 힘들지만, 아키텍처 특화된 'Machine Language'측면에서는 읽기 쉽다. 컴파일 프로그램을 만들기 위해서는 몇가지 과정이 필요하다. 먼저, 프로그래머가 개발 툴을 이용하거나 혹은 텍스트 에디터라도 이용해서 일단 'source code'를 사용하고자 하는 언어로 작성해야한다. 만약에 프로그램이 복잡하다면, 여러개의 파일들로 이루어 질 수도 있다. 그 후 프로그래머는 컴파일하여, 모듈들을 정렬과 연결을 하고, 컴퓨터가 이해할 수 있는 머신 언어로 번역한다.

컴퓨터는 서로 다른 머신의 언어로 대화 할 수 없기 때문에, 컴파일 된 프로그램은 설계된 플랫폼 위에서만 동작 가능하다. 예를 들어, HP-UX에서 작성된 프로그램은 Mac OS나 Solaris같은 컴퓨터에서는 잘 동작하지 않는다. 이 단점에도 불구하고, 컴파일된 프로그램은 인터프리터로 작동하는 것 보다 빠르다는 장점이 있다. 또한, 'recompile'도 가능한 경우가 있기 때문에 다른 여러 플랫폼에서도 동작 가능하다. 이러한 컴파일된 프로그램(compiled programs)을 만드는데 사용하는 언어로는 C, Fortan, COBOL 등이 대표적이다.

## Interpreted Programs

`Interpreted Programs`은 소스 코드가 사실상 프로그램 그 자체이다. 'Script'로 알려진 이러한 프로그램들은 인터프리터를 필요로한다. 이 인터프리터는 명령들을 파싱하고 실행시킨다. Unix Shell 같은 몇몇의 인터프리터는 스크립트를 읽는 즉시 각 커맨드를 실행하기도 한다. 이는 Perl과 같은 다른 인터프리터가 전체 스크립트 분석을 선행한 뒤 머신 언어로 전달하는 것과는 차이가 있다. 'Script'가 주는 이점으로는 매우 'portable'하다는 점도 있다. 어떤 컴퓨터라도 인터프리터만 설치되어 있으면 거의 바뀌는 사항 없이 프로그램을 실행 할 수 있다. 하지만 이러한 부분은 오히려 단점이 될 수도 있는데, 인터프리터가 없다면 실행이 불가능하기 떄문이다. 일반적으로, 인터프리터 언어로 작성된 프로그램은 컴파일된 프로그램보다 느리다는 단점이 있지만, 디버그와 수정에 용이하다. 또 다른 인터프리티드 언어의 예로는 Javascript와 Python 등이 있다.

## Runtime Environments

위에서 살펴본 Computer-specific copiled progrmas와 Interpreted Scripts의 중간단계로는 `programs designed for runtime environments`가 있다. Java와 Smailltalk의 경우 이 방법을 사용한다. 이러한 프로그램을 작성하는데 있어서는 기존의 컴파일 프로그램을 작성하는 것과 유사하다. 차이점은 소스코드를 머신 언어로 컴파일링 하는 대신, 런타임 환경의 가상 머신에서 작동하는 'Byte Code'로 만든다는 점이다. 가상 머신은 이 바이트 코드를 번역하여 컴퓨터에 맞는 명령어로 변환시켜준다. 이러한 접근법의 이점은, 런타임 환경이 전체 소스코드에서 필요한 부분만 즉시 컴파일한다는 점이다. 이를 `Just-in-time compiling`이라고 한다. 하지만 런타임 환경의 가장 큰 문제점은, 제대로 설계되지 않은 프로그램이 런타임 환경에서 거의 모든 코드를 미리 컴파일한 다음 인터프리터를 중복 호출하게 된다는 것이다. 이는 프로그램을 느리게 만든다.

## reference

[link](https://kb.iu.edu/d/agsz)