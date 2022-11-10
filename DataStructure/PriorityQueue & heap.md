# 우선순위 큐란?

사람들의 기다리는 줄처럼 들어온 순서대로 먼저 나가는(FIFO) 구조가 큐라면,
우선 순위 큐는 들어온 순서가 아닌 우선 순위가 높은 순서대로 나가는 구조.

`우선 순위 큐는 힙 이라는 자료구조를 가지고 구현된다.`

<br>

> ❓ 왜 배열로 구현하지 않을까?

- 우선 순위가 높은 순서대로 넣으면, 하나씩 뺄 때 그 순서 그대로 나오므로 괜찮을 수 있음.
- 우선 순위가 중간인 항목을 중간에 삽입해야 할 때는 항목을 하나씩 확인 후 뒤의 항목을 하나씩 밀어야함.
- 삽입 시 최악의 경우 `O(n)` 의 시간이 소요.

<img style="padding:10px" src="https://k.kakaocdn.net/dn/IvYC7/btqvpjKFtX5/zXfxEp44Y41pH9T2xtyt40/img.png"></img>

<img style="padding:10px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2F6HLLY%2FbtqvrVIkihw%2FKquPglj3WBYB47QqcQDjO1%2Fimg.png"></img>

> ❓ 왜 연결리스트로 구현하지 않을까?

- 배열과 마찬가지로 순서대로 넣으면 반환은 O(1)시간 소요.
- 그러나 삽입 시 항목을 배열과 같이 하나씩 확인해야하므로 역시 최악의 경우 `O(n)` 의 시간이 소요.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FbkqoDB%2FbtqvrDuocpa%2FgC8f10abtJxriFYolxa3Yk%2Fimg.png"></img>



# 힙

힙이란? 힙은 트리와 기반의 자료 구조로, `최대 힙`의 경우 부모가 자식보다 크고
`최소 힙`의 경우 부모가 자식보다 작다.

<img style="height:215px;" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FcT2Dxb%2FbtqSATggBLA%2FCIBeKSLq0s6MDTNVM345Jk%2Fimg.png"></img>
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FbwtTZl%2FbtqSASIpEE1%2FzJxtetzfI1OGHucT99Mcuk%2Fimg.png"></img>

## 힙의 특징

- 힙은 최소 | 최대 값을 `O(1)`의 시간복잡도로 얻어낼 수 있음.(root 활용)
- 부모 - 자식간의 관계를 쉽게 설명

<img style="height:215px;" src="https://images.velog.io/images/nnnyeong/post/0cd697f4-d373-4a65-a068-1972d6327d8d/image.png"></img>

- 힙 자료구조는 `완전한 이진트리`로 구현
  (트리의 가장 아래층 빼고는 상단이 모두 채워지고,동시에 두개의 자식만 가질 수 있는 트리)
- 즉, 부모 노드는 항상 자식 노드보다 값이 작아야 하며(최소 힙의 경우),한 레벨이 모두 채워져야 다음 레벨로 트리가 늘어날 수 있다.
- 배열로 구현 가능
- 최소 힙의 특성상 `우선 순위 큐의 최적 자료형`(우선 순위 값을 먼저 뽑아내기 가능)
  ex) 운영체제 내 우선순위 기반 스케쥴링, 다익스트라 알고리즘(최단 거리 구하기 알고리즘) 에서 최소 비용을 기반으로 그래프를 탐색 할 때 사용된다.

# <div style="padding-top:20px">힙으로 우선 순위 큐를 만들어보자!</div>

### 💡 힙 구현

```js
class Heap {
constructor() {
this.heap = []
}

getLeftChildIndex = (parentIndex) => parentIndex _ 2 + 1
getRightChildIndex = (parentIndex) => parentIndex _ 2 + 2
getParentIndex = (childIndex) => Math.floor((childIndex - 1) / 2)
 swap(i1, i2) {
    const temp = this.data[i1];
    this.data[i1] = this.data[i2];
    this.data[i2] = temp;
  }

peek = () => this.heap[0] // 항상 최상위 노드가 peek 가 된다.

 insert = (key, value) => { // 우선순위를 비교하기 위해서 key, value 로 받는다.
    const node = { key, value } // 객체로 node 를 만들고
    this.heap.push(node) // push 한다.
    this.heapifyUp() // 배열에 가장 끝에 넣고, 다시 min heap 의 형태를 갖추도록 한다.
  }
heapifyUp = () => {
    let index = this.heap.length - 1 // 계속해서 변하는 index 값
    const lastInsertedNode = this.heap[index]

    // 루트노드가 되기 전까지
    while (index > 0) {
      const parentIndex = this.getParentIndex(index)

      // 부모 노드의 key 값이 마지막에 삽입된 노드의 키 값 보다 크다면
      // 부모의 자리를 계속해서 아래로 내린다.
      if (this.heap[parentIndex].key > lastInsertedNode.key) {
        this.heap[index] = this.heap[parentIndex]
        index = parentIndex
      } else break
    }

    // break 를 만나서 자신의 자리를 찾은 상황
    // 마지막에 찾아진 곳이 가장 나중에 들어온 노드가 들어갈 자리다.
    this.heap[index] = lastInsertedNode
  }
  remove = () => {
    const count = this.heap.length
    const rootNode = this.heap[0]

    if (count <= 0) return undefined
    if (count === 1) this.heap = []
    else {
      this.heap[0] = this.heap.pop() // 끝에 있는 노드를 부모로 만들고
      this.heapifyDown() // 다시 min heap 의 형태를 갖추도록 한다.
    }


    return rootNode
  }
  heapifyDown = () => {
    let index = 0
    const count = this.heap.length
    const rootNode = this.heap[index]

    // 계속해서 left child 가 있을 때 까지 검사한다.
    while (this.getLeftChildIndex(index) < count) {
      const leftChildIndex = this.getLeftChildIndex(index)
      const rightChildIndex = this.getRightChildIndex(index)

      // 왼쪽, 오른쪽 중에 더 작은 노드를 찾는다
      // rightChild 가 있다면 key의 값을 비교해서 더 작은 값을 찾는다.
      // 없다면 leftChild 가 더 작은 값을 가지는 인덱스가 된다.
      const smallerChildIndex =
        rightChildIndex < count && this.heap[rightChildIndex].key < this.heap[leftChildIndex].key
          ? rightChildIndex
          : leftChildIndex

      // 자식 노드의 키 값이 루트노드보다 작다면 위로 끌어올린다.
      if (this.heap[smallerChildIndex].key <= rootNode.key) {
        this.heap[index] = this.heap[smallerChildIndex]
        index = smallerChildIndex
      } else break
    }

    this.heap[index] = rootNode
  }
}

```

### 💡 구현한 힙을 사용한 우선 순위 큐

```js
class PriorityQueue extends Heap {
  constructor() {
    super();
  }

  enqueue = (priority, value) => this.insert(priority, value);
  dequeue = () => this.remove();
  isEmpty = () => this.heap.length <= 0;
}
```

| 구현 방식 | 삽입  | 삭제  |
| --------- | ----- | ----- |
| 힙        | log N | log N |
