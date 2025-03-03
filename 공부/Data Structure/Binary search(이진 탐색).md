# CS50
많은 사람들의 이름이 있다. Alice부터 Yellow까지 그럼 Mickey Mouse는 어디 있을까?
앞에서 부터 Alice, Arrow, ... 매우 많이 찾아야한다. 그럼 뒤에서부터 Yellow, Toe, Super, ... 여기서도 많이 찾아가야한다. 그럼 우리는 Mickey가 M으로 시작한다는 것을 알고 있다. 그럼 M 보다 먼저 오는 걸 싹 지우면? 그리고 M뒤에 O부터 싹 지우면? M으로 시작하는 이름만 남고 몇번안에 Mickey를 찾을 수 있다.
```
binarySearch(key, array[], min, max)
	if(max < min): return -1
	else: midpoint = findMidPoint(min, max)

	if(array\[midpoint]) < key):
		binarySearch(key, array, midpoint + 1, max)
	else if (array\[midpoint] > key):
		binarySearch(key, array, min, midpoint -1)
	else: return midpoint
```

Binary Search를 사용하기 위해서 선행되야하는 조건이 있다. 예를 들어 숫자 배열은 반드시 정렬이 되어 있어야한다. 그래서 2가지 옵션이 있다. Binary Search를 하기 전에 정렬을 하든지, 숫자를 배열에 넣을 때, 정렬을 하게 만들던지.

그렇게 숫자를 넣든, 빼든 정렬된 상태를 유지하는 데이터 구조가 있다. 바로, Binary Search Tree(이진 탐색 트리)이다. 이진 탐색트리는 3가지 특징이 있다.
- 노드의 왼쪽 하위트리는 노드랑 같거나 작은 값을 가진다.
- 노드의 오른쪽 하위 트리는 노드랑 같거나 큰 값을 가진다.
- 노드의 왼쪽 오른쪽 모두 이진 탐색 트리라는 것이다.


중앙 왼쪽으로는 작은 값이 트리의 최상단에는 중앙값이 오게 된다. 이진 탐색 트리에서 최소값과 최대값을 찾는건 매우 쉽다. 그냥 왼쪽 하위노드만 쫒아가면되고, 오른쪽 하위 노드만 쫒아가면된다.
트리를 배열로 만드는건 왼쪽 하위트리를 모두 작성하고 오른쪽 트리를 작성하면 된다. 단지 오른쪽 하위트리를 작성할 때는 왼쪽 하위 노드 먼저, 그리고 해당 노드를 작성하면 된다. 새로운 숫자를 추가하는 것도 어렵지 않다. 트리의 최상단부터 시작하여 작은지 큰지 비교하며 트리를 따라가서 배치하면 된다. 하지만 제거하는건 조금 다르다. 제거하는 요소가 트리의 마지막 요소인 잎이라면 그냥 제거하면 되지만 트리 중간에 있다면 해당 요소를 삭제하고 트리를 다시 구성해주어야 한다.

# Khan Academy
정렬된 리스트에서 효과적인 알고리즘이다. 하나가 남을때까지 절반씩 나누면서 작동한다. 가장 흔한 방법 중 하나는 배열에섯 이진탐색을 사용하는 것이다. 예를 들어 2백만개가 넘는 별들 중 이름으로 특정 별을 찾아보자. 선형 탐색이라고 불리는 처음부터 끝까지 찾는 알고리즘으로 찾으면 최악의 경우 2백만번 이상 해야만 한다. 하지만 이진탐색을 사용하면 22번 내로 찾을 수 있다.

추측게임을 보자 1~100까지 있을 때, 이미 21과 80을 말했고, 21보다 높고, 80보다 낮다고 했다. 그럼 21과 80사이의 범위를 정답구간으로 생각할 것이다. 그리고 다음 숫자로 53을 얘기하고 53이 높다고 얘기한다면 53~80이라는 절반을 제외하면서 정답범위를 절만으로 만들 수 있을 것이다. 이런 과정을 정확하게 설명한 것이다.
1. Let \[min = 1 \] and \[ max = n\].
2. Guess the average of \[max\] and \[min\], rounded down so that it is an integer.
3. If you guessed the number, stop. You found it!
4. If the guess was too low, set \[min\] to be one larger than the guess.
5. If the guess was too high, set \[max\] to be one smaller than the guess.
6. Go back to step two.
이렇게 설명하는 것이 컴퓨터에게 더욱 알맞다.

직접 구현해보자.
소수 25개로 이루어진 배열이 있다. 여기서 67을 찾을려고 한다. 67이 배열내에 있다면 소수이다. 선형 탐색 즉, 처음부터 탐색한다면 Index 18에 67이 있는 것을 확인할 수 있다. 하지만 18번이나 찾아야한다.
이진탐색을 사용하면 먼저 (0+24)//2 = 12인 index 12인 41부터 찾는다. 41은 67보다 작다. 그러면 (13 + 24)//2 = 18을 찾는다. index 18은 67이다. 2번만에 찾았다.

유사코드
1. Let `min = 0` and `max = n-1`.
2. Compute `guess` as the average of `max` and `min`, rounded down (so that it is an integer).
3. If `array[guess]` equals `target`, then stop. You found it! Return `guess`.
4. If the guess was too low, that is, `array[guess] < target`, then set `min = guess + 1`.
5. Otherwise, the guess was too high. Set `max = guess - 1`.
6. Go back to step 2.

코드로 옮기는 과정
for보다는 while이 더 적합하다. 특정 절차에 따라서 움직이지 않기 때문이다. 만약 배열에 찾는 값이 없다면 -1을 반환하도록 한다. 만약 10을 찾는데 3,4밖에 안 남았다면? 그러면 그 수는 없는 것이다.

최종 의사코드이다.
1. Let `min = 0` and `max = n-1`.
2. If `max < min`, then stop: `target` is not present in `array`. Return `-1`.
3. Compute `guess` as the average of `max` and `min`, rounded down (so that it is an integer).
4. If `array[guess]` equals `target`, then stop. You found it! Return `guess`.
5. If the guess was too low, that is, `array[guess] < target`, then set `min = guess + 1`.
6. Otherwise, the guess was too high. Set `max = guess - 1`.
7. Go back to step 2.

# Top coder
이진탐색은 검색공간을 반으로 줄이면서 대상값을 찾기 위해 O(log N)이상의 비교를 하지 않는다. 로그는 매우 느리게 성장하는 함수이고 백만번에서는 고작 21번만에 찾을 수 있고, 전세계 인구에서 특정 사람을 찾더라도 35번 내에 찾을 수 있다.

## 이산 이진탐색
이진탐색을 시퀀스(배열)로 제한할 이유가 없다. 정의역이 정수집합인 모든 함수에 대해서 이진탐색을 사용할 수 있다. 검색공간(배열에서는 인덱스 중 검색의 시작과 끝)은 함수의 정의역의 하위 구간이고 대상 값은 공역의 요소이다. 
순서집합 S(검색공간)에 대해 정의된 술어 p를 고려한다. 검색 공간은 문제에 대한 후보 솔루션으로 구성된다. 술어는 참 또는 거짓을 반환하는 함수이다. 문제의 정의에 따라 후보 솔루션이 합법적인지(어떤 제약 조건을 위반하지 않는지) 확인하는데 술어를 사용한다.
주요정리라고 부를 수 있는 것은 이진탐색을 사용할 수 있는 것은 오직 S의 모든 x에 대해 p(x)가 모든 y> x에 대해 p(y)를 의미할 때라는 것이다. 이것은 검색공간 후반부를 버릴 때 사용하는 것이다. 이는 ~p(x)가 모든 y < x에 대해 ~p(y)를 함축한다고 말하는 것과 같다. (~는 not이다.) 이는 검색공간 전반부를 버릴때 사용하는 것이다.
술어가 일련의 예답과 일련의 아니오 답을 생성하는 경우에도 이진탐색을 사용할 수 있다는 것을 알 수 있다. 주요 정리의 조건이 충족되면 이진탐색을 사용하여 가장 작은 합법적 솔루션, 즉 p(x)가 참인 가장 작은 x를 찾을 수 있다. 이렇게 술어를 설계하면 알고리즘이 찾아야 할 것을 선택해야 한다. p(x)가 참인 첫번째 x 또는 p(x)가 거짓인 마지막 x를 찾아야 한다. 결국 하나에 정착해야한다.
이진탐색이 술어에 적용될 수 있음을 보이면 된다. p(x)가 모든 y> x에 대해 p(y)를 의미하거나 그 반대이면 된다. 이 부분은 p(x)가 p(x+1)를 의미한다는 것을 귀납법에 따라 진행해보면 된다.
이 추상정의에 대한 소개에서 설명한 정렬된 배열에 대한 간단한 이진 탐색을 변환해 보자. 문제를 다시 표현해 보자. "배열 A와 대상 값이 주어지면, 대상 값보다 크거나 같은 값의 첫 인덱스를 반환합니다."
"A\[x]가 대상값보다 크거나 같은가?"라는 술어에 대해 주요 정리의 조건은 배열이 오름차순으로 정렬되어 있기 때문에 충족되며 A\[x]가 대상값보다 크거나 같으면 그 뒤의 모든 요소도 확실히 대상 값보다 크거나 같다. 이를 샘플 배열에 적용하면 일련의 아니오와 일련의 예로 반환되며 첫번째 예의 인덱스가 이진탐색의 결과와 같다.

이산 알고리즘 구현
중요한 것은 두 숫자(하한과 상한)이 무엇을 의미하는지 정하는 것이다. 이에 대한 답은 p(x)가 참인 첫번째 x를 확실히 포함하는 닫힌 구간이다. 경계설정이 중요하며, 항상 경계가 너무 넓지 않은지 확인해야 한다. 특히 중간값을 계산할 때, 오버플로 오류를 주의 깊게 살펴야한다. int max = 2,147,483,647가 이라면 2,000,000,000을 2개 더하는 것은 오버플로 오류가 발생한다. 이를 해결하기 위해 `int mid = left + (right - left) / 2;` 이런 형태로 중간값을 계산한다. 또한 이렇게 계산하면 `left + rigth`가 음수일 때, 소수점 이하를 절삭해버리는 언어가 있기때문에 저렇게 계산해야 제대로된 값이 나올 수 있다.

실수에서도 이러한 방법을 적용할 수 있다. 단 실수에서는 정확한 값을 찾기는 어렵기 때문에 (소수점이 정확하지 않다) 반복횟수나 범위를 정해서 중단하는 방법이 사용될 수 있다.

## 실사용 예
다른 영역으로 확장하여 사용할 수 있다.
선택했습니다. 이 문제에서 여러 작업자가 여러 서류 보관함을 조사해야 합니다. 모든 캐비닛이 같은 크기가 아니며 각 캐비닛에 몇 개의 폴더가 들어 있는지 알려줍니다. 각 작업자가 순차적으로 캐비닛을 살펴보고 작업자가 살펴봐야 하는 폴더의 최대 개수를 최소화하는 작업을 찾아야 합니다.  
  
문제에 익숙해진 후에는 약간의 창의성이 필요합니다. 사용할 수 있는 작업자의 수가 무제한이라고 가정해 보겠습니다. 중요한 점은 MAX라는 숫자에 대해 각 작업자가 MAX개 이상의 폴더를 조사하지 않아도 되도록 필요한 최소 작업자 수를 계산할 수 있다는 것입니다(가능한 경우). 어떻게 하는지 살펴보겠습니다. 어떤 작업자가 첫 번째 캐비닛을 조사해야 하므로 아무 작업자나 할당합니다. 그러나 캐비닛은 순차적으로 할당해야 하므로(작업자는 2도 조사하지 않고는 캐비닛 1과 3을 조사할 수 없음) 도입한 한계(MAX)를 넘지 않는다면 항상 그를 두 번째 캐비닛에도 할당하는 것이 최적입니다. 한계를 넘을 경우 그의 작업이 완료되었다고 결론 내리고 두 번째 캐비닛에 새 작업자를 할당합니다. 모든 캐비닛이 할당될 때까지 비슷한 방식으로 진행하고 도입한 인위적 한계로 가능한 최소한의 작업자를 사용했다고 주장합니다. 여기서 작업자 수는 MAX에 반비례한다는 점에 유의하세요. 한계를 높게 설정할수록 필요한 작업자 수가 줄어듭니다.  
  
이제 문제 설명에서 요구한 내용을 다시 주의 깊게 살펴보면 실제로는 필요한 작업자 수가 사용 가능한 작업자 수보다 적거나 같도록 가장 작은 MAX를 요구한다는 것을 알 수 있습니다. 이를 염두에 두고 거의 끝났습니다. 점들을 연결하고 이 모든 것이 이진 검색을 사용하여 문제를 해결하기 위해 설정한 프레임에 어떻게 들어맞는지 확인하기만 하면 됩니다.  
  
문제가 우리의 필요에 더 잘 맞게 다시 표현되었으므로 이제 술어를 검토할 수 있습니다. 작업 부하를 분산하여 각 작업자가 제한된 수의 작업자를 사용하여 x개 이상의 폴더를 검토하지 않아도 됩니까? 설명된 탐욕 알고리즘을 사용하여 모든 x에 대해 이 술어를 효율적으로 평가할 수 있습니다. 이것으로 이진 검색 솔루션을 구축하는 첫 번째 부분이 끝났습니다. 이제 주요 정리의 조건이 충족된다는 것을 증명하기만 하면 됩니다. 하지만 x를 늘리면 실제로 최대 작업 부하에 대한 제한이 완화되므로 동일한 수의 작업자만 필요하거나 더 적은 수만 필요하며 더 많은 작업자는 필요하지 않습니다. 따라서 술어가 일부 x에 대해 예라고 말하면 모든 더 큰 x에 대해서도 예라고 말합니다.  
  
요약하자면, 문제를 해결하는 STL 기반 스니펫이 있습니다.
```
int getMostWork(vector folders, int workers) {
  int n = folders.size();
  int lo = * max_element(folders.begin(), folders.end());
  int hi = accumulate(folders.begin(), folders.end(), 0);

  while (lo < hi) {
    int x = lo + (hi - lo) / 2;

    int required = 1, current_load = 0;
    for (int i = 0; i < n; ++i) {
      if (current_load + folders[i] <= x) {
        // the current worker can handle it
        current_load += folders[i];
      } else {
        // assign next worker
        ++required;
        current_load = folders[i];
      }
    }

    if (required <= workers)
      hi = x;
    else
      lo = x + 1;
  }

  return lo;
}
```

신중하게 선택된 하한과 상한에 주목하세요.상한을 충분히 큰 정수로 바꿀 수 있지만, 하한은 가장 큰 캐비닛보다 작아서는 안 됩니다.단일 캐비닛이 모든 작업자에게는 너무 큰 상황을 피하기 위해서입니다.이 경우는 술어에서 올바르게 처리되지 않습니다.또 다른 방법은 하한을 0으로 설정한 다음 너무 작은 x를 술어에서 특별한 경우로 처리하는 것입니다.  
  
해결책이 잠기지 않는지 확인하기 위해, 저는 폴더={1,1} 및 작업자=1인 작은 아니요/예 예제를 사용했습니다.  
  
해결책의 전체 복잡도는 O(n log SIZE)이며, 여기서 SIZE는 검색 공간의 크기입니다.매우 빠릅니다.  
  
보시다시피, 우리는 술어를 평가하기 위해 탐욕적 알고리즘을 사용했습니다.다른 문제에서는 술어를 평가하는 것이 간단한 수학 표현식에서 이분 그래프에서 일치하는 최대 기수를 찾는 것까지 다양할 수 있습니다.


### 결론

포기하지 않고 여기까지 왔다면, 이진 탐색으로 해결할 수 있는 모든 것을 해결할 준비가 되었을 것입니다. 몇 가지 사항을 명심하세요.

- 효율적으로 평가할 수 있고 이진 검색을 적용할 수 있는 술어를 설계합니다.
    
- 찾고 있는 것이 무엇인지 결정하고 검색 공간에 항상 해당 내용이 포함되도록 코드를 작성합니다(존재하는 경우).
    
- 검색 공간이 정수로만 구성된 경우 알고리즘이 잠기지 않는지 확인하기 위해 두 요소 집합에서 알고리즘을 테스트하십시오.
    
- 하한과 상한이 지나치게 제한되지 않았는지 확인합니다. 일반적으로 술어<를 위반하지 않는 한 하한과 상한을 완화하는 것이 좋습니다.
    

  
이진 검색을 사용하여 해결할 수 있는 몇 가지 문제는 다음과 같습니다.  
  

#### 단순한

- [자동차대출](http://community.topcoder.com/stat?c=problem_statement&pm=3970&rd=7993) – SRM 258
    
- [정렬추정](http://community.topcoder.com/stat?c=problem_statement&pm=3561&rd=6519) - SRM 230  
      
    

#### 보통의

- [UnionOfIntervals](http://community.topcoder.com/stat?c=problem_statement&pm=4823&rd=8074) – SRM 277
    
- [모기지](http://community.topcoder.com/stat?c=problem_statement&pm=2427&rd=4765) – SRM 189
    
- [공정한 작업 부하](http://community.topcoder.com/stat?c=problem_statement&pm=1901&rd=4650) - SRM 169
    
- [헤어컷](http://community.topcoder.com/stat?c=problem_statement&pm=4721&rd=8000) – SRM 261 더 하드
    
- [패킹쉐이프](http://community.topcoder.com/stat?c=problem_statement&pm=4751&rd=8067) - SRM 270
    
- [리모트로버](http://community.topcoder.com/stat?c=problem_statement&pm=4022&rd=6534) - SRM 235
    
- [네거티브 포토레지스트](http://community.topcoder.com/stat?c=problem_statement&pm=2946&rd=5856) - SRM 210
    
- [월드피스](http://community.topcoder.com/stat?c=problem_statement&pm=2420&rd=5850) - SRM 204
    
- [유닛 이동](http://community.topcoder.com/stat?c=problem_statement&pm=5921&rd=8075) - SRM 278
    
- [주차](http://community.topcoder.com/stat?c=problem_statement&pm=3530&rd=6535) – SRM 236
    
- [스퀘어프리](http://community.topcoder.com/stat?c=problem_statement&pm=2342&rd=4770) - SRM 190
    
- [플래그](http://community.topcoder.com/stat?c=problem_statement&pm=1206&rd=4540) – SRM 147


# Blueprint

구현에서 관해서 버그 없는 코드를 단 몇분만에 작성하는건 어려운 일이다. 아래는 일부 예시이다.
- 언제 반복조건을 종료하지? `left < right` 또는 `left <= right`?
- `left` and `right` 경계 변수를 초기화하는 방법은?
- 경계를 갱신/업데이트하는 방법은? `left = mid`, `left = mid + 1` and `right = mid`, `right = mid - 1` 4가지 중 적당한 조합을 찾는 방법은?
단순히 '정렬된 배열에서 값 찾기'가 아니라, 더 복잡한 상황에서 이진탐색을 사용할 수 있는데 사람들이 잘못알고 있다.
저는 강력한 이진 탐색 템플릿을 만들었고, 이 템플릿을 약간만 비틀어서 많은 어려운 문제를 해결했습니다.
```python
def binary_search(array) -> int:
    def condition(value) -> bool:
        pass

    left, right = min(search_space), max(search_space) # could be [0, n], [1, n] etc. Depends on problem
    while left < right:
        mid = left + (right - left) // 2
        if condition(mid):
            right = mid
        else:
            left = mid + 1
    return left
```

이 템플릿을 복사하여 붙여넣은 후에 세 부분만 수정하면 되고, 더 이상 코드의 코너 케이스와 버그에 대해 걱정할 필요가 없다는 것입니다 .

- 경계 변수를 올바르게 초기화 `left`하고 검색 공간을 지정합니다. 규칙은 하나뿐입니다. 가능한 모든 요소를 ​​포함하도록`right` 경계를 설정합니다 .
- 반환 값을 결정합니다. `return left` 아니면 `return left - 1`? 기억하세요: while 루프를 종료한 후, `condition`함수를 만족하는 최소 k​는 `left`입니다.
- `condition`을 디자인하세요 . 이것은 가장 어렵고 가장 아름다운 부분입니다. 많은 연습이 필요합니다.

아래에서는 이 강력한 템플릿을 다양한 LeetCode 문제에 적용하는 방법을 보여드리겠습니다.

## 제곱
제곱을 했을 때 입력값보다 크지 않은 가장 작은 수를 찾는 문제이다.
조건은 간단하게 $k^2 > x$ 이고 이때 정답은 $k -1$이다. $right = x$가 아닌 $right = x + 1$로 넣었는데 이는 0, 1에 대한 특이케이스를 처리하기 위함이다.
```python
def mySqrt(x: int) -> int:
    left, right = 0, x + 1
    while left < right:
        mid = left + (right - left) // 2
        if mid * mid > x:
            right = mid
        else:
            left = mid + 1
    return left - 1  # `left` is the minimum k value, `k - 1` is the answer
```

## 포지션 결정
보편적인 이진탐색의 예이다. 수가 들어갈 위치를 찾는 문제이며, `right = len(nums)`인 이유는 넣을 수가 기존의 값보다 모두 크면 배열의 가장 끝에 들어가야하기 때문이다.
```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums)
        while left < right:
            mid = left + (right - left) // 2
            if nums[mid] >= target:
                right = mid
            else:
                left = mid + 1
        return left
```
이러한 경우는 이진탐색을 사용할 수 있다는 것을 한눈에 파악할 수 있다. 하지만 일반적으로 검색공간과 검색타겟을 바로 이용할 수 없는 경우가 대다수이다.
언제 이진탐색을 사용할 수 있을까? 만약 예를 들어 `condition(k) = true`와 `condition(k+1) = true`라는 일련의 단순한 규칙을 발견한다면 이진탐색을 사용할 수 있다.

## D-Day까지 운송하기 위한 패키지 용량
```
Input: weights = [1,2,3,4,5,6,7,8,9,10], D = 5
Output: 15
Explanation: 
A ship capacity of 15 is the minimum to ship all the packages in 5 days like this:
1st day: 1, 2, 3, 4, 5
2nd day: 6, 7
3rd day: 8
4th day: 9
5th day: 10

Note that the cargo must be shipped in the order given, so using a ship of capacity 14 and splitting the packages into parts like (2, 3, 4, 5), (1, 6, 7), (8), (9), (10) is not allowed. 
```

처음에는 weight를 사용해서 접근할 가능성이 크다. 하지만 삽질만 하다가 시간을 버릴 공산이 크다. 하지만 단순하게 생각해보자. 어떤 m만큼의 용량이 D-day까지 짐을 실을 수 있다면, m보다 큰 용량은 다 가능하다는 것이다. => condition(k) = true, condition(k+1) = true가 된다는 것.

condition을 설계해보자. 주어진 capacity를 넣고 D-day안에 옮길 수 있다면 true를 반환, 그렇지 않으면 false를 반환하자.
capacity 경계의 최소는 가장 큰 화물이 된다. 크것보다는 커야 물건을 실을테니까. 경계의 최대는 1번에 다 옮길 수 있는 `sum(weights)`가 될 것이다.
이제 템플릿에 적용하면!
```python
def shipWithinDays(weights: List[int], D: int) -> int:
    def feasible(capacity) -> bool:
        days = 1
        total = 0
        for weight in weights:
            total += weight
            if total > capacity:  # too heavy, wait for the next day
                total = weight
                days += 1
                if days > D:  # cannot ship within D days
                    return False
        return True

    left, right = max(weights), sum(weights)
    while left < right:
        mid = left + (right - left) // 2
        if feasible(mid):
            right = mid
        else:
            left = mid + 1
    return left
```

## 나눈 배열의 가장 큰 합
빈 배열이 아닌 m개로 분할한 각 배열의 합 중 최대값이 가장 작은 것은?
```
Input:
nums = [7,2,5,10,8]
m = 2

Output:
18

Explanation:
There are four ways to split nums into two subarrays. The best way is to split it into [7,2,5] and [10,8], where the largest sum among the two subarrays is only 18.
```

위의 배의 용량과 비슷하게 접근하면 된다. feasible()은 부분배열의 합이 threshold보다 적거나 같으면 true를 반환하고 아니면 false를 반환하도록 한다. 이러면 threshold를 합의 크기로 넣게 되면, 가장 작은 수를 구할 수 있다.
```python
def splitArray(nums: List[int], m: int) -> int:        
    def feasible(threshold) -> bool:
        count = 1
        total = 0
        for num in nums:
            total += num
            if total > threshold:
                total = num
                count += 1
                if count > m:
                    return False
        return True

    left, right = max(nums), sum(nums)
    while left < right:
        mid = left + (right - left) // 2
        if feasible(mid):
            right = mid     
        else:
            left = mid + 1
    return left
```
그럼 `left`가 정말 답인가 의심해보게된다. 생각해보면 우리 검색 스페이스보다 배열에서 만드는 값이 매우 적다는 것을 알 수 있다.
그럼 feasible을 만족하는 최소 k가 있다. 반례를 찾아서 우리가 맞다는 증명을 해보자. 어떤 k에 대해 모든 부분배열이 k보다 작다. 그러면 feasible 함수 내 total변수는 k보다 작을 것이고, feasible(k-1)도 만족할 것이다. 그러나 우리는 k가 최소값이 것을 알고 있다. 따라서 feasible(k-1)은 false를 반환할 것이고, 반례가 되므로 left가 답이 된다는 것을 알게 된다.

## 바나나 먹는 코코

```
Input: piles = [3,6,7,11], H = 8
Output: 4
```

```
Input: piles = [30,11,23,4,20], H = 5
Output: 30
```

```
Input: piles = [30,11,23,4,20], H = 6
Output: 23
```

```python
def minEatingSpeed(piles: List[int], H: int) -> int:
    def feasible(speed) -> bool:
        # return sum(math.ceil(pile / speed) for pile in piles) <= H  # slower        
        return sum((pile - 1) // speed + 1 for pile in piles) <= H  # faster

    left, right = 1, max(piles)
    while left < right:
        mid = left  + (right - left) // 2
        if feasible(mid):
            right = mid
        else:
            left = mid + 1
    return left
```

## 부케를 만들 수 있는 최소일수
```
Input: bloomDay = [1,10,3,10,2], m = 3, k = 1
Output: 3
Explanation: Let's see what happened in the first three days. x means flower bloomed and _ means flower didn't bloom in the garden.
We need 3 bouquets each should contain 1 flower.
After day 1: [x, _, _, _, _]   // we can only make one bouquet.
After day 2: [x, _, _, _, x]   // we can only make two bouquets.
After day 3: [x, _, x, _, x]   // we can make 3 bouquets. The answer is 3.
```

```
Input: bloomDay = [1,10,3,10,2], m = 3, k = 2
Output: -1
Explanation: We need 3 bouquets each has 2 flowers, that means we need 6 flowers. We only have 5 flowers so it is impossible to get the needed bouquets and we return -1.
```

```python
def minDays(bloomDay: List[int], m: int, k: int) -> int:
    def feasible(days) -> bool:
        bonquets, flowers = 0, 0
        for bloom in bloomDay:
            if bloom > days:
                flowers = 0
            else:
                bonquets += (flowers + 1) // k
                flowers = (flowers + 1) % k
        return bonquets >= m

    if len(bloomDay) < m * k:
        return -1
    left, right = 1, max(bloomDay)
    while left < right:
        mid = left + (right - left) // 2
        if feasible(mid):
            right = mid
        else:
            left = mid + 1
    return left
```

## multiplication table에서 k번째 가장 작은 수
```
Input: m = 3, n = 3, k = 5
Output: 3
Explanation: 
The Multiplication Table:
1	2	3
2	4	6
3	6	9

The 5-th smallest number is 3 (1, 2, 2, 3, 3).
```
이렇게만 보면 우리는 힙을 적용하는게 좋아보인다. 최소heap으로 정리한 다음 k번만 pop을 하면 그 수가 바로 k번째 수가 될 테니까. 하지만 문제는 m\*n으로 테이블이 주어지기 때문에 O(mn)이 되어버려서 시간이 많이 소비된다.
하지만 enough함수를 만족하는 최소 num을 구한다면 그게 우리의 답이 될 것이다. 단조로움을 찾는 것이 핵심이다.
enough함수를 설계해보자. row를 잘 살펴보면 배수로 증가하는 것을 확인할 수 있다. ex) 3,6,9,... 따라서, 우리는 num을 확인할 때 열에 따라 확인할 수 있다.
경계의 최소를 1\*1로 설정하고 최대를 m\*n으로 설정한다. 테이블에서 만들어질 수 있는 수 중 가장 큰 수가 mn이다. 경계 내의 어떤 수 num을 enough로 확인하면 num보다 작은 수의 개수를 세면 된다. num을 m으로 나눈 몫은 m열에서 num보다 작은 수의 최대 개수가 되고 열은 n이 최대이므로 둘 중 작은 수를 구하면 num보다 작은 수의 갯수를 구할 수 있게 되는것이다.

```python
def findKthNumber(m: int, n: int, k: int) -> int:
    def enough(num) -> bool:
        count = 0
        for val in range(1, m + 1):  # count row by row
            add = min(num // val, n)
            if add == 0:  # early exit
                break
            count += add
        return count >= k                

    left, right = 1, n * m
    while left < right:
        mid = left + (right - left) // 2
        if enough(mid):
            right = mid
        else:
            left = mid + 1
    return left 
```

이후에는 적용과 증명의 연속으로 다소 비슷함.

