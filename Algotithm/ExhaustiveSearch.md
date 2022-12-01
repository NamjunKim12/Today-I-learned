# 완전탐색 (브루트 포스)

## 정의

완전탐색 (Brute Force)는 **무식하게 가능한 모든 경우의 수를 탐색**하면서 요구조건에 충족되는 결과만을 가져오는 방법이다.
<br><br>
말 그대로 **노가다**
<br><br>

## 고려해야할 것

무턱대고 쉬워보여서 완전탐색 기법을 사용한다면 원하는 결과를 얻을 수 있느나, 시간 초과가 날 확률이 매우 높다.
<br><br>

1. 해결하고자 하는 문제의 가능한 경우의 수를 대략적으로 계산한다.
2. 가능한 모든 방법을 다 고려한다.
3. 실제 답을 구할 수 있는지 적용한다.

## 가능한 모든 방법을 고려하는 방법

### 1. Brute Force 기법

반복, 조건문을 통해 가능한 모든 방법을 무식하게 찾는 기법이다.
<br><br>

자물쇠 암호 찾을 때를 생각하면 좋을 것 같다.
<br><br>

해당 기법을 사용해서 푸는 문제는 거의 나오지 않는다.
<br><br>

### 2. 순열

n개에서 r개를 선택했을 때, 뽑은 r개의 순서를 고려하는 것을 순열이라고 한다.
<br><br>

JavaScript에서 순열을 구현할 때에는 재귀가 사용된다.

```javascript
function Permutation(arr, selectNum) {
  const result = [];

  // 1개를 선택해야할 때, arr의 각 원소를 배열로 감싸서 return
  if (selecNum === 1) {
    return arr.map((item) => [item]);
  }

  arr.forEach((item, index, origin) => {
    // 해당 item을 제외한 새로운 배열 생성
    const rest = [...origin.slice(0, index), ...origin.slice(index + 1)];
    // 재귀함수를 호출하여 나머지에 대해서 순열 구하기
    const permutations = Permutation(rest, selectNumber - 1);
    //
    const attached = permutations.map((item) => [fixed, ...item]);
    //
    result.push(...attached);
  });
  return result;
}
```

### 3. 재귀

반복문을 사용하여 길어지고 복잡한 코드를 재귀 함수를 통하여 간결하게 할 수 있다.
<br><br>

주의할 점은, 종료 조건을 제대로 명시해줘야 한다는 점이다.
<br><br>

```javascript
// 팩토리얼 예시
function factorial(n) {
  if (n <= 1) {
    return n;
  }
  return n * factorial(n - 1);
}
```

### 4. BFS, DFS

BFS, DFS는 비선형 자료구조를 완전탐색할 때 사용된다.
<br><br>

단순 길찾기 문제에서는 BFS, DFS로 충분하나, 장애물이 생기는 등 추가적 연산이 필요할 때 완전탐색 기법을 섞기도 한다.
<br><br>

추후에 진행되니 따로 언급하지는 않겠다.

## 완전탐색 예제

```javascript
// 모의고사 예제
function solution(answers) {
  let answer = [];
  let check1 = [1, 2, 3, 4, 5];
  let check2 = [2, 1, 2, 3, 2, 4, 2, 5];
  let check3 = [3, 3, 1, 1, 2, 2, 4, 4, 5, 5];
  let num1 = answers.filter(
    (item, index) => item === check1[index % check1.length]
  ).length;
  let num2 = answers.filter(
    (item, index) => item === check2[index % check2.length]
  ).length;
  let num3 = answers.filter(
    (item, index) => item === check3[index % check3.length]
  ).length;
  let max = Math.max(num1, num2, num3);
  if (num1 === max) {
    answer.push(1);
  }
  if (num2 === max) {
    answer.push(2);
  }
  if (num3 === max) {
    answer.push(3);
  }
  return answer;
}
```
