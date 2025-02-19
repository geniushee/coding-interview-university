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
