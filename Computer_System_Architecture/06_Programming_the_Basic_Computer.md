# 기본 컴퓨터 프로그래밍

> 본 글은 아래 강의를 바탕으로 작성되었습니다.
>
> [CSA2021 컴퓨터시스템구조 제 6 장 Part-1](https://youtu.be/bx3qZQb0LL8)
>
> [CSA2021 컴퓨터시스템구조 제 6 장 Part-2](https://youtu.be/hXKSCzaYCXk)

<br>

## 목차

[1. 기계어](#1-기계어)

[2. 어셈블리 언어](#2-어셈블리-언어)

[3. 어셈블러](#3-어셈블러)

[4. 프로그램 루프](#4-프로그램-루프)

[5. 산술 및 논리 연산의 프로그래밍](#5-산술-및-논리-연산의-프로그래밍)

[6. 서브루틴](#6-서브루틴)

[7. 입출력 프로그래밍](#7-입출력-프로그래밍)

<br>

## 1. 기계어

기본 컴퓨터가 가진 명령어 symbol은 그에 대응하는 Hexa code가 존재한다.

### 프로그램의 종류

- 이진 코드
  - 기계어 프로그램(코드)
  - 메모리상에 실제 나타나는 형태의 명령어 집합
  - 이진 명령어와 피연산자의 시퀀스로 구성
- 8진/16진 코드
  - 이진 기계어 코드를 8진수, 16진수로 표현
- 기호 코드
  - 이진 기계어 코드에 대하여 문자로 된 심볼로 표현
  - 어셈블리어
- 고급 프로그래밍 언어
  - 하드웨어 구조와 관계없이 문제 해결 논리가 고려된 언어
  - 문제 위주의 기호와 형식 사용
  - 인터프리터, 컴파일러 사용
  - FORTRAN, PASCAL, C, C++, BASIC, Jave 등

일반적으로 기계어는 16진 코드로, 16진 코드를 기호 코드로, 기호 코드를 어셈블리 코드로 변환하여 사용한다. 따라서 근본적으로 어셈블리 코드와 기계어는 동일하다.

<br>

## 2. 어셈블리 언어

### 언어 규칙

1. 라벨 필드: 기호 주소(메모리 주소) 또는 공란
2. 명령어 필드: 기계 명령어(Opcode), 슈도 명령어
3. 코멘트 필드: 명령어에 대한 주석

### 명령어 필드 항목

- 메모리 참조 명령어(MRI)
- 레지스터 참조 명령어(RRI)
- 입출력 명령어(IOI)
- 슈도 명령어: 어셈블리 언어를 편하게 볼 수 있도록 만들어진 명령어

<br>

## 3. 어셈블러

어셈블러는 기호-언어 프로그램을 이진 프로그램으로 번역하는 프로그램이다. MS Macro Assembler, Turbo Assembler 등이 이에 해당한다.

### First Pass

First Pass는 Address-Symbol Table을 작성하는 것이 목표이다.

1. 주소 기호와 이진수 값의 관계표(symbol table) 작성
2. Symbol Table을 출력
3. Location Counter(LC)를 사용하여 프로그램 주소를 카운트

### Second Pass

- 이진수로의 번역을 수행
- 4개 테이블 참조
  - MRI 명령어 table
  - Non-MRI 명령어 table
  - 슈도 명령어 table
  - Symbol Table
- 기계어 코드 출력

<br>

## 4. 프로그램 루프

### 루프를 가지는 프로그램

- 어셈블리어로의 표현
  - 루프 부분
  - 카운터 부분
  - 데이터 array 부분

<br>

## 5. 산술 및 논리 연산의 프로그래밍

- 곱셈 프로그램
- 배정밀도 가산
  - High part와 Low part를 따로 연산
  - Low part의 캐리를 High part에 가산
  - 결과치도 High part, Low part에 별도 저장

<br>

## 6. 서브루틴

<br>

## 7. 입출력 프로그래밍

- 1개 문자의 입출력
- 2개 문자의 패킹
  - 8bit ASCII -> 16bit UniCode
  - SH4 서브루틴 사용
- 버퍼에 문자 저장
- 두 워드의 비교
  - 데이터 감산을 통한 비교
  - 결과가 0인 경우 두 워드는 동일

### 프로그램 인터럽트

1. 레지스터의 내용을 저장
   1. M[xx] <- REGs
   2. IEN <- 0 (by IOFF)
2. FGI/FGO Flag의 값 체크
3. 인터럽트 서비스 루틴 수행
4. 레지스터 내용 원상 복구
   1. REGs <- M[xx]
5. 인터럽트 기능 ON
   1. IEN <- (by ION)
6. 원래 프로그램으로 복귀
