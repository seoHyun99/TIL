# [Algorithm] 깊이 우선 탐색(DFS:Depth First Search)

## Depth First Search란?
- 트리, 그래프를 탐색하는 알고리즘이다.
- root에서 출발하여, backtracking 하기 전까지 각 branch에서 가능한 멀리까지 탐색한다.
- 최초의 자식노드를 확장하여 목표상태가 발견될 때까지 확장하는 무정보 탐색이다.
- 자식노드를 갖지 않는 노드에 이르면 backtrack 하여 다음 노드에서 출발한다.
- 새로이 확장된 모든 노드들은 확장을 위해 LIFO queue에 더해진다.

### 장점
- 현 경로상의 노드들만 기억하면 되므로 저장공간의 수요가 비교적 적다.
- 목표노드가 깊은 단계에 있을 경우 해를 빨리 구할 수 있다.

### 단점
- 해가 없는 경로에 깊이 빠질 가능성이 있다.
- 얻어진 해가 최단 경로가 된다는 보장이 없다.

### 소스 코드

    public class DfsAmTest {

        static int[][] adjacencyMatrix; // 인접행렬
        static boolean[] isVisits; // 정점의 방문 확인
        static int vCount; // 정점의 수
        static int eCount; // 간선의 수

        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);

            vCount = scanner.nextInt();
            eCount = scanner.nextInt();

            adjacencyMatrix = new int[vCount][vCount];
            isVisits = new boolean[vCount];

            // 간선 입력 받기
            for(int i = 0; i < eCount; i++) {
                int t1 = scanner.nextInt();
                int t2 = scanner.nextInt();

                adjacencyMatrix[t1-1][t2-1] = 1;
            }

            dfs(1);
        }

        public static void dfs(int v){
            isVisits[v-1] = true;

            for(int i=1 ;i <= vCount; i++) {
                if(adjacencyMatrix[v-1][i-1] == 1 && !isVisits[i-1]) {
                    System.out.println(v + " 에서 " + i + " 로 이동");
                    dfs(i);
                }
            }
        }
    }
