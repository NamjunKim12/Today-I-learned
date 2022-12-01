# BFS, DFS 

## 📌 그래프 탐색 알고리즘

- 그래프 자료구조 내의 특정 개체를 찾기 위한 알고리즘이다.
- 대표적인 그래프 탐색 알고리즘에는 **BFS, DFS**가 있다.
- 드라마 시청에 비유를 하자면, DFS는 한 시리즈를 끝까지 본 후 다른 시리즈를 보는것, BFS는 보고싶은 모든 드라마를 한화씩 번갈아가며 보는 느낌으로 이해할 수 있다. 
- 그래프 탐색 알고리즘을 활용한 코테 문제 유형에는 1. 경로탐색(최단거리, 시간) 2.연결 유무 판단, 부분 그래프 찾기 3.가능한 모든 조합 만들기의 유형들이 주로 출제된다.


### DFS

![image](https://user-images.githubusercontent.com/69416561/204779769-ae9bcde9-5f2a-4faa-acc1-0714a76bd2f3.png)

- Depth-First-Search 의 약자로, 계층이 아닌 자식을 우선으로 탐색한다.
- 주로 **스택, 재귀함수**를 활용해서 구현한다.
- 최상위 노드(=정점, 버텍스)에서 연결된 자식 노드를 모두 탐색한 후, 더 이상 자식 노드가 없을 때 인접한 상위 노드의 형제 노드를 방문한다. 
- 해당 형제 노드에서도 자식 노드를 탐색하고, 더 이상 자식노드가 없을 경우 다시 인접한 상위 형제의 노드를 방문하는 알고리즘이다.
- 모든 정점들을 방문하고자 할 경우 사용한다.

### DFS 예제 - 타겟 넘버

![image](https://user-images.githubusercontent.com/69416561/204791913-4dbfd52c-daf5-4aaf-a1e0-afd4eefcca37.png)


모든 경우의 수를 따져봐야하므로(모든 정점을 방문해야하므로), DFS로 구현하는것이 낫다.

```js
function solution(numbers, target) {
    var answer = 0;
  // 처음 시작은 개수 0개, 합계 0 으로 시작하면서 모든 경우를 dfs로 탐색
    recur(0, 0);
    return answer;

    function recur(index, sum){
      // leaf node 도착했을 때, 모든 numbers 탐색
        if( index === numbers.length){
          // 주어진 조건에 만족하면 answer++
            if(sum === target ){
                answer++
            }
          // 리턴해주어야함
            return
        }

      // left child 는 +일 경우
        recur(index+1, sum+numbers[index]);
      // right child 는 -일 경우
        recur(index+1, sum-numbers[index]);
    }
}
```
**실행 순서**

해당 문제의 1번 테스트 케이스 기준

![image](https://user-images.githubusercontent.com/69416561/204794329-a55e55d1-f9d5-47cd-a2e5-121de297c50e.png)


1. 14번 라인 `recur(index+1, sum+numbers[index])` 부분이 계속 실행되며 다음 인덱스의 숫자가 (+) 인 자식 노드를 계속 탐색한다.
2. 정점까지 탐색했을 경우(index = 5, sum = 5 일 때) 해당 함수를 스택에서 제거한 뒤, index가 4일 때 `recur(index + 1, sum — numbers[index])` 을 실행하여 (-)인 자식 노드를 탐색한다. 
3. 한 정점까지 탐색했으므로 다시 해당 함수를 스택에서 제거, index가 3일 때 `recur(index + 1, sum — numbers[index])` 을 실행한다.
4. index 4가 (-)일 때 `recur(index + 1, sum + numbers[index])`을 실행하여 index 5가 (+)인 경우의 자식을 탐색한다.
5. 해당 탐색을 마치면 해당 함수를 스택에서 제거한 뒤 `recur(index + 1, sum — numbers[index])`을 실행하여 index 5가 (-)인 경우의 자식을 탐색한다.
6. 다시 index가 2일 때 `recur(index + 1, sum — numbers[index])`을 실행, index 3이 (-)일 때 14번 라인을 실행하여 index 4가 (+)인 경우의 자식 노드를 모두 탐색 후 15번 라인을 실행하며 index 5가 (-)인 경우의 자식 노드를 탐색한다.
7. (+)의 자식 노드 탐색 → (-)의 자식 노드 탐색 순서로 위 과정이 진행되며, index 1이 (-)일 때의 자식 노드의 경우의 수 (+), (-) 를 모두 탐색하면 해당 함수가 종료된다.

```
[+1, +1, +1, +1, +1]
[+1, +1, +1, +1, -1]
[+1, +1, +1, -1, +1]
[+1, +1, +1, -1, -1]
[+1, +1, -1, +1, +1]
[+1, +1, -1, +1, -1]
[+1, +1, -1, -1, +1]
[+1, +1, -1, -1, -1]
.
.
.

```

배열로 풀어보면 해당과같은 과정으로 재귀를 반복하게 된다. 



### BFS 

![image](https://user-images.githubusercontent.com/69416561/204781114-669f51b1-212a-4f93-ba82-6da49c92d646.png)


- Breadth-First-Search의 약자로, 자식보다 층위를 우선적으로 비교하면서 탐색한다.
- 주로 **큐** 자료구조로 구현한다.
- 그래프나 트리에서 큐에서 버텍스를 꺼낸 뒤에 해당 버텍스의 인접 버텍스 중 방문하지 않은 버텍스를 모두 큐에 삽입하고 방문처리한다.
- 임의의 정점이나 최단 거리를 구하는 문제에서 자주 쓰인다.


#### BFS 예제 - 게임 맵 최단거리

https://school.programmers.co.kr/learn/courses/30/lessons/1844

![image](https://user-images.githubusercontent.com/69416561/204796200-6a9d58af-3756-450a-a44a-c566ec3ab970.png)

https://hogumachu.tistory.com/9
