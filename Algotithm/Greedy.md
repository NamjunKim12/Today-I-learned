# 🤑 그리디란?

- greedy; 욕심쟁이 알고리즘. 말그대로 문제를 단순 무식하게, 탐욕적으로 **현재 상황에서 지금 당장 좋은 것만 고르는** 알고리즘
- 그렇다고 그게 최적의 해를 보장하는 것은 아님. 따라서 그리디 알고리즘으로 풀 수 있는 문제인지 추론할 수 있는 능력 필요.
- 팀노트가 필요한 정렬, 최단 경로 등의 문제와 달리 때에 맞는 문제 풀이 방식이 있다.
- 대부분 정렬 알고리즘과 함께 쓰인다.
  <br>

## 문제풀이 TIP

- 문제를 만났을 때 유형 파악이 안된다 -> 그리디를 의심해보자!
- 그래도 안풀린다면 다이나믹이나 그래프를 써서 풀자.
  <br>

## 그리디 알고리즘의 정당성

- 탐욕적 선택 속성(greedy choice property)

  > 탐욕적인 선택이 언제나 최적해를 보장해야한다.

- 최적 부분 구조(optimal substructure)

  > 부분 최적해들이 모여 전체 최적해를 이룬다.

**노드 값의 합을 최대로 만들고 싶다면?**<br>
<img src="./문제1.png"><br>

**매순간 가장 큰 값을 고르면 된다.**<br><br>
<img src="./문제1-1.png">

<br>

## [예제1] 거스름돈 문제

> 당신은 음식점의 계산을 도와주는 점원이다. 카운터에는 거스름돈으로 사용할 500원,100원,50원,10원짜리 동전이 무한히 존재한다고 가정한다. 손님에게 거슬러 줘야 할 돈이 N원일 때 거슬러줘야할 동전의 최소 개수를 구하라. 단 N은 항상 10의 배수이다.

> 💡 문제풀이 핵심: 가장 큰 화폐 단위부터 거슬러 주자! 큰 단위가 항상 작은 단위의 배수 형태이기 때문에 큰 단위부터 거슬러주어야 최적의 해를 찾을 수 있다.

```js
function change(n) {
  let answer = 0;
  const coins = [500, 100, 50, 10];

  coins.forEach((coin) => {
    answer += Math.floor(n / coin);
    n -= coin * Math.floor(n / coin);
  });

  return answer;
}
```

- 시간복잡도: O(k), k는 동전의 종류
  <br>

## [예제 2] 큰 수의 법칙

> 큰 수의 법칙은 다양한 수로 이루어진 배열이 있을 때 주어진 수들을 M번 더하여 가장 큰 수를 만드는 법칙이다. 단, 배열의 특정한 인덱스(번호)에 해당하는 수가 연속해서 K번을 초과하여 더해질 수 없는 것이 이 법칙의 특징이다.

<!-- 예를 들어 순서대로 2, 4, 5, 6으로 이루어진 배열이 있을 때, M이 8이고 K가 3이라면 이 경우 특정한 인덱스의 수가 연속해서 세 번까지만 더해질 수 있으므로 큰 수의 법칙에 따른 결과는 6 + 6 + 6 + 5 + 6 + 6 + 6 + 5 = 46이 된다. 단, 서로 다른 인덱스에 해당하는 수가 같은 경우에도 서로 다른 것으로 간주한다. 배열의 크기 N, 숫자가 더해지는 횟수 M, 그리고 K가 주어질 때 동빈이의 큰 수의 법칙에 따른 결과를 출력하시오. -->

> 💡 문풀 핵심: 결국 쓰이는 건 가장큰 두 수. 가장 큰수를 K번 더하고 두번째로 큰 수를 한 번 더하기를 반복한다.

```js
function(n, m, k, list) {
    let answer = 0;

    list.sort((a, b) => a - b);
    const first = list[n - 1]; // 가장 큰 수
    const second = list[n - 2]; // 두번째로 큰 수

    // 가장 큰 수가 더해지는 횟수
    let count = Math.floor(m / (k + 1)) * k;
    count += m % (k + 1);

  answer += count * first;
  answer += (m - count) * second;

  return answer;
}
```

<img style="padding:10px" src="./문제2.png"></img>
<br>

## [예제 3] 1이 될 때까지

> 어떤수 N이 1이 될 때까지 다음의 두 과정 중 하나를 반복적으로 선택하여 수행하려고한다. 단, 두번째 연산은 N이 K로 나누어떨어질 때만 선택할 수 있다.
>
> 1. N에서 1을 뺀다.
> 2. N을 K로 나눈다.

<!-- 예를 들어 N = 17, K = 4일 경우
1) 17 - 1 = 16

2) 16 // 4 = 4

3) 4 // 4 = 1
전체 과정을 실행한 횟수는 3 -->

> 💡 문풀 핵심: N이 K의 배수가 될 때까지 1씩 뺀다. 그리고 N을 K로 나눈다.

<br>

## [예제 4] 프로그래머스 - 체육복

> 점심시간에 도둑이 들어, 일부 학생이 체육복을 도난당했습니다. 다행히 여벌 체육복이 있는 학생이 이들에게 체육복을 빌려주려 합니다. 학생들의 번호는 체격 순으로 매겨져 있어, 바로 앞번호의 학생이나 바로 뒷번호의 학생에게만 체육복을 빌려줄 수 있습니다. 예를 들어, 4번 학생은 3번 학생이나 5번 학생에게만 체육복을 빌려줄 수 있습니다. 체육복이 없으면 수업을 들을 수 없기 때문에 체육복을 적절히 빌려 최대한 많은 학생이 체육수업을 들어야 합니다.
> 전체 학생의 수 n, 체육복을 도난당한 학생들의 번호가 담긴 배열 lost, 여벌의 체육복을 가져온 학생들의 번호가 담긴 배열 reserve가 매개변수로 주어질 때, 체육수업을 들을 수 있는 학생의 최댓값을 return 하도록 solution 함수를 작성해주세요.

```js
function solution(n, lost, reserve) {
  var answer = [];

  // lost와 reserve의 중복 먼저 제거
  for (let i = 1; i < n + 1; i++) {
    if (lost.includes(i) && reserve.includes(i)) {
      lost = lost.filter((std) => std !== i);
      reserve = reserve.filter((std) => std !== i);
      answer.push(i);
    }
  }

  for (let i = 1; i < n + 1; i++) {
    if (lost.includes(i)) {
      if (reserve.includes(i - 1)) {
        reserve = reserve.filter((item) => item !== i - 1);
        answer.push(i);
      } else if (reserve.includes(i + 1)) {
        reserve = reserve.filter((item) => item !== i + 1);
        answer.push(i);
      }
    } else if (!answer.includes(i)) {
      answer.push(i);
    }
  }

  return answer.length;
}
```
