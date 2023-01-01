# Floating point 

자바스크립트에서 아래 코드를 실행하면 예상되는 결괏값은 무엇일까?

```javascript
0.1 + 0.2
```

0.3 이다. 그러나 자바스크립트는 아래와 같이 예상치 못한 결괏값을 반환한다.

```javascript
0.30000000000000004
```

이유는 컴퓨터의 이진수 체계는 0.1, 0.2, 0.3 과 같은 숫자를 정확하게 표현하는 것이 불가능하다. 현재의 컴퓨터가 이진수 체계를 갖게된 것은 전기신호를 통해 빠른 연산이 가능하기 때문이다. 이진수는 17자리 소수점 자리를 처리할 수 없지만 대부분의 경우 그러한 시스템을
요구하지 않는다. 

아래 코드를 실행하면 원하는 결괏값이 잘 반환된다. 

```javacript
0.1 + 0.4 = 0.5
```

위 설명을 통해 추론할 수 있지만 결괏값 0.5 는 정확히 floating-point number 로 나타낼 수 있는 수이기 때문이다. 
0.3 은 0.33333 에서 rounding 된 숫자일 수 있으나 0.1 과 0.4 는 이진수로 표현가능하며 rounding error 가 상쇄된다. 
물론 0.1 + 0.4 연산 결괏값도 정확하지 않을 수 있다.

0.1 + 0.3 과 같은 경우에는 결과는 실제로 0.4가 아니지만 0.4가 다른 부동 소수점 숫자보다 결과에 더 가까운 가장 짧은 숫자이므로
대부분의 경우 컴퓨터는 부동 소수점 숫자 보다 일반 숫자를 보여준다.

그렇다면 예상된 결괏값을 얻을 수 있도록 하기 위해서는 어떻게 해야할까?

- 돈과 같이 정확한 계산이 요구되는 경우 특별한 데이터 타입을 사용해라.
- 추가 소수점 자리에 대해 필요치 않다면 고정 소수점 자리를 보여주도록 가공해라.
- 소수점 데이터 타입을 이용할 수 없다면 대안으로 integers 타입을 사용하라. 다만 몇가지 단점이 있다. 

앞서 설명한 대로 대부분의 경우 binary floating-point 수 만으로도 잘 동작하지만 돈과 같이 정확한 계산이 요구되는 경우 부적절할 수 있다.

### Limited-Precision Decimal
- 지수가 10진수로 해석된다는 점을 제외하면 기본적으로 IEEE 754 이진 부동 소수점과 동일한 데이터 타입이다.
- 예상치 못한 rounding error 를 피할 수 있다. 
- 부동소수점 데이터 유형 중 빠르고 간결하다.
- 이진수 형태보다 연산이 느리다. 

### Arbitrary-Precision Decimal
- "bignum" 이라고 불리우는 이 타입은 제한된 자리수 유형과 유사하나, 유효숫자 길이를 늘릴 수 있는 데이터 타입이다. 
- 유연하고 더 긴 자리수를 표현할 수 있으나 오버헤드가 있다. 
- 큰 금액의 금액을 표기하는데 사용할 수 있다. 

### Symbolic calculations
- 부정확한 반올림 숫자가 아니라 수학 기호를 사용하여 연산과 표현하는 방식을 말한다. 
- 예를 들어 1/3, square root of 2, e 와 π 와 같은 기호이다. 
- 이러한 수학 시스템은 복잡하고 느리며 수학 지식이 요구된다. 대부분의 프로그래밍에 적합하지 않다. 

그렇다면 더 원론적으로 floating point number 는 왜 존재할까?

## Floating Point Numbers

컴퓨터 메모리는 제한되어 있기 때문에 무한대 소수점을 저장할 수 없다.
따라서 어느 정도의 정확도를 요구하는지, 어떻게 사용될 수인지에 따라 정수 부분과 소수점 부분이 결정될 것이다. 

예를들어 고속도로를 설계하는데 10 미터와 10.0001 미터는 유의미하지 않다. 
그러나 반도체, 마이크로칩을 개발하는데 0.0001 미터는 아주 큰 차이이다. 
또한 물리학자가 빛의 속도를 계산할 때 뉴턴의 중력 상수(약 0.0000000000667)를 함께 계산하는 경우도 있다. 

이러한 엔지니어링, 칩 설계자를 위해서 엄밀한 정확도를 요구하는 숫자가 제공되어야 한다. 
이 경우 부동소수점 수가 필요한 것이다.

## How floating-point numbers work

부동소수점을 이루는 두가지 부분에 대해 알아보자.

```
1.5
```

- significand: 1.5 유효 숫자 부분. 음수도 표현할 수 있다. 
- exponent: significand 부터 상대적인 소수점 위치 값

보통 decimal floating-point numbers 는 아래와 같이 과학 표기법을 가진다. 

| Significand	| Exponent	| Scientific notation	| Fixed-point value |  
|---|---|---|---|
| 1.5 | 	4 |	1.5 ⋅ 104	| 15000 |

거의 모든 하드웨어 및 프로그래밍 언어는 IEEE 754 표준에 정의된 이진 형식의 부동 소수점 숫자를 사용한다. 
일반적인 형식은 총 길이가 32비트 또는 64비트 이다. 

| Format |	Total bits | Significand bits |	Exponent bits |	Smallest number |	Largest number
|---|---|---|---|---|---|
Single precision |	32 |	23 + 1 sign	| 8	| ca. 1.2 ⋅ 10-38	| ca. 3.4 ⋅ 1038

## In javascript

javascript 는 동적 타입 언어이므로  암시적으로 string 과 floating-point number 가 전환된다. 
floating point 를 강제하기 위해서는 `parseFloat` 함수를 사용하면 된다.

### Decimal Types

decimal 타입을 지원하는 javascript 라이브러리가 존재한다.  
round mode 와 다양한 연산을 지원한다.  
아래와 같이 3가지 라이브러리를 지원하는데 이들의 차이점은 [difference](https://github.com/MikeMcl/big.js/wiki#what-is-the-difference-between-bigjs-bignumberjs-and-decimaljs) 이 링크에서 확인할 수 있다. 

- bignumber.js - https://github.com/MikeMcl/bignumber.js
- big.js - https://github.com/MikeMcl/big.js
- decimal.js - https://mikemcl.github.io/decimal.js/

간략하게는 big.js 는 bignumber.js 의 경량화된 버전이다. bignumber.js 는 precision 에 대해 신경쓰지 않아도 되기에 financial application 에 적합하다고 소개한다. decimal.js 는 매우 작거나 큰 값도 효율적으로 처리하기에 scientific application 에 적합하다.



#### Reference
https://floating-point-gui.de/  
