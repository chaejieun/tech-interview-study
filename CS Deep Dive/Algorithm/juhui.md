1. 시간복잡도와 공간복잡도란?
   시간 복잡도와 공간 복잡도는 알고리즘의 효율성을 평가하는 기준입니다.
   시간 복잡도는 입력 크기 n에 따라 수행해야 하는 연산의 수입니다. 주로 O(1), O(n), O(n²), O(log n)과 같은 Big-O 표기법을 사용해서 표현합니다.
   공간 복잡도는 입력 크기 n에 따라 알고리즘이 동작하는 동안 추가로 필요한 메모리 양을 나타냅니다. 시간 복잡도처럼 Big-O로 표현합니다.
   시간 복잡도는 **얼마나 빨리 동작하는가** 공간 복잡도는 **얼마나 많은 메모리를 쓰는가** 평가하는 기준입니다.

2. 피보나치 수열을 코드로 구현하는 방법에 대해서 설명해주세요
   피보나치 수열은 앞 두 수를 더해서 다음 수를 만들어가는 수열입니다.
   구현 방법으로는 단순 재귀, 메모이제이션을 활용한 재귀, 반복문 이렇게 세 가지로 설명할 수 있습니다.
   단순 재귀는 같은 계산을 여러 번 반복하기 때문에 시간 복잡도가 O(2ⁿ)으로 비효율적입니다.
   메모이제이션을 활용한 재귀는 시간 복잡도를 O(n)으로 줄일 수 있지만 추가 메모리 공간이 필요합니다.
   반복문을 이용한 방법이 가장 효율적입니다.
   0번째와 1번째 값을 미리 정해놓고, 2번째부터 n번째까지 for문을 돌려서 이전 두 값을 더해서 갱신해 나갑니다.
   구조 분해 할당을 하여 [prev, curr] = [curr, prev+curr]로 두 값을 동시에 업데이트 하면 변수를 2개만 사용하면서 공간 복잡도를 O(1)로 최소화할 수 있습니다.

3. DFS & BFS 란?
   DFS는 깊이 우선 탐색으로, 한 방향으로 갈 수 있을 만큼 최대한 깊이 내려간 후 막히면 돌아와서 다른 경로를 탐색하는 방식입니다. 스택 자료구조를 사용하거나 재귀호출로 깊이를 따라 들어갑니다. 전체 경로를 추적하거나 모든 경우의 수를 탐색할때 유용합니다.
   BFS는 너비 우선 탐색으로, 현재 노드의 이웃을 모두 방문한 다음 그 다음 단계로 넘어가는 방식입니다. 큐 자료구조를 사용합니다. 최단 경로를 찾거나 레벨별로 탐색해야 하는 문제에 유리합니다.
   **DFS는 깊게, BFS는 넓게** 탐색하는 전략입니다.

4. 거품 정렬(Bubble Sort)란?
   배열의 인접한 두 원소를 비교해서 순차적으로 위치를 바꿔나가며 정렬하는 알고리즘입니다. 이 과정을 끝까지 가장 큰 값이 맨 뒤로 이동하게 되는데, 이런 동작이 마치 거품이 위로 올라가는 것과 비슷하다고 하여 버블 정렬이라는 이름이 되었습니다.
   시간 복잡도는 평균과 최악의 경우 모두 O(n²)로, 데이터가 많을 때는 비효율적이지만, 구현이 매우 단순하고 직관적이어서 정렬 알고리즘의 기본 개념을 설명하거나 교육 목적으로 많이 사용됩니다.

5. 선택 정렬(Selection Sort)란?
   선택 정렬은 배열에서 가장 작은(또는 큰)값을 선택해서 맨 앞부터 차례대로 정렬하는 알고리즘 입니다.
   전체 배열에서 최솟값을 찾아서 첫 번째 원소와 자리를 바꾸고, 그 다음에 두 번째부터 끝까지 중에서 다시 최솟값을 찾아 자리를 바꾸는 방식을 반복합니다.
   시간 복잡도는 평균과 최악 모두 O(n²)로, 데이터가 많을 때는 비효율적입니다.
   하지만 구현이 간단하고, 정렬 과정에서 불필요한 교환이 적다는 장점이 있습니다.

6. 삽입 정렬(Insertion Sort)란?
   삽입 정렬은 배열의 두 번째 원소부터 시작해서. 현재 원소를 그보다 앞에 있는 정렬된 부분과 비교하여 적절한 위치에 삽입하는 방식의 정렬 알고리즘입니다.
   배열을 앞부분(정렬된 구간)과 뒷부분(아직 정렬되지 않은 구간)으로 나누고,
   정렬되지 않은 원소를 하나씩 꺼내어, 정렬된 부분에서 알맞은 위치에 밀어넣듯이 삽입하면서 배열 전체를 정렬합니다.
   시간 복잡도는 평균과 최악의 경우 O(n²)이지만,
   이미 어느 정도 정렬되어 있는 데이터에 대해서는 **O(n)**에 가까운 빠른 성능을 보일 수 있습니다.
   구현이 간단하고, 데이터가 거의 정렬된 상태에서 효율적이라는 장점이 있어서
   작은 데이터나 거의 정렬된 데이터에 자주 사용됩니다.
