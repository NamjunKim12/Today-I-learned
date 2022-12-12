# 동적계획법(Dynamic Programming)

- 큰 문제를 작은 문제로 나눈 후 이를 결합하여 답을 노출해 내는 방법.
- 이때 계산한 값을 저장 해 두었다가 다시 사용하는 <b>메모이제이션(Memoizaion)</b>이 핵심.
- 계산 한 값을 저장하기 때문에 한번 푼 문제는 중복해서 풀지 않는다.

<br/>

## 대표적인 예 피보나치 수열

> 피보나치 수열은 수열 제 0항, 1항은 1로 제쳐두고 2항부터 앞에 두 수를 더한 값을 결과로 두는 수열을 말한다. 피보나치 수열은 다음과 같이 표현할 수 있다.
$$ F(n) = F(n-1) + F(n-2) $$

위와 같이 수열 각각의 항들의 관계를 나타낸 식을 <b>점화식</b>이라 하며 기본적인 재귀함수로 나타낼 수도 있다.

```Js
// 메모이제이션 사용 안함
let noMemFibo = (count) => {
  if (count < 2) {
    return count;
  } else {
    return noMemFibo(count - 1) + noMemFibo(count - 2);
  }
};
```

이 재귀함수를 이용하여 _5_ 를 구하고자 한다면

![피보나치 수열 5](https://user-images.githubusercontent.com/97586683/205997701-c3979e6e-2542-451c-b1dd-fa01092c8f96.png)

위와 같은 방식으로 문제를 나누게 되는데, 5를 구하는데만도 중복되는 값들이 재귀적으로 호출되고 있다. 이 경우에 시간 복잡도는 `O(2n^2)`이기 때문에 숫자가 높아질수록 딜레이는 길어질 것이다.  
이런 경우에 동적계획법을 이용하여 이미 구한 값은 메모이제이션으로 저장을 해놓아 불필요한 연산 횟수를 줄이면 성능에서 이득을 볼 수 있다. 이 경우에는 시간복잡도를 `O(n)` 까지 단축이 가능하다.

<br/>

```Js
// 메모이제이션 사용함
let memFibo = (count) => {
  // 결과를 저장할 객체 선언
  let mem = {};
  let recur = (num) => {
    if (num < 2) { return num };
    // 객체에 key값이 있으면 가져다 쓰고, 없으면 재귀를 통해 작은 문제로 내려감
    let num1 = mem[num - 1] || recur(num - 1);
    let num2 = mem[num - 2] || recur(num - 2);
    mem[num] = num1 + num2;
    return num1 + num2;
  }
  recur(count);
  return mem[count];
}
```

<br/>

위의 두 코드, 일반적인 재귀를 통한 `nonMemFibo`와 동적계획법의 메모이제이션을 사용한 `memFibo` 함수를 이용하여 피보나치 수열의 20번째, 30번째, 40번째 항을 구할 때 소요되는 시간을 콘솔을 찍어보자.

![시간 비교](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcA4udF%2FbtqF9EbgBqT%2FclIiam6V9ghBfC3hreCEP0%2Fimg.png)

메모이제이션을 사용한 함수는 소요시간이 오차범위 내로 큰 변화가 없는 소요시간을 보여주고 있지만, 메모이제이션을 사용하지 않은 함수는 숫자가 커질수록 소요시간이 기하급수적으로 늘어나는 것을 볼 수 있다.

<br/>

## 구현 방식

> 동적 계획법의 구현 방식은 <b>Top-Down</b>방식과 <b>Bottom-Up</b>방식 두 가지로 구현이 가능한데, 아래 코드로 구현 코드의 차이를 보자
<br/>

### _Top-Down_

```Js
let topFibo = (count) => {
  let mem = {};
  let recur = (num) => {
    if (num < 2) { return num };
    let num1 = mem[num - 1] || recur(num - 1);
    let num2 = mem[num - 2] || recur(num - 2);
    mem[num] = num1 + num2;
    return num1 + num2;
  }
  recur(count);
  return mem[count];
}
```

- 큰 문제를 작은 문제로 쪼개며 풀어나간다. 작은 문제가 풀리지 않는다면, 더 작은 문제로 쪼개어 푼다.
- 재귀로 해결 가능

<br/>

### _Bottom-Up_

```Js
let buFibo = (count) => {
  let mem = [0, 1];
  count--;
  while(count > 0){
    if(count === 0) return;
    mem.push(mem[mem.length - 2] + mem[mem.length - 1]);
    count--;
  }
  return mem[mem.length - 1];
}
```

- 작은 문제에서부터 접근하여 큰 문제에 도달한다.
- 반복문으로 해결 가능

<br/>

> 대부분의 문제에서 두 가지 방식으로 모두 문제를 해결 할 수 있고, 둘의 시간 복잡도도 같으나 Top-Down 방식은 재귀함수를 호출하기 때문에 실제로는 Bottom-Up 방식이 성능이 더 좋은 경우가 있다고 한다. 일부 문제에서도 Top-Down 방식으로는 효율성 테스트에서 실패하는 문제를 Bottom-Up 방식으로 수정하면 해결되는 경우가 있다고 하니 두 가지 방식을 모두 숙지하여 적재적소에 사용하는 것이 좋을 듯 하다!
