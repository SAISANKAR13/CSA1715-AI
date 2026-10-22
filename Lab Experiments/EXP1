import heapq

goal = [(1,2,3),(4,5,6),(7,8,0)]

def heuristic(state):
    dist = 0
    for i in range(3):
        for j in range(3):
            val = state[i][j]
            if val == 0: continue
            x, y = divmod(val-1, 3)
            dist += abs(x - i) + abs(y - j)
    return dist

def neighbors(state):
    x, y = [(ix,iy) for ix,row in enumerate(state) for iy,v in enumerate(row) if v==0][0]
    moves = []
    for dx, dy in [(-1,0),(1,0),(0,-1),(0,1)]:
        nx, ny = x+dx, y+dy
        if 0<=nx<3 and 0<=ny<3:
            new = [list(r) for r in state]
            new[x][y], new[nx][ny] = new[nx][ny], new[x][y]
            moves.append(tuple(tuple(r) for r in new))
    return moves

def a_star(start):
    heap = [(heuristic(start), 0, start, [])]
    visited = set()
    while heap:
        est, cost, state, path = heapq.heappop(heap)
        if state == tuple(tuple(r) for r in goal):
            return path + [state]
        if state in visited: continue
        visited.add(state)
        for nxt in neighbors(state):
            if nxt not in visited:
                heapq.heappush(heap, (cost+1+heuristic(nxt), cost+1, nxt, path + [state]))
    return None

# Example
start = ((1,2,3),(4,0,6),(7,5,8))
solution = a_star(start)
for i, s in enumerate(solution):
    print(f"Step {i}:\n" + "\n".join(str(row) for row in s), "\n")
