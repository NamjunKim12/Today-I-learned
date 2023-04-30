# 스택, 큐

> <b>스택(stack)</b> 과 <b>큐(Queue)</b>는 프로그래밍이라는 개념이 탄생할 때부터 가장 고전적인 자료구조 중 하나이다.  
> 이 둘은 구체적인 구현 방식은 생략한 채, 데이터의 추상적 형태와 그 데이터를 다루는 방법만을 정해놓은 <b>ADT(Absctact Data Type)</b> 혹은 <b>추상 자료형</b>이라고 하는데, 그 중에 가장 널리 사용 되는것이 스택과 큐이다.

<br/>

## 스택(Stack)

- 스택이란 마치 탑을 쌓듯 데이터를 추가하는 자료구조이다.
- 먼저 들어간 자료가 나중에 나오는 **후입선출** 자료구조로, **LIFO(Last In First Out)** 라고도 부른다.
- 데이터를 입력하는 `push()` 와 데이터를 제거하는 `pop()` 등의 작업이 가능하다.
- 웹페이지 뒤로가기 기능이나, crtl+Z 로 이전 기능을 취소할때 의 기능 등에 주로 사용된다.

    <img width="600" alt="스택이미지" src="https://miro.medium.com/max/640/1*IOwNU1HsdBktmOqChSjKoA.jpeg">

<br/>

### 스택의 Big-O (시간복잡도)

---

| 삽입 | 삭제 | 검색 |
| :--: | :--: | :--: |
| O(1) | O(1) | O(n) |

- 삽입의 경우에는 스택이 아무리 크더라도 맨 마지막에 하나의 스택만 쌓으면 되므로 시간 복잡도는 **O(1)** 이다.
- 삭제의 경우에도 맨 마지막에 들어온 하나의 스택만 제거하면 되므로 시간복잡도는 **O(1)** 이다.
- 다만 검색의 경우에는 스택의 모든 요소를 찾아야 하는 경우가 생기므로 시간복잡도는 **O(n)** 이다.

<br/>

### 스택의 ADT

---

<br/>

> 구현하기에 앞서 앞서 간단하게 설명한 **ADT(추상 자료형)** 에 대해서 간략하게 보고 넘어갑시다.  
> 아래의 메서드와 같이 구체적인 구현 방식은 생략하고, 데이터의 추상적 형태, 데이터를 다루는 방법만 정해놓은 것입니다.

|       push()        |            pop()            |           peek()            |               lefts()               |          clear()           |            empty()             |
| :-----------------: | :-------------------------: | :-------------------------: | :---------------------------------: | :------------------------: | :----------------------------: |
| 스택에 새 요소 추가 | 스택 맨 위에 있는 요소 삭제 | 스택 맨 위에 있는 요소 확인 | 스택에 있는 모든 요소 문자열로 변환 | 스택에 있는 모든 요소 삭제 | 스택에 남은 요소가 있는지 확인 |

등등..
<br/>

### 스택 예제(프로그래머스 같은숫자는싫어)

---

```JS
function solution(arr) {
  let answer = [];

  for (let i = 0; i < arr.length; i++) {
    if (answer[answer.length - 1] !== arr[i]) {
      // 현재 순회중인 수 가 마지막에 넣은 수와 과 같지 않다면
      answer.push(arr[i]); // answer 배열로 push
    }
  }

  return answer;
}
```

<br/><br/><br/>

## 큐(Queue)

- 큐는 스택과 같이 데이터를 추가하고 삭제하는 자료구조이다.
- 스택과의 차이는 먼저들어간 데이터가 먼저 나오는 **선입선출** 구조로 **FIFO(First In First Out)** 라고도 부른다.
- 데이터를 넣는 쪽을 <b>rear</b>라고 하고 데이터를 가져오는 쪽을 <b>front</b>로 사용한다.
- 데이터를 넣는 작업을 <b>인큐(Enqueue)</b>, 데이터를 가쟈오는 작업을 <b>디큐(Dequeue)</b> 라고 한다.
- 버스틑 타기위해 줄을 선다고 생각하면 된다. 먼저 줄 선 사람이 먼저 탄다.

    <img width="600" alt="큐이미지" src="https://www.javascripttutorial.net/wp-content/uploads/2016/08/JavaScript-Queue-Illustration.png">

<br/>

### 큐의 Big-O(시간복잡도)

---

| 삽입 | 삭제 | 검색 |
| :--: | :--: | :--: |
| O(1) | O(1) | O(n) |

- 큐의 시간복잡도는 스택과 동일하게 삽입과 삭제에서 **O(1)**, 검색에서 **O(n)** 이다.

<br/>

### 큐의 ADT

---

> 큐에서는 큐에 새 요소를 추가하는 **enqueue()**, 맨 앞에 있는 요소를 삭제하는 **dequeue()** 는 필수적으로 필요하다.

|     enqueue()     |         dequeue()         |         clear()          |           empty()            |
| :---------------: | :-----------------------: | :----------------------: | :--------------------------: |
| 큐에 새 요소 추가 | 큐 맨 앞에 있는 요소 삭제 | 큐에 있는 모든 요소 삭제 | 큐에 남은 요소가 있는지 확인 |

### 스택 예제(프로그래머스 기능개발)

---

```JS
function solution(progresses, speeds) {
  let answer = [];
  // 100% 완료 기준으로 (100 - 진도) / 속도 공식을 이용하면 각 작업들이 며칠에 걸쳐서 완료되는지 알아낼 수 있음
  const completeDay = progresses.map(
    (progress, index) => Math.ceil((100 - progress) / speeds[index]) // 소수점 올림처리
  );
  let count = 1; // 작업 일수의 최솟값 1
  let maxDay = completeDay[0];

  for (let i = 1; i < completeDay.length; i++) {
    if (completeDay[i] <= maxDay) {
      // 현재 순회하는 배열 인덱스의 값이 maxDay 보다 작으면
      count++; // count 증가
    } else {
      maxDay = completeDay[i];
      answer.push(count); // 현재 count 의 값을 answer 배열에 push
      count = 1; // count 다시 1로 초기화
    }
  }

  answer.push(count); // 마지막 count 값 answer 배열에 push

  return answer;
}

// 다른 풀이 (while 문을 이용, shift()를 사용하여 큐의 구조가 더 잘 보이는 풀이라서 긁어옴!)
function solution(progresses, speeds) {
  let answer = [];

  while (speeds.length > 0) {
    // speed 배열길이가 0이 될때까지
    let cnt = 0;
    for (let i = 0; i < speeds.length; i++) {
      // progress와 speed 짝지어 더하기
      if (progresses[i] < 100) {
        // 100이 넘어가면 그만 더하기
        progresses[i] += speeds[i];
      }
    }
    while (progresses[0] >= 100) {
      // 맨앞의 progress배열이 100이 넘으면 shift
      progresses.shift();
      speeds.shift(); // speed도 shift
      cnt++;
    }
    if (cnt > 0) {
      answer.push(cnt);
    }
  }
  return answer;
}
```