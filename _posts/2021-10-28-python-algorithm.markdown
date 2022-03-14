---
layout: post
title: "[python]파이썬으로 알고리즘문제를 풀어보았다"
date: 2021-10-28 19:24:50 +0900
categories: [Algorithm]
---

자바로 알고리즘 공부하다가 입력이 너무 긴게 이제서야 진절머리가 나서 파이썬으로 한 번 바꿔볼까?
했지만 적응이 안된다는 그런 이야기...

입력이 자바에 비해 아주아주 간결해져서 신세계이긴한데 아직 파이썬이랑 낯가리는중

1번. 백준 2468 - 안전영역

```python
import sys
input = sys.stdin.readline

n = int(input())
mat = []
for i in range(n):
    mat.append(list(map(int, input().split())))

dx = [0,0,-1,1]
dy = [-1,1,0,0]

def bfs(sx, sy, visit, limit):
    visit[sx][sy] = True
    q = []
    q.append([sx,sy])
    while q:
        x, y = q.pop(0)
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            if nx<0 or nx>=n or ny<0 or ny>=n or visit[nx][ny]: continue
            if mat[nx][ny] > limit:
                visit[nx][ny] = True
                q.append([nx, ny])

ans=0
rain = 0
while True:
    cnt = 1
    visit = [[0] * n for _ in range(n)]

    for i in range(n):
        for j in range(n):
            if (not visit[i][j]) and mat[i][j] > rain:
                bfs(i, j, visit, rain)
                cnt +=1
    if cnt== 1:
        break
    ans = max(ans, cnt-1)
    rain +=1

print(ans)
```

2번. 백준 1399 - 단어수학

```python
n = int(input())
ss = []

alpha = [0] * 26

for _ in range(n):
    ss.append(input())

for s in ss:
    base = pow(10, len(s) - 1)
    for i in range(len(s)):
        alpha[ord(s[i]) - ord('A')] += int(base)
        base /= 10

alpha.sort(reverse=True)

ans = 0
for i in range(9, 0, -1):
    ans += i * alpha[9-i]

print(ans)
```

...당분간은 섞어쓸 듯 하다
