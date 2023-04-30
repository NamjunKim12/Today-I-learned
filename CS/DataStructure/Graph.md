# 그래프


## 📌그래프란?
![image](https://user-images.githubusercontent.com/69416561/204725091-9d386463-3620-4084-9a37-fb7cfaef09e1.png)

- 자료, 개체 간의 연결관계를 나타내는 비선형 자료구조이다. 
- 어떤 자료를 포함하는 **정점(Vertex)과 정점 간의 연결관계를 나타내는 간선(Edge, ===Arc)** 으로 이루어져있다.
- 다른 Vertex로부터 오는 Edge의 갯수를 **진입차수(In-degree)**, 다른 Vertex로 가는 Edge의 갯수를 **진출차수(Out-Degree)** 라고 한다. 


## 📌그래프의 종류
![image](https://user-images.githubusercontent.com/69416561/204730738-da50cf95-0880-48b3-9b9f-99f6d4b53b28.png)

- 무방향 그래프: (간선의) 방향이 없는 그래프
- 방향 그래프: 방향성이 있는 그래프
- 가중치 그래프: 간선의 가중치값이 존재하는 그래프
- 루트없는 트리: 간선을 통해 정점 간 잇는 방법이 한가지인 그래프(*트리의 정의)
- 이분 그래프: 그래프의 정점을 겹치지 않게 두 그룹으로 나눈 후 다른 그룹끼리만 간선이 존재하게 분할할 수 있는 그래프
- 사이클이 없는 방향 그래프: 정점에서 출발해 자기 자신으로 돌아오는 경로(사이클)가 없는 그래프
- 해당 그래프 이외에도 한 정점이 모든 정점과 연결된 완전 그래프, 연결되지 않은 정점이 있는 단절 그래프 등 여러 종류가 있다. 

## 📌그래프의 표현
![image](https://user-images.githubusercontent.com/69416561/204733352-133220b3-7691-405c-bcb8-920e97fcdf62.png)

- 그래프는 추상적인 자료구조이기 때문에, 우리가 이를 실제로 구현할때는 **배열, 연결 리스트 자료구조**를 활용한다.


### 인접 행렬: 2차원 배열로 정점 간의 간선의 존재 여부를 1 또는 0으로 표기하는 방식 
- 간선의 수와 무관하게 항상 n² 크기의 2차원 배열이 필요하므로 메모리 공간이 낭비된다.
- 2차원 배열에 모든 정점들의 간선 정보가 있기 때문에, **두 정점을 연결하는 간선을 조회할 때** O(1) 시간복잡도로 가능하다.
- 그래프의 **모든 간선의 수**를 알아내려면 인접행렬 전체를 확인해야 하므로 O(n²)의 시간이 소요된다.
- 간선이 많이 존재하는 밀집 그래프일 경우 효과적이다.


### 연결 리스트: 정점 개수만큼 리스트를 만들어 각각의 정점 리스트에 간선을 추가하는 방식

- 그래프를 나타내는 가장 일반적인 방식이다.
- 존재하는 간선만 관리하면 되므로, 메모리 사용측면에서 보다 효율적이다.
- 그래프의 **모든 간선의 수**를 알아내려면 각 정점의 헤더 노드부터 모든 인접리스트를 탐색해야 하므로 O(V+E)의 시간이 소요된다.
- **두 정점을 연결하는 간선을 조회**하거나 **정점의 차수**를 알기 위해서는 정점의 인접 리스트를 탐색해야 하므로 정점의 차수만큼의 시간이 필요하다. **O(degree(v))**


## 📌[JS] 객체와 클래스로 구현한 그래프

### 무방향 그래프

```js
class UndirectedGraph {
  constructor() {
    this.edges = {};
  }
  // 정점 추가하기
  addVertex(vertex) {
    this.edges[vertex] = {}; //
  }

  // 간선 추가하기
  addEdge(vertex1, vertex2, weight=0) {
    this.edges[vertex1][vertex2] = weight;
    this.edges[vertex2][vertex1] = weight;
  }

  // 간선 삭제하기
  removeEdge(vertex1, vertex2) {
    if (this.edges[vertex1] && this.edges[vertex1][vertex2] !== undefined) {
      delete this.edges[vertex1][vertex2];
    }
    if (this.edges[vertex2] && this.edges[vertex2][vertex1] !== undefined) {
      delete this.edges[vertex2][vertex1];
    }
  }

  // 정점 삭제하기 (하나의 정점이 삭제될 때는 그 정점과 연결된 간선이 삭제되니까 상대편 정점에서도 그 간선을 지워줘야 한다.)
  removeVertex(vertex) {
    for (let adjacentVertex in this.edges[vertex]) {
      this.removeEdge(adjacentVertex, vertex);
    }
    delete this.edges[vertex];
  }
}

const graph1 = new UndirectedGraph();
graph1.addVertex(1);
graph1.addVertex(2);
graph1.addVertex(3);
graph1.addVertex(4);
graph1.addVertex(5);
graph1.addEdge(1, 2, 1);
graph1.addEdge(1, 5, 88);
graph1.addEdge(2, 3, 8);
graph1.addEdge(3, 4, 10);
graph1.addEdge(4, 5, 100);
console.log(graph1.edges);

const graph2 = new UndirectedGraph();
graph2.addVertex(1);
graph2.addVertex(2);
graph2.addVertex(3);
graph2.addVertex(4);
graph2.addVertex(5);
graph2.addEdge(1, 2, 1);
graph2.addEdge(1, 5, 88);
graph2.addEdge(2, 3, 8);
graph2.addEdge(3, 4, 10);
graph2.addEdge(4, 5, 100);
graph2.removeVertex(5);
graph2.removeVertex(1);
graph2.removeEdge(2, 3);
console.log(graph2.edges);

```
![image](https://user-images.githubusercontent.com/69416561/204750846-970066ec-dff0-4e92-b95d-9c91584bff0a.png)
![image](https://user-images.githubusercontent.com/69416561/204750934-390d46f7-a1a1-4d22-88ad-0591d273ecb3.png)

- 위의 그림은 graph1의 구현 결과이고, 아래 그림은 그래프2의 구현 결과이다.

### 방향 그래프

```js

class DirectedGraph {
  constructor() {
    this.edges = {};
  }
  //정점을 추가하는 메서드
  addVertex(vertex) {
    this.edges[vertex] = {};
  }
  //간선을 추가하는 메서드
  addEdge(departure, destination, weight=0) {
    // 시작 정점, 도착 정점, 가중치
    this.edges[departure][destination] = weight;
  }
}
const graph1 = new DirectedGraph();
graph1.addVertex("A");
graph1.addVertex("B");
graph1.addVertex("C");
graph1.addEdge("A", "B", 1);
graph1.addEdge("B", "C", 2);
graph1.addEdge("C", "A", 3);
console.log(graph1.edges);

```
![image](https://user-images.githubusercontent.com/69416561/204751187-8ed4a9a2-ee7e-4473-a157-6f2264034b43.png)
