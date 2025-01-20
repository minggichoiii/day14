# day14
from collections import deque

# 입력 받기
N, M, V = map(int, input().split())
graph = [[] for _ in range(N + 1)]  # 1번부터 N번까지의 정점

# 간선 정보 입력 받기
for _ in range(M):
    u, v = map(int, input().split())
    graph[u].append(v)
    graph[v].append(u)

# 각 정점에 대해 방문 여부를 체크
visited_dfs = [False] * (N + 1)
visited_bfs = [False] * (N + 1)

# 1. DFS 구현 (재귀)
def dfs(v):
    visited_dfs[v] = True
    print(v, end=" ")
    
    # 방문할 수 있는 정점들을 번호가 작은 순서대로 방문하기 위해 정렬
    for neighbor in sorted(graph[v]):
        if not visited_dfs[neighbor]:
            dfs(neighbor)

# 2. BFS 구현 (큐 이용)
def bfs(v):
    queue = deque([v])
    visited_bfs[v] = True
    
    while queue:
        current = queue.popleft()
        print(current, end=" ")
        
        # 방문할 수 있는 정점들을 번호가 작은 순서대로 방문하기 위해 정렬
        for neighbor in sorted(graph[current]):
            if not visited_bfs[neighbor]:
                visited_bfs[neighbor] = True
                queue.append(neighbor)

# DFS와 BFS 실행
dfs(V)  # DFS 출력
print()  # DFS와 BFS의 출력 구분을 위한 개행
bfs(V)  # BFS 출력
