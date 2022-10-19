# 정렬 알고리즘

## 정렬이란? 
- 어떤 데이터들이 주어졌을때 이를 정해진 순서대로 나열하는 문제이다.
- 실제 컴퓨터 분야에서 사용하는 데이터의 경우 숫자, 어휘순으로 정렬한 다음 사용해야하는 경우가 항상 발생하기 때문에 이를 얼마나 효과적으로 해결하느냐가 중요하다.
- 데이터가 정렬되어있다면 **이진탐색** 이라는 강력한 알고리즘을 사용할 수 있다. 
- 코테를 통과해야하기때문 .....



# 시간복잡도가 O(n²)인 정렬

## 버블정렬 (Bubble Sorting)

<img width="494" alt="스크린샷 2022-10-19 오후 9 46 44" src="https://user-images.githubusercontent.com/69416561/196694841-b5d08ee8-8a4f-4840-8886-ed84a422d4f5.png">


- 가장 원시적인 형태의 정렬 알고리즘
- 배열내 모든 원소에 대해 인접한 원소끼리 비교하며 인덱스 i에 대해 i번째 원소가 i+1번째 원소보다 클경우 두 원소를 스왑하며 정렬한다. 
- **자료에 중복이 있는 경우엔 스왑하지 않는다.(stable 정렬)**
- 배열의 크기가 n일 경우 n-1번째, n번째 요소까지 모두 비교한다.
- 이런 작동 방식 때문에 자료의 개수가 많아질수록 성능이 매우 떨어진다.
- Worst case의 시간 복잡도는 O(n²), Best Case의 시간 복잡도는 O(n)이다.  
- 너무 비효율적이라 웬만하면 안쓰는 알고리즘이다. 이런게 있다는 정도만 알아두면 좋을 것 같다.


- 버블 정렬을 1회씩 수행할때마다 정렬할 원소가 하나씩 줄어드는것을 고려하여 알고리즘으로 구하면 다음과같다.
```js
  const bubbleSort = (arr) => {
    for(let i = 0; i<arr.length; i++){//순차적으로 비교하기 위한 반복문
      for(let j = 0; j < arr.length - (i+1); j++){// 끝까지 돌았을때 다시 처음부터 비교하기 위한 반복문
        if(arr[j]>arr[j+1]){// 두수를 비교해서 앞 수가 뒷 수보다 크면
          [arr[j], arr[j+1]]=[arr[j+1], arr[j]]// 두 수를 서로 바꾼다
        }
      }
    )
    
  return arr;
  }
```

## 선택 정렬(Selection Sort)

![스크린샷 2022-10-19 오후 7 20 53](https://user-images.githubusercontent.com/69416561/196695047-190eeacb-cc6e-4914-ad0c-83bc94652799.png)


- 버블 정렬이 비교하고 바로 바꿔 넣는 걸 반복한다면 이쪽은 배열을 처음부터 훑어서 가장 작은 수를 제일 앞에 가져다 놓는다. 
- 버블정렬과 비교방식은 동일하지만 데이터 위치는 n번째 회전이 끌날 때마다 n번째 데이터의 위치가 정해진다.
- Best, Worst Case **모두 시간 복잡도가 O(n²)**가 걸리므로 성능이 매우 떨어진다. 
- 버블 정렬만큼 간단하고 성능도 좋지 않아 잘 안쓴다. **(다만 30이하의 작은 수에서는 효과적일 수 있다.)**

```js
function selectionSort (array) {
  for (let i = 0; i < array.length; i++) {//처음부터 훑으면서
    let minIndex = i; 
    for (let j = i + 1; j < array.length; j++) {// 최솟값의 위치를 찾음
      if (array[minIndex] > array[j]) {
        minIndex = j;
      }
    }
    if (minIndex !== i) { //최소값이 제자리에 없다면
      let swap = array[minIndex];//최솟값을 저장
      array[minIndex] = array[i]; 
      array[i] = swap; // 최솟값을 제일 앞으로보냄
    }
  }
  return array;
}
console.log(selectionSort([5, 4, 3, 2, 1]));
```



## 삽입정렬(Insertion Sorting)
![스크린샷 2022-10-19 오후 7 33 40](https://user-images.githubusercontent.com/69416561/196695212-7ede64ca-34ed-41a7-869b-c19c1f56f933.png)


- 정렬을 진행할 원소의 인덱스보다 낮은 곳에 있는 원소들을 탐색하며 알맞은 위치에 삽입해주는 정렬 알고리즘이다.
- 첫번째 원소는 자신보다 낮은 인덱스의 원소가 없으므로 **두번째 인덱스의 원소부터 탐색**한다. 
- 알고리즘이 동작하는 동안 계속해서 정렬이 진행되므로 **반드시 맨 왼쪽 인덱스까지 탐색하지 않아도 된다는 장점**이 있다. 
- 중복된 데이터의 경우 정렬을 실행하지 않는다.
- Best Case의 경우 시간복잡도는 O(n), Worst Case의 경우는 O(n²)이다.

```js
function InsertionSort(array) {
  let i = 1, j, temp;
  for (i; i < array.length; i++) {
    temp = array[i]; // 새로운 숫자를 선택함
    for (j = i - 1; j >= 0 && temp < array[j]; j--) { // 선택한 숫자를 이미 정렬된 숫자들과 비교하며 넣을 위치를 찾는 과정, 선택한 숫자가 정렬된 숫자보다 작으면
      array[j + 1] = array[j]; // 한 칸씩 뒤로 밀어낸다
    }
    array[j + 1] = temp; // 마지막 빈 칸에 선택한 숫자를 넣어준다.
  }
  return array;
};
```


# 시간복잡도가 O(nlog n)인 정렬
## 병합정렬/ 합병정렬(머지소트,Merge sort)

 ![image](https://w.namu.la/s/1850a8d6f7f4bbc1343082a38bd4a3fb8170dfbbc1af00ae1923cfb86b5412314824821d60b902216b3eff6830527194d0fae3222ae4843b68665848713b2ce95fdffb41629356ac1b0268848f92ee6aedb9e4392d8d2354b3751261b6a220be00a32807da16ec2401c57f0d62d0162b)
 
 ![스크린샷 2022-10-19 오후 7 36 33](https://user-images.githubusercontent.com/69416561/196695308-5d9056b0-346b-45ba-8ba0-31d9fcc60107.png)


- 삽입정렬보단 복잡하지만, 성능이 훨씬 좋은 정렬 방식이다.
- 원소 개수가 1 또는 0이 될 때까지 두 부분으로 쪼개고 쪼개서 자른 순서의 역순으로 크기를 비교해 병합해 나간다.병합된 부분 안은 이미 정렬되어 있으므로 전부 비교하지 않아도 제자리를 찾을 수 있다. 
- 중복된 값이 있다면 순서가 바뀌지 않는다.
- Divide and Conquer, **문제를 잘개 쪼개어 해결하는 분할 정복 개념이 적용**된 대표적 알고리즘이다. 
- 병합정렬은 최선, 최악의 모든 경우에도 O(nlogn)의 시간 복잡도를 갖기 때문에 **데이터 분포의 영향을 덜 받는다. 즉 어떤 경우에도 좋은 성능을 보장받을 수 있다.**
- **별도의 메모리 공간이 필요**하여 정렬할 데이터의 양이 많을 경우 그만큼 이동 횟수가 많아져 시간적인 낭비도 많아지게 된다. 

```js
// 재귀를하는 부분(merge Sort), 앞의 두수와 비교하는 부분(merge)의 두 함수로 이루어짐
var mergeSort = function(array) {
  if (array.length < 2) return array; // 원소가 하나일 때는 그대로 내보냅니다.
  var pivot = Math.floor(array.length / 2); // 대략 반으로 쪼개는 코드
  var left = array.slice(0, pivot); // 쪼갠 왼쪽
  var right = array.slice(pivot, array.length); // 쪼갠 오른쪽
  return merge(mergeSort(left), mergeSort(right)); // 재귀적으로 쪼개고 합칩니다.
}
function merge(left, right) {
  var result = [];
  while (left.length && right.length) {
    if (left[0] <= right[0]) { // 두 배열의 첫 원소를 비교하여
      result.push(left.shift()); // 더 작은 수를 결과에 넣어줍니다.
    } else {
      result.push(right.shift()); // 오른쪽도 마찬가지
    }
  }
  while (left.length) result.push(left.shift()); // 어느 한 배열이 더 많이 남았다면 나머지를 다 넣어줍니다.
  while (right.length) result.push(right.shift()); // 오른쪽도 마찬가지
  return result;
};

mergeSort([5,2,4,7,6,1,3,8]); // [1, 2, 3, 4, 5, 6, 7, 8]

```



## 퀵 정렬(Quick Sort)


![스크린샷 2022-10-19 오후 8 59 21](https://user-images.githubusercontent.com/69416561/196695527-cb318457-396e-4781-8598-2ea4a697e727.png)


- 위 알고리즘들 보다 복잡하지만 제일 효율적인 알고리즘이다. **병합 정렬보다 '평균적으로' 두 배 빠르다.**
- 피벗(중심축)인 인덱스를 정하고, 이 피벗보다 작은 값들은 왼쪽으로, 큰 값들은 오른쪽으로 보내는 것이다. 
- 이렇게 피벗을 정해서 왼쪽 오른쪽으로 나누고 다시금 왼쪽 오른쪽에 대해 재귀적으로 pivot을 정해서 왼쪽 오른쪽을 나누고... 이 과정을 반복하면 정렬이 완성된다.
- 피벗을 정하는 방법을 '파티션' 이라고 하고, **보통 양끝값을 피벗으로 정하거나 중심값을 피벗으로 정하는것이 일반적이다.**
- 병합 정렬과 똑같은 분할 정복 알고리즘을 사용한다.
- **중복되는 값이 있을 경우 순서가 바뀔 수 있다.**

### 구체적인 정렬 방식
- 1단계) 분할 : 입력된 배열을 피벗을 기준으로 2개의 부분 배열로 분할한다.
- 2단계) 정복 : 부분 배열을 정렬한다. 부분 배열의 크기가 충분히 작지 않으면 재귀를 이용해서 다시 분할 정복 방식을 이용한다. 
- 3단계) 결합 : 순환 호출이 한 번 진행될 때마다 최소한 하나의 원소는 최종적으로 위치가 정해지므로, 이 알고리즘은 반드시 끝난다는 것을 보장할 수 있다. 

```js

//// 첫번째 방식

const swap = function (array, front, back) {
	const tmp = array[front];
	array[front] = array[back];
	array[back] = tmp;
}


//피벗을 잡는 방식을'파티션'이라고 하고, 배열의 양끝값을 피벗으로 잡는 방식을 로무토 파티션이라고 한다.
const lomutoPartition = function (array, start, end) {
	const pivotValue = array[end]; // lomuto's partition 은 항상 맨끝을 pivot으로 정한다.
	let pivotIndex = start;

	for (let index = start; index < end; index++) {
		if (array[index] < pivotValue) { // pivotValue보다 작으면 
			swap(array, index, pivotIndex);	// pivotIndex 와 swap 하고
			pivotIndex += 1; // pivotIndex 증가
		}
	}

	swap(array, pivotIndex, end); // pivotValue를 중간에 오게하기 위해서
	return pivotIndex;
}

const quickSortWithLomuto = function (array, start = 0, end = array.length - 1) { // 초기값: 배열의 시작과 끝
	if (start >= end) return; // ending condition	

	let pivotIndex = lomutoPartition(array, start, end);
	quickSortWithLomuto(array, start, pivotIndex - 1); // divide and conquer: left
	quickSortWithLomuto(array, pivotIndex + 1, end); // right
	
	return array;
}

const arr = [4, -1, 0, -8, 0, 8, 91, 2, 3, 4, 98, 911, 21];
const result1 = quickSortWithLomuto(arr);
console.log(result1);

// 배열의 중간 인덱스 값을 피벗으로 잡는 방식을 호어 파티션이라고 부른다.

const swap = function (array, front, back) {
	const tmp = array[front];
	array[front] = array[back];
	array[back] = tmp;
}

const hoarePartition = function (array, start, end) {
	const pivotValue = array[ Math.floor((start + end) / 2) ]; // 물리적으로 중간을 pivotValue로 정한다.

	while (start <= end) { // 교차 지점이 오기 전까지
		while (array[start] < pivotValue) start = start + 1; // array의 왼쪽에서 pivotValue보다 크거나 같은 값을  찾는다.
		while (array[end] > pivotValue) end = end - 1; // array의 오른쪽에서 pivotValue보다 작거나 같은  값을 찾는다.

		if (start <= end) { // 교차 되기 전이라면
			swap(array, start, end); // pivotValue 보다 크거나 같은값과, 작거나 같은값을 swap 한다.
			start = start + 1; // 그 다음 search를 위해서 start 1증가
			end = end - 1; // end 1감소
		}
	}

	return start; // 교차되고 난후 start를 그 다음 border index로 리턴한다. 
}


const quickSortWithHoare = function (array, start = 0, end = array.length - 1) { // 초기값: 배열의 시작과 끝
	if (start >= end) return; // ending condition 

	let borderIndex = hoarePartition(array, start, end);
	quickSortWithHoare(array, start, borderIndex - 1); // border의 왼쪽
	quickSortWithHoare(array, borderIndex, end); // border의 오른쪽

	return array;
}
const arr = [4, -1, 0, -8, 0, 8, 91, 2, 3, 4, 98, 911, 21];
const result2 = quickSortWithHoare(arr);
console.log(result2)

//=====================
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
- **분할정복 알고리즘**에 속한다.
- 둘 다 탐색할 배열의 크기를 쪼개서 **재귀적으로 구현**한다는 특징이 있다. 
#### 차이점 
- 퀵정렬의 속도가 병합정렬보다 평균적으로 2배 정도 빠르다.
- 병합정렬은 배열을 분할하는 방식이 절반으로 쪼개는 것 한가지이고, 퀵정렬은 피벗을 정하는방식(파티션)에 따라 수많은 방식이 존재한다.(보통은 무작위or중간값을 피벗으로 잡는 방식을 선택) 
- 병합정렬은 중복데이터의 순서가 바뀌지않는 stable한 정렬이고, 퀵정렬은 '일반적으로는' unstable한 정렬이다.(파티션에따라 stable하게 구현가능)
- '보통' 퀵 정렬은 병합정렬과 달리 다른 메모리 공간을 사용하지 않는다. 오직 재귀 콜 스택을 위한 메모리만 사용된다. 


## 참고자료

- [제로초 블로그 - 알고리즘 카테고리](https://www.zerocho.com/category/Algorithm?page=3)
- [자바스크립트로 병합 정렬 구현하기](https://jun-choi-4928.medium.com/javascript%EB%A1%9C-merge-sort-%EB%B3%91%ED%95%A9%EC%A0%95%EB%A0%AC-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0-c13c3eee6570)
- [자바스크립트로 퀵 정렬 구현하기](https://jun-choi-4928.medium.com/javascript%EB%A1%9C-quick-sort-%ED%80%B5-%EC%A0%95%EB%A0%AC-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0-76bf539abc0d)
- [프로그래머스 정렬 고득점Kit](https://school.programmers.co.kr/learn/courses/30/parts/12198)


