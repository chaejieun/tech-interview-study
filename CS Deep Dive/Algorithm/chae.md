# 📅 2025/04/29
# 시간복잡도란(Time Comlexity)?
- 컴퓨터 프로그램의 입력값과 연산 수행 시간의 상간관계를 나타내는 척도
- 시간 복잡도란 크기 n의 모든 입력에 대해 걸리는 최대의 시간 (최악의 경우로 알고리즘 성능 파악)
- 시간 개념보다는 알고리즘이 실행될 때 동작하는 연산의 횟수가 몇 번인지 세는 것
- 성능평가 유형으로 best, average, worst가 있는데 이 중 최악의 경우로 알고리즘 성능을 평가

> 👉 **알고리즘을 위해 필요한 연산의 횟수**

---

### 시간복잡도 그래프 
![alt text](image.png)
- 자료의 수가 증가함에 따라 소요되는 처리시간 증가율을 그래프로 나타낸 것

---

## 🔍 예제
### 예제1 - O(1)
```java
if(n%2 == 0) {
    System.out.println("짝수");
} else {
    System.out.println("홀수");
}
```
=> 짝수, 홀수 두 단계에 걸쳐 진행하지만, O(1)의 시간복잡도를 가짐

### 예제2 - O(n)
```java
for(int i=0; i<n; i++) {
    System.out.println(n);
}
```
=> 이 함수는 O(n)의 시간복잡도를 가짐

---

# 공간복잡도란?

- 알고리즘 수행 시 사용하는 **메모리의 양**
- 주로 **배열, 리스트, 재귀 호출 스택** 등에서 메모리 사용량이 결정됨

### 공간 종류
1. **고정 공간**: 입력 크기와 무관한 공간 (예: 변수 선언)
2. **가변 공간**: 입력 크기에 따라 변하는 공간 (예: 배열, 동적 할당 등)

> 👉 **알고리즘을 위해 필요한 메모리의 양**

---

### ✨ 정리 포인트
- 시간복잡도: 연산 횟수 기준
- 공간복잡도: 메모리 사용량 기준
- 알고리즘 성능을 종합적으로 판단할 때 둘 다 중요함

---
---
---

# 피보나치 수열(Fibonacci Sequence) 이란?
- 0, 1, 1, 2, 3, 5, 8, 13, 21, 34 ....
- 점화식(재귀 관계)

  > **F(n) = F(n-1) + F(n-2)**  
  > **F(0) = 0, F(1) = 1**

---

## 🔍 예제
### 예제1 - 재귀(Recursive)
```java
public static int fibRecursive(int n) {
    if (n <= 1) return n;
    return fibRecursive(n - 1) + fibRecursive(n - 2);
}
```
=> 시간복잡도: O(2^n) — 비효율적
=> 공간복잡도: O(n) — 호출 스택

### 예제2 - 메모이제이션(Top-Down DP)
```java
public static int fibMemo(int n, int[] memo) {
    if (memo[n] != -1) return memo[n];
    if (n <= 1) return n;
    memo[n] = fibMemo(n - 1, memo) + fibMemo(n - 2, memo);
    return memo[n];
}

// 사용 예시
int n = 10;
int[] memo = new int[n + 1];
Arrays.fill(memo, -1);
System.out.println(fibMemo(n, memo));  // 결과: 55
```
=> 시간복잡도: O(2^n) — 비효율적
=> 공간복잡도: O(n) — memo 배열과 재귀 호출 스택

### 예제3 - 바텀업(Bottom-Up DP)
```java
public static int fibBottomUp(int n) {
    if (n <= 1) return n;
    int[] dp = new int[n + 1];
    dp[0] = 0;
    dp[1] = 1;

    for (int i = 2; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }

    return dp[n];
}

```
=> 시간복잡도: O(n)
=> 공간복잡도: O(n)

### 예제4 - 공간 최적화(변수 2개만 사용)
```java
public static int fibOptimized(int n) {
    if (n <= 1) return n;
    int a = 0, b = 1;

    for (int i = 2; i <= n; i++) {
        int temp = a + b;
        a = b;
        b = temp;
    }

    return b;
}
```
=> 시간복잡도: O(n)
= > 공간복잡도: O(1) 가장 효율적

---


### ✨ 정리 포인트
- 피보나치 수열은 F(n) = F(n-1) + F(n-2)의 점화식을 따르는 문제 
- 가장 단순한 재귀 방식은 코드가 짧지만, 중복 호출로 인해 시간복잡도가 O(2^n)이라 비효율적
- 그래서 보통 메모이제이션(Top-Down) 활용하거나 반복문 기반 바텀업(Bottom-Up)  방식을 사용해 시간복잡도를 O(n)으로 개선
- 특히 실무에서는 공간까지 고려해 O(1) 공간복잡도로 구현하는 최적화 방식까지 사용해야 한다

---
---
---


# DFS(깊이 우선 탐색, Depth-First Search)란 ?
- 한 방향으로 **끝까지 탐색**하고, 더 이상 갈 수 없을 때 **되돌아가서 다른 경로**를 탐색하는 알고리즘
- **재귀** 또는 **스택(Stack)** 을 사용해서 구현.
- 주로 **그래프 탐색**, **사이클 감지**, **경로 찾기**, **백트래킹 문제** 등에 사용.

### 동작과정
1. 현재 노드를 방문하고, 방문 표시를 합니다.
2. 인접한 노드 중 방문하지 않은 노드가 있다면 그 노드로 이동하고 다시 탐색을 반복합니다.
3. 더 이상 방문할 노드가 없다면 이전 노드로 되돌아갑니다 (Backtracking).

### 시간복잡도
- **O(V + E)**

## 예제 
### 백준 2667번: 단지 번호 붙이기
Q. 정사각형 모양의 지도가 주어지며, 1은 집이 있는 곳을, 0은 집이 없는 곳을 나타냅니다. 상하좌우로 연결된 집들을 하나의 단지로 정의하고, 총 단지 수와 각 단지에 속하는 집의 수를 오름차순으로 출력하는 문제입니다.

```java 
import java.io.*;
import java.util.*;

public class Main {
    static int N;
    static int[][] map;
    static boolean[][] visited;
    static List<Integer> houseCounts;
    static int count;

    // 상하좌우 이동을 위한 배열
    static int[] dx = {-1, 1, 0, 0};
    static int[] dy = {0, 0, -1, 1};

    // DFS 메서드
    public static void dfs(int x, int y) {
        visited[x][y] = true;
        count++;

        for (int i = 0; i < 4; i++) {
            int nx = x + dx[i];
            int ny = y + dy[i];

            // 지도 범위 내에 있고, 집이 있으며, 아직 방문하지 않은 경우
            if (nx >= 0 && ny >= 0 && nx < N && ny < N) {
                if (map[nx][ny] == 1 && !visited[nx][ny]) {
                    dfs(nx, ny);
                }
            }
        }
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        N = Integer.parseInt(br.readLine());
        map = new int[N][N];
        visited = new boolean[N][N];
        houseCounts = new ArrayList<>();

        // 지도 정보 입력
        for (int i = 0; i < N; i++) {
            String line = br.readLine();
            for (int j = 0; j < N; j++) {
                map[i][j] = line.charAt(j) - '0';
            }
        }

        // 전체 지도 탐색
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                // 집이 있고, 아직 방문하지 않은 경우
                if (map[i][j] == 1 && !visited[i][j]) {
                    count = 0;
                    dfs(i, j);
                    houseCounts.add(count);
                }
            }
        }

        // 단지 수 출력
        System.out.println(houseCounts.size());

        // 각 단지 내 집의 수를 오름차순으로 정렬하여 출력
        Collections.sort(houseCounts);
        for (int c : houseCounts) {
            System.out.println(c);
        }
    }
}

```

### 입력 예시
```
7 
0110100 
0110101 
1110101 
0000111 
0100000 
0111110 
0111000
```
---

### 출력 예시
```
3 
7 
8 
9
```
---
---
---

# BFS(너비 우선 탐색, Breadth-First Search)란 ?
- 그래프나 트리에서 **너비 우선**으로 탐색 진행하는 알고리즘 
- 주로 **최단 경로**를 찾는 문제나, **레벨별 탐색**을 요구하는 문제에서 사용

### 동작과정
1. **큐(Queue)**에 시작 노드를 넣고 시작.
2. 큐에서 노드를 하나씩 꺼내며 그 노드와 연결된 노드를 큐에 추가.
3. 이미 방문한 노드는 다시 방문하지 않도록 **방문 체크**.
4. 큐에 탐색할 노드가 더 이상 없을 때까지 반복.

### 시간복잡도
- **O(V + E)**

## 예제 
### 백준 1926번: 그림
Q. 어떤 큰 도화지에 그림이 그려져 있을 때, 그림의 개수와 그 중 가장 넓은 그림의 넓이를 출력하는 문제입니다.​

- **그림의 정의**: 1로 연결된 부분을 하나의 그림으로 간주합니다.
- **연결의 기준**: 상하좌우로 연결된 경우만을 연결된 것으로 간주하며, 대각선은 연결로 보지 않습니다.
- **그림의 넓이**: 그림에 포함된 1의 개수입니다

```java 
import java.io.*;
import java.util.*;

public class Main {
    static int n, m;
    static int[][] paper;
    static boolean[][] visited;

    // 상하좌우 이동을 위한 배열
    static int[] dx = {-1, 1, 0, 0}; // 상, 하
    static int[] dy = {0, 0, -1, 1}; // 좌, 우

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        // 도화지의 세로(n)와 가로(m) 크기 입력
        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());

        paper = new int[n][m];
        visited = new boolean[n][m];

        // 도화지 정보 입력
        for (int i = 0; i < n; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < m; j++) {
                paper[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        int numberOfPictures = 0; // 그림의 개수
        int maxArea = 0; // 가장 넓은 그림의 넓이

        // 도화지를 순회하면서 BFS 수행
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (paper[i][j] == 1 && !visited[i][j]) {
                    int area = bfs(i, j);
                    numberOfPictures++;
                    maxArea = Math.max(maxArea, area);
                }
            }
        }

        // 결과 출력
        System.out.println(numberOfPictures);
        System.out.println(maxArea);
    }

    // BFS 메서드
    public static int bfs(int x, int y) {
        Queue<Point> queue = new LinkedList<>();
        visited[x][y] = true;
        queue.offer(new Point(x, y));
        int area = 1;

        while (!queue.isEmpty()) {
            Point current = queue.poll();

            // 상하좌우로 이동
            for (int i = 0; i < 4; i++) {
                int nx = current.x + dx[i];
                int ny = current.y + dy[i];

                // 도화지 범위 내에 있고, 그림이 그려져 있으며, 아직 방문하지 않은 경우
                if (nx >= 0 && ny >= 0 && nx < n && ny < m) {
                    if (paper[nx][ny] == 1 && !visited[nx][ny]) {
                        visited[nx][ny] = true;
                        queue.offer(new Point(nx, ny));
                        area++;
                    }
                }
            }
        }

        return area;
    }

    // 좌표를 나타내는 Point 클래스
    static class Point {
        int x, y;

        Point(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }
}

```

### 입력 예시
```
6 5
1 1 0 1 1
0 1 0 0 0
0 0 0 0 0
1 0 1 1 1
0 0 0 0 0
1 1 1 1 1
```
---

### 출력 예시
```
4
9
```
---

# 📅 2025/05/19
# 거품 정렬(Bubble Sort)란?
- 인접한 두 요소를 비교하여 의도한 순서가 될 때까지 교체하는 정렬 알고리즘.

### 동작과정
- 배열의 처음부터 끝까지 인접한 두 요소를 비교
- 앞 요소가 뒷 요소보다 크면 두 요소를 교환
- 이렇게 한 바퀴 돌면 가장 큰 값이 배열의 끝으로 이동
- 위 과정을 전체 길이 - 1 만큼 반복

### 시간복잡도
- **O(n²)**


### 예제
```java
public class BubbleSortExample {
    public static void bubbleSort(int[] arr) {
        int n = arr.length;
        boolean swapped;

        // 총 n-1번 반복
        for (int i = 0; i < n - 1; i++) {
            swapped = false;

            // 인접한 요소 비교 및 스왑
            for (int j = 0; j < n - 1 - i; j++) {
                if (arr[j] > arr[j + 1]) {
                    // swap
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;

                    swapped = true;
                }
            }

            // 만약 한 번도 swap 안 했다면 이미 정렬된 상태 → 종료
            if (!swapped) break;
        }
    }

    public static void main(String[] args) {
        int[] numbers = {5, 2, 9, 1, 5, 6};
        bubbleSort(numbers);
        for (int num : numbers) {
            System.out.print(num + " ");
        }
    }
}
```
---
# 선택 정렬(Selection Sort)란?
- 배열에서 가장 작은(또는 큰) 값을 선택해서 정렬되지 않은 영역의 맨 앞과 교환하는 방식

## 동작과정
- 전체 배열 중 가장 작은 값을 찾아 첫 번째 요소와 교환
- 그 다음 작은 값을 찾아 두 번째 요소와 교환
- 이를 배열 끝까지 반복

## 시간복잡도
**O(n²)**

## 예제
```java
public class SelectionSortExample {
    public static void selectionSort(int[] arr) {
        int n = arr.length;

        // 마지막 요소는 자동으로 정렬됨
        for (int i = 0; i < n - 1; i++) {
            int minIndex = i;

            // 최소값의 인덱스를 찾는다
            for (int j = i + 1; j < n; j++) {
                if (arr[j] < arr[minIndex]) {
                    minIndex = j;
                }
            }

            // 현재 위치와 최소값 위치 교환
            int temp = arr[minIndex];
            arr[minIndex] = arr[i];
            arr[i] = temp;
        }
    }

    public static void main(String[] args) {
        int[] numbers = {64, 25, 12, 22, 11};
        selectionSort(numbers);
        for (int num : numbers) {
            System.out.print(num + " ");
        }
    }
}
```

---

# 삽입 정렬(Insertion Sort)란?
- 데이터를 **하나씩 꺼내서 앞쪽에 정렬된 데이터들과 비교해 알맞은 위치에 '삽입'**하는 방식

## 동작과정
- 두 번째 원소부터 시작해서 앞쪽 원소들과 비교
- 앞의 원소가 크면 한 칸씩 뒤로 밀고
- 삽입할 위치를 찾으면 그 자리에 삽입

## 시간복잡도
**O(n2)**

## 예제
```java
public class InsertionSortExample {
    public static void insertionSort(int[] arr) {
        int n = arr.length;

        for (int i = 1; i < n; i++) {
            int key = arr[i];       // 삽입할 값
            int j = i - 1;

            // key보다 큰 값을 오른쪽으로 이동
            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j--;
            }

            // key를 삽입할 위치에 넣는다
            arr[j + 1] = key;
        }
    }

    public static void main(String[] args) {
        int[] arr = {5, 2, 4, 6, 1, 3};
        insertionSort(arr);
        for (int num : arr) {
            System.out.print(num + " ");
        }
    }
}
```

# 📅 2025/06/02
# 퀵 정렬(Quick Sort)란?
- 분할 정복 알고리즘의 하나로, 평균적으로 매우 빠른 수행 속도를 자랑하는 정렬 방법

## 동작과정
1. 리스트 안에 있는 한 요소를 선택한다. 이렇게 고른 원소를 **피벗(pivot)** 이라고 한다.
2. 피벗을 기준으로 피벗보다 작은 요소들은 모두 피벗의 왼쪽으로 옮겨지고 피벗보다 큰 요소들은 모두 피벗의 오른쪽으로 옮겨진다. (피벗을 중심으로 왼쪽: 피벗보다 작은 요소들, 오른쪽: 피벗보다 큰 요소들)
3. 피벗을 제외한 왼쪽 리스트와 오른쪽 리스트를 다시 정렬한다.
- 분할된 부분 리스트에 대하여 **순환 호출** 을 이용하여 정렬을 반복한다.
- 부분 리스트에서도 다시 피벗을 정하고 피벗을 기준으로 2개의 부분 리스트로 나누는 과정을 반복한다.
4. 부분 리스트들이 더 이상 분할이 불가능할 때까지 반복한다.
- 리스트의 크기가 0이나 1이 될 때까지 반복한다

## 시간복잡도
- O(NlogN)

## 예제
```java
public class SimpleQuickSort {

    // 퀵 정렬의 메인 메서드
    public void quickSort(int[] arr, int low, int high) {
        if (low < high) {
            // 피벗을 기준으로 배열을 분할하고 피벗의 최종 위치를 받아요.
            int pi = partition(arr, low, high);

            // 피벗 왼쪽 부분과 오른쪽 부분을 각각 재귀적으로 정렬합니다.
            quickSort(arr, low, pi - 1);
            quickSort(arr, pi + 1, high);
        }
    }

    // 배열을 분할하는 메서드 (피벗 기준 왼쪽은 작은 값, 오른쪽은 큰 값)
    private int partition(int[] arr, int low, int high) {
        // 가장 오른쪽 원소를 피벗으로 선택 (다양한 피벗 선택 전략이 있어요)
        int pivot = arr[high];
        int i = (low - 1); // 피벗보다 작은 값들의 '경계' 인덱스

        for (int j = low; j < high; j++) {
            if (arr[j] <= pivot) {
                i++;
                swap(arr, i, j); // 피벗보다 작거나 같으면 왼쪽으로 이동
            }
        }
        swap(arr, i + 1, high); // 피벗을 최종 위치에 놓습니다.
        return i + 1; // 피벗의 최종 위치를 반환
    }

    // 두 원소의 위치를 바꾸는 헬퍼 메서드
    private void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    // 예제 실행
    public static void main(String[] args) {
        int[] data = {5, 3, 8, 4, 2, 7, 1, 6};
        System.out.print("정렬 전: ");
        for (int n : data) System.out.print(n + " ");

        new SimpleQuickSort().quickSort(data, 0, data.length - 1);

        System.out.print("\n정렬 후: ");
        for (int n : data) System.out.print(n + " ");
        System.out.println();
    }
}
```


# 병합 정렬(Merge Sort)란?
- 병합 정렬은 **분할 정복(Divide and Conquer)** 알고리즘의 하나로, 리스트를 절반으로 계속 나누고(분할), 나뉜 부분들을 각각 정렬한 뒤(정복), 다시 합치면서(결합) 전체 리스트를 정렬하는 방식입니다.

## 동작과정
1. 분할(Divide): 정렬할 리스트를 두 개의 거의 같은 크기의 부분 리스트로 나눕니다. 이 과정을 각 부분 리스트의 크기가 1이 될 때까지 재귀적으로 반복합니다. (크기가 1인 리스트는 그 자체로 정렬된 것으로 간주합니다.)
2. 정복(Conquer): 분할된 각 부분 리스트에 대해 재귀적으로 병합 정렬을 수행합니다.
3. 결합(Combine) / 병합(Merge): 정렬된 두 개의 부분 리스트를 하나의 정렬된 리스트로 합칩니다. 이 과정에서 두 부분 리스트의 원소들을 비교하여 정렬된 순서대로 새로운(임시) 배열에 저장하고, 다시 원래 배열로 복사합니다.

## 시간복잡도
- O(NlogN)

## 예제
```java
import java.util.Arrays; // 배열 출력을 위해 임포트

public class MergeSort {

    /**
     * 병합 정렬의 메인 함수
     * @param arr 정렬할 배열
     */
    public void mergeSort(int[] arr) {
        // 배열이 비어있거나 원소가 하나 이하면 정렬할 필요가 없음
        if (arr == null || arr.length <= 1) {
            return;
        }
        // 실제로 정렬을 수행하는 재귀 호출 시작
        // 임시 배열을 미리 생성하여 재귀 호출마다 생성하는 오버헤드를 줄임
        mergeSort(arr, new int[arr.length], 0, arr.length - 1);
    }

    /**
     * 재귀적으로 배열을 분할하고 정렬하는 함수
     * @param arr 원본 배열
     * @param temp 임시 저장 공간 (병합 시 사용)
     * @param low 배열의 시작 인덱스
     * @param high 배열의 끝 인덱스
     */
    private void mergeSort(int[] arr, int[] temp, int low, int high) {
        // 정렬할 부분 배열의 크기가 1이 될 때까지 분할
        if (low < high) {
            // 중간 지점 계산
            int mid = low + (high - low) / 2; // (low + high) / 2 와 같지만 오버플로우 방지

            // 왼쪽 부분 배열 재귀적으로 정렬
            mergeSort(arr, temp, low, mid);
            // 오른쪽 부분 배열 재귀적으로 정렬
            mergeSort(arr, temp, mid + 1, high);

            // 정렬된 두 부분 배열을 병합
            merge(arr, temp, low, mid, high);
        }
    }

    /**
     * 두 개의 정렬된 부분 배열을 하나의 정렬된 배열로 병합하는 함수
     * @param arr 원본 배열
     * @param temp 임시 저장 공간 (병합 시 사용)
     * @param low 첫 번째 부분 배열의 시작 인덱스
     * @param mid 첫 번째 부분 배열의 끝 인덱스 (두 번째 부분 배열의 시작 - 1)
     * @param high 두 번째 부분 배열의 끝 인덱스
     */
    private void merge(int[] arr, int[] temp, int low, int mid, int high) {
        // 병합할 부분 배열의 원소들을 임시 배열에 복사
        // System.arraycopy(원본 배열, 원본 시작 인덱스, 대상 배열, 대상 시작 인덱스, 복사할 길이)
        System.arraycopy(arr, low, temp, low, high - low + 1);

        int i = low;       // 왼쪽 부분 배열의 시작 인덱스
        int j = mid + 1;   // 오른쪽 부분 배열의 시작 인덱스
        int k = low;       // 병합된 결과를 저장할 원본 배열의 시작 인덱스

        // 두 부분 배열을 비교하여 원본 배열에 정렬된 순서로 채워넣음
        while (i <= mid && j <= high) {
            if (temp[i] <= temp[j]) { // 안정 정렬을 위해 '작거나 같을 때' 사용
                arr[k] = temp[i];
                i++;
            } else {
                arr[k] = temp[j];
                j++;
            }
            k++;
        }

        // 왼쪽 부분 배열에 남은 원소가 있다면 모두 복사
        while (i <= mid) {
            arr[k] = temp[i];
            i++;
            k++;
        }

        // (오른쪽 부분 배열에 남은 원소가 있다면 모두 복사 - 필요 없음, 이미 그 자리에 있으므로)
        // 사실 이 부분은 필요 없을 수도 있음. 왜냐하면, 오른쪽 배열의 남은 원소들은 이미 제자리에 있거나
        // 아니면 다음 비교에서 남은 원소들이기 때문.
        // 하지만 명시적으로 작성하는 경우도 있음:
        // while (j <= high) {
        //     arr[k] = temp[j];
        //     j++;
        //     k++;
        // }
    }

    // 메인 함수 (예제 실행)
    public static void main(String[] args) {
        int[] arr1 = {12, 11, 13, 5, 6, 7};
        System.out.println("정렬 전 배열 1: " + Arrays.toString(arr1));

        MergeSort sorter = new MergeSort();
        sorter.mergeSort(arr1);
        System.out.println("정렬 후 배열 1: " + Arrays.toString(arr1));
        System.out.println("------------------------------------");

        int[] arr2 = {38, 27, 43, 3, 9, 82, 10};
        System.out.println("정렬 전 배열 2: " + Arrays.toString(arr2));
        sorter.mergeSort(arr2);
        System.out.println("정렬 후 배열 2: " + Arrays.toString(arr2));
    }
}
```


# 힙 정렬(Heap Sort)란?
- 힙 정렬은 **힙(Heap)**이라는 특수한 자료구조를 활용하여 정렬을 수행하는 알고리즘입니다. 힙은 완전 이진 트리 형태를 가지며, 항상 부모 노드의 값이 자식 노드의 값보다 크거나(최대 힙) 작거나(최소 힙) 같다는 규칙을 유지합니다. 힙 정렬은 주로 **최대 힙(Max Heap)**을 사용하여 정렬합니다.

## 힙 정렬의 핵심 아이디어
- **완전 이진 트리**의 일종으로 우선순위 큐를 위하여 만들어진 자료구조
- 최댓값, 최솟값을 쉽게 추출할 수 있는 자료구조

## 동작방식
- 내림차순 정렬을 위해서는 최대 힙을 구성하고 오름차순 정렬을 위해서는 최소 힙을 구성하면 된다.

1. 정렬해야 할 n개의 요소들로 최대 힙(완전 이진 트리 형태)을 만든다.
    - 내림차순을 기준으로 정렬
2. 그 다음으로 한 번에 하나씩 요소를 힙에서 꺼내서 배열의 뒤부터 저장하면 된다.
3. 삭제되는 요소들(최댓값부터 삭제)은 값이 감소되는 순서로 정렬되게 된다.
니다.

## 시간복잡도
- O(NlogN)

## 예제
```c
/* 현재 요소의 개수가 heap_size인 힙 h에 item을 삽입한다. */
// 최대 힙(max heap) 삽입 함수
void insert_max_heap(HeapType *h, element item){
  int i;
  i = ++(h->heap_size); // 힙 크기를 하나 증가

  /* 트리를 거슬러 올라가면서 부모 노드와 비교하는 과정 */
  // i가 루트 노트(index: 1)이 아니고, 삽입할 item의 값이 i의 부모 노드(index: i/2)보다 크면
  while((i != 1) && (item.key > h->heap[i/2].key)){
    // i번째 노드와 부모 노드를 교환환다.
    h->heap[i] = h->heap[i/2];
    // 한 레벨 위로 올라단다.
    i /= 2;
  }
  h->heap[i] = item; // 새로운 노드를 삽입
}
```