# Algorithm
> 코딩테스트에 필요한 알고리즘 

**BFS** / **DFS** / **Union Find** / **위상정렬** / **다익스트라** / **트라이**

### BFS ([대표문제 백준 7576번 토마토](https://www.acmicpc.net/problem/7576))
  import sys
  from collections import deque

  ##sys.stdin = open("input.txt","rt")

  input = sys.stdin.readline

  dr = [0,0,1,-1]
  dc = [1,-1,0,0]

  if __name__ == "__main__" :
      M,N = map(int,input().split())
      box = []
      for _ in range (N) :
          box.append(list(map(int,input().split())))
      q = deque()
      cnt = 0 ## 안 익은 토마토의 갯수
      for i in range (N) :
          for j in range (M) :
              if box[i][j] == 1 :
                  q.append((i,j))
              elif box[i][j] == 0 :
                  cnt += 1
      if cnt == 0 :
          print(0)
          sys.exit()
      day = 0
      while q :
          day += 1
          tmp = len(q)
          while tmp :
              tmp -= 1
              r,c = q.popleft()
              for i in range (4) :
                  nr = r + dr[i]
                  nc = c + dc[i]
                  if nr<0 or nr>=N or nc<0 or nc>=M : ## 범위를 벗어날 때
                      continue
                  if box[nr][nc] == 1 or box[nr][nc] == -1 : ## 이미 익은 토마토거나 토마토가 들어있지 않은 칸
                      continue
                  box[nr][nc] = 1
                  cnt -= 1  ## 토마토가 익는다
                  q.append((nr,nc))
                  if cnt == 0 :
                      print(day)
                      sys.exit()
      print(-1)



