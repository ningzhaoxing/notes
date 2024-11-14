# Dijkstra算法

## 代码

```c++
#include <iostream>
using namespace std;

#define INF 9999999
#define MAXN 200
int begin_idx, end_idx, n, k, map[MAXN][MAXN], dis[MAXN], visited[MAXN];

/*
5
6
0 1
0 2 60
0 3 30
0 4 50
1 2 20
1 4 10
3 4 10
*/

void dijkstra() {
    int m_len, index;
    for (int i=0;i<n;i++) {
        dis[i] = map[begin_idx][i]; //初始化dis
    }

    for (int i=0;i<n;i++) {
        m_len = INF;
        index = i;
        //查找最短未访问距离
        for (int j = 0; j < n; j++) {
            if (dis[j] < m_len && !visited[j]) {
                m_len = dis[j];
                index = j;
            }
        }
        visited[index] = true;
        for (int j = 0; j < n; j ++) {
            int step_len = m_len + map[index][j];
            if (step_len < dis[j]) {
                //更新距离
                dis[j] = step_len;
                visited[j] = false;
            }
        }
    }
    cout << dis[end_idx] << endl;
}



int main() {
    int a, b, len;
    cin >> n >> k >> begin_idx >> end_idx;
    fill(dis, dis+MAXN, false);
    fill(visited, visited+MAXN, false);
    for (int i=0;i<MAXN;i++) {
        fill(map[i], map[i]+MAXN, INF);
    }
    visited[begin_idx] = true;
    for (int i=0;i<k;i++) {
        cin >> a >> b >> len;
        map[a][b] = map[b][a] = len;
    }
    dijkstra();
    return 0;

}
```

