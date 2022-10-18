# 정렬 알고리즘





# 시간복잡도가 O(n²)인 정렬

## 버블정렬 (Bubble Sorting)

 ![image](https://user-images.githubusercontent.com/69416561/195910781-1adbdd2a-1eb6-4ac4-b094-2ebdeff29ed3.png)


- 가장 원시적인 형태의 정렬 알고리즘
- 배열내 모든 원소에 대해 인접한 원소끼리 비교하며 인덱스 i에 대해 i번째 원소가 i+1번째 원소보다 클경우 두 요소를 스왑하며 정렬한다. 
- 배열의 크기가 n일 경우 n-1번째, n번째 요소까지 모두 비교한다.
- 이런 작동 방식 때문에 자료의 개수가 많아질수록 성능이 매우 떨어진다.
- Worst case의 시간 복잡도는 O(n²), Best Case의 시간 복잡도는 O(n)이다.  
- 너무 비효율적이라 웬만하면 안쓰는 알고리즘이다. 이런게 있다는 정도만 알아두면 좋을 것 같다.


- 버블 정렬을 1회씩 수행할때마다 정렬할 원소가 하나씩 줄어드는것을 고려하여 알고리즘으로 구하면 다음과같다.
```js
  const bubbleSort = (arr) => {
    for(let i = 0; i<arr.length; i++){
      for(let j = 0; j < arr.length - (i+1); j++){
        if(arr[j]>arr[j+1]){
          [arr[j], arr[j+1]]=[arr[j+1], arr[j]]
        }
      }
    )
    
  return arr;
  }
```


## 삽입정렬(Insertion Sorting)

 ![image](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/insertionsort.png)

- 정렬을 진행할 원소의 인덱스보다 낮은 곳에 있는 원소들을 탐색하며 알맞은 위치에 삽입해주는 정렬 알고리즘이다.
- 첫번째 원소는 자신보다 낮은 인덱스의 원소가 없으므로 두번째 인덱스의 원소부터 탐색한다. 
- 알고리즘이 동작하는 동안 계속해서 정렬이 진행되므로 반드시 맨 왼쪽 인덱스까지 탐색하지 않아도 된다는 장점이 있다. 
- 중복된 데이터의 경우 정렬을 실행하지 않는다.
- Best Case의 경우 시간복잡도는 O(n), Worst Case의 경우는 O(n²)이다.

```js
function insertionSort (array) {
  for (let i = 1; i < array.length; i++) {
    let cur = array[i];
    let left = i - 1;

    while (left >= 0 && array[left] > cur) {
      array[left + 1] = array[left];
      array[left] = cur;
      cur = array[left];
      left--;
    }
  }
  return array;
}
```

## 선택 정렬

- 버블 정렬이 비교하고 바로 바꿔 넣는 걸 반복한다면 이쪽은 일단 1번째부터 끝까지 훑어서 가장 작은 게 1번째, 2번째부터 끝까지 훑어서 가장 작은 게 2번째……해서 (n-1)번 반복한다.
- 버블정렬과 비교방식은 동일하지만 데이터 위치는 n번째 회전이 끌날 때마다 n번째 데이터의 위치가 정해진다.
- Best, Worst Case 모두 시간 복잡도가 O(n²)가 걸리므로 성능이 매우 떨어진다. 

```js
function selectionSort (array) {
  for (let i = 0; i < array.length; i++) {
    let minIndex = i;
    for (let j = i + 1; j < array.length; j++) {
      if (array[minIndex] > array[j]) {
        minIndex = j;
      }
    }
    if (minIndex !== i) {
      let swap = array[minIndex];
      array[minIndex] = array[i];
      array[i] = swap;
    }
    console.log(`${i}회전: ${array}`);
  }
  return array;
}
console.log(selectionSort([5, 4, 3, 2, 1]));
```

# 시간복잡도가 O(nlog n)인 정렬
## 병합정렬/ 합병정렬(머지소트,Merge sort)

 ![image](https://w.namu.la/s/1850a8d6f7f4bbc1343082a38bd4a3fb8170dfbbc1af00ae1923cfb86b5412314824821d60b902216b3eff6830527194d0fae3222ae4843b68665848713b2ce95fdffb41629356ac1b0268848f92ee6aedb9e4392d8d2354b3751261b6a220be00a32807da16ec2401c57f0d62d0162b)

- 원소 개수가 1 또는 0이 될 때까지 두 부분으로 쪼개고 쪼개서 자른 순서의 역순으로 크기를 비교해 병합해 나간다.병합된 부분 안은 이미 정렬되어 있으므로 전부 비교하지 않아도 제자리를 찾을 수 있다. 
- Divide and Conquer, 즉 분할 정복 개념이 적용된 대표적 알고리즘이다. 
- 병합정렬은 최선, 최악의 모든 경우에도 O(nlogn)의 시간 복잡도를 갖기 때문에 데이터 분포의 영향을 덜 받는다. 즉 어떤 경우에도 좋은 성능을 보장받을 수 있다.
- 별도의 메모리 공간이 필요하여 정렬할 데이터의 양이 많을 경우 ㄱ만큼 이동 횟수가 많아져 시간적인 낭비도 많아지게 된다. 


- 자바스크립트로 머지소트를 구현하기 위해선 두가지 함수가 필요하다. 이미 정렬된 배열을 인자로 받아 합치는 함수와, 배열을 반으로 쪼개서 합치는 함수에 인자를 넘겨주는 함수로 구현한다. 

```js
const merge = function (left, right) { // 정렬된 왼쪽과 오른쪽 배열을 받아서 하나로 합치는 순수한 함수
	// left, right already sorted
	const result = [];
	while (left.length !== 0 && right.length !== 0) {
		left[0] <= right[0] ? result.push(left.shift()) : result.push(right.shift());	
	}

	return [...result, ...left, ...right]; // 아래 세줄과 같은 역할을 하는 코드
    // if(left.length === 0) results.push(...right);
    // if(right.length === 0) results.push(...left);
    // return results;
}

const mergeSort = function (array) {
	// ending condition: length === 1 인 배열이 들어올 때, 정렬이 끝난 것. 
	if (array.length === 1) return array;

	// 2로 나누고 내림을 해야
	// length 가 2일 때도 안전하게 배열을 slice 할 수 있다.
	const middleIndex = Math.floor(array.length / 2); 
	const left = array.slice(0, middleIndex);
	const right = array.slice(middleIndex);

	// 재귀로 계속해서 반으로 나누면서 length 가 1이 될때까지 쪼개고, 
	// 거꾸로 올라오면서 순수한 함수인 merge에 인자로 넣어서 다시 병합되어서 최종값을 리턴한다.
	return merge(mergeSort(left), mergeSort(right));
}


const arr = [4, -1, 0, -8, 0, 8, 91, 2, 3, 4, 98, 911, 21];

const result = mergeSort(arr);
console.log(result);

```



## 퀵 정렬(Quick Sort)
![Image](https://mblogthumb-phinf.pstatic.net/MjAxNjExMjVfMTM0/MDAxNDgwMDM1Njc3MDc3.-BzXnvTma6VWXgVrdKk9drbNVyeAjYpzM8LWREz2eTgg.m89qmJhFXGrEN991hlVuSdpaPbTauFlyF-boPDafarUg.JPEG.occidere/%25EC%25A4%2591%25EA%25B0%2584%25EA%25B0%2592%25ED%2580%25B5%25EC%25A0%2595%25EB%25A0%25AC.jpg?type=w800)

- 피벗(중심축)을 정하고, 중심 축보다 작은 값들은 왼쪽으로 큰 값들은 오른쪽으로 보내는 것이다. 
- 이렇게 피벗을 정해서 왼쪽 오른쪽으로 나누고 다시금 왼쪽 오른쪽에 대해 재귀적으로 pivot을 정해서 왼쪽 오른쪽을 나누고... 이 과정을 반복하면 정렬이 완성된다.

### 구체적인 정렬 방식
- 1단계) 분할 : 입력된 배열을 피벗을 기준으로 2개의 부분 배열로 분할한다.
- 2단계) 정복 : 부분 배열을 정렬한다. 부분 배열의 크기가 충분히 작지 않으면 재귀를 이용해서 다시 분할 정복 방식을 이용한다. 
- 3단계) 결합 : 순환 호출이 한 번 진행될 때마다 최소한 하나의 원소는 최종적으로 위치가 정해지므로, 이 알고리즘은 반드시 끝난다는 것을 보장할 수 있다. 

```js

// 간편하나 메모리 공간을 많이 차지하는 방식
const quickSort = function (arr) {
  if (arr.length <= 1) return arr; // 1. 먼저, 배열의 길이가 1과 같거나 작게 될 경우 배열을 바로 리턴한다.

  const pivot = arr[0]; //2. 리스트 가운데 하나의 원소를 고르고 pivot 이라고 한다. : 첫번째 인덱스를 pivot으로 정했다.
  const left = [];
  const right = [];

  for (let i = 1; i < arr.length; i++) {
    if (arr[i] <= pivot) left.push(arr[i]);
    else right.push(arr[i]); //3. 배열 안에서 pivot을 제외한 모든 요소를 탐색해서 pivot보다 작으면 left, 크면 right라는 배열에 넣는다. 
  }

  const lSorted = quickSort(left); //4. left와 right에 값이 모두 넣어졌으면 각각의 배열에 대해 quickSort를 재귀적으로 다시 호출한다.
  const rSorted = quickSort(right);
  return [...lSorted, pivot, ...rSorted]; // 5. left, pivot, right를 합쳐서 리턴한다.

};


```

### 퀵소트와 머지소트 비교
#### 공통점
- 분할정복 알고리즘에 속한다.
- 둘 다 탐색할 배열의 크기를 쪼개서 재귀적으로 이용한다는 특징이 있다. 
#### 차이점 
- 병합정렬은 배열을 분할하는 방식이 절반으로 쪼개는 것 한가지이고, 퀵정렬은 피벗을 정하는방식(파티션)에 따라 수많은 방식이 존재한다.(보통은 무작위or중간값을 피벗으로 잡는 방식을 선택) 
- 병합정렬은 중복데이터의 순서가 바뀌지않는 stable한 정렬이고, 퀵정렬은 '일반적으로는' unstable한 정렬이다.(파티션에따라 stable하게 구현가능)
- 퀵 정렬은 병합정렬과 달리 다른 메모리 공간을 사용하지 않는데. 오직 재귀 콜 스택을 위한 메모리만 사용된다. 

