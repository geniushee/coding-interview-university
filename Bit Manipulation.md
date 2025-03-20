기본적인 명령어

| and | &   | not         | ~   |
| --- | --- | ----------- | --- |
| or  | \|  | left shift  | <<  |
| xor | ^   | right shift | >>  |

```
AND - Only true if both input bits are true.
0 & 0 = 0
1 & 0 = 0
0 & 1 = 0
1 & 1 = 1

10010110 & 00110010 => 00010010


OR
0 | 0 = 0
1 | 0 = 1
0 | 1 = 1
1 | 1 = 1

10010110 & 00110010 => 1011110


XOR
0 ^ 0 = 0
1 ^ 0 = 1
0 ^ 1 = 1
1 ^ 1 = 0

10010110 ^ 00110010 => 10100100

NOT
~0 = 1
~1 = 0

~10010110 => 01101001


Left Shift
00010110 << 00000010 => 01011000

Right Shift
00010110 >> 00000010 => 00000101

```

Left Shift는 1번 옮길때마다 2씩 곱하는 효과가 있다. 또한 가장 오른쪽에는 0이 추가된다. 하지만 데이터 크기를 넘어서 1이 왼쪽으로 이동된다면 버려지게 된다.

Right Shift는 1번 옮길때마다 2로 나누는 효과가 있다. 또한 가장 왼쪽에는 0이 추가된다. 가장 오른쪽의 0 또는 1은 버려지게 된다.

## Bit Mask 활용방법
### 1. 특정 비트 설정 (set  a bit)
어떤 비트를 1로 만들고 싶다면 OR 연산자(|)를 사용한다.
```python
def set_bit(x, position):
	mask = 1 << position
	return x | mask

# x = 00000110, position = 00000101, mask = 00100000, result = 00100110
```

### 2. 특정 비트 지우기(Clear a bit)
어떤 비트를 0으로 만들고 싶다면 AND연산자(&)와 NOT 연산자 (~)를 사용한다.
```python
def clear_bit(x, position):
	mask = 1 << position
	return x & ~mask

# x = 00000110, position = 00000010, mask = 00000100, result = 00000010
```


### 3. 특정 비트 토글하기(Flip a bit)
```python
def flip_bit(x, position):
	mask = 1 << position
	return x ^ mask

# x = 01100110, position = 00000010, mask = 00000100, result = 01100010
```

---
### IS BIT SET
해당 위치의 BIT가 1인지 0인지 확인한다. 위치를 2x0으로 옮긴후 1과 AND 연산자(&)를 사용하여 사용한다.
```python
def is_bit_set(x, position):
	shifted = x >> position
	return shifted & 1

# x = 01100110, position = 00000101, shifted = 0000011 result = true
```


### MODIFY BIT
State의 값에 따라서 변경 및 삭제가 이루어 집니다.
```python
def modify_bit(x, position, state):
	mask = 1 << position
	return (x & ~mask) | (~state & mask)
# state가 1이면 set하고 0이면 clear한다.

# x = 00000110, position = 00000101, state = 00000001, mask = 00100000
# ~mask = 11011111, ~state = 11111111, result = 00100110

# x = 00000110, position = 00000010, state = 00000000, mask = 00000010
# ~mask = 11111101, ~state = 00000000, result = 00000010
```

`x & ~mask`는 위에서 봤던 특정 비트 지우기와 동일하게 동작합니다. 그리고 `state`가 1일 때 `~state & mask`는 `mask`와 동일합니다. 따라서 `state = 1`이면 1로 변경이 되고 `state = 0`이면 해당 포지션의 비트가 삭제됩니다.
이때, 1의 NOT은 -1로 BIT는 `1`로 꽉 채워지게 되는데 보수의 개념이 사용됩니다. 그리고 0의 NOT은 즉, 음수 0은 존재하지 않기 때문에 함수의 결과로 포지션의 1이 지워지게 됩니다. (일단 0이던 1이던 지우고 state가 1이면 추가, 0이면 그대로 반환)
>보수 더했을 때, 0이 되는 수

---
## BIT TRICKS

1. 짝수 확인 방법
	1. 모든 2진수에서 홀수는 가장 오른쪽이 1이므로 이진수 확인만 하면된다. 모듈로(%) 연산 없이
	2. x & 1 == 0 (짝수)
	3. not(x & 1) (짝수)
2. 2의 거듭제곱인지 확인
	1. x & x-1 == 0
	2. 2의 거듭제곱은 1이 1개만 있고 나머지는 0이다. 이때, 1을 빼면 원래 1이 있던 자리 이하의 모든 자리수가 0에서 1로 변경(채워지고) & 연산자를 사용하면 같은 위치의 1이 없으므로 0을 반환하게 된다.


## EXERCISE
write a function to count the number of bits that are different between tow numbers

http://bits.stephan-brumme.com/
http://h14s.p5r.org/2012/09/0x5f3759df.html/
http://en.wikipedia.org/wiki/Fast_inverse_square_root

