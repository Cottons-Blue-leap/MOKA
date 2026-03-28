---
name: Python 3.12 공식 문서 학습
description: Python 3.12 공식 문서 전체 학습 완료 - Tutorial/Language Reference/What's New/Library Reference/HOWTOs
type: reference
---

# Python 3.12 공식 문서 학습 완료

**학습일:** 2026-03-28
**소스:** https://docs.python.org/3.12/
**설치 버전:** Python 3.12

## 학습 범위

### 1. Tutorial (16챕터 전체)
- Ch1: Whetting Your Appetite
- Ch2: Using the Interpreter (인터프리터 호출, 인코딩)
- Ch3: Informal Introduction (숫자, 문자열, 리스트)
- Ch4: Control Flow (if/for/while/match, 함수 정의, *args/**kwargs, /, *, lambda)
- Ch5: Data Structures (리스트 메서드/컴프리헨션, tuple, set, dict, 루핑 기법)
- Ch6: Modules (모듈/패키지, __init__.py, 상대/절대 import, __all__)
- Ch7: Input/Output (f-string, str.format(), 파일 I/O, json)
- Ch8: Errors & Exceptions (try/except/else/finally, ExceptionGroup, except*, add_note)
- Ch9: Classes (스코프/네임스페이스, 상속/다중상속, MRO, name mangling, 이터레이터, 제너레이터)
- Ch10-11: Standard Library Tour (os, re, math, datetime, random, statistics, logging, threading, decimal 등)
- Ch12: Virtual Environments & pip
- Ch15: Floating-Point Arithmetic
- Ch16: Appendix (인터랙티브 모드, 실행 스크립트)

### 2. Language Reference (10챕터 전체)
- **렉서 분석:** 라인 구조, 인덴트/디덴트 토큰화, 키워드 35개, 소프트 키워드 4개(match/case/type/_), 리터럴(문자열/숫자/f-string 전체 문법), 이스케이프 시퀀스, 연산자/구분자
- **데이터 모델:** 객체(identity/type/value), 표준 타입 계층(None~내부 타입), 특수 메서드 60+개 (__new__/__init__/__del__/__repr__/__str__/__hash__/__eq__/__lt__/__add__/__getattr__/__setattr__/__getitem__/__len__/__call__/__enter__/__exit__/__iter__/__next__/__buffer__ 등), 디스크립터 프로토콜, __slots__, 코루틴
- **실행 모델:** 코드 블록, LEGB 스코프 규칙, global/nonlocal, 어노테이션 스코프(3.12 신규), 지연 평가
- **표현식:** 연산자 우선순위 18단계, 왈러스 연산자(:=), 조건 표현식, 제너레이터 표현식, yield/yield from, await
- **단순문:** 할당(일반/증강/어노테이트), assert, pass, del, return, yield, raise(체이닝/from), break, continue, import, global, nonlocal, type문(3.12 신규)
- **복합문:** if, while, for, try(except/except*/else/finally), with, match(패턴 매칭 전체), 함수 정의(데코레이터/async), 클래스 정의, 코루틴(async def/for/with), 타입 파라미터 리스트(3.12 신규)

### 3. What's New in Python 3.12
- **PEP 695:** 타입 파라미터 구문 (def func[T](), class Bag[T], type Point = ...)
- **PEP 701:** f-string 개선 (따옴표 재사용, 무제한 중첩, 주석, 백슬래시 허용)
- **PEP 684:** 인터프리터별 GIL (C-API 전용, 3.13에서 Python API 예정)
- **PEP 669:** 저영향 모니터링 (sys.monitoring)
- **PEP 709:** 컴프리헨션 인라이닝 (최대 2배 속도 향상)
- **PEP 688:** 버퍼 프로토콜 Python 접근 (__buffer__)
- **향상된 에러 메시지:** import 제안, self.attr 제안, 구문 교정
- **PEP 692:** TypedDict로 **kwargs 타이핑
- **PEP 698:** @override 데코레이터
- **최적화:** asyncio 최대 75% 향상, isinstance 2-20배, tokenize 64%, super() 호출 최적화
- **제거:** distutils, imp, asynchat/asyncore, smtpd
- **보안:** HACL* 기반 해시 구현, CVE 2024-4030 대응

### 4. Library Reference (핵심)
- **내장 함수 69개 전체:** abs, aiter, all, any, ascii, bin, bool, breakpoint, bytearray, bytes, callable, chr, classmethod, compile, complex, delattr, dict, dir, divmod, enumerate, eval, exec, filter, float, format, frozenset, getattr, globals, hasattr, hash, help, hex, id, input, int, isinstance, issubclass, iter, len, list, locals, map, max, memoryview, min, next, object, oct, open, ord, pow, print, property, range, repr, reversed, round, set, setattr, slice, sorted, staticmethod, str, sum, super, tuple, type, vars, zip, __import__
- **내장 타입 전체:** int(bit_length/bit_count/to_bytes/from_bytes), float(as_integer_ratio/is_integer/hex), complex, bool, str(70+ 메서드), bytes/bytearray(decode/fromhex/hex), list(sort), tuple, range, set/frozenset, dict(keys/values/items 뷰), memoryview
- **표준 라이브러리 234+ 모듈 구조:** 34개 카테고리 (텍스트/바이너리/데이터타입/수학/함수형/파일/DB/압축/파일형식/암호화/OS/동시성/네트워킹/인터넷/마크업/개발/디버깅/패키징/런타임/언어서비스 등)

### 5. HOWTOs (18개)
- Annotations, Argparse, Descriptor, Enum, Functional Programming, ipaddress, Logging, Logging Cookbook, Regex, Sorting, Unicode, urllib, Curses, Isolating Extensions, MRO, Socket, Porting Extensions, GDB, DTrace/SystemTap, perf profiler
